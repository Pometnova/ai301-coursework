# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| env-recorded | The Environment block of the Candidate repro report, read against the Issue section and the bug-report template in Repo facts (evidence guide: Environment) | Pass if the report gives the values the repo's bug-report template's fields ask for (with no template: the tool version or commit hash and the OS), whether pasted as raw command output or written out by the candidate, each as a concrete value, not "latest", "current", or "my machine"; and if the tested version differs from the issue's, the report says so. | required |
| trigger-matches | The steps and command blocks in the Candidate repro report, read against the reproduction in the Issue section (evidence guide: Steps) | Pass if the report runs the same command and input as the issue, or explicitly states what it changed. | required |
| steps-followable | The steps and command blocks in the Candidate repro report (evidence guide: Steps) | Pass if every step is a concrete command, input, or UI action another person can perform. Fail if any step only describes an action ("set it up", "run the tool"). | required |
| behavior-matches | The output excerpts, logs, or screenshots in the Candidate repro report, read against the behavior described in the Issue section (evidence guide: Behavior shown) | Pass if the report includes a concrete artifact showing the same error message, exit code, or visible symptom the issue describes; or if the report states the issue did not reproduce and shows the output it got instead. Fail if the artifact shows a different error, or if no artifact is shown. Judge only the artifact shown in the report; do not re-run the steps. | required |
| claims-backed | The claims in the Candidate claim comment and Candidate repro report, read against the artifacts in the Candidate repro report (evidence guide: Honesty) | Pass if the claim that the issue's reported behavior occurred is backed by an artifact shown in the report. Secondary or explanatory claims (for example, a variation the candidate ran to isolate the cause) do not need their own shown artifact, as long as the core claim is backed. | required |
| ai-disclosure | The Candidate claim comment and Candidate repro report, read against the contribution policy in Repo facts (evidence guide: Comms) | Read the contribution policy in Repo facts. If it requires stating that AI was used, pass if at least one comment (claim or repro) discloses AI use, names what it helped with, and states the candidate verified the work. Do not require proof that AI was actually used before applying this rule: fail if the policy requires disclosure "in any form" or similarly broad language and neither comment contains a disclosure statement, regardless of how the writing reads. If the policy only requires comments be human-written (with no disclosure statement needed), pass unless the comment itself reads as AI-generated. If it says nothing about AI, pass. | required |
| claim-specific | The Candidate claim comment, read against the Issue section (evidence guide: Comms) | Pass if the claim comment names at least one detail specific to this issue: error text, a command, a file or function, or a version. | required |

## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict;
unclear counts as fail." -->

Accept only if every required check passes. Preferred checks never change the verdict. A check that does not apply (the policy does not require AI disclosure, or the issue reproduced so no cannot-reproduce statement is needed) grades pass. An unclear grade on a required check counts as fail.
