# Local event finder

A coding agent plugin for discovering, scoring, and shortlisting events from user-provided preferences.

Supports optional calendar integration.

## Setup

Open this folder in your coding agent and copy the prompt below. Replace the FILL IN YOUR PREFERENCE text with your actual preferences before sending it.

```text
Set up this event scanner runtime for me.

First create my local preference files:

cp preferences/taste-profile.example.md preferences/taste-profile.md
cp preferences/sources.example.md preferences/sources.md

Then replace the <PLACEHOLDER> blocks in the copied files with my preferences below.

Interests to add to my taste profile:
- (FILL IN YOUR PREFERENCE, eg ceramics, techno, traveling, italian wines, DIY, ...)

Dealbreakers to add:
- (FILL IN YOUR PREFERENCE, eg age restrictions, audience restrictions, fully booked events, ...)

Primary sources for standard locations:

Default location: (FILL IN YOUR PREFERENCE: eg your home city)
- (Optional: FILL IN YOUR PREFERENCE, list of sources where you usually find good local events, preferably URLs)

Optional additional standard location: (FILL IN YOUR PREFERENCE, eg your working location)
- (Optional: FILL IN YOUR PREFERENCE, list of sources where you usually find good local events, preferably URLs)

Optional: install the Calendar tool so the scanner can use calendar availability and add selected events when I explicitly ask.

Optional: create a weekly automation from this runtime folder, running (FILL IN YOUR PREFERENCE, eg "weekly on Mondays at 09:00 AM, my local time zone. Find events for the next week.").
```
