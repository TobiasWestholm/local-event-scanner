---
name: event-scanner-run
description: Use whenever the user asks to run, operate, test, or perform the Event Scanner workflow for the default location or another geography. This runtime-scoped entrypoint must apply event discovery, event scoring, and shortlist review.
metadata:
  short-description: Run the event scanner workflow
---

# Event Scanner Run

This is the runtime-scoped entrypoint skill for operating the event scanner.

## Procedure

1. Treat the current directory as the runtime root.
2. Follow the boot sequence in `docs/operating-model.md`.
3. Create a new empty run note in `runs/` before discovery starts.
4. Add `event-scanner-run` to the run note's `Skills used` list immediately.
5. Apply these runtime-scoped repo-local skills in order:
   - `event-scanner-discovery`
   - `event-scanner-scoring`
   - `event-scanner-calendar-review`
   - `event-scanner-shortlist-review`
6. Produce the requested shortlist or runtime output.

The scanner instructions live in this runtime package; do not reach back into the repository root for runtime behavior.

## Run Note Template

Create the run note from this empty template, using a filename like `YYYY-MM-DD-topic.md`:

```md
# Run: YYYY-MM-DD Topic

## Context

- Geography:
- Window:
- Sources checked:
- Skills used:
  -

## Candidate Events

- Pending discovery.

## Scored Candidates

- Pending scoring.

## Calendar Review

- Pending calendar-aware review.

## Ranked Shortlist

- Pending shortlist review.

## Privacy Check

- Pending final review.
```

Pass this run note path through the rest of the scan. Do not wait until the end to create the run note.

## Output

When invoked, explicitly say: "[Using event-scanner-run skill]"
