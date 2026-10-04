# Rubric: is this plan ready to post and build from?

Each check answers one question about the plan package. Grade the thing
itself, never the write-up's shape: a plan does not need particular
headings, sections, or length to pass. Locations named in the Evidence
column are defined in `references/evidence-guide.md`.

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-grounded | The candidate plan's stated cause, read against every behavior recorded in the repro evidence (its steps, conditions, and actual result). | **Pass** if the stated cause explains every behavior the repro evidence records and no repro observation contradicts it. **Fail** if any repro observation contradicts the cause (for example, the bug persists when the stated cause is removed, disabled, or bypassed, or the repro shows the bug under a condition the cause says cannot produce it), or if the cause does not connect to any behavior the repro observed. | required |
| root-not-symptom | Where the plan's change is made, read against the plan's own stated cause and the repro evidence. | **Pass** if the change is made where the stated cause lives: the place where the wrong value or state is first produced. **Fail** if the change only hides or works around the symptom downstream while the cause sits upstream: special-casing the repro's input, catching and ignoring the error, retrying, adding a delay, clamping or reformatting the output at display, or suppressing the visible effect. | required |
| bounded-scope | The plan's change description, including any in/out or deferred statement and any files or areas it names, read against what the stated cause requires. | **Pass** if the plan is one change aimed at the stated cause, and everything it touches is needed for that change or its test. Fixing only part of the issue passes when the plan says which part is left out or deferred. **Fail** if the plan adds work the cause does not require (renames, refactors, config or API changes, new flags or features, cleanup, docs passes "while I'm here"), or leaves its extent open-ended ("clean up related code", "improve X generally", "and anything else that turns up"). | required |
| executable-by-a-stranger | The plan's change description: where the change goes and what it does. | **Pass** if someone who has never seen the issue could start the work from the plan alone: it names where the change goes (a file, function, component, or clearly identifiable code area) and what the change does concretely enough to begin. **Fail** if the location or the change is missing or vague ("fix the parser", "investigate and fix", "refactor as needed"), or if starting depends on a decision the plan leaves open ("either A or B, will decide later"). | required |
| test-decisive | The plan's test or verification statement, read against the repro evidence's steps and actual result. | **Pass** if the plan names a concrete check that exercises the reproduced behavior (re-running the repro steps, or a test that runs the same path) and states the observable result expected after the fix, so a stranger can compare before and after. **Fail** if there is no test, if the test is vague ("see if it works", "test it", "make sure nothing breaks"), if it only runs existing tests without anything that exercises the reproduced behavior, or if no expected-after result is stated. | required |
| comment-faithful | The candidate plan comment, read against the candidate plan and against the maintainer signals in the thread highlights. | **Pass** if the comment states the same cause, change, and proof as the plan, promises nothing the plan does not contain, and responds to every maintainer signal in the thread (a request, constraint, direction, or decision from a maintainer or collaborator). A thread with no maintainer signals passes the second half automatically. **Fail** if the comment contradicts the plan or promises more than it (other fixes, extra features, a broader change), if it contains no plan at all ("I can fix this, please assign me"), or if it ignores or contradicts a maintainer signal (for example, the plan adds a flag after a maintainer said "no new flags"). | required |
| repo-conventions | The plan comment and the plan, read against the repo-facts block: contribution policy, contributing asks, and AI-use or disclosure rules. | **Pass** if the plan and comment meet every stated repo requirement that applies to a plan or its upcoming pull request, or if no stated requirement applies. **Fail** if they break a stated requirement: a required AI-use disclosure is missing, the policy requires discussion or approval before a pull request and the comment skips it, the policy limits or refuses outside pull requests and the comment ignores that, or a stated contribution rule the plan must follow is contradicted. Missing polish is not a failure; only a stated requirement counts. | required |
| honest-uncertainty | Claims in the plan and comment about what was tested, verified, or covered, read against the repro evidence's environment and steps. | **Pass** if every claim about testing, verification, platforms, versions, or coverage matches what the package shows was actually done, and real unknowns are named as unknowns. **Fail** if the plan or comment presents something untested as established ("fixes all cases", "verified on Windows" when only macOS was run, "no other callers affected" with nothing checked). The stated cause itself is graded by diagnosis-grounded, not here. | preferred |

## Verdict rule

- **accept** if every `required` check passes.
- **reject** if any `required` check fails or is `unclear`.
- `preferred` checks never change the verdict; report them in the
  summary only.
- `unclear` is allowed only when the evidence a check needs is truly
  absent from the package (the section is missing or empty). When the
  evidence is present, the grader must choose pass or fail, even if
  the call is close.
- Each check is graded on its own. A failure on one check never
  changes the grade of another.
