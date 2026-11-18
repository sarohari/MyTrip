# Spec 08 — Printable Itinerary

**Status:** Proposed for design  
**Requirements:** REQ-PRINT-001..005, REQ-DAY-002, REQ-ITEM-006, REQ-TIME-002; AC-006

## Objective

Provide a clean read-only itinerary that can be printed or saved as PDF through the browser, without exposing costs unless the user chooses to include them.

## User flow

1. Open the itinerary from a trip workspace.
2. Review the read-only day-by-day content.
3. Choose whether costs are included.
4. Select Print / Save as PDF to open the browser print dialog.

## Content contract

- Show trip name and date range.
- Show each day in order, including free/roaming days, day title/location, and notes.
- Show chosen items only, with times and explicit timezone, location, notes, and booking references where present.
- Show stay check-in and checkout dates.
- Include costs only according to the visible user choice; do not include costs by default until the default is decided.
- Do not include editing controls in the printed output and do not describe the PDF as a backup or editable copy.
- Undecided slots may be omitted from the share itinerary unless design opts to show them clearly as undecided; do not present an unchosen candidate as booked/chosen.

## Print behavior

- Use a dedicated print stylesheet. Hide app navigation/buttons, preserve readable typography, repeat or preserve day headings where possible, and avoid splitting a single item across pages when practical.
- Use the browser's print flow; do not generate a remote or server-side PDF and do not add a PDF library for MVP.
- The HTML view shall be readable on a phone before printing. Printed/saved output shall be readable on phone PDF viewers.

## Acceptance checks

- Print/save an itinerary containing timed items, untimed items, free days, notes, references, and a stay.
- Verify timezone labels and check-in/check-out presentation.
- Verify costs are absent when excluded and present when explicitly included.
- Verify print layout hides app controls and is legible across pages and on a phone PDF viewer.
- Confirm the PDF is read-only and cannot restore trip data.

## Design decisions

- Default cost inclusion (recommend default off for family sharing).
- Whether undecided slot placeholders belong in the printed itinerary.
- Exact handling for empty days and long notes during page breaks.

## Dependencies

Specs 01–03 and 07.
