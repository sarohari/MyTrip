# Task 00-02 — App Shell and Base Styles

**Status:** Ready after 00-01  
**Design:** [Design 00](../design/00-technical-foundation-design.md), sections 3, 4, and 7  
**Spec:** [Spec 00](../spec/00-technical-foundation.md)  
**Depends on:** [00-01](00-01-initialize-app-foundation.md)

## Objective

Build the shared responsive application shell and baseline visual/accessibility styles that later feature screens will use.

## Work

- Implement semantic app landmarks and a consistent page container.
- Add global tokens, reset/base styles, typography, focus treatment, and layout styles.
- Add minimal shared button, form-field, and status-label primitives only where needed by the shell.
- Provide mobile and desktop navigation placeholders for the four trip workspace views.
- Add visible focus, keyboard-operable controls, text labels for status, and reduced-motion handling.
- Keep the layout usable without horizontal overflow at phone width; use persistent workspace navigation on wider screens.

## Acceptance criteria

- Shell renders at narrow phone, tablet, and desktop widths without horizontal scrolling for primary navigation.
- All visible shell actions work by keyboard and have visible focus.
- Landmarks and headings form a useful document structure.
- Status is conveyed with text/icon as well as any color treatment.
- Interactive controls have clear labels and practical touch areas.
- No remote fonts or icon services are loaded.

## Not included

Feature-specific pages, final workspace content, data behavior, and print styling.
