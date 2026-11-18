# Spec 03 — Days, Items, and Scheduling

**Status:** Proposed for design  
**Requirements:** REQ-DAY-001..005, REQ-ITEM-001..009; AC-001, AC-005

## Objective

Specify day editing, all item types, quick-add/edit behavior, and moving/reordering items between a day and the trip's unscheduled list.

## Day behavior

- Generated trip days support title, location label, notes, and a free/roaming-day toggle.
- Free/roaming days count as planned time and remain visible even with no scheduled items.
- Items can be unassigned (unscheduled) or assigned to one day. Day order is persisted.
- Mobile users can reorder and move items using explicit controls; drag-and-drop is not required.

## Item behavior

- Types: transport, stay, attraction/activity, food, other.
- Statuses: idea, shortlisted, booked, done, cancelled.
- Common fields: title, status, applicable date/time, optional end date/time, location/area, estimated/actual cost, currency, notes, optional link.
- Transport fields: mode, origin, destination; optional carrier, service number, booking reference.
- Stay fields: check-in, check-out, derived nights, optional address and booking reference.
- Booking fields: reference and cancellation deadline.
- Quick-add form adapts to type and focuses on common fields; advanced/optional fields remain accessible without blocking save.
- Edit, duplicate, and delete actions operate on one item. Duplicates receive new IDs and no invalid slot/day references.
- A stay is associated with both its check-in and check-out dates for display. Its complete cost is attributed to check-in date in the Costs view.

## Validation

- Required title and type must be present.
- If an end time is entered, it must be valid relative to its start time under the date/time rules.
- A stay requires check-in and check-out; checkout must be after check-in. Nights are derived, never manually edited.
- Optional fields may be blank. Saving is not blocked by advisory schedule warnings.

## Acceptance checks

- Add, edit, duplicate, and delete one item of each type.
- Verify type-specific fields persist and appear in relevant item details.
- Assign, move, reorder, and unschedule items using phone-sized controls.
- Confirm free day remains visible with no items.
- Confirm stay displays on check-in and checkout dates and has correct derived nights.
- Conduct a timed quick-add usability walkthrough; the common item flow completes in under 30 seconds.

## Design decisions

- Type-specific quick-add defaults and which fields are required for each type.
- Ordering for untimed items and items with identical start times.
- Whether one item can span multiple days other than stays (current requirement does not define this).

## Dependencies

Specs 00, 01, and 02.
