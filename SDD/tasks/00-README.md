# Design 00 — Implementation Tasks

Tasks derived from [Design 00 — Technical Foundation](../design/00-technical-foundation-design.md) and [Spec 00](../spec/00-technical-foundation.md). They define work only; no implementation is included here.

## Recommended order

| Order | Task | Result | Depends on |
|---|---|---|---|
| 00-01 | [Initialize app foundation](00-01-initialize-app-foundation.md) | Vite + React + TypeScript static app scaffold | — |
| 00-02 | [Create app shell and base styles](00-02-app-shell-and-base-styles.md) | Responsive semantic shell and shared styles | 00-01 |
| 00-03 | [Add hash routing](00-03-hash-routing.md) | Route parsing/building and route states | 00-02 |
| 00-04 | [Configure GitHub Pages deployment](00-04-github-pages-deployment.md) | Build and deploy static `dist/` output | 00-01; repo decisions |
| 00-05 | [Add offline app shell](00-05-offline-app-shell.md) | Service-worker precache and safe update behavior | 00-01, 00-03 |
| 00-06 | [Apply privacy and dependency boundaries](00-06-privacy-and-dependency-boundaries.md) | No trip-data network path or unnecessary runtime service | 00-01..05 |
| 00-07 | [Verify technical foundation](00-07-foundation-verification.md) | Manual evidence for Spec 00 quality/acceptance checks | 00-01..06 |

## Cross-task rules

- Follow the design's proposed source boundaries; feature specs may extend them.
- Keep trip record persistence implementation in Spec 01 tasks, not in the technical-foundation scaffold task.
- Do not add analytics, external fonts, maps, PDF generation, or spreadsheet dependencies.
- Do not commit real trip data or secrets.
- Complete the open repository visibility, deployment branch, and Pages URL decisions before publishing.
