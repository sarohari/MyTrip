# Spec 01 — Domain Model and Persistence

**Status:** Proposed for design  
**Requirements:** REQ-SCOPE-002..005, REQ-DATA-001..005; AC-007

## Objective

Define the canonical trip records and safe local persistence contract used by every view and feature.

## Data model contract

Design a versioned data envelope containing trips. Each trip owns its days, decision slots, and items, either nested or referenced by stable IDs. At minimum, model:

- **Trip:** ID, name, start/end date, home currency, optional budget, exchange rates, created/updated timestamps.
- **Day:** ID, date-only value, title, location label, free/roaming flag, notes, item ordering.
- **Slot:** ID, title, optional day/date range, chosen item ID or null, optional comparison metadata only if supported by the requirements.
- **Item:** ID, optional slot/day assignment, type, status, title, local date/time fields, location, estimated/actual whole-number costs and currency codes, notes/link, booking fields, and type-specific transport/stay fields.
- **Dismissed warning state:** stable warning identity and the data signature/condition it applies to, so a changed condition can be shown again.

Use stable IDs. Derived values such as stay nights, converted totals, timeline ordering, and warnings should be computed from canonical records rather than saved as a second source of truth.

## Persistence contract

1. Use browser `localStorage`; isolate storage access behind a persistence module.
2. Store a schema version and validate records when reading them.
3. Prefer one versioned record per trip plus a small trip index. Writes to one trip should not rewrite unrelated trips.
4. Save each successful user edit automatically. Expose a save/error state if storage is unavailable or a write fails.
5. Add explicit version-to-version migration functions before changing stored record shapes.
6. Deleting a trip removes its records; deleting a slot or item removes or repairs references atomically at the application-action boundary.
7. Do not implement trip-data import/export, JSON backup, or remote synchronization.
8. Explain that data stays in this browser profile and may be lost if site data is cleared or the user changes browser/device.

## Acceptance checks

- Create, edit, and reload multiple trips; each remains isolated.
- Simulate invalid stored JSON, an unknown schema version, and storage write failure; show a recoverable message and do not silently overwrite valid data.
- Delete a trip, slot, and item and confirm no dangling references remain.
- Confirm no persisted trip fields are sent in network requests.

## Design decisions

- Exact record envelope/key names and migration policy.
- Whether invalid records can be repaired, quarantined, or only reported.
- Save/error indicator behavior and recovery copy.
- Warning dismissal identity/signature behavior.

## Dependencies

Spec 00.
