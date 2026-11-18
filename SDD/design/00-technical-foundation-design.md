# Design 00 — Technical Foundation

**Status:** Draft design for Spec 00  
**Spec:** [00 — Technical Foundation](../spec/00-technical-foundation.md)  
**Stack recommendation:** [MVP Technical Recommendation](DIY%20Trip%20Planner%20%E2%80%93%20MVP%20Technical%20Recommendation.md)

## 1. Design goals

- Ship one static client-side app that is simple to host and cheap to maintain.
- Keep trip data on the user's device and keep the app shell available offline after its first load.
- Support GitHub Pages repository-path hosting without server rewrites.
- Establish shared UI, accessibility, and performance rules for the feature specs.
- Avoid dependencies and services that do not support an MVP requirement.

## 2. Chosen baseline

| Concern | Design choice |
|---|---|
| Language | TypeScript |
| UI | React |
| Build/dev server | Vite; output directory `dist/` |
| Styling | Native CSS, organized as global tokens/reset plus feature/component styles; no component framework |
| Routing | Hash routes (`#/trips`, `#/trips/{tripId}/timeline`, etc.) |
| Hosting | GitHub Pages, default `github.io` address initially |
| Offline | Service worker precaches the versioned static app shell |
| App data | Browser storage is specified in Spec 01; no API calls or hosted database |
| Print | Browser print dialog with a dedicated print stylesheet, specified in Spec 08 |

### Routing decision

Use hash-based URLs so GitHub Pages always serves the same static document, including on refresh and when the site is hosted below a repository path. Initial route set:

- `#/trips` — trip list and empty state
- `#/trips/new` — create trip
- `#/trips/{tripId}/timeline` — trip workspace default
- `#/trips/{tripId}/costs`
- `#/trips/{tripId}/undecided`
- `#/trips/{tripId}/bookings`
- `#/trips/{tripId}/itinerary` — read-only print view

The router shall validate the route shape and trip ID before rendering. Unknown routes show a not-found state with a route back to Trips. Route changes shall use browser history so Back and Forward work. Never put trip titles, costs, notes, links, or other trip content in the URL; only opaque IDs and view names are allowed.

For MVP scale, use a small route resolver around `window.location.hash` and the History API rather than adding a routing package. Keep route parsing isolated so a router can replace it without affecting feature views if navigation grows.

## 3. Application structure

Proposed source layout (feature specs may add files within these boundaries):

```text
src/
  main.tsx                 # React root and app bootstrap
  app/
    App.tsx                # Route resolution and top-level layout
    routes.ts              # Hash route parsing/building
  domain/
    types.ts               # Shared domain types
    selectors/              # Derived view data (added by feature specs)
  storage/
    persistence.ts         # Storage boundary (defined in Spec 01)
  components/
    AppShell.tsx
    Button.tsx
    FormField.tsx
    StatusLabel.tsx
  features/                # trips, days, items, slots, views, print
  styles/
    tokens.css
    base.css
    layout.css
    print.css
  service-worker.ts        # Precache/update behavior
index.html
vite.config.ts
```

Feature components shall depend on shared domain actions/selectors, not read or write browser storage directly. The storage boundary shall be the only layer that serializes app records. The top-level app shell owns responsive navigation and global save/offline status surfaces; individual specs define feature-specific screens.

## 4. Startup and navigation behavior

1. Browser loads `index.html` and versioned JS/CSS assets from GitHub Pages or the service-worker cache.
2. App bootstrap registers the service worker where supported and resolves the hash route.
3. The storage layer loads/migrates the local trip index and the selected trip records.
4. App renders the trip list, selected feature view, or a recoverable error state.
5. Route changes render views without a full document navigation. Refresh preserves the hash route and returns to the same view if the trip still exists.
6. If a route points to a missing trip, show a clear message and link to the trip list; do not create an empty trip silently.

The app shall distinguish network availability from data availability. A loaded app with local records remains usable offline. Show a compact offline state only when useful; do not imply that data is being synchronized.

## 5. Static build and GitHub Pages deployment

### Build configuration

- Vite builds static content into `dist/`.
- `base` is supplied at build time. For a project site, it is `/{repository-name}/`; for a user/organization root site it is `/`.
- Internal app navigation uses hash routes and asset URLs honor Vite's base path.
- Build must not require secrets or environment variables containing user/trip data.

### Deployment flow

1. A push to the selected deployment branch starts GitHub Actions.
2. Workflow checks out source, installs the locked dependency set, and runs the production build.
3. Workflow publishes only `dist/` using GitHub Pages deployment actions.
4. A failed build does not replace the currently published site.
5. The repo owner can redeploy a prior successful commit by rerunning/reverting through normal GitHub workflow.

The published output contains app code and static assets only. No server endpoints, secret values, `.env` files, or local trip records are part of the artifact. Keep repository visibility as a deployment decision; do not put personal travel records or production trip data in source control.

## 6. Offline shell and service-worker lifecycle

