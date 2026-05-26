# Event Scanner Runtime — Claude Code Instructions

This folder is a self-contained event scanner runtime. Your job is to discover, score, and shortlist real events that fit the user's taste profile. Read this file first, then follow the boot sequence below before doing any event work.

## Boot Sequence

Read these files before every scan. They are the authoritative runtime state:

1. [`docs/operating-model.md`](docs/operating-model.md) — how scans work end to end
2. [`docs/privacy-and-access.md`](docs/privacy-and-access.md) — what you may and may not store
3. [`preferences/sources.md`](preferences/sources.md) — primary sources per location; resolve scan location here
4. [`preferences/taste-profile.md`](preferences/taste-profile.md) — interests, dealbreakers, and surprise signals
5. [`preferences/scoring-rubric.md`](preferences/scoring-rubric.md) — ranking factors, labels, and explanation requirements
6. [`preferences/availability-rules.md`](preferences/availability-rules.md) — geography, practicality caveats, calendar privacy

Do not skip or defer any of these reads. They are small files. Read them all before discovery starts.

## Mandatory Skill Pipeline

Every scan must invoke these repo-local skills via the Skill tool, in this exact order:

1. `event-scanner-run` — creates the run note in `runs/` before any other work starts
2. `event-scanner-discovery` — finds candidate events from primary and public sources
3. `event-scanner-scoring` — scores and ranks candidates using the rubric
4. `event-scanner-calendar-review` — checks calendar practicality (uses availability only, not event details)
5. `event-scanner-shortlist-review` — produces the final ranked shortlist in the run note

Each skill logs itself to the run note when it starts. If a skill is skipped, that is a defect — call it out and repair it before finishing.

For adding a specific event to Google Calendar, invoke the `event-scanner-add-to-calendar` skill only when the user explicitly asks.

## Quick Reference

**Default location:** Copenhagen area  
**Standard locations:** Copenhagen area, Malmö  
**Scan location rule:** Use the user's requested location. If none given, use Copenhagen area.

**Primary sources are defined in [`preferences/sources.md`](preferences/sources.md).** Check them first for any standard location before using public sources. Do not propose new primary sources during normal scans.

**Scoring labels:** Strong pick / Worth considering / Maybe / Skip for now  
**Near-term window bias (≤14 days):** prefer short, free/cheap, low-commitment events  
**Farther-future bias:** allow longer, higher-commitment, travel-adjacent events when fit is strong

**Dealbreakers (always filter out):** fully booked, women/non-binary only, student-only, under-30-only, strongly misaligned with vegan/feminist/consent-aware values

## Privacy Rules

- Store only: public event metadata, source links, run summaries, calendar availability summaries (open/tight/conflict)
- Never store: raw calendar event titles, attendees, descriptions, or private notes
- Never log liked/disliked events unless the user explicitly asks
- Never apply taste-profile or source updates during a scan — only after `event-scanner-add-to-calendar` is used, and only in chat with user approval
- Calendar writes only when the user explicitly asks to add a specific suggested event

## Runtime Boundary

Read and write inside this runtime folder only. Files outside this package are project-implementation files — do not modify them unless the user explicitly asks to change the project itself.

Add code only when repeated manual work becomes painful or brittle. Prefer docs, skills, and run notes over scripts.

## Run Notes

Run notes live in [`runs/`](runs/). The `event-scanner-run` skill creates the note before discovery starts. Each subsequent skill appends itself. The final run note contains the ranked shortlist, reasons, caveats, source links, and next actions — with all temporary candidate and scoring sections removed before finishing.

Never create the run note at the end of a scan. It must exist before discovery starts.
