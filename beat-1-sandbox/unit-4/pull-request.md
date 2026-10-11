# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s3/pull/126

**Branch**

fix/54-resume-section-whitespace

## My pr-precheck verdict on my draft

I ran my tool in live mode on my draft (title, description, `git diff main...HEAD`, and my
`plan.md`) before opening the pull request, and again after each fix.

1. First live run: **reject**. Deciding check: `repo-checks-run`, with this evidence line:

   > docs/CONTRIBUTING.md asks for five local checks including 'cd frontend && npm ci && npm test -- --run'; the description never mentions the local frontend run (only the CI checkbox).

   It also reported a contradiction: my `plan.md` said ruff, black and mypy were not
   installed, while my description reported their local results.

   Fixes: I added a row for the frontend tests to the description's Testing table ("Not run
   locally: this PR changes no files under `frontend/` … CI's `frontend` job will run it"),
   and I added an Oct 10 update to the Deviations section of `plan.md` saying the lint tools
   were installed and run.

2. Second live run, on the fixed draft: **accept**. All seven required checks passed;
   `title-clear` (preferred) passed.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Smoke run, `--limit 3` (pkg-01 to pkg-03), partial, no `eval-run.txt` written:

   `agreement: 2/3 scored items`

   This run did not test my Unit 4 tool. My Unit 3 plan-check files were still installed in
   `~/.claude/skills/pr-precheck/` (an old `rubric.md` in my Downloads folder had the same
   name). The table showed it: pkg-02 `failed: comment-faithful`, a Unit 3 check name.

2. Smoke run, `--limit 3`, after installing my Unit 4 files:

   `agreement: 3/3 scored items`

   `categories: clear-accept 1/1  silent-drift 1/1  standards-wall 1/1`

3. Full run, 20 packages, saved with `--save-run eval-run.txt`:

   `agreement: 19/20 scored items  (bar: 18/20: PASS)`

   `categories: clear-accept 6/7  not-tested 4/4  silent-drift 4/4  standards-wall 2/2  unreviewable 3/3`

   The only disagreement was pkg-08. I did not edit `SKILL.md`, `rubric.md`, `procedure.md`
   or `references/evidence-guide.md` after this run. The last score in this list, 19/20,
   matches the agreement line in `eval-run.txt`.

**Package analysis**

Package: pkg-08 (jesseduffield/lazygit#5883, category clear-accept).

My rubric decided: reject. The only failed check was `repo-checks-run`; the other six
required checks and `title-clear` passed. Its evidence line:

> Repo checklist asks for 'code formatted', but the only evidence is the bare claim 'code formatted' with no command or result; go generate (no cheatsheet diff), go test, and the integration test do name results.

The gold label said: accept. Its note reads:

> error toast instead of the dead stash prompt, the plan's smallest-surface option; before/after flow shown, integration test added, lazygit checklist (i18n, tests, cheatsheets) satisfied

Why my rubric read it that way. The package's Repo facts say the template asks for a
requirements checklist that includes "code formatted". The PR's Requirements line answers:

> cheatsheets regenerated (no binding changes, no diff); code formatted; integration test added; new error text internationalised; no UserConfig changes.

My `repo-checks-run` check fails a check the repo asks for when "the evidence for it is only
a generic claim ("tests pass", "verified", "works") that names no command or result". "code
formatted" names no command (such as `gofmt`) and no output, so the grader applied that
fail condition. The gold label treats a checklist answer for a mechanical item like
formatting as enough. The rest of the package agreed with the gold note: the
before/after flow is shown and the integration test is in the diff.

**Check rationale**

The check, exactly as it reads in `tools/pr-precheck/rubric.md`:

```
| repo-checks-run | The PR's test evidence, read against the plan's test plan (checks beyond the repro tests) and the repo-facts block (any checks the repo asks contributors to run). | **Pass** if every check that the repo or the plan asks for either shows its actual output, names a specific observed result (what was run and what it showed), or is named as not run with a reason. **Fail** if a check the repo or plan asks for is not mentioned at all, or the evidence for it is only a generic claim ("tests pass", "verified", "works") that names no command or result. | required |
```

Why it reads that way:

- My first version failed any check whose evidence was a claim without pasted output. I
  tested it by hand on calib-01 (gold accept), whose smoke check says only "renders
  gruvmax-fang unchanged". The first version rejected calib-01, so I changed it to pass "a
  specific observed result (what was run and what it showed)" and to fail only a generic
  claim.
- I kept "or is named as not run with a reason". My reason: "I'd allow a missing check to
  pass if it is honestly disclosed and the PR still provides sufficient evidence that the
  change works. This avoids rejecting honest PRs over unrelated failures, while still
  requiring evidence that the change is correct." The evidence that the change works is
  checked separately by `before-after-shown`, so a PR that ran nothing still fails there.
- My own PR needed this rule: my live run first rejected it because the frontend tests were
  not mentioned, and it passed once the description named them as not run, with the reason.

**Trade-offs**

pkg-08 is a case I accept this check will miss. It reads a checklist answer like "code
formatted" as a generic claim, while the gold label accepts it. I did not loosen the check,
because the same loosening (accepting checklist answers without a command or result) could
also let "tests pass"-style evidence through in the not-tested category, which agreed 4/4.
I did not test a looser version with `--only` and canaries, so I do not know what it would
change; I kept the 19/20 run, which passes the bar with every category matched.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
