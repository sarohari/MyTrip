# Spec 00 — Technical Foundation

**Status:** Proposed for design approval  
**Source:** [MVP Technical Recommendation](../design/DIY%20Trip%20Planner%20%E2%80%93%20MVP%20Technical%20Recommendation.md)  
**Requirements:** REQ-GOAL-001..003, REQ-SCOPE-001..006, REQ-QUAL-001..004; AC-008

## Objective

Define the static app foundation, development/build choices, hosting shape, responsive/accessibility baseline, and offline behavior before feature specs are implemented.

## Design contract

1. Build a client-side web app using Vite, React, and TypeScript.
2. Deploy static build output to GitHub Pages. There is no application server, API, account service, hosted database, or trip-data upload.
3. Use hash-based client routing so repository subpath hosting does not require server rewrites.
4. Use plain CSS or CSS modules and semantic HTML. Add a UI framework only if the design shows a concrete need.
5. The app shall be responsive and usable at phone and desktop widths. Core actions shall be reachable with keyboard input and status shall not be conveyed by colour alone.
6. Register a service worker that precaches the static app shell. Once a user has loaded the app successfully, the cached shell shall open offline. No remote travel content is cached.
7. PWA installation prompts and installability are not MVP requirements.
8. GitHub Pages serves only app assets. Trip content shall not be placed in URLs, telemetry, analytics, cookies, or network requests.
9. Use the default `github.io` URL initially unless a custom domain is selected separately.

## Quality constraints

- Each primary view shall render in under one second for a trip with up to 200 items on a mid-range phone under normal conditions.
- Support current Chrome, Safari, Firefox, and Edge on desktop and mobile.
- Keep runtime dependencies small and avoid server-side rendering frameworks.

## Acceptance checks

- Production build contains static assets and runs from the configured GitHub Pages base path.
- Navigation works on direct page refresh for all hash routes.
- After a successful online load, the app shell opens with network access disabled.
- Verify keyboard access, visible focus, readable contrast, and non-colour status cues in each feature spec's screens.
- Confirm no requests include trip content.

## Dependencies and decisions

- Depends on a selected GitHub repository and Pages configuration. Confirm source visibility and plan eligibility before deployment.
- Design decision: choose minimal CSS organization and service-worker implementation (native or small Vite plugin).
- Design decision: define the test device/browser set for the performance and mobile requirements.

## Out of scope

Backend services, server rendering, user accounts, analytics, APIs, map providers, install prompts, and custom domain purchase.
