# Spec 02 — Trip List and Trip Management

**Status:** Proposed for design  
**Requirements:** REQ-TRIP-001..006

## Objective

Specify trip creation, editing, duplication, deletion, and the trip list, including date-range changes.

## User flows

1. From the trip list, create a trip by entering name, start date, end date, home currency, and optional total budget.
2. Open a trip to its workspace.
3. Edit trip details; duplicate a trip as a separate trip with new IDs; delete after explicit confirmation.
4. Change trip dates and review days/items that are now outside the range before committing the change.

## Behavior rules

- Start date and end date are required; end date cannot precede start date.
- Generate one day for each local calendar date in the inclusive range.
- A trip list row/card shows name, date range, and a concise status summary. Define the summary in design (suggested: booked item count plus undecided slot count).
- Deletion confirmation identifies the trip by name. Cancelling confirmation leaves all data unchanged.
- Date edits never silently delete, move, or change item dates. Present affected records and explicit options to retain outside-range items or adjust/remove them.
- Duplicate operation creates independent trip/day/slot/item IDs and references. It must not modify the original trip.

## Acceptance checks

- Create trips with and without a budget; reject invalid date order.
- Confirm generated dates include both endpoints and remain calendar dates in the device-local timezone.
- Edit, duplicate, and delete a trip; verify duplicate changes do not affect original.
- Shorten/extend dates with assigned, unscheduled, and multi-day stay items; review the chosen date-change behavior before saving.

## Design decisions

- Exact trip status summary.
- Date-change options and treatment of days versus items outside range.
- Whether trip name is required to be non-empty after trimming.

## Dependencies

Specs 00 and 01.
