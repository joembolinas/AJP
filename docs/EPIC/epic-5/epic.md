---
title: "Epic PRD: Phase 4 - Navigation & Content Filtering"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
epic_id: EPIC-005
status: Planned
source: ''
author: Portfolio Owner
post_slug: epic-5-navigation
categories: [docs, project]
tags: [navigation, filtering, ux]
ai_note: Assisted by AI (GitHub Copilot)
summary: Epic PRD defining chronological navigation, category/skill filtering, and progressive enhancement behaviors for the portfolio UI.
date: 2025-12-04
---

## 1. Epic Name

Navigation & Content Filtering

---

## 2. Goal

### Problem

With dozens of items per term, visitors cannot quickly find relevant work. Static pages without filters overwhelm users and make skill discovery impossible.

### Solution

Implement timeline navigation, category/skill filters, and optional search that work with and without JavaScript. Filters should respond within 100 ms on modern browsers, expose state via URLs, and remain accessible via keyboard.

### Impact

| Metric | Target | Measurement |
|--------|--------|-------------|
| Filter latency | ≤100 ms per interaction | Performance mark |
| Progressive enhancement | Full content visible when JS disabled | Manual test |
| URL shareability | Filter state encoded in query params | QA checks |
| Accessibility | 0 critical issues in axe for nav/filter controls | Axe report |

---

## 3. User Personas

- **Visitor (Admissions/Recruiter)**: Needs to filter by skill or category to find relevant work quickly.
- **Portfolio Owner**: Wants to highlight recent term automatically while enabling deep dives.
- **AI Assistant**: Requires documented filter APIs to suggest future enhancements.

---

## 4. Journeys

1. Visitor lands on term timeline, selects `T3-AY2025`, filters to `reflections` + `communication` skill, and shares URL.
2. Owner toggles `skills` filter to craft custom demo link for interview prep.
3. Visitor on low-end device without JS still scrolls chronological list and uses anchor navigation.

---

## 5. Business Requirements

### Functional

- FR-NAV-001: Provide term navigation component listing all available terms with counts.
- FR-NAV-002: Implement category filters (academic, reflection, achievement, assignment, extracurricular) with multi-select support.
- FR-NAV-003: Implement skill filters with chips derived from content graph.
- FR-NAV-004: Encode filter state in query parameters for shareability and back/forward navigation.
- FR-NAV-005: Provide clear-all and active filter summary.
- FR-NAV-006: Provide no-JS fallback (shows all content + anchor jumps).

### Non-Functional

- NFR-NAV-001: Filtering operations must complete within 100 ms for 200 cards on target hardware.
- NFR-NAV-002: Controls must be operable via keyboard and screen readers (aria-pressed, aria-controls, etc.).
- NFR-NAV-003: Avoid reflow jank on mobile by using CSS transitions and requestAnimationFrame.

---

## 6. Success Metrics

| KPI | Target | Method |
|-----|--------|--------|
| Filter accuracy | 100% matching items reflect selected filters | Automated tests |
| URL reproducibility | Filters persisted after refresh/share | Manual QA |
| Progressive enhancement | Works identically with JS disabled (shows all content) | Manual QA |
| Accessibility | 0 axe violations for filters and nav | CI |

---

## 7. Out of Scope

| Item | Reason | Future Epic |
|------|--------|-------------|
| Full-text search | Nice-to-have; revisit later | Backlog |
| Recommendation engine | Requires analytics | Future phase |
| Server-side filtering | Static site constraint | N/A |

---

## 8. Business Value

Value: Medium-High. Filtering is the primary way busy reviewers find relevant stories, directly impacting usability and perceived polish.

---

## 9. Dependencies

| Dependency | Type | Impact |
|------------|------|--------|
| Content graph (Epic 3) | Internal | Supplies metadata + counts |
| Component library (Epic 4) | Internal | Provides filter UI elements |
| Validation rules (Epic 2) | Internal | Ensures metadata accurate |

---

## 10. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Filter logic drifts from metadata schema | Medium | Medium | Reuse content graph + central filter utility |
| Performance regressions on mobile | Medium | Medium | Use virtualization or CSS-only hiding, throttle events |
| URL state complexity | Low | Medium | Use small, human-readable query params (`?term=T3&cat=reflection,academic`) |

---

## 11. Acceptance Criteria

- AC-EPIC-005-01: Selecting multiple categories filters cards with AND logic (within category) and OR logic across category vs skill.
- AC-EPIC-005-02: Clearing filters restores full list without page reload.
- AC-EPIC-005-03: Filter state encoded in query params and restored on refresh.
- AC-EPIC-005-04: Navigation and filter controls pass keyboard navigation checklist.

---

## 12. Related Documents

- [Epic Breakdown](../PHASE-2/Epic-breakdown.md)
- [Component System (EPIC-004)](../epic-4/epic.md)
- [Content Graph Spec](../PHASE-1/Project_Specification.md#content-pipeline)

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 16:47
