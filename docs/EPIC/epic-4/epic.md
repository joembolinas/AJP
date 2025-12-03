---
title: "Epic PRD: Phase 4 - Component-Based Presentation Layer"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
epic_id: EPIC-004
status: Planned
source: ''
author: Portfolio Owner
post_slug: epic-4-presentation
categories: [docs, project]
tags: [components, accessibility, design]
ai_note: Assisted by AI (GitHub Copilot)
summary: Epic PRD covering the atomic component system that renders portfolio content with accessibility and responsive guarantees.
date: 2025-12-04
---

## 1. Epic Name

Component-Based Presentation Layer

---

## 2. Goal

### Problem

Even with clean content, the portfolio lacks reusable UI building blocks. Building one-off pages leads to inconsistent UX, accessibility issues, and brittle layouts that break when new categories are added.

### Solution

Create an atomic design system (atoms, molecules, organisms, templates) implemented with semantic HTML, BEM-style CSS, and progressive enhancement. Components must be accessibility-first, responsive down to 320px, and easily composed for future terms.

### Impact

| Metric | Target | Measurement |
|--------|--------|-------------|
| Component coverage | All core content types (projects, reflections, achievements, assignments) | UI audit |
| Accessibility score | ≥95 Lighthouse accessibility | CI Lighthouse run |
| Responsive compliance | Works from 320px to 1440px without layout bugs | Visual regression tests |
| Reuse | ≥80% of UI built using shared components | Storybook inventory |

---

## 3. User Personas

- **Portfolio Visitor**: Needs consistent, legible layouts and accessible interactions.
- **Portfolio Owner**: Wants a library of blocks to assemble new pages quickly without rewriting CSS.
- **AI Assistant**: Requires documented components to generate compliant markup when requested.

---

## 4. High-Level User Journeys

1. Visitor opens portfolio on mobile, uses skip links, and expands a reflection card to read more.
2. Owner adds a new achievement entry that automatically receives correct badge styling and metadata layout.
3. AI helper scaffolds a new template using available organisms and molecules defined in documentation.

---

## 5. Business Requirements

### Functional (FR-UI-*)

- FR-UI-001: Implement atom components (tags, badges, date pills, skill chips) with semantic HTML and BEM classes.
- FR-UI-002: Implement molecule components (content card header, metadata stack, accordion controls) with accessible ARIA attributes.
- FR-UI-003: Implement organism components (term sections, navigation shell, filter panel placeholder) using responsive layout primitives.
- FR-UI-004: Provide template-level compositions for landing page, term detail, and content detail views.
- FR-UI-005: Build component documentation (props, accessibility notes, usage snippets) inside `/docs/components/`.

### Non-Functional

- NFR-UI-001: CSS must follow BEM (Block__Element--Modifier) with single-responsibility files.
- NFR-UI-002: No component may rely solely on color to convey meaning; provide iconography or labels.
- NFR-UI-003: Provide keyboard access for expand/collapse, carousels, and tabs.
- NFR-UI-004: All assets must pass color contrast ≥4.5:1.

---

## 6. Success Metrics

| KPI | Target | Method |
|-----|--------|--------|
| Component completeness | 100% of planned atoms/molecules/organisms built | Storybook progress |
| Accessibility regressions | 0 critical issues in axe scans | CI axe reports |
| Responsive validation | 0 blockers in 320px/768px/1440px breakpoints | Visual regression |
| Documentation coverage | 100% components documented with usage example | Docs review |

---

## 7. Out of Scope

| Item | Reason | Future Epic |
|------|--------|-------------|
| Dynamic filtering logic | Implemented in Epic 5 | Epic 5 |
| Final data binding | Powered by Epic 6 | Epic 6 |
| Brand identity redesign | Post-launch improvement | Backlog |
| Theme switching | Nice-to-have | Future term |

---

## 8. Business Value

Value: High. Consistent, accessible components elevate perceived quality, shorten development time, and ensure future content looks cohesive without extra CSS work.

---

## 9. Dependencies

| Dependency | Type | Impact |
|------------|------|--------|
| Epic 1 foundation | Internal | Provides tooling, linting, and folder structure |
| Epic 2 validation | Internal | Supplies accessibility requirements |
| Design guidelines from spec | External doc | Source for component naming + semantics |

---

## 10. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Scope creep on components | Medium | Medium | Prioritize MVP set tied to requirements |
| CSS regressions across breakpoints | Medium | Medium | Add Storybook visual regression + responsive preview |
| Inaccessible interactions | Low | High | Use axe + manual keyboard testing per component |
| Over-customization reduces reuse | Low | Medium | Document modifiers and stick to base tokens |

---

## 11. Acceptance Criteria

- AC-EPIC-004-01: All interactive components include keyboard focus styles and ARIA attributes.
- AC-EPIC-004-02: Mobile layout renders without horizontal scroll for 320px viewport.
- AC-EPIC-004-03: Components meet color-contrast requirements and pass automated axe scans.
- AC-EPIC-004-04: Component documentation describes structure, states, and references requirement IDs.

---

## 12. Related Documents

- [Epic Breakdown](../PHASE-2/Epic-breakdown.md)
- [Project Specification Sections 8 & 11](../PHASE-1/Project_Specification.md)
- [Accessibility Guidelines](../../.github/instructions/markdown.instructions.md)

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 16:40
