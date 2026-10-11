# Procedure: how this tool grades a PR package

Follow these steps in order, exactly as written. Write notes as you
go; later steps use the notes, not memory. Where a step does not cover
a situation, say so in the summary instead of inventing a step.

## Read order

The plan and the diff are read before the description, so the tool
forms its own view of what changed before it reads what the PR claims
changed. A description that says "no changes beyond the plan" must not
shape how the diff is read.

Eval mode (the bundle is the whole world; do not fetch anything):

1. **Repo facts.** Record: whether the repo has a PR template, and if
   so its sections, checklist items, and issue-link line; every check
   the repo asks contributors to run; any stated AI-use or disclosure
   policy, quoted. Write "none stated" for anything absent.
2. **Issue and thread highlights.** Note what the issue asks to be
   fixed, in one line, and any maintainer request or constraint in the
   thread. These are context; no check grades the issue itself.
3. **Plan context.** Record, before opening the Candidate PR:
   - the repro evidence's before result for each reproduced failure
     (R1, R2, ...);
   - each change step of the plan (S1, S2, ...);
   - the Files list and the "not in scope" line, quoted;
   - each test in the test plan (T1, T2, ...), marking which ones
     re-run a reproduced failure, and the expected-after result for
     each, quoted;
   - any deviation note, quoted.
4. **Diff.** Record each changed file, and each hunk as its own line
   (H1, H2, ...): the file, and what the hunk adds or removes in a few
   words. Do this before reading the description.
5. **Commits.** Note the commit list.
6. **Title and description.** Record: the title; every claim the
   description makes about what changed (D1, D2, ...); any deviation
   or limitation it states; whether it links the issue; the template
   sections it contains; any AI-use disclosure, quoted.
7. **Test evidence.** For each test and check, record the command or
   name, whether output is shown, and the after result, quoted.

Live mode: read `scope.md` first, as SKILL.md requires, then follow
the same seven steps with the live sources from
`references/evidence-guide.md`: `.github/PULL_REQUEST_TEMPLATE.md`,
`docs/CONTRIBUTING.md`, and any AI-use policy in the repo (step 1); the
issue and its comments (step 2); `plan.md` with its Deviations section
(step 3); `git diff main...HEAD`, three dots, run from the working copy
(step 4); `git log --oneline main..HEAD` (step 5); the draft title and
description (step 6); the student's captured test output (step 7).
Read `voice-guide.md` last.

## Evidence gathering

Each evidence family uses the notes from the read order. Gather
anything extra listed here before running any check.

- **Plan fidelity** (matches-plan, description-faithful): pair the
  notes from steps 3, 4, and 6. Extra:
  - for each hunk H, write the step S or deviation note it serves, or
    "none";
  - for each step S, write the hunk H that does it, or "not in diff"
    and whether anything names it as left out or deferred;
  - for each description claim D, write the hunk that supports it, or
    "not in diff", or "contradicted by H...";
  - list every hunk marked "none" and whether the description
    mentions it.
- **Test evidence** (before-after-shown, repo-checks-run): pair the
  notes from steps 1, 3, and 7. Extra:
  - for each test T that re-runs a reproduced failure, write: before
    shown (here or in R), after output shown (yes/no), after result
    matches the expected-after (yes/no);
  - for each other test in the plan and each check the repo asks for,
    write one of: "output shown", "specific result named", "not run,
    reason given", "generic claim only", "not mentioned".
- **Diff quality** (diff-clean): the hunk notes from step 4. Extra:
  read every added and removed line, and mark any debug statement,
  commented-out or dead code, whitespace or formatting change on a
  line the fix does not touch, or file unrelated to the fix.
- **Standards and comms** (template-filled, ai-disclosure,
  title-clear): pair the notes from steps 1 and 6. Extra:
  - for each template section, write "filled", "empty", or
    "placeholder";
  - for each checklist item, write "checked", "unchecked with reason",
    or "unchecked, no reason";
  - treat the package as AI-assisted work, and write whether the repo
    or template asks for an AI disclosure (yes/no) and, if yes, what
    the disclosure must name; then whether the description's
    disclosure names it.

## Check execution

1. Run the checks in the order of the rubric's table.
2. For each check, use only the notes gathered for its family and the
   package part named in that check's Evidence column. If the notes do
   not settle it, re-read that part only, never the whole package.
3. Apply the check's pass condition exactly as written. Grade `pass`
   or `fail`.
4. Grade `unclear` only when the part the check needs is truly absent
   from the package (missing or empty). If the evidence is present,
   choose `pass` or `fail`, even when the call is close.
5. Write one line of evidence per check: the quote or fact that
   decided it (for example, "H2 edits names.py; the plan's Files list
   names only export.py; no deviation note").
6. Grade each check on its own. A failure on one check never changes
   the grade of another.
7. Live mode only: after all checks, hold the draft title and
   description against `voice-guide.md` and list any broken rule,
   quoting the line that breaks it. These notes never change any
   grade.

## Verdict assembly

1. Apply the rubric's verdict rule to the grades of the `required`
   checks: every required check `pass` gives `accept`; any required
   check `fail` or `unclear` gives `reject`.
2. `preferred` checks never change the verdict. List their grades in
   the summary only.
3. Name the deciding check:
   - for `reject`: the first required check, in rubric table order,
     that is `fail` or `unclear`; quote its evidence line;
   - for `accept`: state that all required checks passed.
4. Write a short summary: one line per check, then the verdict and the
   deciding check, then (live mode) any voice-guide notes.
5. End with the JSON block defined in SKILL.md, with every check, its
   grade, and its evidence line. Nothing may follow the JSON block.
