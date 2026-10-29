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

**Unit 6: Installed the voice guard and wrote a memory file for my pyfixest clone**

I merged my three voice-guide copies into one file, added rules for claims, questions, and pings, and installed the guard as a hook. The wiring test was blocked, so I knew the hook runs before any comment goes out. My rule on completion dates was too broad: repro-check flagged "by Monday" in my claim, even though it was only a report-back date, so I removed the date before posting. I also wrote a 33-line CLAUDE.local.md from one scoped run over the docs folder, and kept it out of git with .git/info/exclude.

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

Issue #957 asks for the R examples in Peng Ding's open-access book *Linear Model and Extensions* to be rewritten in Python with pyfixest. The docs folder `docs/textbook-replications/` has pages for other books but nothing for chapter 2 of this book. Chapter 6 is only in open PR #1592.

**Expected Behavior**

A docs page shows the chapter 2 example in pyfixest: it loads the book's Galton data, computes the OLS line with the book's formula and with `pf.feols`, and gets the same coefficients the book prints (22.63624 and 0.6373609).

**Current Behavior**

There is no chapter 2 page. A reader who wants this example in Python has only the book's R script, `chapter02.R`.

**Affected Components**

`docs/textbook-replications/` (a new page, `ding_chapter02.qmd`). The page uses `pf.feols` and `.coef()`. No Python code in the package changes.

**Toolkit**

