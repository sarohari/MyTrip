# Task 00-05 — Offline App Shell

**Status:** Ready after 00-01 and 00-03  
**Design:** [Design 00](../design/00-technical-foundation-design.md), section 6  
**Spec:** [Spec 00](../spec/00-technical-foundation.md)  
**Depends on:** [00-01](00-01-initialize-app-foundation.md), [00-03](00-03-hash-routing.md)

## Objective

Cache the static app shell so a user who has loaded the app successfully can reopen it offline.

## Work

- Add service-worker registration that does not block app startup if registration fails or is unsupported.
- Precache the current build's app document, versioned JS/CSS, and required local assets.
- Serve the cached app shell for offline navigation; hash routes continue to resolve within that shell.
- Cache only same-origin static app resources. Do not cache user content, external URLs, or network API data.
- Version caches and remove only older caches owned by this app.
- Apply app updates on a later load to avoid replacing active code mid-edit.
- Document that first successful load is required before offline use.

## Acceptance criteria

- After successful online load, disable network and reopen the app; app shell loads.
- Registration/installation failures leave the online app usable.
- Updating the app does not remove unrelated origin caches.
- No remote resources or trip content are added to a cache.
- A service-worker update does not force a mid-session reload.

## Not included

Install prompts, background sync, server-side caching, API data caching, or cross-device data access.
