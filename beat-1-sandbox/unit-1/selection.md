# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/54

**Verdict output**


**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
All three URLs are in the scoped repo (codepath/pathreview-ai301-fa26-s3), so all three are gradable. Repo-level evidence is shared: last default-branch commit 2f4e82f by Andrew Burke (human) on 2026-09-16, two days ago; repo not archived, last push 2026-09-16; docs/CONTRIBUTING.md sets testing/CI conditions but states no AI ban. The repo has zero pull requests of any state, and none of the three issues has an assignee or a single comment — so the claim family is clean across the board. Per the Path Review house rule, classmate claims wouldn't have blocked anything anyway.

All three accept. Ranked by fit:

1. #11 — Architecture doc doesn't explain the hybrid retrieval scoring formula. Best fit: it's a documentation change to one file (docs/ARCHITECTURE.md, 3.5 KB), no code, and the subject matter is a scoring formula that blends vector and keyword scores — numeric reasoning close to your data-analysis background. It's also the gentlest possible first pass through the Git/GitHub workflow, which is the part that's new to you.
2. #54 — Resume section detection fails on text with leading whitespace. A small, self-contained Python bug in ingestion/parsers/resume_parser.py: regex anchors that don't tolerate indentation. Text wrangling is adjacent to your BeautifulSoup/pandas cleaning work, and the issue hands you a runnable repro plus three named failing tests in tests/unit/test_resume_parser.py, so you'll know when you're done. Note docs/CONTRIBUTING.md: seeded bugs carry a @pytest.mark.xfail(strict=True) marker you must remove as part of the fix, or CI fails.
3. #61 — Health check DB probe passes a raw SQL string. Objectively the smallest change (wrap "SELECT 1" in sqlalchemy.text()), but it sits in api/routes/health.py — an API route plus SQLAlchemy session handling, which is the web-framework territory your profile flags as unfamiliar. Fine as a second contribution; ranked last only on fit, not on quality.

One tension worth naming: the rubric's scope-fits check passes any issue doable as one PR, so it can't distinguish #11's 2–3 hour doc write-up from #61's one-line fix. If you want effort to influence the outcome rather than just my ranking, that belongs in rubric.md as a preferred check — your rubric currently has no preferred checks at all, so nothing but the fit profile is doing the ordering.

[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/11",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Commit 2f4e82f by human author Andrew Burke (Aburke225) on 2026-09-16, 2 days before capture"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "isArchived:false, pushedAt 2026-09-16T21:50:20Z (2 days)"},
      {"name": "scope-fits", "grade": "pass", "evidence": "One bounded doc task: 'Add a section explaining the scoring logic with an example' in docs/ARCHITECTURE.md; no sub-item split, no design debate, zero comments"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: [], no linked PRs (repo has no PRs at all), zero comments"},
      {"name": "human-authored", "grade": "pass", "evidence": "Opened by Aburke225 (COLLABORATOR), not a [bot] username"},
      {"name": "ai-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md state CI/test conditions only; no AI-contribution ban anywhere in repo"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/54",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Commit 2f4e82f by human author Andrew Burke (Aburke225) on 2026-09-16, 2 days before capture"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "isArchived:false, pushedAt 2026-09-16T21:50:20Z (2 days)"},
      {"name": "scope-fits", "grade": "pass", "evidence": "Single bug in _detect_sections() in ingestion/parsers/resume_parser.py with a runnable repro and 3 named failing tests; one PR's worth of work, no split requested"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: [], no linked PRs (repo has no PRs at all), zero comments"},
      {"name": "human-authored", "grade": "pass", "evidence": "Opened by Aburke225 (COLLABORATOR), not a [bot] username"},
      {"name": "ai-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md state CI/test conditions only; no AI-contribution ban anywhere in repo"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s3/issues/61",
    "checks": [
      {"name": "maintainer-alive", "grade": "pass", "evidence": "Commit 2f4e82f by human author Andrew Burke (Aburke225) on 2026-09-16, 2 days before capture"},
      {"name": "repo-in-use", "grade": "pass", "evidence": "isArchived:false, pushedAt 2026-09-16T21:50:20Z (2 days)"},
      {"name": "scope-fits", "grade": "pass", "evidence": "One-line fix in api/routes/health.py (wrap 'SELECT 1' in sqlalchemy.text()) with exact error text given; no split requested, no core-internals warning"},
      {"name": "unclaimed", "grade": "pass", "evidence": "assignees: [], no linked PRs (repo has no PRs at all), zero comments"},
      {"name": "human-authored", "grade": "pass", "evidence": "Opened by Aburke225 (COLLABORATOR), not a [bot] username"},
      {"name": "ai-policy", "grade": "pass", "evidence": "docs/CONTRIBUTING.md and .github/PULL_REQUEST_TEMPLATE.md state CI/test conditions only; no AI-contribution ban anywhere in repo"}
    ],
    "verdict": "accept"
  }
]
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

After the first full run of all issues, the score was 18/20. It stayed 18/20 after 2 full runs. All five categories were covered, except: issue-01 and issue-20.

For issue-01, the initial rule rejected umbrella issues, so the model 
saw five files as separate tasks, even though it was really one job.
Running --only issue-01 --out debug.json showed that the model read this issue as 5 deliverables, not one bounded task. So I rewrote the rule to stop counting files and instead ask: "Could one person do this as one PR?" After re-running issue-01 alone, it passed.

Issue-20 consistently failed against the gold label. debug.json showed all 5 existing checks passing, but the issue was opened by cursor[bot], which none of my checks looked at. After I added a new check, human-authored, it passed too.

**Issue analysis**

After the initial run, issue-20 passed, but the gold label rejected it.

My rubric passed all five initial checks: the repository was active and in use, the task was a single, bounded feature, and no one had claimed it. However, my rubric didn't take into account that the issue was opened by cursor[bot], not a human. None of my checks looked at who opened the issue at all.

**Check rationale**

"human-authored	issue's "opened by" line, including the (ROLE) tag	issue author is not a bot (username does not end in [bot])	required" 

This rule checks whether the issue was opened by a human, not a bot, by verifying its role tag. I added this check to prioritize issues that were created by a human over those automatically generated by a bot. An issue created by a bot may describe a real problem, but it doesn't prove that a human reported the issue or that a maintainer confirmed the project actually wants it. I made this check required, so it rejects all bot-created issues rather than just rank them lower.

**Trade-offs**

This check rejects issues created by a bot even though they may be legitimate issues that can be resolved, but my check is designed to prioritize issues created by a real person who can provide feedback. 
A bot could file an accurate bug report or a useful feature idea. However, my check rule could not tell the difference between a good and bad issue, so I accept losing some good cases in exchange for a simple and reliable signal.

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

1. The problem I chose matches my interests because it not only passes all my checks, but also has the "good first issue" and "tier-1" labels, and the bug to be fixed requires knowledge of Python, which is my primary programming language.
2. The verdict determined that all three problems passed my rubric. However, it doesn't determine which problem is potentially suitable for me, given my experience and knowledge in the field. So I used my skills fit ranking to choose the problem that best suits me, rather than relying on the accept/reject verdict.
3.  This is the first time I'm claiming and reproducing an issue, so it will definitely take more time to figure everything out and get it right. I'll need to ensure the commit is formatted correctly and that all 5 CI checks pass.


---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
