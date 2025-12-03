---
title: "Epic PRD: Phase 4 - Content Integration & Population"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
epic_id: EPIC-006
status: Planned
source: ''
author: Portfolio Owner
post_slug: epic-6-content
categories: [docs, project]
tags: [content, integration, data]
ai_note: Assisted by AI (GitHub Copilot)
summary: Epic PRD for integrating validated Term 3 content into the presentation layer, preserving metadata and filters.
date: 2025-12-04
---

## 1. Epic Name

Content Integration & Population

---

## 2. Goal

### Problem

The current prototype showcases components but lacks real academic content, preventing stakeholders from assessing the narrative quality or validating filters.

### Solution

Import the validated Term 3 corpus (projects, reflections, achievements, assignments) into the production-ready layouts. Ensure metadata, skills, and term ordering remain intact and that sensitive data is removed.

### Impact

| Metric | Target | Measurement |
|--------|--------|-------------|
| Content coverage | 100% of Term 3 files represented | Content manifest review |
| Metadata fidelity | 0 mismatches between source and rendered cards | Automated diff |
| Accessibility | ≥95 Lighthouse Accessibility | CI report |
| Link integrity | 0 broken links per `npm run check:links` | Validator |

---

## 3. Personas

- **Admissions reviewer**: Needs real samples to evaluate breadth/depth.
- **Portfolio owner**: Needs to demonstrate achievements and reflections with proper context.
- **Instructor**: Wants evidence that assignments and reflections are preserved verbatim.

---

## 4. Journeys

1. Admissions reviewer lands on T3-AY2025 and browses assignments in chronological order without encountering placeholders.
2. Portfolio owner shares filtered view for `achievements` + `leadership` showing real content cards.
3. Instructor verifies that a reflection entry retains quotes, citations, and rubric references.

---

## 5. Business Requirements

### Functional

- FR-CONT-001: Import all validated Markdown files from Term 3 manifest.
- FR-CONT-002: Map metadata (term, category, skills, tags, summary) to component props.
- FR-CONT-003: Render content cards grouped by term with sticky headings.
- FR-CONT-004: Generate highlights for each content section (achievements, reflections, etc.).
- FR-CONT-005: Provide skill progression summary derived from metadata counts.

### Non-Functional

- NFR-CONT-001: Content build completes within 5 minutes for 300 files.
- NFR-CONT-002: No PII or sensitive data exposed.
- NFR-CONT-003: Render order deterministic (date desc, fallback title asc).

---

## 6. Success Metrics

| KPI | Target | Validation |
|-----|--------|------------|
| Content parity | 100% cards match manifest | Scripted comparison |
| Skills coverage | Skill counts visible for all skills used ≥3 times | UI review |
| Build time | ≤5 min in CI | GitHub Actions logs |

---

## 7. Out of Scope

| Item | Reason |
|------|--------|
| Term 4+ ingestion | Future release once new data ready |
| Automated content summarization | Requires NLP service |
| Localization | Only English in this phase |

---

## 8. Business Value

High. Real content unlocks stakeholder feedback, demonstrates compliance with academic evidence requirements, and validates earlier infrastructure investment.

---

## 9. Dependencies

| Dependency | Type | Notes |
|------------|------|-------|
| Content pipeline (Epic 3) | Internal | Supplies normalized Markdown + graph |
| Components (Epic 4) | Internal | Cards, grids, badges |
| Navigation (Epic 5) | Internal | Filters must recognize new content |

---

## 10. Risks & Mitigation

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Incomplete metadata for some files | Medium | High | Run validation gate before import, fallback UI message |
| Large HTML output size | Medium | Medium | Use excerpt summaries + lazy-load media |
| Sensitive info leak | Low | High | Redact at source, add `content_audit.json` |

---

## 11. Acceptance Criteria

- AC-EPIC-006-01: All Term 3 content files appear in UI with correct metadata.
- AC-EPIC-006-02: Category/skill filters operate on real data.
- AC-EPIC-006-03: Internal/external links resolve and are target-safe.
- AC-EPIC-006-04: Build pipeline fails if manifest counts mismatch.

---

## 12. References

- [Epic Breakdown](../PHASE-2/Epic-breakdown.md#epic-6-content-integration--population)
- [Content Graph Spec](../PHASE-1/Project_Specification.md#content-pipeline)
- [Component Library (EPIC-004)](../epic-4/arch.md)

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 17:05
