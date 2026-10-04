# Plan: issue #54, resume section detection fails on text with leading whitespace

Issue: codepath/pathreview-ai301-fa26-s3#54
Author: Pometnova
Branch (planned): `fix/54-resume-section-whitespace`
Base: `main` at `2f4e82f`

## Repro evidence

My posted repro comment on #54 (commit `2f4e82f`, Python 3.12.7, macOS arm64) ran the issue's snippet unchanged:

```
Expected: ['Education', 'Skills']
Actual: []
```

I also ran a control on 2026-10-02, the same text with the four leading spaces removed. This control is not in my posted comment:

```
INDENTED []
CONTROL ['Education', 'Skills']
```

The five tests marked `xfail(strict=True, reason="issue #54: ...")` in `tests/unit/test_resume_parser.py`, run with `--runxfail`, fail at lines 35, 61, 114, 152 and 175. Every input they use is indented: the fixture `sample_resume_text` in `tests/conftest.py` and the strings inside the tests.

## 1. Diagnosis

Two functions in `ingestion/parsers/resume_parser.py` match the start of a line without allowing leading whitespace:

- `_detect_sections()`, lines 134-137: all four patterns put the section name immediately after `^` or `\n`. In `    Education:` four spaces come first, so none of the patterns match and `detected_sections` is `[]`.
- `_strip_markdown()`, line 101: `^#+\s+` puts `#` immediately after the line start. An indented `    # Header` is not matched, so the `#` stays in the text.

The control run shows the leading spaces are what break detection: the same text without them returns `['Education', 'Skills']`. The three tests the issue names (lines 35, 61, 152) fail on missing sections. The other two (lines 114 and 175) fail on the `#` that `_strip_markdown()` left behind. Both are the same cause.

The change belongs in these patterns, not in the input. Both parse routes (PDF text and Markdown) call the same `_detect_sections()`, and the patterns are where the mismatch is.

## 2. Scope

In scope:
- The four patterns in `_detect_sections()` (lines 134-137).
- The header pattern in `_strip_markdown()` (line 101).
- Removing the five `xfail` markers that cite #54 in `tests/unit/test_resume_parser.py`, as `docs/CONTRIBUTING.md` requires.
- Two new tests in the same file.

Not in scope:
- The repeated `\n` patterns in `_detect_sections()`. They duplicate the `^` patterns under `re.MULTILINE`. They stay as they are, with only the whitespace allowance added.
- PDF text extraction, and `ingestion/pipeline.py`.
- Lint or type findings elsewhere, and the baseline suppressions in `pyproject.toml`. `grep -n "54" pyproject.toml` finds no suppression for #54.
- The order of the returned list (`list(set(detected))` does not guarantee an order).
- The 6 failing tests in `tests/unit/test_review_service.py` on my machine. They fail with "async def functions are not natively supported" because `pytest-asyncio` is not installed in my `.venv`. They are unrelated to #54.

## 3. Files

- `ingestion/parsers/resume_parser.py`: lines 101 and 134-137.
- `tests/unit/test_resume_parser.py`: remove 5 markers, add 2 tests.

## 4. Approach

1. In `_detect_sections()`, insert `[^\S\r\n]*` after `^` and after `\n` in each of the four patterns. It means any run of whitespace except line breaks, including a non-breaking space. Zero is allowed, so unindented headers still match.
2. In `_strip_markdown()`, change line 101 to `re.sub(r"^([^\S\r\n]*)#+\s+", r"\1", content, flags=re.MULTILINE)`. The group keeps the indentation and removes only the `#`.
3. Delete the five `@pytest.mark.xfail(...)` decorators that cite #54.
4. Add two tests to `TestResumeParser`:
   - `_detect_sections()` on text whose headers are indented with a non-breaking space (`\u00a0`) returns `['Education', 'Skills']`, compared after `sorted()`.
   - `_detect_sections()` on the unindented control text still returns `['Education', 'Skills']`, compared after `sorted()`.

## 5. Test plan

Before (already recorded, on unchanged `main`):
- Repro command: `INDENTED []` and `CONTROL ['Education', 'Skills']`.
- `python -m pytest tests/unit/test_resume_parser.py -q -rxX -p no:cacheprovider`: `5 passed, 5 xfailed`.
- The same with `--runxfail`: `5 failed, 5 passed`, failing at lines 35, 61, 114, 152 and 175.
- `make test-unit`: `6 failed, 369 passed, 53 xfailed` (428 tests).

After the change, I expect:
- Repro command, with `sorted()` around the INDENTED result: `INDENTED ['Education', 'Skills']` and `CONTROL ['Education', 'Skills']`.
- `python -m pytest tests/unit/test_resume_parser.py -q -p no:cacheprovider`: 12 passed, 0 failed, 0 xfailed.
- `make test-unit`: `6 failed, 376 passed, 48 xfailed` (430 tests). The same 6 `test_review_service.py` failures remain.

## 6. Risks

- Not yet run: I have not run the new patterns. The numbers in the test plan are my expectations, from reading the code.
- Lint and types: `ruff`, `black` and `mypy` are not installed in my `.venv`, so I cannot run `make check` locally. I will say so in the PR, and rely on CI for those jobs.
- Behavior change for indented text: indented lines that start with a section word now match, for example a bullet line such as `    Summary: ...`. That could add a section name that was not detected before.
- Downstream use: in `ingestion/pipeline.py`, `detected_sections` is logged (line 90), and `parse_result.metadata` is copied into the metadata passed to `strategy_selector.chunk(...)` together with `parse_result.text`. So indented Markdown will now reach the chunker without its `#` markers, as unindented Markdown already does, and indented text will carry a non-empty section list. I have not read `strategy_selector` or the chunkers, so I do not know whether they read `detected_sections`.
- `[^\S\r\n]` also matches a form feed (`\f`). I have not checked whether extracted PDF text contains one before a header.
- First pull request from a fork: per `docs/CONTRIBUTING.md`, CI may wait for a maintainer to approve it.

## Deviations

The change matched the plan: the same two files, the four patterns in _detect_sections() and line 101 in _strip_markdown() (version b, which keeps the indentation), the five xfail markers removed, and the two new tests. The expected results in section 5 held: 12 passed in tests/unit/test_resume_parser.py, and 6 failed, 376 passed, 48 xfailed in make test-unit. The same 6 failures in test_review_service.py were there before the change (pytest-asyncio is not installed in my environment).

Two differences in how I built it, neither of which changed the plan:
- I applied the edits with Claude Code in auto mode, not with manual approval as I had intended. I read the full git diff before committing, and it matched the plan line by line.
- Claude Code first wrote the non-breaking spaces in the new test as literal U+00A0 characters, not as the \u00a0 escape in the plan. I replaced them with the escape before committing.

Not done yet: lint and type checks (ruff, black and mypy are not installed here, so they will only run in CI), and I did not check whether the chunkers read detected_sections. The posted plan comment on #54 is still accurate, so no follow-up comment is needed.
