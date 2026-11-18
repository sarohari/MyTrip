# Task 00-01 — Initialize App Foundation

**Status:** Ready after repository setup  
**Design:** [Design 00](../design/00-technical-foundation-design.md), sections 2–3 and 8  
**Spec:** [Spec 00](../spec/00-technical-foundation.md)  
**Depends on:** A writable project repository

## Objective

Create the smallest working static app foundation using Vite, React, and TypeScript.

## Work

- Initialize package metadata and a locked dependency file.
- Add Vite, React, TypeScript, and the minimum required development dependencies.
- Add the HTML entry and React bootstrap.
- Configure a production build to emit static files to `dist/`.
- Add minimal source folders following the design (`app`, `domain`, `storage`, `components`, `features`, `styles`). Keep feature behavior stubbed until its feature tasks.
- Add standard local development and production build scripts.
- Ensure no app data, secrets, or environment-specific personal values are included in the repo.

## Acceptance criteria

- App starts locally and shows a minimal placeholder screen.
- Production build emits `dist/index.html` and static assets.
- TypeScript checks the app source during the build workflow.
- Dependency list contains no server, database, analytics, map, spreadsheet, or PDF-generation package.
- `.gitignore` excludes build output and local environment files.

## Not included

Trip models/persistence, final screen design, feature forms, routing behavior, deployment workflow, and offline cache.
