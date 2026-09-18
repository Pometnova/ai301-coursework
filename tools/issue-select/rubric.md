# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| maintainer-alive | "last 5 default-branch commits" under Repo facts (dates and author names) | at least 1 commit by a human author (name not ending in [bot]) within 60 days of the capture date | required |
| repo-in-use | "archived:" on the repo line; "last push to any branch" under Repo facts | not archived AND last push within 90 days of the capture date | required |
| scope-fits | issue body and Comments section | one bounded task: not an umbrella/tracking issue — test: could this reasonably be done as ONE pull request by one person? If yes, pass regardless of how many files it touches. Fail only if the issue explicitly asks for it to be split into multiple issues/PRs, or assigns different pieces to different people, no unsettled design debate about the core task itself (a minor, clearly-labeled sub-point still being discussed does not fail the issue), no maintainer saying it touches core internals, not a usage question. A short body alone is not a fail | required |
| unclaimed | "this issue: assignees:" and "linked PRs:" under Repo facts; Comments section | no assignee, no open linked PR, no claim comment newer than 120 days. Closed unmerged PRs do not count as a claim | required |
| human-authored | issue's "opened by" line, including the (ROLE) tag | issue author is not a bot (username does not end in [bot]) | required |
| ai-policy | "contribution policy" line under Repo facts | no outright ban on AI-generated contributions. Conditions (disclosure, testing) and silence both pass | required |



## Verdict rule

<!-- State how the grades above combine into accept or reject, and how
unclear is treated. Example shape (write your own): "accept if every
required check passes; preferred checks never change the verdict, they
rank accepted issues; unclear counts as fail." -->

Accept only if every required check passes. Unclear counts as fail.