- Tool: Claude Code with my CLAUDE.local.md from unit 6. I used it to read the issue thread, PR #1592, and the repo's testing policy, then compared the book's data file with the Rdatasets CSV.
- What it produced: the gap (no chapter 2 page; chapter 6 only in open PR #1592), the book's data file on Dataverse (fileId 10123762), and a match: 934 rows, largest difference 1.4e-14, coefficients 22.636241 and 0.637361 from both the book's formula and `pf.feols`.
- Difficulties: my CLAUDE.local.md marked the single-page render command as "NOT VERIFIED," and pixi 0.83 rewrote `pixi.lock` on the first run.
- What changed: I verified the render command and added `--frozen`, taken from the repo's CI settings, so `pixi.lock` stays untouched.

---
## Reproduction Process

**Environment Setup**

macOS 26.6.2 on an Apple-silicon (arm64) Mac, Python 3.12.7. I made a fresh virtual environment (`.venv-957`) so nothing from my other projects affects the result, then ran `pip install pyfixest`, which installed pyfixest 0.60.0, pandas 3.1.0, and numpy 2.5.4. I used pip instead of the repo's pixi setup for this first check, because I only needed `pf.feols` on a CSV file. I will set up pixi when I build the docs page. No problems came up. Matplotlib built its font cache on the first run, which only made that run slower.

**Steps to Reproduce**

1. Create and activate a fresh environment: `python3 -m venv .venv-957`, then `source .venv-957/bin/activate`.
2. Install pyfixest: `pip install pyfixest`.
3. Load Galton's data and fit the chapter 2 regression in `repro_ch2.py`: `df = pd.read_csv(URL)` with the Rdatasets GaltonFamilies CSV, then `pf.feols("childHeight ~ midparentHeight", data=df)` and `print(fit.coef())`.
4. Run `python repro_ch2.py` and compare the coefficients with chapter 2 of Peng Ding's *Linear Model and Extensions*.
5. Observed result: 934 rows. Intercept 22.636241 and slope 0.637361. The book prints 22.63624 and 0.6373609, so both match to every printed digit.

**Reproduction Evidence**

- **Commit showing reproduction:** none. This check ran outside my pyfixest fork.
- **Screenshots/logs:** output of `python repro_ch2.py`:
  `(934, 9)` / `Intercept 22.636241` / `midparentHeight 0.637361`
- **My findings:** The gap is real: pyfixest's docs/textbook-replications/ folder has no page for Ding's book, and chapter 6 is only in open PR #1592. The chapter 2 example is reproducible with pyfixest. Chapter 2 prints coefficients only, not standard errors, so I compared coefficients only. I loaded the data from the public Rdatasets CSV, which is the same data as the R package HistData the book uses. I have not opened the book's Dataverse files yet, so I will check them against this CSV before I build the page.
- Update 2026-10-29: I checked the book's Dataverse file (GaltonFamilies.txt, fileId 10123762): 934 rows, the same values as the Rdatasets CSV (largest difference 1.4e-14), and the same coefficients. I posted the comparison on the issue: https://github.com/py-econometrics/pyfixest/issues/957#issuecomment-6509857306

**Toolkit**

- Tool: repro-check, run on my claim draft and my repro report together.
- What it produced: accept, with all 7 checks passing, including behavior-matches (my output next to the book's values) and claims-backed (the standard-error promise from my claim honestly walked back).
- Difficulties: on my first claim draft, it flagged "I'll report what I find here by Monday" as a completion date, even though it was only a report-back date.
- What changed: I removed the date from my claim. In the repro, I stated plainly that chapter 2 has no standard errors, instead of leaving my claim's promise open.

---

## Solution Approach

**Analysis**

The gap is in `docs/textbook-replications/`: it has pages for the Mixtape, *The Effect*, and *Causal Inference: The Brave and True*, but nothing for chapter 2 of Ding's book. The book's `chapter02.R` reads `GaltonFamilies.txt` with `read.table`, computes the means, standard deviations, and correlation of `midparentHeight` and `childHeight`, sets the slope to `cor × sd_y / sd_x` and the intercept to `mean_y − slope × mean_x`, and draws a ggplot scatter plot with the fitted line. Each step has a direct Python match: `pd.read_csv` for the data, pandas for the formula, `pf.feols("childHeight ~ midparentHeight")` for the model, and matplotlib for the plot.

**Proposed Solution**

Add one page, `docs/textbook-replications/ding_chapter02.qmd`. It loads `GaltonFamilies.txt` from the book's Dataverse files (fileId 10123762), with an explicit user agent the same way #1592 does. It computes OLS with the book's formula, fits the same model with `pf.feols`, shows that both match the book's printed values, and draws the scatter plot with the fitted line in matplotlib. I write the page text in my own words and do not copy the book.

I will not change: `_quarto.yml`, `index.qmd`, `resources.qmd`, or `ding_linear_models.qmd` (to avoid a conflict with #1592); any Python code in `pyfixest/`; `pixi.lock`; or rendered output in `docs/_freeze/`.

Because I don't edit `index.qmd`, the page won't appear in the Textbook Replications list yet. I'll add it there in a follow-up after #1592 merges, or move chapter 2 into `ding_linear_models.qmd` if the maintainers prefer.

**Implementation Plan**

1. Create branch `docs/ding-chapter-2` from `master`.
2. Add `ding_chapter02.qmd` with a title, a short intro (book, Dataverse DOI, CC0 license, link to #957), and a setup cell.
3. Add a cell that loads GaltonFamilies from Dataverse. (fileId 10123762 is `GaltonFamilies.txt` in the book's Dataverse files. I checked the file page title and compared the file with the Rdatasets CSV: 934 rows, same values.)
4. Add a cell with the book's formula: means, standard deviations, correlation, slope, intercept.
5. Add a cell with `pf.feols` and a comparison to the formula and the book's printed values.
6. Add a matplotlib cell: a jittered scatter plot (fixed seed) with the fitted line.
7. Test: before the change, rendering `ding_chapter02.qmd` fails because the page doesn't exist. After the change, `pixi run --frozen -e docs quarto render docs/textbook-replications/ding_chapter02.qmd` runs every cell, and the coefficients are 22.636241 and 0.637361, matching the book's 22.63624 and 0.6373609. Also run `pixi run --frozen lint` and `git diff --check master...HEAD`. I checked this render command on master with an existing page, `mixtape.qmd`, on 2026-10-29: all cells ran and the HTML was built. I haven't run it on the new page yet.

**Toolkit**

- Tool: plan-check, run on plan.md and a draft plan comment (not posted) for issue #957.
- What it produced: accept, with all 8 checks passing. The first run was also accept, but it listed three gaps: the plan didn't say the page would be missing from the index list, the render command looked unverified, and the Dataverse fileId wasn't tied to a check.
- Difficulties: my procedure.md assumes a bug with failing runs and controls, so plan-check had to improvise for a docs addition. It also read the old "NOT VERIFIED" note in my CLAUDE.local.md.
- What changed: I added the index-list deferral, the fileId check, and the mixtape render check to plan.md and the comment, and updated CLAUDE.local.md. I would add a docs-addition case to procedure.md.

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
