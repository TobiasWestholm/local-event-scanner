# Operating Model

This runtime should feel native to your coding agent: mostly documents, skills, checklists, and run notes, with code added only when it clearly reduces repeated friction.

## Boot Sequence

Read these files before every scan:

1. `docs/privacy-and-access.md` — storage and access rules
2. `preferences/sources.md` — primary sources per location; resolve scan location here
3. `preferences/taste-profile.md` — interests, dealbreakers, and surprise signals
4. `preferences/scoring-rubric.md` — ranking factors, labels, and explanation requirements
5. `preferences/availability-rules.md` — geography, practicality caveats, calendar privacy

## Skill Pipeline

Invoke these repo-local skills in order for every scan:

1. `event-scanner-run` — creates the run note before any other work starts
2. `event-scanner-discovery` — finds candidate events from primary and public sources
3. `event-scanner-scoring` — scores and ranks candidates using the rubric
4. `event-scanner-calendar-review` — checks calendar practicality
5. `event-scanner-shortlist-review` — produces the final ranked shortlist in the run note

Each skill logs itself to the run note when it starts. A skipped skill is a defect — call it out and repair it before finishing.

For adding a specific event to Google Calendar, invoke `event-scanner-add-to-calendar` only when the user explicitly asks.

## Quick Reference

- **Default location:** Copenhagen area
- **Standard locations:** Copenhagen area, Malmö
- **Scan location rule:** use the user's requested location; if none given, use the default
- **Scoring labels:** Strong pick / Worth considering / Maybe / Skip for now
- **Near-term (≤14 days):** prefer short, free/cheap, low-commitment events
- **Farther-future:** allow longer, higher-commitment events when fit is strong
- **Dealbreakers (always filter out):** fully booked, women/non-binary only, student-only, under-30-only, strongly misaligned with vegan/feminist/consent-aware values

## Runtime Boundary

Operate inside this runtime package.

Read runtime instructions, preferences, repo-local skills, and run notes from this folder. Write runtime outputs inside this folder. Treat files outside this package as project-building files unless the user explicitly asks to modify the project.

## Running An Event Scan

1. Read the relevant preferences in `preferences/`.
2. Invoke `event-scanner-run`, which creates an empty run note in `runs/`.
3. Each runtime skill logs itself in that run note when it starts.
4. Resolve the requested location from `preferences/sources.md`; if the user did not specify a location, use the configured default location.
5. Use user-listed priority sources for the requested location first, when they exist.
6. Discover candidate events and preserve source links.
7. Normalize candidates into comparable notes.
8. Score candidates using `preferences/scoring-rubric.md`.
9. Apply calendar-aware review when calendar context is available or explicitly provided.
10. Populate the existing run note with the ranked shortlist, reasons, caveats, source links, and next actions.
11. Remove temporary candidate, scoring, and calendar-review sections before finishing the run note.
12. Do not create the run note at the end of the scan.

## Source Handling

- User-listed sources have priority.
- Standard locations and the default location are defined in `preferences/sources.md`.
- If the user does not specify a location, use the default location.
- If the requested location has no primary sources, explore public event sources for that location and keep source links.
- Newly discovered sources may be used for exploration or verification, but normal scans should not propose or log new primary sources.
- Suggest new primary sources only in chat after the user explicitly adds an event to Google Calendar and the event came from a non-primary source.
- Prefer public event pages, venue listings, newsletters, ticketing pages, and other public event listings.

## Recommendation Behavior

- Rank events by fit, interest, novelty, practicality, and confidence.
- Apply date-window practicality: for the next 14 days, prefer shorter, cheaper, lower-friction events; for farther-future scans, allow longer and more expensive events when the fit is strong.
- Keep explanations human-readable.
- Prefer a compact shortlist over exhaustive coverage.
- Include caveats instead of silently dropping borderline events.

## Calendar-Aware Review

Calendar context is optional and manual-first. Use it only to judge practicality for shortlisted candidates.

Preferred access path:

- Use Google Calendar availability lookup for the requested scan window.
- Prefer busy/free windows over reading event details.
- Query only the calendar and time range needed for the scan.

Allowed calendar signals:

- Busy/free status for the requested event windows.
- Broad conflict severity, such as open, tight, or conflict.
- Practical buffers before or after an event.
- User-provided availability constraints.

Do not store raw calendar event titles, attendees, locations, descriptions, private notes, or account data in run notes. Record only availability summaries and recommendation caveats.

## Calendar Event Creation

Calendar event creation is request-only. Use it only when the user explicitly asks to add a specific suggested event to Google Calendar.

Required fields:

- Title.
- Time and date.
- Address, or link if online.
- Description.

If any required field is missing or ambiguous, ask for the missing detail before creating the calendar event. Do not infer uncertain times, locations, or online links.
After adding an event to the calendar, always perform the post-add learning check in `event-scanner-add-to-calendar`. Send the result in chat only. Do not write these suggestions into run notes.

## Privacy Behavior

- Store only event metadata, source links, run summaries, and explicit preference choices.
- Store only calendar availability summaries, not raw calendar event details.
- Do not store raw private data.
- Do not log liked/disliked events unless the user asks.
- Perform source and taste-profile learning checks only after `event-scanner-add-to-calendar` is used, and only as a chat message. Apply changes only after approval.

## Low-Code Boundary

Use docs and skills first. Add code only when:

- Repeated parsing becomes tedious.
- Dedupe becomes unreliable.
- Validation needs deterministic checks.
- Formatting run outputs by hand becomes annoying.

When adding code, keep it small, boring, and subordinate to the runtime docs.
