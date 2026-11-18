# DIY Trip Planner — MVP Requirements

**Status:** Refined requirements for spec and design work  
**Version:** 1.0  
**Priority:** Every requirement in this MVP document is in scope unless explicitly labelled optional. Stable IDs are intended for design specs, implementation tasks, and acceptance checks.

## 1. Purpose and scope

### 1.1 Goal

REQ-GOAL-001. The app shall let a person plan a DIY trip in one structured place, including transport, stays, attractions and activities, food, and free or roaming days.

REQ-GOAL-002. The app shall support manual entry and organisation of information researched elsewhere. AI features and travel/booking integrations are outside the MVP.

REQ-GOAL-003. The app shall be useful to the author for planning a real family trip and may be used by other people at no charge.

### 1.2 MVP boundaries

REQ-SCOPE-001. The MVP shall be a responsive web app that works on mobile and desktop browsers.

REQ-SCOPE-002. The MVP shall have no accounts, backend, cloud sync, collaboration, or third-party travel data APIs.

REQ-SCOPE-003. Trip data shall remain in the browser on the device where it was entered. The app shall not send trip data to the hosting service or another service.

REQ-SCOPE-004. The app shall be usable offline after its first successful load.

REQ-SCOPE-005. The MVP shall not provide JSON, CSV, or Excel trip-data export or import. Printing/saving the read-only itinerary as PDF is the only export function in scope; a PDF is not a restorable trip backup.

REQ-SCOPE-006. Sharing shall mean printing/saving the read-only itinerary as PDF using the browser. The MVP shall not create a hosted share link or standalone HTML export.

## 2. Trips and trip list

REQ-TRIP-001. A user shall be able to create a trip with a name, start date, end date, home currency, and optional total budget.

REQ-TRIP-002. A user shall be able to edit, duplicate, and delete a trip. The app shall ask for confirmation before deleting a trip.

REQ-TRIP-003. A user shall be able to keep multiple trips in the browser.

REQ-TRIP-004. The trip list shall show each trip's name, date range, and a concise status summary.

REQ-TRIP-005. When a trip's dates change, the app shall identify days/items outside the new range and ask the user how to proceed. It shall not silently shift or delete items.

REQ-TRIP-006. Trip days shall be generated for every calendar date from the start date through the end date, inclusive.

## 3. Trip workspace and days

REQ-VIEW-001. Opening a trip shall show a workspace with Timeline, Costs, Undecided, and Bookings views.

REQ-DAY-001. Each generated day shall support a title, a location label, and free-text notes.

REQ-DAY-002. A day shall be markable as a free or roaming day. It shall count as planned time and shall appear in the timeline and printed itinerary.

REQ-DAY-003. Each day shall support an ordered list of assigned items. Users shall be able to reorder items and move items between days using controls usable on mobile.

REQ-DAY-004. The trip shall have an unscheduled-items list for items not assigned to a day.

REQ-DAY-005. The trip workspace shall provide one place to view and manage items that have not yet been scheduled.

## 4. Items

REQ-ITEM-001. An item shall belong to one trip and have one of these types: transport, stay, attraction/activity, food, or other.

REQ-ITEM-002. An item shall support a title, type, status, start date/time where applicable, optional end date/time, location/area, estimated cost, actual cost, currency, notes, and optional link.

REQ-ITEM-003. Item status shall be one of: idea, shortlisted, booked, done, or cancelled.

REQ-ITEM-004. A transport item shall support mode (flight, train, bus, car, or other), origin, destination, optional carrier, service/flight number, and booking reference.

REQ-ITEM-005. A stay item shall support check-in date, check-out date, derived number of nights, optional address, and booking reference.

REQ-ITEM-006. A stay shall appear on the timeline/itinerary on its check-in and check-out dates. Its full estimated and actual cost shall be attributed to its check-in date in daily cost totals.

REQ-ITEM-007. Item entry shall use a quick-add form with relevant defaults for the chosen type. A common item shall be addable in under 30 seconds.

REQ-ITEM-008. A user shall be able to edit, duplicate, and delete an item.

REQ-ITEM-009. Booking references and cancellation deadlines shall be available on items. The Bookings view shall show booked items, dates, references, and cancellation deadlines.

## 5. Decision slots and options

REQ-SLOT-001. A user shall be able to create a decision slot for a trip, such as a stay choice or a transport choice.

REQ-SLOT-002. A decision slot shall support multiple candidate items of different item types.

REQ-SLOT-003. A decision slot may be assigned to a day/date range or left unscheduled.

REQ-SLOT-004. A decision slot shall have zero or one chosen option. Choosing an option shall retain the other options and mark them as not chosen.

REQ-SLOT-005. Only the chosen option shall count toward timeline totals, cost totals, and clash checks. A slot with no chosen option shall be identified as undecided.

REQ-SLOT-006. The user shall be able to compare slot options side by side using their common fields, including cost, dates/times, location, notes, and link.

REQ-SLOT-007. Changing the chosen option shall update all views and totals immediately.

REQ-SLOT-008. The Undecided view shall list all slots with no chosen option and shortlisted items that are not chosen.

## 6. Timeline, costs, and bookings

REQ-TIMELINE-001. The Timeline view shall show each trip day and its chosen items in time order. Items without a time shall still appear on their assigned day.

REQ-TIMELINE-002. The Timeline view shall show undecided slots as placeholders on their assigned day/date range, or in the unscheduled area if they have no date.

