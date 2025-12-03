---
title: "Epic PRD: Phase 3 - Content Extraction & Transformation Pipeline"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
epic_id: EPIC-003
status: Planned
author: Portfolio Owner
source: ''
post_slug: epic-3-content-pipeline
categories: [docs, project]
tags: [content, pipeline, automation]
ai_note: Assisted by AI (GitHub Copilot)
summary: Epic PRD describing the ingestion, transformation, and graph-building pipeline for Academic Journey Portfolio content.
date: 2025-12-04
---

## 1. Epic Name

Content Extraction & Transformation Pipeline

---

## 2. Goal

### Problem

Term-based academic files live across desktop folders and repositories with inconsistent metadata. Manual copy-paste into the portfolio risks errors, stale content, and weeks of reformatting whenever a new term is added.

### Solution

Build an automated pipeline that harvests markdown content from configured source directories, validates metadata, normalizes formats, converts markdown to safe HTML, and outputs structured JSON graphs ready for rendering. The pipeline must handle incremental updates and provide clear reporting.

### Impact

| Metric | Target | Measurement |
|--------|--------|-------------|
| Extraction coverage | 100% of files under configured root | Pipeline manifests |
| Processing throughput | 60 files/minute on laptop hardware | CLI timing |
| Re-run speed | Skip unchanged files with checksum cache | Build logs |
| Data quality | 0 schema regressions passed downstream | Validation report |

---

## 3. User Personas

- **Content Curator**: Configures new term folders and needs confidence that all artifacts were imported without manual spot checks.
- **Portfolio Owner (Developer)**: Uses the generated content graph to power components; wants predictable data contracts and incremental builds.
- **Automation Bot (CI)**: Runs nightly harvests to detect divergence between source files and deployed content.

---

## 4. High-Level User Journeys

1. **Initial Harvest**: Owner sets `CONTENT_ROOT` -> runs `npm run content:sync` -> pipeline scans directories -> validation errors surfaced -> normalized data written to `data/graph.json`.
2. **Incremental Update**: New reflection added -> pipeline detects checksum delta -> only impacted nodes re-render -> build finishes within SLA.
3. **New Term Onboarding**: Owner updates manifest to include `T4-AY2025` path -> CLI verifies structure -> adds term metadata and indexes without touching code.

---

## 5. Business Requirements

### Functional Requirements

- FR-CP-001: Support multiple root directories defined in `content-sources.json` with per-source include/exclude patterns.
- FR-CP-002: Parse front matter, normalize dates, categories, terms, and derive slugs.
- FR-CP-003: Convert markdown to sanitized HTML/AST while preserving callouts and code blocks.
- FR-CP-004: Build term, category, and skill indexes plus relationship graph (term -> items, items -> skills).
- FR-CP-005: Emit manifest, error log, and stats summary for CI consumption.
- FR-CP-006: Provide adapter interface for future data sources (e.g., Google Docs export).

### Non-Functional Requirements

- NFR-CP-001: Pipeline must run cross-platform and complete under 5 minutes for 200 files.
- NFR-CP-002: Memory footprint must stay below 512MB to support Codespaces.
- NFR-CP-003: Log output must be structured JSON to feed dashboards.
- NFR-CP-004: Re-processing unchanged files should be avoided through hashing/cache directory.

---

## 6. Success Metrics

| KPI | Target | Method |
|-----|--------|--------|
| Automated ingestion | 100% of T3-AY2025 content imported | Audit checklist |
| Incremental accuracy | 0 missed updates during regression test | Snapshot diff |
| Error transparency | 100% errors include file path + hint | CLI QA |
| Configurability | New source added in <10 minutes | Onboarding drill |

---

## 7. Out of Scope

| Item | Reason | Future Epic |
|------|--------|-------------|
| Visual presentation of processed data | Owned by component epic | Epic 4 |
| Manual content editing UI | Not part of static site scope | Backlog |
| Automated OCR/import of PDFs | Research topic | Future term |
| Deployment automation | Managed in CI/CD epic | Epic 7 |

---

## 8. Business Value

Value: High. The pipeline unlocks all downstream epics by supplying reliable, normalized content, eliminating manual reformatting, and ensuring terms can be added without engineering effort.

---

## 9. Deliverables Checklist

| Deliverable | Status | Notes |
|-------------|--------|-------|
| Source manifest format | ⏳ Pending | Document JSON schema |
| Extraction CLI | ⏳ Pending | `npm run content:sync` |
| Markdown parser + sanitizer | ⏳ Pending | Remark + DOMPurify |
| Content graph JSON | ⏳ Pending | Expose indices & metadata |
| Pipeline documentation | ⏳ Pending | Include troubleshooting |

---

## 10. Dependencies

| Dependency | Type | Impact |
|------------|------|--------|
| Epic 1 foundation | Internal | Provides repo structure + scripts |
| Epic 2 validation | Internal | Validators run before ingestion |
| Access to `T3-AY2025` folder | External | Source of truth for pilot |

---

## 11. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Diverse folder naming conventions | Medium | Medium | Use configurable glob patterns + mapping rules |
| Large files slow down parsing | Medium | Low | Stream reading and warn when exceeding threshold |
| Sanitization strips intentional HTML | Low | Medium | Allow safe whitelist and document usage |
| Cache invalidation bugs | Medium | Medium | Include cache-busting flag and regression tests |

---

## 12. Acceptance Criteria

- AC-EPIC-003-01: Given a configured content root, when the pipeline runs, then every markdown file with valid metadata appears in the generated graph.
- AC-EPIC-003-02: Given unchanged files, when re-running the pipeline, then the runtime drops by at least 50% thanks to caching.
- AC-EPIC-003-03: Given malformed front matter, when processing occurs, then the run fails fast with actionable messaging and does not emit partial data.
- AC-EPIC-003-04: Given a new term entry in the manifest, when processing occurs, then term metadata is added without modifying code.

---

## 13. Related Documents

- [Epic Breakdown](../PHASE-2/Epic-breakdown.md)
- [Project Specification](../PHASE-1/Project_Specification.md)
- [Validation System (EPIC-002)](../EPIC/epic-2/epic.md)

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 16:30
