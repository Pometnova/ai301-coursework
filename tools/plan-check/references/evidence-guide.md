# Evidence guide: where evidence lives in a plan package

This is the map for every check in `rubric.md`. For each evidence
family it says WHERE to look (in an eval bundle, and in live mode) and
WHAT GOOD LOOKS LIKE there.

An eval bundle has six parts: Repo facts, Issue, Thread highlights,
Repro evidence, Candidate plan, Candidate plan comment. The plan's
parts may not carry headings; find the content (cause, change, test,
claims) wherever it sits.

In live mode the sources are: the student's draft `plan.md` and draft
plan comment; the issue page and its comments
(`gh issue view <number> --repo <repo> --comments`); the student's own
posted repro comment on that issue; and the repo's written rules
(`docs/CONTRIBUTING.md`, `.github/PULL_REQUEST_TEMPLATE.md`).

## Diagnosis and grounding

Used by: `diagnosis-grounded`, `root-not-symptom`.

- Where it lives (eval): the cause statement in the Candidate plan,
  and the Repro evidence block: its environment, steps, any control or
  changed condition, and the actual result.
- Where it lives (live): the cause in the draft `plan.md`, and the
  student's posted repro comment on the issue (environment, steps,
  output). Other users' repro comments are context, not the student's
  evidence.
- What good looks like: the stated cause explains every behavior the
  repro recorded, including any control run (for example, the same
  input without the triggering condition works). The change is placed
  where the cause first produces the wrong value or state, not where
  the wrong result becomes visible.

## Scope

Used by: `bounded-scope`.

- Where it lives (eval): the Candidate plan's change description, any
  in / out / deferred statement, and any files or areas it names; the
  Issue body for what the issue asks.
- Where it lives (live): the scope and files in the draft `plan.md`;
  the issue body; the repo's rules on unrelated changes (in
  `docs/CONTRIBUTING.md`: no bulk lint or type fixes, do not edit
  annotated `# noqa` lines, baseline cleanup goes in its own PR).
- What good looks like: one change aimed at the stated cause. Anything
  the issue asks for that the plan does not fix is named as left out
  or deferred. Nothing is added "while I'm here".

## Executability

Used by: `executable-by-a-stranger`.

- Where it lives (eval): the Candidate plan's change description:
  where the change goes and what it does.
- Where it lives (live): the files and approach in the draft
  `plan.md`; the named files or functions should exist in the repo.
- What good looks like: the plan names a file, function, or clearly
  identifiable code area, and a concrete action ("allow leading
  whitespace before the header pattern in `_detect_sections()`"), with
  no open either/or decision left for later.

## Test plan

Used by: `test-decisive`.

- Where it lives (eval): the Candidate plan's test or verification
  statement, read against the Repro evidence block's steps and actual
  result.
- Where it lives (live): the test plan in the draft `plan.md`; the
  student's repro steps; the repo's tests for the issue (in this repo,
  `tests/unit/`, where seeded-bug tests carry
  `@pytest.mark.xfail(strict=True, reason="issue #<n>: ...")`); the
  repo's test commands (`make test-unit`).
- What good looks like: the plan re-runs the repro steps (or a test
  that runs the same code path) and states the exact result expected
  after the fix, next to the result seen before, so a stranger can
  compare them. Where seeded-bug tests exist, the plan says they must
  pass with their `xfail` markers removed.

## Honesty

Used by: `honest-uncertainty`.

- Where it lives (eval): every claim in the Candidate plan and the
  Candidate plan comment about what was tested, verified, or covered,
  read against the Repro evidence block's environment and steps.
- Where it lives (live): the risks or unknowns in the draft `plan.md`,
  its Deviations section, and the claims in the draft comment.
- What good looks like: claims match what was actually run (the same
  platform, version, and inputs). Things not yet checked are named as
  unknown. A change of plan during the build is recorded in the
  Deviations section, with what changed and why.

## Comms

Used by: `comment-faithful`, `repo-conventions`.

- Where it lives (eval): the Candidate plan comment, read against the
  Candidate plan, the Thread highlights, and the Repo facts block
  (contribution policy, contributing asks, AI-use rules).
- Where it lives (live): the draft plan comment; the issue's comments;
  `docs/CONTRIBUTING.md` and `.github/PULL_REQUEST_TEMPLATE.md`.
- Who counts as a maintainer signal: comments from a maintainer or
  collaborator, or a policy stated in the repo's docs. Other
  contributors' claims, repro reports, and linked pull requests are
  not maintainer signals; they do not block the plan and do not need
  an answer.
- What good looks like: the comment states the same cause, change, and
  proof as the plan and promises nothing more. It responds to each
  maintainer request or constraint. It follows every written repo
  requirement that applies to the plan or its coming pull request.
