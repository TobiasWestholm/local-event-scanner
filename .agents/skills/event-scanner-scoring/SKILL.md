---
name: event-scanner-scoring
description: Use during every Event Scanner run when scoring candidate events against preferences, availability rules, date-window practicality, and dealbreakers.
metadata:
  short-description: Score event candidates
---

# Event Scanner Scoring

Use this skill when evaluating candidate events against the human's preferences.

## Inputs

- Candidate events.
- `preferences/taste-profile.md`.
- `preferences/scoring-rubric.md`.
- `preferences/availability-rules.md`.

## Procedure

1. Add `event-scanner-scoring` to the current run note's `Skills used` list before scoring work starts.
2. Read the taste profile and scoring rubric.
3. Compare each event against fit, practicality, novelty, timing, price friction, and confidence.
4. Apply hard dealbreakers from the taste profile before recommending an event.
5. Apply date-window practicality from the scoring rubric: near-term scans should prefer shorter, cheaper, lower-friction events; farther-future scans may favor bigger commitments when fit is strong.
6. Assign one recommendation label:
   - Strong pick
   - Worth considering
   - Maybe
   - Skip for now
7. Explain the reason in plain language.
8. Mention missing details and uncertainty.
9. Replace the run note's `Scored Candidates` placeholder with scored candidates or a concise scoring summary.

## Output Shape

```md
## Event Title

- Label:
- Why it fits:
- Caveats:
- Next action:
- Source:
- Confidence:
```

## Rule

Do not suggest preference updates during scoring or normal scans. Learning suggestions belong only in `event-scanner-add-to-calendar` after the user explicitly adds an event to Google Calendar.

## Output

When invoked, explicitly say: "[Using event-scanner-scoring skill]"
