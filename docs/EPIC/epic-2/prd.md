---
title: "Feature PRD: Content Schema & Validation System"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
source: ''
author: Portfolio Owner
post_slug: epic-2-validation-prd
categories: [docs, spec]
tags: [validation, schema, automation]
ai_note: Assisted by AI (GitHub Copilot)
summary: Product requirements describing the content schema, validation CLI, and automated quality checks that enforce metadata integrity for Epic 2.
date: 2025-12-04
epic_id: EPIC-002
status: Planned
---

## 1. Feature Name

Content Schema & Validation Toolkit

---

## 2. Epic Link

- `[EPIC-002 PRD](./epic.md)`
- `[EPIC-002 Architecture](./arch.md)`
- `[Phase 2 Epic Breakdown](../PHASE-2/Epic-breakdown.md)`

---

## 3. Goal

### Problem

Without a schema-backed validation layer, inconsistent metadata slips into the repository, making downstream automation unreliable and harming site credibility.

### Solution

Define a versioned schema, implement a CLI validator with modular rules, and integrate link and accessibility checks so contributors receive immediate, actionable feedback locally and in CI.

### Impact

- Eliminate 100% of schema violations before merge.
- Reduce manual review time for metadata issues by 80%.
- Provide transparent validation reports for auditing.

---

## 4. User Personas

- **Portfolio Owner**: Wants deterministic scripts before pushing changes.
- **Content Curator**: Needs descriptive errors tied to the actual markdown file.
- **Reviewer**: Prefers validation artifacts to quickly verify compliance.

---

## 5. User Stories

- As a contributor, I want validation errors to point to the file and line so I can fix them quickly.
- As the owner, I want to block merges if any validation errors exist so production stays stable.
- As a reviewer, I want to download a summary artifact so I can verify what the validator checked.
- As an automation bot, I want standard exit codes so workflows can fail fast.

---

## 6. Requirements

### Functional Requirements

1. Provide JSON Schema definitions under `config/schema/` with `$id` versioning.
2. Build CLI using Node + Ajv validator with plug-in system for category, tag, and term checks.
3. Implement link checker supporting retries, timeout config, and allowlist.
4. Integrate accessibility lint (alt text, heading levels, ARIA references) using remark plugins.
5. Output machine-readable report (JSON) plus developer-friendly console summary.
6. Support watch mode to re-run validation on file change.

### Non-Functional Requirements

1. CLI completes within 30 seconds for 100 markdown files.
2. Works offline for schema validation; link checker gracefully skips offline runs with warning.
3. Configurable severity levels (error, warning, info) with defaults stored in `validation.config.mjs`.
4. Provide 90% unit test coverage for rule helpers.

---

## 7. Acceptance Criteria

- Given a file missing `title`, when running `npm run validate`, then the CLI exits with code 1 and prints the missing field.
- Given a category not in `categories.txt`, when validation runs, then the CLI points to the offending line with allowed values.
- Given a markdown link returning 404 twice, when the link checker runs, then the error is recorded with HTTP status.
- Given `--report` flag, when validation completes, then `.reports/validation.json` is produced with counts by severity.
- Given `--fix` flag is not supported, when users pass it, then CLI explains manual fix is required (explicitly out of scope).

---

## 8. Dependencies

| Item | Type | Notes |
|------|------|-------|
| Epic 1 Scripts | Internal | Provides `npm run validate` hook |
| `categories.txt` | Data | Source of allowed categories |
| GitHub Actions | Tooling | Executes validation job |

---

## 9. Release Plan

1. Draft schema + config definitions.
2. Implement Ajv-based schema validator with tests.
3. Add link checker module with concurrency support.
4. Layer accessibility lint via remark.
5. Wire CLI to npm scripts and CI, finalize docs.

---

## 10. Out of Scope

- Auto-fixers for metadata or content.
- Translation or localization checks.
- Validation of binary assets (PDF/PowerPoint).
- Spell-checking, grammar enforcement.

---

## 11. Open Questions & Assumptions

- Should link checker skip `.local` domains by default?
- Need decision on storing term definitions in JSON vs YAML.
- Assume contributors run Node 18+ locally; no backwards compatibility promised.

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 16:15
