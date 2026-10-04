# Procedure: how this skill grades a plan package

Follow these steps in order, exactly as written. Write notes as you
go; later steps use the notes, not memory. Where a step does not cover
a situation, say so in the summary instead of inventing a step.

## Read order

Evidence is read before claims, so the plan's stated cause cannot bias
what the evidence is taken to show.

Eval mode (the bundle is the whole world; do not fetch anything):

1. **Repo facts.** Note every stated requirement: contribution policy,
   contributing asks, AI-use or disclosure rules, limits on outside
   pull requests. Write "none stated" if there are none.
2. **Issue.** Note what the issue asks to be fixed, in one or two
   lines, and the reporter's expected behavior.
3. **Thread highlights.** Note only maintainer signals: requests,
   constraints, directions, or decisions from a maintainer or
   collaborator. Other contributors' claims, repro reports, and linked
   pull requests are not signals. Write "no maintainer signals" if
   there are none.
4. **Repro evidence.** Before reading the plan, record:
   - the environment (versions, platform, setup);
   - each failing run as its own line (B1, B2, ...): the exact command
     or input, and the observed result;
   - each control run as its own line (C1, C2, ...): what changed
     (for example, the trigger removed or a component disabled), the
     exact command or input, and the observed result.
   Keep failing runs and controls separate; this is what tells the
   reported bug apart from an unrelated failure.
5. **Candidate plan.** Record: the stated cause; where the change goes
   (file, function, or area); what the change does; anything stated
   as in, out, or deferred; the test or verification step and its
   expected-after result (quote it); and every claim about what was
   tested or verified.
6. **Candidate plan comment.** Sort its statements into two kinds:
   - claims about what was done ("reproduced on 0.64.1");
   - promises about future work ("will add a test", "PR to follow").
   Record each one.

Live mode: read `scope.md` first, as SKILL.md requires, then follow
the same six steps with the live sources from
`references/evidence-guide.md`: the repo's `docs/CONTRIBUTING.md` and
`.github/PULL_REQUEST_TEMPLATE.md` (step 1); the issue body (step 2);
the issue's comments, keeping only maintainer signals (step 3); the
student's own posted repro comment (step 4); the draft `plan.md`,
including its Deviations section (step 5); the draft plan comment
(step 6). Read `voice-guide.md` last.

## Evidence gathering

Each evidence family uses the notes from the read order. Gather
anything extra listed here before running any check.

- **Diagnosis and grounding:** notes from step 4 (B and C lines) and
  the stated cause and change location from step 5. Extra: for each B
  and C line, write whether the stated cause explains it (yes / no),
  and where the change is placed relative to where the wrong value or
  state is first produced.
- **Scope:** the issue's ask from step 2 and the in / out / deferred
  notes from step 5. Extra: list everything the plan will touch, and
  mark each item "needed for the cause or its test" or "not needed".
- **Executability:** the change location and action from step 5.
  Extra: note any either/or decision the plan leaves open.
- **Test plan:** the test step and quoted expected-after result from
  step 5, next to the B lines from step 4. Extra: note whether the
  test runs the same command, input, or code path as a B line.
- **Honesty:** the claims from steps 5 and 6, next to the environment
  and runs from step 4. Extra: mark each claim "matches what was run"
  or "goes beyond what was run". Promises are not claims and are not
  marked here.
- **Comms:** the requirements from step 1, the maintainer signals from
  step 3, and the claims and promises from step 6. Extra: mark each
  promise "in the plan" or "not in the plan", and each maintainer
  signal "answered" or "not answered".

## Check execution

1. Run the checks in the order of the rubric's table.
2. For each check, use only the notes gathered for its family and the
   package part named in that check's Evidence column. If the notes
   do not settle it, re-read that part only, never the whole package.
3. Apply the check's pass condition exactly as written. Grade `pass`
   or `fail`.
4. Grade `unclear` only when the part the check needs is truly absent
   from the package (missing or empty). If the evidence is present,
   choose `pass` or `fail`, even when the call is close.
5. Write one line of evidence per check: the quote or fact that
   decided it.
6. Grade each check on its own. A failure on one check never changes
   the grade of another.
7. Live mode only: after all checks, review the draft comment's
   wording against `voice-guide.md` and list any broken rule, quoting
   it. These notes never change any grade.

## Verdict assembly

1. Apply the rubric's verdict rule to the grades of the `required`
   checks: every required check `pass` gives `accept`; any required
   check `fail` or `unclear` gives `reject`.
2. `preferred` checks never change the verdict. List their grades in
   the summary only.
3. Name the deciding check:
   - for `reject`: the first required check, in table order, that is
     `fail` or `unclear`; quote its evidence line;
   - for `accept`: state that all required checks passed.
4. Write a short summary: one line per check, then the deciding check,
   then (live mode) any voice-guide notes.
5. End with the JSON block defined in SKILL.md, with every check, its
   grade, and its evidence line. Nothing may follow the JSON block.
