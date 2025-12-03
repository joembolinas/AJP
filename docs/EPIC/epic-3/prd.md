---
title: "Feature PRD: Content Extraction & Transformation Pipeline"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
source: ''
author: Portfolio Owner
post_slug: epic-3-content-pipeline-prd
categories: [docs, spec]
tags: [content, pipeline, automation]
ai_note: Assisted by AI (GitHub Copilot)
summary: Product requirements detailing the extraction CLI, normalization routines, and graph builder that power Epic 3.
date: 2025-12-04
epic_id: EPIC-003
status: Planned
---

## 1. Feature Name

Content Harvest & Transformation Engine

---

## 2. Epic Link

- `[EPIC-003 PRD](./epic.md)`
- `[EPIC-003 Architecture](./arch.md)`
- `[Validation Toolkit](../epic-2/epic.md)`

---

## 3. Goal

### Problem

Content lives across multiple folders with inconsistent metadata, making it tedious to import and dangerous to keep synchronized.

### Solution

Provide a deterministic command-line tool that reads a manifest of sources, validates metadata, transforms markdown into sanitized HTML plus JSON nodes, and emits a relationship graph for downstream consumption.

### Impact

- Zero manual copy/paste between terms.
- Repeatable extractions that finish in minutes, not hours.
- Reliable data contracts that unlock component work.

---

## 4. User Personas

- **Portfolio Owner**: Runs the CLI locally before committing to verify new content.
- **Automation Bot**: Executes nightly to detect drift between sources and repo.
- **Reviewer**: Checks manifest and summary outputs to ensure coverage.

---

## 5. User Stories

- As the owner, I want to point the CLI at a manifest so that I can sync entire terms with one command.
- As a curator, I want warnings for skipped files so that I can fix metadata quickly.
- As CI, I want a machine-readable output so that I can compare past runs.
- As a reviewer, I want stats per term so that I know what changed.

---

## 6. Requirements

### Functional

1. Manifest-driven source discovery with include/exclude globs per entry.
2. Front matter parser that enriches nodes with normalized term, date, category, and skill arrays.
3. Markdown-to-HTML conversion with configurable plugins (callouts, tables, code fences).
4. Content graph builder generating `data/content-graph.json`, `data/term-index.json`, `data/skill-index.json`.
5. Incremental cache keyed by file checksum to skip unchanged transformations.
6. Summary report listing imported files, warnings, errors, and runtime metrics.

### Non-Functional

1. CLI completes under 5 minutes for 200 files on laptop hardware.
2. Works offline aside from optional external metadata lookups.
3. Provides `--dry-run` mode to preview changes.
4. Includes 85% unit test coverage for parsers and adapters.

---

## 7. Acceptance Criteria

- Given a manifest with two folders, when the CLI runs, then content from both folders appears in the graph with correct term labels.
- Given a file missing required front matter, when the CLI runs, then it exits non-zero and logs the offending field.
- Given unchanged content, when the CLI runs twice, then the second execution skips at least 80% of files.
- Given `--report reports/pipeline.json`, when the CLI finishes, then that file includes counts for imported, skipped, warning, and error states.

---

## 8. Dependencies

| Dependency | Notes |
|------------|-------|
| Validation Toolkit (EPIC-002) | Runs before extraction; CLI should fail if validation fails |
| Source directories | Access to `C:/Users/ADMIN/Desktop/School File/T3-AY2025` |
| Node.js runtime | Shared toolchain from Epic 1 |

---

## 9. Release Plan

1. Define manifest schema plus config loader.
2. Implement parser and sanitizer modules with tests.
3. Build graph builders and indexes.
4. Add cache and reporting.
5. Document CLI usage and integrate with npm scripts/CI.

---

## 10. Out of Scope

- GUI for configuring sources.
- Automatic pulling from remote repositories (future integration work).
- Binary/PDF conversion.

---

## 11. Open Questions

- Should we provide optional image optimization during extraction or leave to a later phase?
- Where should cache files live (`.cache/` vs `%LOCALAPPDATA%`)?
- Do we need to support zipped archives as sources?

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 16:32
