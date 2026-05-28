---
name: event-scanner-calendar-review
description: Use during every Event Scanner run after scoring and before shortlist review when calendar context is available, user-provided, or requested. Checks event timing against availability while preserving privacy.
metadata:
  short-description: Review calendar practicality
---

# Event Scanner Calendar Review

Use this skill to adjust event practicality using calendar availability context.

## Inputs

- Scored candidate events.
- Event date/time and expected duration.
- Calendar availability context, when available or provided by the user.
- Google Calendar availability lookup, when the connector is available.
- `docs/privacy-and-access.md`.
- `preferences/availability-rules.md`.
- `preferences/scoring-rubric.md`.

## Procedure

1. Add `event-scanner-calendar-review` to the current run note's `Skills used` list before calendar review starts.
2. If Google Calendar is available, use availability lookup for only the requested scan window and calendar IDs needed, usually `primary`.
3. Prefer busy/free windows. Do not read event details unless the user explicitly asks.
4. If no calendar context is available, write that calendar review was skipped because no availability context was provided.
5. If calendar context is available, compare candidate event windows against availability.
6. Classify each relevant event as:
   - Open
   - Tight
   - Conflict
7. Adjust practicality and caveats using the scoring rubric.
8. Replace the run note's `Calendar Review` placeholder with concise availability notes.
9. Do not record raw calendar event titles, descriptions, attendees, locations, account data, or private notes.

## Output Shape

```md
## Calendar Review

- Event title: Open/Tight/Conflict.
  - Practical effect:
  - Caveat to show:
```

## Rule

Calendar review should influence ranking and caveats, but it should not expose private calendar details in the final shortlist or run note.

## Output

When invoked, explicitly say: "[Using event-scanner-calendar-review skill]"
