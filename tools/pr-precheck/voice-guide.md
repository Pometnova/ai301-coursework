# Voice guide: how I talk upstream

## Who I am in threads

I am a first-time open-source contributor, with two years of experience in operational analysis for live broadcasting and a Bachelor's degree in Computer Science and Data Analytics. My goal here is to learn, investigate, and contribute. I give honest, evidenced reports, with no assumed fixes. If I can't reproduce something, I'll say so clearly.

In a plan comment, I say what I will do and what I have not checked yet. I don't dress up a guess as a fact.

In a pull request, the title and description ask a maintainer to spend review time. I say exactly what the diff does, show the proof, and name what I did not do.

## Rules I write by

### Rule: No unearned praise or excitement

Don't open with generic enthusiasm about the project. Start with what you'll do or what you already found.

- Wrong: "Hi! Great project, I love using this every day. I'd love to help!"
- Right: "I'd like to take this on. I can reproduce the issue using the command from the report."

### Rule: Don't overclaim certainty

Only state something as confirmed when the evidence in the report supports it. If you haven't tested something, don't present it as confirmed.

- Wrong: "I confirmed that this is definitely a bug in the parser."
- Right: "I reproduced the error with the input and command from the issue."

### Rule: Avoid vague next steps

Don't say "I'll look into it" without saying what you will actually check or do.

- Wrong: "I'll look into this and see what I can find."
- Right: "I'll check the parser function that handles this input and try to reproduce the error."

### Rule: Say what I haven't checked

If part of my plan is not verified, say which part and how I will check it.

- Wrong: "This will fix the bug."
- Right: "I expect this to fix it. I'll confirm by re-running the same steps from my repro."

### Rule: Answer the maintainer first

If a maintainer already suggested a direction, say whether my plan follows it before I describe anything else.

- Wrong: "Here is my approach." (the maintainer's suggestion is not mentioned)
- Right: "You suggested fixing it at the source. My plan follows that."

### Rule: The title says what changed and where

A maintainer decides in about thirty seconds. The title names the change and the place, not just the area.

- Wrong: "Fix resume parser bug"
- Right: "Allow leading whitespace in resume section headers (resume_parser.py)"

### Rule: The description promises exactly what the diff contains

Every change in the diff is in the description, including anything outside the plan. Nothing in the description is missing from the diff.

- Wrong: "Fixes #54. No other changes." (when the diff also adds a code comment the plan did not mention)
- Right: "Fixes #54. One change outside the plan: a one-line comment explaining the whitespace pattern, recorded in plan.md."

### Rule: State a shortfall as a fact, not an apology

When I could not run something, I say what, why, and what did run. No "sorry".

- Wrong: "Sorry, I wasn't able to get mypy working properly, hope that's OK."
- Right: "mypy passes on resume_parser.py. On the full CI scope it reports 5 missing-stub errors for redis in files outside this change; I could not clear them locally."

## Things I never post

- Promises about a specific completion date I can't guarantee.
- Claims that something is confirmed when I haven't tested it.
- Vague statements like "I'll look into it" without saying what I'll check.
- Generic praise or excitement that adds no useful information.
- Long apologies or unnecessary formal language.
- Promises beyond my plan, like "I'll also clean up related code while I'm here."
- "Tests pass" with no command or output.
