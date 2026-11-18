# Spec 04 — Decision Slots

**Status:** Proposed for design  
**Requirements:** REQ-SLOT-001..008; AC-002

## Objective

Specify how a user gathers alternatives, compares them, and chooses at most one candidate for a trip decision.

## Behavior contract

1. A slot has a title, optional day/date range, candidate items, and zero or one chosen item.
2. Candidate items may have different types. The comparison shows common fields together and type-specific fields where available; missing fields display consistently as unavailable/blank.
3. A slot may have no date and appears in the unscheduled area.
4. Choosing an option updates the slot's chosen item reference. Other candidates remain stored and visible as unchosen; do not add an invented item status for this relationship.
5. An undecided slot has no chosen item. It appears in the Undecided view and as a timeline placeholder when dated.
6. Only the chosen item contributes to timeline totals, cost totals, and overlap checks. Unchosen slot candidates remain available for comparison but are excluded from those calculations.
7. Changing a choice refreshes dependent views and calculations immediately from canonical data.
8. An item belongs to at most one decision slot. Removing a chosen candidate clears the choice and returns the slot to undecided.

## Acceptance checks

- Create a slot with three candidates of different types and compare shared fields.
- Leave the slot undated and undecided; verify it appears under unscheduled/undecided.
- Assign it a date; verify timeline placeholder.
- Choose, change, and clear the choice; verify other candidates remain and dependent views/totals update.
- Confirm unchosen candidate costs and times do not affect totals or clash warnings.

## Design decisions

- Candidate selection flow: create item inside slot or attach an existing item.
- How side-by-side comparison adapts on narrow screens (suggested: stacked option cards with aligned field labels).
- Whether a chosen item can be moved outside the slot without deleting it.

## Dependencies

Specs 01, 02, and 03.