REQ-COST-001. Each item shall support an estimated cost and actual cost in a selected currency.

REQ-COST-002. Cost entry and display shall use whole-number amounts with no fractional/decimal units.

REQ-COST-003. The user shall be able to set a manual exchange rate for each non-home currency used in a trip. Totals shall be converted to the trip's home currency using the saved rates.

REQ-COST-004. The Costs view shall show estimated and actual totals by item category and by trip day, plus trip budget and remaining budget. Stay costs shall be assigned to the check-in date.

REQ-COST-005. The app shall clearly indicate when the estimated total is greater than the trip budget.

REQ-BOOKING-001. The Bookings view shall list all items with booked status and show their dates, booking references, and cancellation deadlines when present.

## 7. Local time and timezone display

REQ-TIME-001. The app shall use the device's current local timezone for all trip dates and times. It shall not convert an item's time based on its location.

REQ-TIME-002. Whenever a time is displayed, the interface shall explicitly show the applicable timezone using its abbreviation and UTC offset where the browser provides them.

REQ-TIME-003. Trip dates shall be treated as calendar dates in the device's local timezone and shall not shift to a different calendar date due to UTC conversion.

## 8. Checks and warnings

REQ-WARN-001. The app shall warn when two chosen, timed items assigned to the same day have overlapping time ranges.

REQ-WARN-002. Warnings shall be advisory. They shall not block saving or editing.

REQ-WARN-003. A user shall be able to dismiss an individual warning. A dismissed warning shall remain dismissed for the same underlying condition until that condition changes.

## 9. Read-only itinerary and printing

REQ-PRINT-001. The app shall provide a clean, read-only itinerary view for the trip, designed for phone readability.

REQ-PRINT-002. The itinerary shall show day-wise plans, times with explicit timezone, locations, booking references, notes, free/roaming days, and stay check-in/check-out dates.

REQ-PRINT-003. A user shall be able to invoke the browser's print flow from the itinerary view. The print layout shall be clean and readable when printed or saved as PDF.

REQ-PRINT-004. Before printing, the user shall be able to choose whether costs are included in the itinerary.

REQ-PRINT-005. The printed itinerary shall not imply that it can restore or edit trip data.

## 10. Persistence and data integrity

REQ-DATA-001. The app shall save changes automatically to browser storage and retain them after refresh or reopening the app in the same browser profile.

REQ-DATA-002. The app shall display a clear notice that trip data is stored only in this browser/device and can be lost if browser site data is cleared or the user changes device/browser.

REQ-DATA-003. Deleting a trip, slot, or item shall not leave broken references in the remaining trip data.

REQ-DATA-004. Stored trip records shall include a schema version so a future app version can identify and migrate older data.

REQ-DATA-005. The app shall not make network requests containing trip content.

## 11. Quality requirements

REQ-QUAL-001. For a trip with up to 200 items, each primary view shall render in under one second on a mid-range phone under normal conditions.

REQ-QUAL-002. The core workflow—create a trip, add items, create a decision slot, compare options, and choose an option—shall be usable without instructions.

REQ-QUAL-003. The interface shall be keyboard navigable, use sufficient colour contrast, and never communicate status by colour alone.

REQ-QUAL-004. The app shall support current versions of Chrome, Safari, Firefox, and Edge on desktop and mobile.

## 12. Acceptance scenarios

AC-001. A user creates a trip, adds an item of every type, and sees the items on the correct trip days.

AC-002. A user creates a slot with three options of different types, leaves it unscheduled, compares the options, chooses one, changes the choice, and sees the timeline and cost totals update.

AC-003. A user enters costs in two currencies, sets an exchange rate, and sees estimated, actual, budget, and remaining totals in the home currency.

AC-004. Two overlapping chosen items on one day produce a dismissible warning that does not block saving.

AC-005. A stay appears on its check-in and check-out dates and its full cost appears against the check-in date.

AC-006. The user prints/saves the read-only itinerary as PDF. The result is readable on a phone and includes free/roaming days and timezone labels.

AC-007. After refresh or reopening the same browser profile, saved trip data remains available. The app explains that it has no cross-device sync or restorable data export.

AC-008. Every primary view meets the performance, accessibility, and browser support requirements above.

## 13. Explicitly out of scope for MVP

SCOPE-OUT-001. AI-assisted entry, AI grouping, AI-generated itineraries, or AI warnings.

SCOPE-OUT-002. Accounts, cloud sync, cross-device access, collaboration, comments, voting, or hosted share links.

SCOPE-OUT-003. Live travel prices, availability, transit times, opening hours, booking, or affiliate links.

SCOPE-OUT-004. JSON, CSV, or Excel data import/export; spreadsheet templates; or standalone HTML itinerary export.

SCOPE-OUT-005. Map view, reusable trip templates, per-category budgets, traveller counts/per-person costing, custom comparison attributes, pros/cons, configurable schedule warnings, stay continuity checks, and transfer-buffer checks.

## 14. Deferred spec decisions

These are not blockers to the product scope. Record a design decision before implementation of the affected behavior.

DEC-001. Confirm the storage mechanism and key/schema migration strategy.

DEC-002. Define how the app handles a device timezone change after trips have been entered; all displayed values should continue to follow the current device-local-time requirement.

DEC-003. Define whether costs are included by default in the print view; the user must be able to choose whether costs appear.
