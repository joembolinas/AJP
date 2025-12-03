---
title: "Feature PRD: Navigation & Filtering Experience"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
feature_id: EPIC-005-F1
status: Planned
summary: Defines feature-level scope for the navigation timeline, category and skill filters, and URL-state restoration.
categories: [docs, project]
tags: [navigation, filtering, ux]
author: Portfolio Owner
ai_note: Assisted by AI (GitHub Copilot)
date: 2025-12-04
---

## Overview

This feature introduces timeline navigation and multi-dimensional filtering to the Academic Journey Portfolio. It relies on metadata from the content graph to filter up to 200 cards without reloading the page and exposes state via URLs for sharable deep links.

---

## Objectives

- Deliver a responsive navigation menu that highlights active term and exposes keyboard/assistive tech affordances.
- Enable AND/OR filtering between categories, skills, and term facets.
- Persist filter state in URL parameters and restore on page load.
- Provide accessible fallbacks when JavaScript is disabled.

---

## Functional Requirements

| ID | Description | Priority |
|----|-------------|----------|
| FR-005-01 | Render horizontal timeline (desktop) and accordion (mobile) with sticky positioning. | Must |
| FR-005-02 | Display filter drawer with multi-select category chips and skill tags. | Must |
| FR-005-03 | When a filter toggles, update card visibility instantly and announce via ARIA live region. | Must |
| FR-005-04 | Persist selected filters and term in URL query params. | Must |
| FR-005-05 | Provide `Clear filters` button that resets state and focus. | Should |
| FR-005-06 | Expose `data-filter-*` attributes on cards for future automation. | Should |
| FR-005-07 | Provide minimal search input (string contains) for card title filtering if time permits. | Could |

---

## Non-Functional Requirements

- NFR-005-01: Render under 60 ms on cold load using content graph JSON.
- NFR-005-02: Maintain 60fps transitions by batching DOM writes via requestAnimationFrame.
- NFR-005-03: Provide SSR-friendly markup to keep filters functional even when JS fails (progressive enhancement).

---

## User Stories

1. As a reviewer, I can filter by `achievements` and `leadership` skills, and copy the URL to revisit the same view later.
2. As the owner, I can preselect `T3-AY2025` via query params when sharing the latest term.
3. As a low-vision user, I can navigate filters via keyboard + screen reader without confusion.

---

## Dependencies

| Item | Description | Owner |
|------|-------------|-------|
| Component tokens | Filter chips, badges, timeline component | Epic 4 |
| Content graph | JSON metadata including term, category, skills | Epic 3 |
| Validation schema | Ensures metadata completeness | Epic 2 |

---

## Release Plan

1. Build filter utilities and sample dataset locally.
2. Implement UI states in Storybook, run accessibility checks.
3. Integrate into main layout, wire to content graph.
4. Test URL persistence, progressive enhancement, and fallback rendering.
5. Update documentation + screencasts.

---

## Measurements

- Lighthouse Accessibility ≥ 95 for pages with filters.
- 0 console errors/warnings during interaction.
- 0 regressions in existing epics (verify via visual regression tests).

---

## Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Filter logic duplication between client-side and build-time | Inconsistent results | Share utilities across pipelines |
| Query param collisions | Broken URLs | Namespace parameters (e.g., `ajpTerm`) |
| Complexity in focus handling | Accessibility failures | Follow WAI-ARIA Authoring Practices, write unit tests |

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 16:47
