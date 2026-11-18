# Task 00-03 — Hash Routing

**Status:** Ready after 00-02  
**Design:** [Design 00](../design/00-technical-foundation-design.md), sections 2 and 4  
**Spec:** [Spec 00](../spec/00-technical-foundation.md)  
**Depends on:** [00-02](00-02-app-shell-and-base-styles.md)

## Objective

Implement the minimal hash router and route helpers for the MVP screen map.

## Work

- Parse/build `#/trips`, `#/trips/new`, and trip routes for Timeline, Costs, Undecided, Bookings, and Itinerary.
- Keep route parsing isolated in `src/app/routes.ts` (or equivalent).
- Listen for hash changes and support browser Back/Forward.
- Render route content without full-document navigation.
- Validate route shape and opaque trip ID presence; render not-found or missing-trip states with a path back to Trips.
- Never include trip content in routes.

## Acceptance criteria

- Each defined route selects the expected placeholder view.
- Back and Forward change the displayed route correctly.
- Refresh retains the selected hash route.
- Unknown route and missing trip render recoverable states.
- URL contains only route names and opaque IDs, no titles, costs, notes, links, or references.
- Routes work when the document is served below a GitHub Pages repository path.

## Not included

Loading real trip records, feature-view implementation, authorization, server routes, or a third-party routing framework.
