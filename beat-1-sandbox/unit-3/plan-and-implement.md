# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

Pometnova

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/54#issuecomment-5948223530

Plan for #54, built from my repro above (commit 2f4e82f).

**What I found:** two functions in `ingestion/parsers/resume_parser.py` match at the start of a line and do not allow leading whitespace: the four section patterns in `_detect_sections()` (lines 134-137) and the `#` pattern in `_strip_markdown()` (line 101). A control run with the same text and the four leading spaces removed returns `['Education', 'Skills']`, so the spaces are the trigger. The five `xfail` tests that cite #54 all use indented text; run with `--runxfail`, they fail at lines 35, 61, 114, 152 and 175.

**What I'll do:** allow leading whitespace, but not line breaks, in those patterns with `[^\S\r\n]*`, and remove the five `xfail` markers as `docs/CONTRIBUTING.md` asks. I'll add two small tests: headers indented with a non-breaking space, and the unindented control. I'll build it on my fork, on branch `fix/54-resume-section-whitespace`. Not in scope: the repeated `\n` patterns, PDF extraction, `ingestion/pipeline.py`, and lint findings elsewhere.

**How I'll prove it:** re-run my repro. Before: `INDENTED []`. After, I expect `INDENTED ['Education', 'Skills']` with the control unchanged, and `tests/unit/test_resume_parser.py` passing with no markers. These are expectations; I have not run the change yet.

**Not checked yet:** whether the chunkers read `detected_sections` (I have only seen `pipeline.py` log it and pass it on). `ruff`, `black` and `mypy` are not installed on my machine, so lint and type checks will only run in CI.

---

## Your branch

**Branch**

fix/54-resume-section-whitespace

**Evidence**

**Before** (unchanged `main`, commit 2f4e82f). Repro command and output:

```
python -c "from ingestion.parsers.resume_parser import ResumeParser; r = ResumeParser(); t = '\n    John Smith\n    john@example.com\n\n    Education:\n    - B.S. Computer Science\n\n    Skills: Python\n'; print('INDENTED', r.parse(t).metadata['detected_sections']); c = '\nJohn Smith\njohn@example.com\n\nEducation:\n- B.S. Computer Science\n\nSkills: Python\n'; print('CONTROL', sorted(r.parse(c).metadata['detected_sections']))"
INDENTED []
CONTROL ['Education', 'Skills']
```

Tests before, with the xfail markers lifted (`--runxfail`):

```
python -m pytest tests/unit/test_resume_parser.py --runxfail -q --tb=line -p no:cacheprovider
5 failed, 5 passed in 0.04s
(failing lines: test_resume_parser.py:35, :61, :114, :152, :175)
```

```
make test-unit
6 failed, 369 passed, 53 xfailed, 21 warnings in 13.97s
```

**After** (branch fix/54-resume-section-whitespace, commit 2ed9372). Same repro, with sorted() on both results:

```
python -c "from ingestion.parsers.resume_parser import ResumeParser; r = ResumeParser(); t = '\n    John Smith\n    john@example.com\n\n    Education:\n    - B.S. Computer Science\n\n    Skills: Python\n'; print('INDENTED', sorted(r.parse(t).metadata['detected_sections'])); c = '\nJohn Smith\njohn@example.com\n\nEducation:\n- B.S. Computer Science\n\nSkills: Python\n'; print('CONTROL', sorted(r.parse(c).metadata['detected_sections']))"
INDENTED ['Education', 'Skills']
CONTROL ['Education', 'Skills']
```

```
python -m pytest tests/unit/test_resume_parser.py -q -p no:cacheprovider
............                                                             [100%]
12 passed in 0.09s
```

```
make test-unit
6 failed, 376 passed, 48 xfailed, 21 warnings in 5.43s
```

The 6 failures are the same before and after. They are all in tests/unit/test_review_service.py and say "async def functions are not natively supported" because pytest-asyncio is not installed in my virtual environment. They are not related to this change.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Smoke test, `--limit 3` (pkg-01 to pkg-03), partial run, no `eval-run.txt` written:

   `agreement: 3/3 scored items`

2. Full run, 20 packages, saved with `--save-run eval-run.txt`:

   `agreement: 18/20 scored items  (bar: 18/20: PASS)`

   Category line of that run:

   `categories: clear-accept 6/7  scope-creep 4/4  thread-convention 1/2  unbuildable 3/3  wrong-cause 4/4`

   The two disagreements were pkg-14 (gold accept, my verdict reject) and pkg-20 (gold reject, my verdict accept). Every category scored at least once.

I did not edit `rubric.md`, `references/evidence-guide.md`, `procedure.md` or `SKILL.md` between the two runs. The `sha256` prefixes in the `eval-run.txt` header (`f27cdb2bc0fff729`, `2e5e442fbb5d21fe`, `4447b58ff36516f7`, `4688d0d0f4cf6cb3`) matched my installed files when I checked them after the run. The last score in this list, 18/20, matches the agreement line in `eval-run.txt`.

**Package analysis**

Package: pkg-20 (ghostty-org/ghostty#11261, category thread-convention).

My rubric decided: accept. `failed_checks` was empty and all 8 checks passed.

The gold label said: reject. Its note reads:

> excellent bounded plan that follows the thread's direction, but the comment contains no AI-use disclosure and ghostty's stated policy requires disclosing all AI usage; every package here is treated as AI-assisted work

Why my rubric read it that way. The package's Repo facts do state the rule:

> All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance

and the plan comment contains no disclosure. My `repo-conventions` check passed it anyway, with this evidence line:

> No claim or sign of AI involvement appears in the plan or comment, so the AI-disclosure requirement is not shown to apply at this stage

The check's pass condition says "or if no stated requirement applies", and the grader used that exit. My rubric never tells the grader to treat a plan as AI-assisted, so the disclosure rule never counted as applying to this author. The other seven checks passing was correct: the plan follows the maintainer's direction and is bounded.

**Check rationale**

The check, exactly as it reads in `tools/plan-check/rubric.md`:

```
| repo-conventions | The plan comment and the plan, read against the repo-facts block: contribution policy, contributing asks, and AI-use or disclosure rules. | **Pass** if the plan and comment meet every stated repo requirement that applies to a plan or its upcoming pull request, or if no stated requirement applies. **Fail** if they break a stated requirement: a required AI-use disclosure is missing, the policy requires discussion or approval before a pull request and the comment skips it, the policy limits or refuses outside pull requests and the comment ignores that, or a stated contribution rule the plan must follow is contradicted. Missing polish is not a failure; only a stated requirement counts. | required |
```

Why it reads that way:

- I rejected one combined comms check. I split comms into `comment-faithful` (the thread) and `repo-conventions` (the repo's written rules), because a package can have no thread comments at all (calib-01 says "0 comments total") and the thread-convention category has only two packages, so one muddled check could miss both.
- I rejected judging polish. The row ends "Missing polish is not a failure; only a stated requirement counts", so a plan is held for breaking a written rule, not for style.
- "that applies" and "or if no stated requirement applies" are there so a plan is not failed for rules that do not concern it.
- I did not revise this row after the full run; it is the version the run graded.

**Trade-offs**

The wording "that applies" and "or if no stated requirement applies" gives up catching a stated requirement when nothing in the package shows it applies to the author. pkg-20 is the case it missed: the policy was stated, the disclosure was missing, and the check passed it. I accept that miss for this run. I did not test a stricter version, for example one that assumes every plan is AI-assisted, so I do not know what it would do to the other 19 packages, including the 6 clear-accepts that agreed. I kept the current run instead of spending a second full run.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in `tools/plan-check/`.