### Cache contents and strategy

- Precache the current build's `index.html`, JavaScript, CSS, and local static assets required to render the shell.
- Use versioned asset URLs from the production build. Cache same-origin app assets only.
- Do not cache external resources, trip data, booking links, or arbitrary user-provided URLs.
- For app shell navigation, serve the cached `index.html` when offline. Since internal routes are hashes, all workspace routes share this document.
- No runtime network-data cache is needed because the MVP has no remote product data.

### Updates and failure states

- A new service worker installs a new app-shell cache. After activation, it removes only old caches owned by this app.
- When an update is ready, the app shall avoid replacing active JS mid-edit. It should either apply on next load or offer a simple “Update available — reload” action. The design favors applying on next load.
- If service workers are unavailable, app remains usable online; offline behavior is best-effort for that browser.
- The first visit requires a successful download before offline use is available.
- Service-worker registration errors must not block normal app startup.

## 7. Responsive and accessible presentation

### Layout

- Mobile-first layout; optimize for a narrow phone viewport first and widen progressively.
- On small screens, use a compact top bar and an accessible menu/tab treatment for the four workspace views. Keep primary add/edit actions reachable without horizontal scrolling.
- On larger screens, show persistent workspace navigation and use available width for comparison and summaries.
- Use content-driven breakpoints, not device-specific user-agent detection.
- Avoid horizontal scrolling for primary workflows. Wide comparisons may use stacked cards on narrow screens.

### Interaction/accessibility baseline

- Use semantic landmarks (`header`, `nav`, `main`, `footer` where appropriate), headings in hierarchy, native form controls, and buttons for actions.
- All controls have programmatic labels; errors are associated with fields and announced when appropriate.
- Keyboard users can reach every action, see focus, and move through a predictable order. Dialogs (such as delete confirmation) keep focus inside while open and return focus to their trigger when closed.
- Status labels include text/icons, never colour alone. Warning and save states have text.
- Contrast shall meet WCAG 2.2 AA for text and interactive controls. Do not rely on colour as the only distinction.
- Target touch controls around 44 CSS pixels where practical; ensure spacing avoids accidental adjacent activation.
- Respect reduced-motion preferences and do not make animation necessary to understand state.

## 8. Performance and dependency budget

- Do not add charting, map, PDF-generation, spreadsheet, analytics, or global state packages for this foundation.
- Use React and TypeScript at runtime/build time; add a date, schema, or icon dependency only in the feature spec that justifies it.
- Prefer locally bundled assets and system fonts; do not fetch web fonts or icon libraries at runtime.
- Initial app shell should stay small enough to meet the under-one-second view requirement on a mid-range phone. Treat bundle size as a monitored build output, not as a substitute for measuring view rendering.
- Avoid rendering every item editor at once. Feature specs should render visible days/items and derive summaries without expensive repeated calculations.

## 9. Security and privacy boundary

- Do not include analytics or third-party scripts in MVP.
- Do not transmit trip names, dates, costs, notes, item links, references, or other trip content.
- Render user-entered text as text; do not inject it as HTML.
- If opening a user-supplied external link, use a safe new-tab policy (`noopener`, `noreferrer`) and make the destination clear.
- Do not store app data in the URL or clipboard unless a future, explicit feature requires it.

## 10. Verification plan for this foundation

Verification is defined here for future implementation; no implementation or tests are part of this design document.

| Area | Verification evidence |
|---|---|
| GitHub Pages path | Production build loads from project-site subpath; assets resolve; hash routes survive refresh |
| Offline | First successful online load, then disable network and reopen app; shell and local trip views remain available |
| Network privacy | Browser network inspection confirms requests contain no trip data |
| Responsive | Manual review at narrow phone, tablet, and desktop viewports; core navigation/actions have no horizontal overflow |
| Accessibility | Keyboard-only walkthrough, visible focus, labels/errors, screen-reader landmark/heading scan, contrast check |
| Browser support | Smoke-check current Chrome, Safari, Firefox, and Edge on desktop; current mobile Safari and Chrome |
| Performance | Measure primary view render for a 200-item fixture on a documented mid-range phone; target below one second |

## 11. Decisions and assumptions

### Decided in this design

- Native CSS, no component framework.
- Minimal in-house hash router, no routing dependency for MVP.
- Static-only deployment; GitHub Actions publishes `dist/`.
- Service worker applies app updates on a later load to avoid changing code during an edit.
- No analytics, external fonts, or external runtime dependencies.

### Still to decide before deployment

- GitHub repository and whether its source is public or private; verify Pages eligibility under the selected plan.
- Deployment branch and exact Pages URL/base path.
- Representative mid-range phone and browser versions for performance/support evidence.

## 12. Traceability

This design realizes the technical constraints in REQ-SCOPE-001..006 and REQ-QUAL-001..004. Feature behavior, local persistence details, and print behavior remain defined in Specs 01–08 and are not duplicated here.
