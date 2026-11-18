# Spec 07 — Local Time and Warnings

**Status:** Proposed for design  
**Requirements:** REQ-TIME-001..003, REQ-WARN-001..003; AC-004

## Objective

Define local calendar/time handling and advisory overlap warnings consistently across forms and views.

## Local time contract

- Treat trip dates as date-only calendar values (`YYYY-MM-DD`); do not round-trip them through UTC timestamps.
- Store entered event date/time as local wall-clock date/time values. Do not convert times based on item location.
- Every displayed time includes the device's current timezone abbreviation and UTC offset where available.
- A date without a time remains date-only and must not shift when rendered.
- If browser APIs cannot produce an abbreviation, show the timezone identifier or UTC offset so the timezone remains explicit.

## Overlap checks

- Compare chosen, timed items assigned to the same trip day.
- An overlap exists when the intervals intersect with positive duration. Items without an end time need a design-defined default duration or must be excluded until an end is entered.
- Ignore unchosen slot candidates and cancelled items for clash checks.
- Show warnings adjacent to the affected day/items and in a discoverable warning summary.
- Warnings are advisory and do not block save/edit.
- Dismissal is scoped to a stable warning condition. If either interval changes so the overlap condition changes, show the warning again.

## Acceptance checks

- Dates remain the same calendar date through save/reload under non-UTC device timezone.
- Every rendered time shows an explicit timezone marker and offset.
- Detect exact overlap, partial overlap, adjacency without overlap, no overlap, and missing end time.
- Ignore unchosen options; report chosen item clashes.
- Dismiss a warning, confirm it stays dismissed while unchanged, then edit an interval and confirm applicable warning reappears.
- Save/edit remains available when a warning is present.

## Design decisions

- Device timezone change behavior for existing local wall-clock times.
- Clash rule for items with missing end times and cross-midnight intervals.
- Exact warning placement, wording, and dismissal lifetime.

## Dependencies

Specs 00–04 and 01 for persisted warning dismissal.
