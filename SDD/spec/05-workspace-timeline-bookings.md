# Spec 05 — Workspace, Timeline, and Bookings

**Status:** Proposed for design  
**Requirements:** REQ-VIEW-001, REQ-TIMELINE-001..002, REQ-BOOKING-001; AC-001, AC-002

## Objective

Define the trip workspace and read views that present the canonical records: Timeline, Costs, Undecided, and Bookings.

## Navigation

- Opening a trip enters its workspace and presents named navigation to Timeline, Costs, Undecided, and Bookings.
- Views read from the same records and derived selectors; editing an item/slot is reflected in every view after save.
- Workspace includes an accessible return path to the trip list.

## Timeline

- Show every trip day in date order, including empty/free days.
- Show chosen items in chronological order. Untimed items appear after timed entries unless design selects another stable order.
- Show dated undecided slots as placeholders. Show undated items and slots in an unscheduled section.
- For a stay, show check-in and checkout dates; avoid rendering duplicate cost entries for the stay.
- Show concise item summaries with type/status cues and a direct edit/open action.

## Undecided view

- List slots with no chosen option and shortlisted items that are not chosen.
- Provide a route/action to compare candidates or schedule an item.

## Bookings view

- Include items whose status is booked.
- Show booking reference, dates/times, type, and cancellation deadline when present.
- Use explicit empty state when no booked items exist.

## Acceptance checks

- Navigate among all four views on phone and desktop.
- Change a chosen option and verify Timeline and Undecided reflect it immediately.
- Verify timeline ordering, undated items, free days, and placeholders.
- Verify Bookings includes only booked items and optional booking fields display correctly.

## Design decisions

- Workspace navigation pattern and mobile navigation treatment.
- Exact content of the trip list status summary.
- Whether booked options in an undecided slot appear in Bookings (suggestion: include only if item status is booked, while retaining undecided state in the Undecided view).

## Dependencies

Specs 01–04 and 07 for time labels.
