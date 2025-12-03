---
title: "Architecture: Content Schema & Validation System"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
source: ''
author: Portfolio Owner
post_slug: epic-2-validation-arch
categories: [architecture, docs]
tags: [validation, schema, tooling]
ai_note: Assisted by AI (GitHub Copilot)
summary: Architecture plan for the schema-driven validation toolkit that enforces AJP content quality.
date: 2025-12-04
epic_id: EPIC-002
status: Planned
---

## 1. Epic Architecture Overview

The validation system is a Node-based toolkit composed of modular rules orchestrated by a single CLI. Each rule (schema, taxonomy, accessibility, links) exposes a consistent interface so new checks can be registered without touching the core runner. Results feed into JSON reports for CI and enriched console output for local contributors. The architecture favors configuration over code by sourcing categories, terms, and severity settings from config files under `config/`.

---

## 2. System Architecture Diagram

```text
Sources (markdown files) --> Validation CLI --> Console Reporter
          |                        |                    |
          |                        |                    v
          |                        |          Report Writer (.reports/*.json)
          |                        v                    |
          |               External Websites <-----------+
          |                        |
          v                        v
     Link Checker -----------> GitHub Actions (CI gate)
```

---

## 3. High-Level Features & Technical Enablers

### Features

- Schema validation rule referencing JSON Schema definitions with version pinning.
- Taxonomy validation referencing categories.txt, skills.json, and term regexes.
- Accessibility lint rule built on remark plugins for heading order, alt text, and ARIA attributes.
- Link checker with concurrency controls, retries, and allow/deny lists.
- Report generator that outputs JSON plus optional JUnit for CI integration.

### Technical Enablers

- Ajv for schema validation with custom keywords.
- Remark + rehype plugin ecosystem for AST-level checks.
- Node fetch (or undici) for HTTP link validation with caching.
- Chokidar or fs.watch for optional watch mode.
- Shared config loader module to read validation.config.mjs.

---

## 4. Technology Stack

- Node.js 18 LTS, ECMAScript Modules.
- Ajv 8.x for JSON Schema validation.
- Remark/Unified for markdown AST traversal.
- Chalk or colorette for console formatting.
- undici/fetch for HTTP requests.
- Jest or Vitest for unit testing rule modules.

---

## 5. Technical Value

Value: High. Enforcing data integrity early prevents expensive fixes in Epic 4-6 and ensures CI remains trustworthy.

---

## 6. T-Shirt Size Estimate

Size: M (1 week). Requires multiple rules, config plumbing, and integration tests.

---

## 7. Deployment Considerations

- GitHub Actions job `validate.yml` should run validators in parallel steps when possible (schema + accessibility + links) to keep runtime below target.
- Provide CLI flags to skip link checks in local/offline scenarios but never in CI.
- Cache HTTP responses using `.cache/validation-links.json` between runs to reduce noise and timeouts.

---

## 8. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Overly strict schema blocking future content types | Medium | Medium | Support schema versioning plus compatibility mode |
| Link checker causes flaky CI due to external outages | Medium | Medium | Allow retry and soft-fail external-only errors with overrides |
| Accessibility lint produces false positives on code blocks | Low | Low | Skip fenced code regions and allow inline ignores |

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 16:22
