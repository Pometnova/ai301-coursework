# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of your claim and reproduction on the issue you chose in Unit 1, and of the
evaluation runs that produced `eval-run.txt`. This file is graded at the path above; a copy
kept anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your identity upstream

**GitHub username**

Pometnova

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/54#issuecomment-5840573412

I'd like to work on this one. I'll start by checking `_detect_sections()` in `resume_parser.py` to confirm how it handles leading whitespace, then put together a reproduction report with the environment and steps.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/54#issuecomment-5841549433

Environment: PathReview commit 2f4e82f (2026-09-16), macOS 26.6.2 (arm64), Python 3.12.7. Installed with `pip install -e .` in a virtual environment; no Docker/database needed.

Steps: fresh clone, `python3 -m venv .venv && source .venv/bin/activate && pip install -e .`, then ran the issue's exact reproduction:

    from ingestion.parsers.resume_parser import ResumeParser
    r = ResumeParser()
    res = r.parse('\n    John Smith\n    john@example.com\n\n    Education:\n    - B.S. Computer Science\n\n    Skills: Python\n')
    print(res.metadata['detected_sections'])

Expected: `['Education', 'Skills']`. Actual: `[]`.

Cause: `_detect_sections()` anchors its regex patterns (e.g. `^education\s*[:|-]`) directly at `^`/`\n` with no allowance for leading whitespace, so the indented section headers in this input never match.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Smoke test (--limit 3, 3 packages): 2/3 agreement. pkg-01 and pkg-02 agreed with gold; pkg-03 disagreed (gold accept, mine reject, failed claims-backed). Reading pkg-03 and its per-check evidence showed claims-backed was rejecting a secondary, explanatory claim that had no artifact of its own, even though the core bug claim was fully backed. Fixed claims-backed to only require the core claim to have a shown artifact. Re-ran --only pkg-03,pkg-01,pkg-02 as canaries: 3/3 agreement.

First full run (20 packages): 16/20 agreement, below the 18/20 bar. Four disagreements: pkg-03 (failed ai-disclosure, gold accept), pkg-05 (failed env-recorded, gold accept), pkg-07 (failed ai-disclosure, gold accept), pkg-19 (gold reject, mine accept).

Fixed env-recorded so "Template present" accepts values the candidate wrote out, not only pasted raw command output (pkg-05 required only the values a bug-report template's fields ask for). Re-ran --only pkg-05,pkg-01,pkg-13,pkg-16 as canaries: 4/4 agreement.

Fixed claim-specific's weight from preferred to required, so a boilerplate claim comment can hold a package even with a technically perfect repro (pkg-19). Re-ran --only pkg-19,pkg-01,pkg-07,pkg-09 as canaries: 4/4 agreement.

Second full run (20 packages): 20/20 agreement, bar: PASS, every category matched (clear-accept 8/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4). All four known disagreements resolved with no new ones introduced.

Fixed ai-disclosure with a fourth case: when a policy requires disclosure "in any form" and neither comment discloses, the check now fails by default instead of asking the grader to judge whether the writing looks AI-generated. This addressed model-variance flips seen on pkg-03 and pkg-20 across runs with identical rubric text. Re-ran --only pkg-20,pkg-03,pkg-07,pkg-13 as canaries: 4/4 agreement.

Confirming full run (--save-run eval-run.txt): 20/20 agreement, bar: PASS, all categories matched (clear-accept 8/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4). This is the run committed as eval-run.txt.


**Package analysis**

pkg-20 (source: ghostty-org/ghostty#13604) has a strict AI-disclosure policy requiring "all AI usage in any form" to be disclosed, naming the tool and extent of assistance. Neither the candidate's claim comment nor its repro report contained any disclosure statement, and the writing was highly polished and structurally uniform (a formal "Environment / Steps / Expected / Actual" report with no personal voice), consistent with AI-generated text. The gold label is reject.

Early versions of my ai-disclosure check read this inconsistently: on one run it graded pass, on another it flipped to fail with the same rubric text, because the check asked the grader to decide whether the writing "looked AI-generated" before applying the disclosure rule, and that judgment wasn't stable across runs. I fixed this by adding a fourth case: when a policy requires disclosure "in any form" and no disclosure statement appears in either comment, the check now fails by default, regardless of how the writing reads. This removed the need for the grader to infer AI use from style, and pkg-20 now reads reject consistently.

**Check rationale**

ai-disclosure | The Candidate claim comment and Candidate repro report, read against the contribution policy in Repo facts (evidence guide: Comms) | Read the contribution policy in Repo facts. If it requires stating that AI was used, pass if at least one comment (claim or repro) discloses AI use, names what it helped with, and states the candidate verified the work. Do not require proof that AI was actually used before applying this rule: fail if the policy requires disclosure "in any form" or similarly broad language and neither comment contains a disclosure statement, regardless of how the writing reads. If the policy only requires comments be human-written (with no disclosure statement needed), pass unless the comment itself reads as AI-generated. If it says nothing about AI, pass. | required

This check went through three versions before reaching its current form. The first version only asked whether a policy "requires or discusses" disclosure, which the model read inconsistently: it once treated ripgrep's "comments must be human-written" rule (pkg-03) as if it demanded a disclosure statement, when the policy actually requires no disclosure at all, only human authorship. I split the rule into three explicit policy types: disclosure required, human-authorship required with no disclosure needed, and no AI language at all.

That version fixed pkg-03 and pkg-07, but pkg-20 still flipped between pass and fail across identical re-runs, because the rule asked the grader to judge whether undisclosed writing "looked AI-generated" before deciding the check applied at all, an unstable, subjective step. I rejected that approach in favour of the current sentence, "do not require proof that AI was actually used... fail if the policy requires disclosure in any form... and neither comment contains a disclosure statement, regardless of how the writing reads." This puts the burden on the disclosure statement existing, not on the grader inferring intent from style, which removed the run-to-run inconsistency.

**Trade-offs**

env-recorded's "Template present" rule accepts environment values the candidate wrote out by hand, not only values pasted as raw command output (e.g. pkg-05's conda version/OS stated in prose rather than a pasted `conda info` block). This trades a small amount of rigor, a candidate could in theory type made-up values instead of running the real command, for correctly accepting reports like pkg-05 that give accurate, concrete values in a different format. I accept this: the check still fails vague or placeholder values ("latest", "my machine"), so the remaining risk is a candidate fabricating specific numbers, which is a different, rarer failure mode than the one this check targets.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/repro-check/`.
