# Evidence guide: where evidence lives in a PR package

This is the map for every check in `rubric.md`. For each evidence
family it says WHERE to look (in an eval bundle, and in live mode) and
WHAT GOOD LOOKS LIKE there.

An eval bundle has these parts: a header (id, source, capture date),
Repo facts, Issue, Thread highlights, Plan context, and Candidate PR.
The Plan context holds the repro evidence the plan built on and the
plan itself: its change steps, its "not in scope" line, its Files
list, and its test plan. The Candidate PR holds the Title,
Description, Commits, Diff, and Test evidence. Parts may not carry
these exact headings; find the content wherever it sits.

In live mode the sources are: the student's `plan.md` with its
Deviations section (in the course repo, `beat-1-sandbox/unit-3/plan.md`,
or the house plan for a house-chain student); the branch's diff,
`git diff main...HEAD` (three dots), and commit list,
`git log --oneline main..HEAD`, run from the working copy; the draft PR
title and description; the student's captured test output; the issue
and its comments (`gh issue view <number> --repo <repo> --comments`);
and the repo's written rules (`.github/PULL_REQUEST_TEMPLATE.md`,
`docs/CONTRIBUTING.md`).

## Plan fidelity (harness category: silent-drift)

Used by: `matches-plan`, `description-faithful`.

- Where it lives (eval): the Plan context's change steps, "not in
  scope" line, and Files list; any deviation note in the Plan context
  or the Description; the Diff's changed files and hunks; the
  Description's claims about what changed.
- Where it lives (live): the steps, scope, and Files section of
  `plan.md` and its Deviations section; the output of
  `git diff --stat main...HEAD` (which files) and
  `git diff main...HEAD` (which hunks); the draft description.
- What good looks like: every changed file and hunk traces to a plan
  change step or to a recorded deviation note, and every plan change
  step appears in the diff or is named as left out or deferred. The
  description claims only what the diff does and names every change
  outside the plan.
- Silent drift looks like: a hunk in a file the plan never names, or
  in an area the plan lists as not in scope, with no note anywhere
  (more than the plan); a plan step missing from the diff with nothing
  saying so (less than the plan); or a description that says "no
  changes beyond the plan" over a diff that has them.

## Test evidence (harness category: not-tested)

Used by: `before-after-shown`, `repo-checks-run`.

- Where it lives (eval): the Test evidence section, read against the
  Plan context's test plan (each test it names, and the expected-after
  result for each) and the repro evidence (the before result). The
  repo's own checks are named in the Repo facts block (contribution
  docs, template checklist) or in the test plan.
- Where it lives (live): the student's captured before and after
  output for the repro command; the output of the repo's test and
  lint commands (in this repo: `make test-unit`, `ruff check .`,
  `black --check .`, `mypy ...`, as `docs/CONTRIBUTING.md` and the PR
  template list them); the test plan in `plan.md`.
- What good looks like: every test in the test plan that re-runs a
  reproduced failure shows its actual output after the change, the
  before result is visible here or in the repro evidence, and each
  after result matches the stated expected-after. Every other check
  the repo or plan asks for shows its output, names a specific
  observed result (what was run and what it showed), or is named as
  not run with a reason.
- Not good: "tests pass", "verified", or "works" with no command or
  result; a test the plan names that the evidence never mentions; an
  after result that differs from the expected-after.

## Diff quality (harness category: unreviewable)

Used by: `diff-clean`.

- Where it lives (eval): every added and removed line in the Diff,
  and the file list in its headers; the Commits list.
- Where it lives (live): `git diff main...HEAD` line by line;
  `git diff main...HEAD --check` for trailing whitespace;
  `git status` for stray files.
- What good looks like: every added or removed line is part of the
  planned change, a test for it, or a change named in a deviation
  note.
- Debris looks like: debug prints or logging left in; commented-out
  or dead code; whitespace, quote, or line-wrap changes on lines the
  fix does not touch; files unrelated to the fix (scratch files,
  editor settings, lock files nobody asked for).

## Standards and comms (harness category: standards-wall)

Used by: `template-filled`, `ai-disclosure`, `title-clear`.

- Where it lives (eval): the Repo facts block: whether the repo has a
  PR template and what its sections, checklist, and issue-link line
  ask; the contribution policy; any stated AI-use policy. Then the
  Title and Description, to see whether each ask is met.
- Where it lives (live): `.github/PULL_REQUEST_TEMPLATE.md`,
  `docs/CONTRIBUTING.md`, and any AI-use policy in the repo; the draft
  title and description.
- Treat every package as AI-assisted work. Whether a disclosure rule
  applies depends only on what the repo or template asks, never on
  whether the PR shows signs of AI use.
- What good looks like: if the repo has a template, every section has
  real content (not empty, not the template's placeholder text), every
  checklist item is checked or left unchecked with a stated reason,
  and the issue is linked where the template asks. If the repo states
  an AI policy or the template has a disclosure section, the
  description discloses AI use the way it asks (for example, the tool
  and the type and extent of help). The title names what changed and
  where.
- Not good: an empty or placeholder section; an unchecked box with no
  reason; a missing issue link; no AI disclosure where one is asked;
  a title like "fix bug".
