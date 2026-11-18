# DIY Trip Planner — MVP Specs

These specs turn the numbered MVP requirements into design/build units. Each file is scoped so it can be designed and implemented in sequence; stable requirement IDs remain the source of truth for scope.

## Recommended sequence

| Order | Spec | Primary scope | Depends on |
|---|---|---|---|
| 00 | [Technical foundation](00-technical-foundation.md) | Vite/React/TypeScript, GitHub Pages, offline shell, baseline architecture | — |
| 01 | [Domain model and persistence](01-domain-model-and-persistence.md) | Entities, localStorage, schema versioning, data safety | 00 |
| 02 | [Trip list and trip management](02-trip-management.md) | Trip CRUD, dates, trip list, date edits | 01 |
| 03 | [Days, items, and scheduling](03-days-items-and-scheduling.md) | Days, item forms/types, unscheduled list, move/reorder | 01, 02 |
| 04 | [Decision slots](04-decision-slots.md) | Candidate options, comparison, choose/undecided state | 03 |
| 05 | [Workspace, timeline, and bookings](05-workspace-timeline-bookings.md) | Workspace navigation and read views | 02, 03, 04 |
| 06 | [Costs and currency](06-costs-and-currency.md) | Whole-number cost entry, exchange rates, budget totals | 03, 04 |
| 07 | [Local time and warnings](07-local-time-and-warnings.md) | Device-local date/time display and clash warnings | 03, 04 |
| 08 | [Printable itinerary](08-printable-itinerary.md) | Read-only itinerary and browser print/PDF | 03, 04, 07 |

The design document for the first spec is [Design 00 — Technical Foundation](../design/00-technical-foundation-design.md).

Implementation planning for Design 00 is tracked as separate files in [SDD/tasks](../tasks/00-README.md).

## Traceability

| Requirement group | Covered by |
|---|---|
| REQ-GOAL, REQ-SCOPE, REQ-QUAL | 00 |
| REQ-DATA | 01 |
| REQ-TRIP | 02 |
| REQ-DAY, REQ-ITEM | 03 |
| REQ-SLOT | 04 |
| REQ-VIEW, REQ-TIMELINE, REQ-BOOKING | 05 |
| REQ-COST | 06 |
| REQ-TIME, REQ-WARN | 07 |
| REQ-PRINT | 08 |
| AC-001, AC-005 | 02, 03, 05, 06, 08 |
| AC-002 | 04, 05, 06 |
| AC-003 | 06 |
| AC-004 | 07 |
| AC-006 | 08 |
| AC-007 | 01 |
| AC-008 | 00 and applicable feature specs |

## Spec conventions

- A requirement ID in a spec means the spec defines its design contract; it does not change requirement scope.
- Any unresolved choice is explicitly marked **Design decision**. Resolve it in design before implementing the dependent behavior.
- Out-of-scope features remain excluded even if a related entity has optional fields.
- Keep all views derived from the same persisted records; do not add duplicate sources of truth.
