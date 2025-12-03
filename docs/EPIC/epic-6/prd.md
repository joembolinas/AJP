---
title: "Feature PRD: Content Integration Run"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
feature_id: EPIC-006-F1
status: Planned
summary: Details the content ingestion, transformation, and presentation feature delivering real Term 3 artifacts.
categories: [docs, project]
tags: [content, integration]
author: Portfolio Owner
ai_note: Assisted by AI (GitHub Copilot)
---

## Overview

This feature takes the validated Term 3 manifest, runs it through the extraction pipeline, enriches the content graph, and binds results to the presentation templates so the site displays authentic academic work.

---

## Objectives

- Populate every component demo with real data from `/content/t3-ay2025`.
- Ensure metadata (skills, categories, terms) flows through to filters and badges.
- Provide summary statistics (count per category, skills per term).
- Prevent publication of redacted or sensitive entries.

---

## Functional Requirements

| ID | Description | Priority |
|----|-------------|----------|
| FR-006-01 | Import manifest `content-manifest.json` and verify counts. | Must |
| FR-006-02 | Map Markdown to HTML + excerpt (first 280 chars) for cards. | Must |
| FR-006-03 | Generate collections per category and per skill. | Must |
| FR-006-04 | Produce featured highlights (top 3 items per category). | Should |
| FR-006-05 | Emit JSON for analytics dashboard (future). | Could |
| FR-006-06 | Provide manual override for hiding entries via `hidden: true`. | Should |

---

## Non-Functional Requirements

- NFR-006-01: Build memory footprint < 1 GB when processing 500 files.
- NFR-006-02: Sanitized HTML using DOMPurify server-side to avoid XSS.
- NFR-006-03: Provide deterministic slugs (kebab-case) for stable anchors.

---

## User Stories

1. As the owner, I can run `npm run content:sync` to import Term 3 and see counts logged.
2. As a reviewer, I can expand a project card to read sanitized HTML content.
3. As the owner, I can hide a draft entry with `hidden: true` and the build excludes it.

---

## Acceptance Tests

- AT-006-01: Build fails if processed count differs from manifest total.
- AT-006-02: Random spot check reveals metadata parity for 5 sampled items.
- AT-006-03: Axe scan passes on pages populated with content.

---

## Dependencies

| Dependency | Description |
|------------|-------------|
| Validation CLI | Ensures source files conform before import |
| Graph Builder | Supplies relationships for skills/categories |
| Component Templates | Provide layout for cards and highlights |

---

## Release Plan

1. Run dry-run import with 5 sample files to verify mapping.
2. Execute full import, review generated JSON + logs.
3. Wire components and snapshots in Storybook.
4. Conduct content QA (metadata parity, redactions) with checklist.
5. Demo to stakeholders, capture feedback, finalize documentation.

---

## Metrics & Monitoring

- Content parity script logs diff summary.
- Build pipeline artifact `content-report.json` archived per run.
- Manual QA checklist stored in `docs/reports/content-audit.md`.

---

## Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Markdown with custom HTML breaks sanitization | Medium | Add allowlist + test fixtures |
| Large images slow builds | Low | Reference CDN assets or resize |
| Hidden entries still referenced by filters | Medium | Filter utilities skip `hidden` flag |

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 17:05
