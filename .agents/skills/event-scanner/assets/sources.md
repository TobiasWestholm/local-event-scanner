# Event Sources

User-listed sources are primary for their standard location. The agent may use other public sources for verification or one-off discovery, but should not add or log new primary-source suggestions during normal scans.

## Standard Locations

The scanner can support any number of user-defined standard locations. There must always be at least one standard location.

The user defines standard locations and provides primary sources for them. Do not invent primary sources for a standard location.

Default location: Copenhagen area.

Current standard locations:

- Copenhagen area.
- Malmö.

If the user does not specify a location when asking for suggestions, use the default location.

If the requested location has primary sources below, check those first. If the requested location has no primary sources, or is not a standard location yet, explore public event sources for that location and keep source links for every candidate.

## Copenhagen Area

Primary sources:

| Name | URL | Type | Notes |
| --- | --- | --- | --- |
| VisitCopenhagen Events | https://www.visitcopenhagen.com/explore/events-cid58/events-cid59?sort=DATE | Public event listing | Broad Copenhagen events; good first pass for culture, seasonal events, and visitor-friendly listings. |
| Facebook Events | https://www.facebook.com/events/ | Social event platform | Useful for community, venue, nightlife, pop-up, and smaller local events. Access and search quality may depend on login/session state. |
| Eventbrite Copenhagen | https://www.eventbrite.dk/d/denmark--copenhagen/events/ | Ticketing and event listing | Good for workshops, talks, parties, food/drink, markets, and paid/free registration events. |
| University of Copenhagen / DIKU Events | https://di.ku.dk/english/events/ | University event calendar | Useful for AI, computer science, science, sustainability, public talks, workshops, and research-adjacent events. |
| Oplevelser i Kobenhavn | https://oplevelser-i-koebenhavn.dk/ | Local event and experience listing | Useful Danish-language Copenhagen source for activities, experiences, and local happenings. |
| Resident Advisor Copenhagen | https://es.ra.co/events/dk/copenhagen | Music and nightlife listing | Strong source for electronic music, club nights, DJs, and late-night events. |
| Meetup | https://www.meetup.com/ | Community event platform | Useful for talks, learning, tech, hobbies, language exchange, and recurring community events. Search for Copenhagen-specific groups/events. |
| Applied Futures | https://appliedfutures.io/#upcoming | AI event listing | Copenhagen-focused AI events; check first for any AI-related scan in the Copenhagen area. |

## Malmö

Primary sources:

| Name | URL | Type | Notes |
| --- | --- | --- | --- |
| Malmö Events | https://malmo.se/evenemang | Municipal event listing | Broad Malmö events; good first pass for public culture, local happenings, family-friendly events, and city-run programming. |
| Meetup | https://www.meetup.com/ | Community event platform | Useful for talks, learning, tech, hobbies, language exchange, and recurring community events. Search for Malmö-specific groups/events. |

## Source Rules

- Resolve the requested location before discovery starts.
- Check primary sources for the requested location first when they exist.
- If no location is requested, use the default location.
- Preserve source links for every candidate event.
- Prefer public pages, public event listings, venue listings, newsletters, and ticketing pages.
- Check for new primary-source suggestions only after `steps/step-5-add-to-calendar.md` is followed. Send suggestions in chat only, and only when the added event came from a source not covered here.
