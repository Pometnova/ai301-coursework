# Contribution: Translate Peng Ding's Linear Models book into pyfixest

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Olena Pometnova
**GitHub Username:** Pometnova
**Issue:** https://github.com/py-econometrics/pyfixest/issues/957
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Installed the issue-scout over my Unit 1 skill and wrote my first search strategy**

I wrote three search queries from my fit profile (Excel, SQL, and four named data tools) and eight ranking filters, then ran one scan: 300 results, 83 after ranking, 5 graded, 3 accepted. Testing the queries before the scan caught two mistakes: quoting "excel OR xlsx" made gh search for one exact phrase (0 results), and --owner apache pulled in unrelated Apache projects, so I removed the quotes and switched to --repo. The scan ranked a 2018 pandas issue first, so I added a free ranking rule that drops issues older than two years. It also accepted a personal 18-star repo; I left that unfixed because search results have no star count, so that check would belong in the rubric, not the strategy.

**Unit 6: [one line on the tool work]**

[2-4 sentences: the voice-guard, the repo-memory file. What broke or
fell short, and what changed because of it. "Nothing broke" counts when
it is true - say how you know.]

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

In Unit 5, I ran my scout's search: three queries returned 300 results, and 83 were left after ranking. My scout graded 5 and accepted 3. I decided to work on apache/datafusion-comet #4420, a Claude skill for reviewing documentation. My scout graded it directly on October 21 and accepted it, but that same evening another contributor left a "take" comment on GitHub and was assigned to it. I realized that a shortlist goes out of date quickly, and that grading and claiming an issue should happen at the same time.

I returned to the Issue Selection site and chose 18 candidates from Apache AGE and Airflow. I used Claude to check their GitHub threads, and almost every one already had a claim comment, an open pull request, was too large, or was more than two years old, which my own ranking rule filters out. Claude then scanned the rest of the site for data-tool issues and found pyfixest #957. It asks contributors to rewrite the R examples from Peng Ding's open-access textbook *Linear Model and Extensions* in Python with pyfixest, as documentation pages. My scout rejected it on two checks: scope-feasible failed because the issue covers the whole book, and unclaimed failed because an open pull request (#1592) is linked to it.

I still chose #957 because I only claimed one chapter of the book, Chapter 2, and not the entire book. The open pull request #1592 is for Chapter 6, so it doesn't overlap with my work. The issue also had no comments or assignee. This work aligns with my goal as a data analyst. Chapter 2 is about simple linear regression: one variable explains another. I'll run the R code from the book, then write the same analysis in Python using pyfixest's `feols` function and check that the coefficients and standard errors match R's. The result will be a documentation page on the pyfixest website written in Quarto, so I'll also learn how documentation is created and tested in a real project. My scout looked at the entire issue, not just my chapter. It saw a book with multiple chapters and said the work was too large. It also saw an open pull request and said someone had already taken the issue, but that pull request is for a different chapter. My claim comment: https://github.com/py-econometrics/pyfixest/issues/957#issuecomment-6460279179


**Toolkit**

- Tool: issue-scout in direct mode (`issue-scout: grade <URL>`), after this week's scope patch. I graded #957 and re-graded #4420.
- What it produced: reject for #957 (`scope-feasible`: the issue covers the whole book; `unclaimed`: open PR #1592). Reject for #4420 (`unclaimed`: assigned to another contributor), which had been an accept on October 21.
- Difficulties: the scout grades the whole issue, so it rejects an umbrella issue even when I claim one part of it. Its `unclaimed` check cannot tell that PR #1592 is about a different chapter.
- What changed: I replaced my `scope-fits` check with `scope-feasible`, which adds a difficulty note instead of rejecting issues with open edges. I would also change `unclaimed` so it checks whether a linked PR covers the same part I want to claim.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
