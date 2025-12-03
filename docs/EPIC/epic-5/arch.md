---
title: "Architecture: Navigation & Content Filtering"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
artifact_id: EPIC-005-ARCH
status: Planned
summary: Architectural approach for term timeline, filter utilities, state management, and progressive enhancement.
categories: [docs, architecture]
tags: [navigation, filtering, accessibility]
ai_note: Assisted by AI (GitHub Copilot)
---

## Architecture Overview

The navigation and filtering system layers user interactions on top of the static content graph. Filters are generated during build time and hydrated at runtime to deliver sub-100 ms responses while remaining fully accessible without JavaScript.

### Key Components

| Component | Purpose |
|-----------|---------|
| `timeline-nav` | Renders chronological term list with sticky behavior |
| `filter-drawer` | Houses category and skill chips plus clear button |
| `filter-store` | Lightweight state container syncing UI + URL |
| `filter-utils` | Shared predicate helpers that reuse content graph schema |

### Interaction Flow

```text
User Action -> Filter UI -> filter-store -> filter-utils -> DOM updater
                                  |                     |
                             URL params           Live region notice
```

## Technology Stack

- Eleventy data cascade to inject content graph JSON.
- Vanilla TypeScript modules compiled via Vite.
- URLSearchParams for state persistence.
- CSS custom properties for theming (ties into Epic 4 design tokens).

## Data Flow

```text
content graph JSON -> filter-utils -> derived indexes
                                 -> filter-store defaults -> UI state
```

- Derived indexes include sets per term, per category, and per skill to minimize iteration.
- Filters reference card IDs rather than DOM nodes to support virtualization later.

## Progressive Enhancement

1. Server-rendered markup includes plain lists (all cards visible) with `data-filter-category` attributes.
2. On hydration, script enhances filter controls, adds event listeners, and manipulates `hidden` attributes rather than removing DOM nodes.
3. Without JS, anchor-based navigation (`#T3-AY2025`) remains functional.

## Accessibility

- Timeline uses `<nav aria-label="Academic terms">` with proper focus outlines.
- Filter chips expose `aria-pressed` and keyboard activation via `Space`/`Enter`.
- Live region announces filter result counts.
- Screen reader instructions included via visually hidden text.

## Performance Considerations

- Precompute filter indexes during build to avoid O(n*m) loops.
- Batch DOM writes, only toggle `hidden` and `aria-hidden` attributes.
- Use `ResizeObserver` to adjust sticky offsets for smaller devices.

## Deployment & Testing

- Unit tests for filter-utils (Jest/Vitest) covering predicate correctness.
- Storybook stories for timeline and drawer with AXE automated checks.
- Integration tests verifying URL-state restoration through Playwright.

## Risks

| Risk | Mitigation |
|------|------------|
| Large query params when many skills selected | Cap at 10 selections or use compressed tokens |
| Sticky nav overlapping content | Use CSS `scroll-margin-top` tokens |
| Accessibility regressions | Include axe CI gate + manual keyboard checklist |

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 16:47
