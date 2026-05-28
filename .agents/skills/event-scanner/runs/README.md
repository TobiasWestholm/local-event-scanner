# Run Notes

Store short summaries of useful event scans here.

## Naming

Use this pattern:

```text
YYYY-MM-DD-topic.md
```

Examples:

```text
2026-05-07-copenhagen-manual-v0.md
2026-05-14-weekend-scan.md
```

## Final Run Note Shape

```md
# Run: YYYY-MM-DD Topic

## Context

- Geography:
- Window:
- Sources checked:
- Skills used:
  -

## Ranked Shortlist

1. Event title
   - Label:
   - Why it fits:
   - Caveats:
   - Next action:
   - Source:
   - Confidence:

## Privacy Check

- No raw private account or calendar details stored.
```

## Update Rule

`event-scanner` creates the working run note before discovery starts. During the run, skills may use temporary `Candidate Events`, `Scored Candidates`, and `Calendar Review` sections as working areas. Each skill adds itself to `Skills used` when it starts.

Before finishing, `event-scanner-shortlist-review` removes those temporary sections and keeps only:

- `Context`
- `Ranked Shortlist`
- `Privacy Check`
