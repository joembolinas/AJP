---
title: "Epic PRD: Phase 3 - Content Schema & Validation System"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
epic_id: EPIC-002
status: Planned
author: Portfolio Owner
source: ''
post_slug: epic-2-validation
categories: [docs, spec]
tags: [validation, schema, automation]
ai_note: Assisted by AI (GitHub Copilot)
summary: Epic PRD describing the metadata schema, validation CLI, and automated quality gates required to protect portfolio content integrity.
date: 2025-12-04
---

## 1. Epic Name

Content Schema & Validation System

---

## 2. Goal

### Problem

Academic content entering the portfolio lacks a rigorous metadata contract. Missing front matter, invalid categories, and broken links could propagate into the UI, damaging trust and wasting debugging time. Manual reviews do not scale for 1,000+ files.

### Solution

Define a canonical content schema, implement automated validators, and expose a CLI plus CI entry point that blocks bad data from landing in `main`. Validation must cover structure, taxonomy, accessibility hints, and reference integrity, with actionable error messages for students and AI agents.

### Impact

| Metric | Target | Measurement |
|--------|--------|-------------|
| Front matter compliance | 100% of tracked files | Schema validation report |
| Validation runtime | <30s for 100 files | CLI timing |
| Error clarity | 90% of failures resolved without follow-up | Developer survey |
| Broken link count | 0 in published site | Link checker logs |

---

## 3. User Personas

- **Content Curator**: Imports new markdown content and needs feedback on metadata quality.
- **Portfolio Owner**: Requires deterministic, scripted validation before opening PRs.
- **Automation Bot (CI)**: Runs validations headlessly and must fail fast with non-zero exit codes.

---

## 4. High-Level User Journeys

1. **Local Authoring Flow**: Author edits markdown -> runs `npm run validate` -> schema checker reports issues inline -> author fixes and reruns until clean.
2. **CI Quality Gate**: Pull request triggers GitHub Action -> validator re-runs with same config -> workflow blocks merge if any severity `error` remains.
3. **Link Integrity Review**: Weekly scheduled job runs link checker across built site -> outputs report highlighting regressions -> owner triages.

---

## 5. Business Requirements

### Functional Requirements

- Define JSON Schema capturing required front matter fields (title, summary, categories, tags, date, term, type, ai_note) with regex validation (VAL-001, VAL-007, VAL-008, VAL-009, VAL-010).
- Build Node-based CLI `npm run validate` executing schema checks, category lookups, and term format enforcement.
- Implement broken link detection (internal + external) with actionable URLs (VAL-002).
- Add accessibility lint covering alt text, heading order, ARIA attributes in markdown (VAL-011...VAL-015).
- Produce validation summary file under `.reports/validation.json` for CI artifacts.
- Allow configuration overrides via `config/validation.config.mjs` without editing code.

### Non-Functional Requirements

- Validation must run cross-platform (Windows, macOS, Linux) with no native dependencies.
- CLI should exit non-zero on any `error` severity, warnings allowed but logged.
- Schema definitions versioned; breaking changes require migration notes.
- Validators must support 1,000+ files with <500MB memory footprint.

---

## 6. Success Metrics

| KPI | Target | Method |
|-----|--------|--------|
| Automated coverage | 95% of requirements enforced by scripts | Mapping doc |
| False positive rate | <5% of validation errors reopened | Issue tracker |
| Scheduled job reliability | 99% success over 30 days | CI analytics |
| Documentation completeness | 100% of checks documented in `docs/validators.md` | Doc audit |

---

## 7. Out of Scope

| Item | Reason | Future Epic |
|------|--------|-------------|
| UI rendering of validation results | Concern of presentation layer | Epic 4 |
| Content ingestion automation | Implemented in pipeline epic | Epic 3 |
| Spell-checking or grammar lint | Nice-to-have post-launch | Backlog |
| Non-markdown assets (PDF validation) | Requires different tooling | Future research |

---

## 8. Business Value

**Value: High.** Automated validation prevents regressions, protects brand quality, and keeps the project manageable as content volume grows. The schema also serves as documentation for students authoring new work.

---

## 9. Deliverables Checklist

| Deliverable | Status | Notes |
|-------------|--------|-------|
| JSON Schema definition | ⏳ Pending | Cover all required fields + enums |
| Validation CLI | ⏳ Pending | Node-based script with watch mode |
| Link checker | ⏳ Pending | Reuse `broken-link-checker` or custom fetch |
| Accessibility lint rules | ⏳ Pending | Integrate remark/markdownlint plugins |
| Documentation (`docs/validation.md`) | ⏳ Pending | Include troubleshooting |

---

## 10. Dependencies

| Dependency | Type | Impact |
|------------|------|--------|
| Epic 1 Foundation | Internal | Requires npm scripts, repo structure |
| Categories list (`categories.txt`) | Data | Source of allowed values |
| GitHub Actions | Tooling | Executes validators in CI |

---

## 11. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Schema too rigid for future terms | Medium | Medium | Version schema and document migration path |
| Validation runtime grows >30s | Medium | Medium | Implement incremental caching and concurrency |
| Link checker false positives | Medium | Low | Allow suppression config per domain |
| Accessibility lint noise | Low | Medium | Provide severity levels and overrides |

---

## 12. Acceptance Criteria

- AC-EPIC-002-01: When invalid front matter is committed, `npm run validate` fails with field-specific guidance.
- AC-EPIC-002-02: Link checker identifies broken internal links before deployment.
- AC-EPIC-002-03: Accessibility lint verifies alt text, heading order, and ARIA references with 0 critical violations.
- AC-EPIC-002-04: Validation summary file captures counts by severity and is uploaded in CI artifacts.
- AC-EPIC-002-05: Documentation includes quickstart, troubleshooting, and requirement traceability.

---

## 13. Related Documents

- [Project Specification](../PHASE-1/Project_Specification.md)
- [Epic Breakdown](../PHASE-2/Epic-breakdown.md)
- [Validation CLI Design (future)](../PHASE-3/Validation_Design.md)

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 16:10
