# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

<!-- Where the environment record lives, and what a sufficient one
looks like against the issue's stated target. -->

**Where it lives**
- Eval: the Environment block of the Candidate repro report. Compare it against the version and OS stated in the Issue section and the bug-report template in Repo facts.
- Live: the environment lines at the top of my repro draft. Compare them against the issue body on GitHub and the repo's bug-report template.

**What good looks like**
- Template present: pass if the report includes every environment field the repo's bug-report template requires.
- No template: pass if the report includes the tool version (or commit hash) and the operating system.
- Exact values: every field must be a concrete value (e.g., `4.53.3`, `macOS 15.5`). Placeholders such as "latest", "current", or "my machine" fail.
- Version mismatch: if the tested version differs from the version in the issue, the report must state the difference explicitly.

## Steps

<!-- Where the reproduction steps live, and what makes them followable
by a stranger, starting state to trigger. -->

**Where it lives**
- Eval: the steps and command blocks in the Candidate repro report, compared to the reproduction in the Issue section.
- Live: the steps and commands in my repro draft, compared to the reproduction in the issue body on GitHub.

**What good looks like**
- Trigger: pass if the report uses the same command and input as the issue, or explicitly states what was changed.
- Followable: pass if every step is a concrete command, input, or UI action that another person can perform.

## Behavior shown

<!-- Where the artifacts live (output excerpts, logs, screenshots),
and what it means for an artifact to show the issue's behavior rather
than an adjacent one. -->

**Where it lives**
- Eval: the output, logs, screenshots, or other artifacts in the Candidate repro report, compared to the behavior described in the Issue section.
- Live: the output, logs, screenshots, or other artifacts in my repro draft, compared to the behavior described in the issue body on GitHub.

**What good looks like**
- Artifact: pass if the report includes an output excerpt, log, screenshot, or other concrete artifact from the reproduction.
- Match: pass if the artifact shows the same error message, exit code, or visible symptom described in the issue.

## Honesty

<!-- Where claims and their backing meet: how to tell a report that
says exactly what happened (including an honest cannot-reproduce) from
one that claims more than its evidence shows. -->

**Where it lives**
- Eval: claims in the Candidate claim comment and Candidate repro report, compared to the evidence in the Candidate repro report and the Issue section.
- Live: claims in my claim draft and repro draft, compared to the evidence in my repro draft and the issue body on GitHub.

**What good looks like**
- Scope: pass if the report does not claim results, testing, or conclusions that its evidence does not show.
- Cannot reproduce: if the issue did not reproduce, pass if the report clearly states that and provides evidence of the failed reproduction.

## Comms

<!-- Where the words meet the repo: the claim comment against the
issue, the comments against the repo's stated templates and
contribution policy (including AI-use disclosure requirements), and
what specific-and-honest looks like next to boilerplate. -->

**Where it lives**
- Eval: the Candidate claim comment and Candidate repro report, compared to the contribution policy in Repo facts and the issue details.
- Live: `claim.md` and `repro.md`, compared to the repository's `CONTRIBUTING.md` and the issue body on GitHub.

**What good looks like**
- AI disclosure: read the contribution policy in Repo facts. If it requires stating that AI was used, pass if at least one comment (claim or repro) discloses AI use, names what it helped with, and states the candidate verified the work. Do not require proof that AI was actually used before applying this rule: fail if the policy requires disclosure "in any form" or similarly broad language and neither comment contains a disclosure statement, regardless of how the writing reads. If the policy only requires comments be human-written (with no disclosure statement needed), pass unless the comment itself reads as AI-generated. If it says nothing about AI, pass.
- Specific: pass if the claim comment includes a detail specific to the issue, such as error text, a command, a file or function, or a version.
