# Task 00-06 — Privacy and Dependency Boundaries

**Status:** Ready after 00-01 through 00-05  
**Design:** [Design 00](../design/00-technical-foundation-design.md), sections 8–9  
**Spec:** [Spec 00](../spec/00-technical-foundation.md)  
**Depends on:** [00-01](00-01-initialize-app-foundation.md) through [00-05](00-05-offline-app-shell.md)

## Objective

Establish the static app's privacy boundary and keep external runtime dependencies out of the MVP foundation.

## Work

- Review dependencies and remove packages not required by the approved design.
- Confirm no analytics, third-party scripts, remote fonts, map services, API clients, or telemetry are configured.
- Confirm route helpers accept only route identifiers and never serialize trip content.
- Establish safe rendering conventions for user-entered strings (render as text, never HTML).
- Establish safe external-link behavior (`noopener`, `noreferrer`) for user-provided links.
- Confirm the app does not persist trip data in cookies, URLs, or the clipboard.

## Acceptance criteria

- Runtime dependency review matches the approved design.
- Browser network inspection shows no trip content is transmitted.
- User-provided text is rendered as text.
- External links opened in a new context use safe opener/referrer settings.
- No app analytics or third-party runtime scripts are present.

## Not included

Feature-specific storage serialization and validation; these belong to Spec 01.
