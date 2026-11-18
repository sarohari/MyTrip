# Task 00-07 — Foundation Verification

**Status:** Ready after 00-01 through 00-06  
**Design:** [Design 00](../design/00-technical-foundation-design.md), section 10  
**Spec:** [Spec 00](../spec/00-technical-foundation.md)  
**Depends on:** [00-01](00-01-initialize-app-foundation.md) through [00-06](00-06-privacy-and-dependency-boundaries.md)

## Objective

Collect manual verification evidence that the technical foundation meets Spec 00 before feature work builds on it.

## Verification checklist

- Production build loads at the selected GitHub Pages URL/base path; all assets resolve.
- Every hash route survives refresh and browser Back/Forward navigation.
- After a successful online visit, the app shell opens with network access disabled.
- Network inspection confirms no trip data is transmitted.
- Keyboard-only walkthrough confirms navigation, visible focus, and operable controls.
- Screen-reader inspection confirms useful landmarks/headings and accessible labels for shell controls.
- Contrast and non-colour status cues are checked.
- Current Chrome, Safari, Firefox, and Edge desktop; mobile Safari and Chrome are smoke-checked.
- A documented mid-range phone can render each primary view for a 200-item fixture under one second.
- Record browser/device versions, build revision, observed results, and any accepted limitations.

## Completion criteria

- Every checklist item has a pass/fail result and brief evidence.
- Failures are linked to follow-up tasks before feature specs depend on the affected behavior.
- Do not mark Spec 00 complete while an acceptance check is failing without an explicit design decision.
