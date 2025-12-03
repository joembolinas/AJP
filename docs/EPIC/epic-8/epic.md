---
title: "Epic PRD: Phase 5 - Testing & Quality Assurance"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
epic_id: EPIC-008
status: Planned
source: ''
author: Portfolio Owner
post_slug: epic-8-quality
categories: [docs, project]
tags: [testing, qa, automation]
ai_note: Assisted by AI (GitHub Copilot)
summary: Epic PRD covering automated testing strategy for the Academic Journey Portfolio, including unit, integration, accessibility, and visual tests.
date: 2025-12-04
---

## 1. Epic Name

Testing & Quality Assurance

---

## 2. Goal

### Problem

Without automated tests, regressions in the content pipeline, components, or accessibility can ship unnoticed, eroding trust and increasing manual QA burden.

### Solution

Establish a comprehensive testing stack (unit, integration, E2E, accessibility, visual regression) with coverage targets and CI enforcement.

### Impact

| Metric | Target | Measurement |
|--------|--------|-------------|
| Code coverage | ≥80% statements/lines | Jest/Vitest report |
| E2E suite duration | ≤5 min for core journeys | Playwright logs |
| Accessibility violations | 0 critical issues | axe/Pa11y report |
| Visual diffs | <2% change unless approved | Percy/Chromatic |

---

## 3. Personas

- **Maintainer**: Wants guardrails before merging features.
- **Reviewer**: Needs confidence that UI remains accessible.
- **Automation bot**: Reports quality status in CI summaries.

---

## 4. Journeys

1. Developer updates a component; unit tests plus visual snapshots verify behavior before merge.
2. Pipeline runs Playwright scenario: user filters term + skill, expands card, verifies content renders.
3. Accessibility audit fails due to missing aria-label; CI surfaces actionable log.

---

## 5. Business Requirements

### Functional

- FR-QA-001: Provide unit tests for validators, parsers, and utilities.
- FR-QA-002: Provide integration tests covering extraction + build pipeline.
- FR-QA-003: Provide Playwright E2E tests for navigation/filter journeys.
- FR-QA-004: Provide accessibility tests using axe-core/Pa11y for key pages.
- FR-QA-005: Provide visual regression tests for core templates via Percy/Chromatic.
- FR-QA-006: Publish consolidated quality report (`quality-report.md`).

### Non-Functional

- NFR-QA-001: All tests finish within 5 minutes on CI runners.
- NFR-QA-002: Coverage threshold enforced at 80%.
- NFR-QA-003: Tests resilient to timezone/locale differences.

---

## 6. Success Metrics

| KPI | Target |
|-----|--------|
| Quality gate pass rate | ≥95% |
| Visual diff false positives | <5% |
| Accessibility regressions caught pre-merge | 100% |

---

## 7. Out of Scope

| Item | Reason |
|------|--------|
| Mobile device lab testing | Use responsive E2E instead |
| Load testing | Static site, low need |
| Fuzz testing | Not critical in Phase 1 |

---

## 8. Business Value

Medium-High. Automated tests reduce manual QA cycles, support fearless refactoring, and prove compliance with school accessibility requirements.

---

## 9. Dependencies

| Dependency | Notes |
|------------|-------|
| CI/CD (Epic 7) | Executes suites |
| Components (Epic 4) | Provide UI under test |
| Content (Epic 6) | Supplies data for integration/E2E |

---

## 10. Risks & Mitigation

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Flaky E2E tests | Medium | Medium | Use deterministic data, retry logic |
| Visual diff noise | Medium | Low | Use device pixel ratio normalization |
| Accessibility tooling drift | Low | Medium | Pin versions, run weekly audit |

---

## 11. Acceptance Criteria

- AC-EPIC-008-01: Coverage report meets ≥80% across statements/branches/lines.
- AC-EPIC-008-02: Playwright tests cover nav/filter/expand journeys.
- AC-EPIC-008-03: axe-core scan returns zero critical issues for home page + sample term.
- AC-EPIC-008-04: Visual regression baseline captured and tracked in CI.

---

## 12. References

- [Epic Breakdown](../PHASE-2/Epic-breakdown.md#epic-8-testing--quality-assurance)
- [Project Specification - Testing Strategy](../PHASE-1/Project_Specification.md#testing-strategy)

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 17:28
