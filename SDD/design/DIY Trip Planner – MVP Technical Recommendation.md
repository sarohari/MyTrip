# DIY Trip Planner — MVP Technical Recommendation

**Purpose:** A proposed technical baseline for the design/specification stage. This document records implementation recommendations separately from product requirements. Confirm or revise its decisions before creating implementation specs.

## 1. Recommendation summary

Build a client-side, static web app with **Vite, React, and TypeScript**, store trip records in **browser `localStorage`**, deploy the generated static files to **GitHub Pages**, and use a **service worker** to cache the app shell for offline use after first load.

The app should have no server runtime, database service, account system, or API dependency. GitHub Pages serves the app code; trip data remains in the user's browser.

## 2. Proposed stack

### 2.1 App and build

- **TypeScript** for the application code and domain model.
- **React** for the interactive UI and reusable forms/views.
- **Vite** for local development and static production builds.
- **CSS modules or plain CSS** for responsive styling. Avoid a large UI framework unless the design stage identifies a concrete need.
- **Hash-based client routing** so trip/workspace routes work when hosted under a GitHub Pages repository path without requiring server-side rewrites.

### 2.2 Browser storage

- Use the browser's `localStorage` API for the MVP's small, text-based trip dataset.
- Store a versioned application data envelope and validate records when loading them.
- Prefer one versioned record per trip plus a small trip-index record, rather than rewriting every trip when one changes.
- Save after each successful user edit and handle storage errors explicitly (for example, quota exceeded or browser storage unavailable). Show a visible save/error state.
- Add migration functions keyed by schema version before changing persisted record shapes.
- Do not store trip data in cookies, URLs, telemetry, analytics, or remote logs.

**Tradeoff:** `localStorage` is simple and sufficient for the MVP's expected data size, but it is synchronous and browser-profile-specific. If the product later needs large attachments, more complex querying, or robust multi-record transactions, migrate to IndexedDB. The product requirement remains local browser storage either way.

### 2.3 Offline and installability

- Add a service worker that precaches the static app shell and serves it when the network is unavailable.
- Do not cache remote travel data because the MVP has no such integrations.
- PWA installation is not required by the current requirements; a manifest/install prompt can be added later without changing the data model.
- Verify the first-load boundary: the app cannot work offline before its files have been downloaded once.

### 2.4 Dates, timezone, and currency

- Represent trip days as date-only values (`YYYY-MM-DD`), avoiding conversion through UTC timestamps.
- Represent user-entered times as local date/time values. Display the current device timezone label and UTC offset using the browser's `Intl.DateTimeFormat` facilities.
- Use an established date utility only if native date handling proves insufficient during design; keep the dependency small and avoid hidden timezone conversion.
- Store monetary values as whole-number amounts, matching the MVP requirement to skip decimal places. Store the currency code beside each amount.
- Use a manual per-trip exchange-rate table. Define rate direction and display precision in the data/UI spec even though entered costs are whole numbers.
- Use `Intl.NumberFormat` for currency display, with a product decision for currencies that conventionally display fractional units.

### 2.5 Printing to PDF

- Provide a dedicated read-only itinerary route/view and a print action that calls the browser print flow.
- Use print CSS (`@media print`) to hide app navigation and controls, preserve day headings, avoid splitting an item across pages where practical, and include the selected cost visibility setting.
- Do not add a PDF-generation library for the MVP. The user saves to PDF using the browser's print dialog.

### 2.6 Validation and errors

- Define TypeScript domain types for Trip, Day, Slot, Item, and Warning.
- Validate persisted records at the storage boundary. A small schema-validation library such as Zod is optional; native checks may be adequate if validation stays small.
- Keep derived values (nights, converted totals, chosen-option totals, warnings) computed from source records rather than stored redundantly wherever practical.
- Use browser-generated IDs and explicit referential cleanup when deleting trips, slots, or items.

## 3. Hosting and deployment

- **Host:** GitHub Pages, serving the static Vite build.
- **Repository:** use a public repository on GitHub Free if that matches the author's source visibility preference; confirm the applicable GitHub plan if private source is required.
- **Deployment:** build and publish the generated static output with GitHub Actions. Configure the Vite base path for the selected Pages URL.
- **Domain:** the default `github.io` address is sufficient for MVP; a custom domain is optional and may have separate registration costs.
- **Runtime cost:** no application server or database hosting cost. Hosting availability, terms, and quotas are controlled by GitHub and should be rechecked before launch.

GitHub Pages documents a 1 GB published-site limit and a soft 100 GB/month bandwidth limit: [GitHub Pages limits](https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits). Pages is static hosting; it does not provide private trip storage or cross-device sync.

## 4. Suggested architecture boundaries

Keep the code separated into these small areas so specs can map to implementation units:

1. **Domain model:** types and rules for trips, days, items, slots, totals, and warnings.
2. **Persistence:** versioned localStorage read/write, validation, migrations, and save status.
3. **Application state/actions:** create/edit/delete/move/choose operations, with derived view data.
4. **Views:** trip list, trip workspace, timeline, costs, undecided, bookings, and print itinerary.
5. **Presentation:** responsive components and print-specific CSS.
6. **Offline shell:** service-worker registration and static asset caching.

All views should read from the same persisted source records and use shared derived selectors for totals, timeline ordering, and warnings.

## 5. Design decisions to record

Before implementation specs are written, decide:

- Whether GitHub source is public or private and confirm the Pages eligibility for the chosen plan.
- How the localStorage save model handles a failed write and what recovery message the user sees.
- The exact schema envelope and migration policy for future app versions.
- Whether a time remains tied to the local wall-clock value after the device timezone changes. The current product requirement says to use the device's current local timezone, so it should not silently reinterpret stored trip dates.
- Exchange-rate direction, precision, and behavior when a foreign currency has no configured rate.
- The default cost visibility setting for printing.
- Browser and mobile print behavior to support in the acceptance checks.

## 6. Not recommended for MVP

- A backend or hosted database: not needed for the agreed local-only scope.
- Next.js/SSR: adds server/framework complexity to a static client-side product.
- Excel/CSV parsing or JSON restore: explicitly out of MVP scope.
- A map provider, travel APIs, analytics, or account service: adds external dependencies and does not support the MVP's core workflow.
- A large component/design system or state-management framework before the UI and data flows justify it.
