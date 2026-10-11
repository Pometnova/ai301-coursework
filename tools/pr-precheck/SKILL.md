---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer one question about one PR package: is this ready to submit?

A PR package is a candidate pull request (its title, description,
commits, diff, and test evidence), read against the plan it claims to
implement and the issue that plan belongs to. Grade exactly one
package per run. Do not answer any other question: do not review code
style beyond what the rubric checks, do not judge whether the plan was
a good idea, and do not answer from gut feel. Answer only by executing
the components in this directory.

## Inputs and modes

Decide the mode first, then read only that mode's inputs.

**Eval mode** is used when the input is a package bundle (a markdown
file with Repo facts, Issue, Thread highlights, Plan context, and a
Candidate PR). The bundle is the whole world: every fact comes from
the bundle text. Do not fetch anything, do not read any other file
outside this skill directory, and do not look up the live issue.
Always grade the complete package: run every check in `rubric.md` and
apply the full verdict rule.

**Live mode** is used when the student asks you to check their own PR
before opening it. Read these inputs, from these sources:

- The plan: the student's `plan.md`, including its Deviations section
  (in the course repo at `beat-1-sandbox/unit-3/plan.md`). A
  house-chain student reads the house plan and the house repro pack
  instead; the same checks grade the same things.
- The diff: everything the branch changes relative to the repo's
  default branch, produced by `git diff main...HEAD` (three dots), run
  from the working copy of the fork. Use `git diff --stat main...HEAD`
  for the file list and `git log --oneline main..HEAD` for the commits.
- The draft PR title and description, as the student provides them.
- The test evidence: the student's captured before and after output
  and the output of the repo's own checks.
- The issue and its thread: `gh issue view <number> --repo <repo>
  --comments`.
- The repo's stated asks: `.github/PULL_REQUEST_TEMPLATE.md`,
  `docs/CONTRIBUTING.md`, and any AI-use policy in the repo.

`references/evidence-guide.md` says where each fact lives in both
modes.

## The scope seam (live mode only)

In live mode, read `scope.md` before anything else. It names the only
repo a PR may target and the house rules there (PR from the student's
own fork branch named `fix/<issue-number>-<slug>`, one PR per issue,
the PR template always used). Apply those rules as evidence for the
checks that read them.

- If the PR targets any repo other than the one `scope.md` names,
  refuse to grade and say so.
- If the scope's repo line is still a bracketed placeholder, stop
  without grading and tell the student to get the cohort's scope file
  from the instructor. Never guess a scope.

In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, after all checks are graded, read `voice-guide.md` (the
student's own rules for how they write upstream) and hold the draft PR
title and description against each rule. In the summary, list every
rule the draft breaks and quote the line that breaks it. These notes
never change any check's grade or the verdict on their own, because no
rubric check reads the voice guide.

In eval mode, ignore `voice-guide.md` entirely.

## Component reads

- `rubric.md` defines the checks (name, evidence, pass condition,
  weight) and the verdict rule. It decides WHAT is graded.
- `references/evidence-guide.md` maps where each evidence family lives
  in a package and what good looks like there. It decides WHERE to
  look.
- `procedure.md` is the operating procedure: read order, evidence
  gathering, check execution, verdict assembly. It decides HOW and IN
  WHAT ORDER. Execute it exactly as written.

When the procedure is silent on a step you need, do not improvise
around it: note the gap in the summary ("procedure gap: ...") and
continue with the steps it does give.

If `rubric.md` has no checks written in it, or `procedure.md` has no
steps written in it, refuse to grade and say which file is empty.
Template comments do not count as content; only written text does.
Never invent checks or steps at runtime.

## Verdict and output

The verdict is binary: `accept` means ready to submit; `reject` means
hold. There is no third verdict and no score. Put any reservations in
the evidence lines of the checks, never in the verdict.

Before the JSON block, write a short readable summary: one line per
check with its grade, then the verdict and the deciding check (as
`procedure.md` defines it), then, in live mode only, any voice-guide
notes. Then end the reply with the fenced JSON block below. It must be
valid JSON, it must be the last thing in the reply, and nothing may
follow it. Do not add, remove, rename, or reorder fields.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote
  that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a short, terse PR can be ready, and
  a long, confident one can hide drift. Read the diff, the evidence,
  and the description against the plan, the issue, and the repo's
  stated asks, never against formatting or length.
- The rubric decides: if a check passes by its stated condition but
  feels wrong, it still passes. Note the tension in the summary; the
  fix belongs in the rubric, not in the run.
- The procedure decides how: follow `procedure.md` as written and
  report its gaps instead of inventing steps.
- Treat `unclear` as the rubric's verdict rule directs. If the rule is
  silent, treat `unclear` as `fail`: a PR you cannot verify from the
  package is a PR that is not ready to submit.
