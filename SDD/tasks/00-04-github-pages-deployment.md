# Task 00-04 — GitHub Pages Deployment

**Status:** Blocked on repository/deployment choices  
**Design:** [Design 00](../design/00-technical-foundation-design.md), section 5  
**Spec:** [Spec 00](../spec/00-technical-foundation.md)  
**Depends on:** [00-01](00-01-initialize-app-foundation.md), a selected repository, deployment branch, and Pages URL/base path

## Objective

Configure automated static deployment of the Vite production output to GitHub Pages.

## Work

- Record the selected repository, source visibility, deployment branch, and final Pages URL.
- Configure Vite's `base` for project-site subpath or root-site hosting.
- Add a GitHub Actions workflow that checks out source, installs the locked dependency set, builds the app, and publishes only `dist/`.
- Grant only the permissions needed for Pages deployment.
- Ensure a failed build does not publish a broken artifact.
- Document how to trigger/recover a deployment through GitHub Actions.

## Acceptance criteria

- A successful workflow publishes the expected static app assets.
- App loads at the configured Pages URL and all assets resolve.
- Hash routes work on refresh at the Pages URL.
- Published artifact contains no `.env`, secrets, trip records, source-only files, or unrelated artifacts.
- A failing build exits without publishing a new site version.

## Blocker

The source repository, visibility, deployment branch, and URL were not selected in Design 00. This task can be prepared, but publication must wait for those values.
