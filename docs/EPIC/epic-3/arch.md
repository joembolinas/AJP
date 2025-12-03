---
title: "Architecture: Content Extraction & Transformation Pipeline"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
source: ''
author: Portfolio Owner
post_slug: epic-3-content-pipeline-arch
categories: [architecture, docs]
tags: [content, pipeline, automation]
ai_note: Assisted by AI (GitHub Copilot)
summary: Architecture view of the ingestion pipeline, adapters, and graph builders defined in Epic 3.
date: 2025-12-04
epic_id: EPIC-003
status: Planned
---

## 1. Architecture Overview

The pipeline is organized into four stages: source discovery, validation hand-off, transformation, and publishing. Sources are described in JSON manifests and scheduled via npm scripts. Each stage communicates through typed events so adapters remain decoupled. Outputs are normalized JSON graphs stored under `data/` and consumed by downstream build steps.

---

## 2. Processing Flow

```text
content-sources.json
        |
        v
 Source Loader ---> Validation (EPIC-002)
        |                 |
        |                 v
        |          Validated Markdown
        v
 Adapter Pool (filesystem, repo, future APIs)
        |
        v
 Markdown Parser --> Sanitizer --> Node Mapper
        |
        v
 Graph Builder ---> data/content-graph.json
        |
        +--> data/term-index.json
        +--> data/skill-index.json
        |
        v
 Summary Reporter + Cache Manager --> CI artifacts
```

---

## 3. Components & Enablers

- **Source Loader**: Reads manifest entries, resolves glob patterns, attaches metadata.
- **Adapter Interface**: Allows new backends (local FS today, remote repo later) without rewriting pipeline.
- **Parser & Sanitizer**: Remark-based pipeline with custom plugins for academic callouts and math formatting.
- **Graph Builder**: Creates normalized entities plus adjacency lists (term->items, skills->items).
- **Cache Manager**: Stores file checksums and transformation outputs to speed up re-runs.
- **Reporter**: Emits JSON + console summaries with severity counts and performance metrics.

Technical enablers include Node 18, remark, gray-matter, DOMPurify, LowDB (or plain JSON) cache, and winston/pino logging for structured output.

---

## 4. Technology Stack

- Node.js 18 LTS, ECMAScript Modules.
- remark/rehype plugins, gray-matter, DOMPurify.
- chokidar (watch mode) and fast-glob for file discovery.
- pino or winston for logging, Ajv for manifest validation.
- Jest/Vitest for unit tests, smoke tests executed via Playwright CLI.

---

## 5. Deployment & Operations

- CLI exposed via `npm run content:sync` and scheduled in CI (nightly + on-demand).
- Cache stored under `.cache/content-pipeline` with option to override location using env var.
- Reports uploaded as workflow artifacts so reviewers can download run history.
- Secrets are not required because pipeline reads local files only; manifest paths kept outside repo root via `.env.local`.

---

## 6. Technical Value & Estimate

Value: High — unlocks all downstream integration work.

T-shirt Size: M/L (1-2 weeks) depending on adapter complexity.

---

## 7. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Large file set slows builds | Medium | Medium | Parallelize parsing, add concurrency controls |
| Cache corruption | Low | Medium | Include checksum of cache + fallback clean command |
| Adapter explosion | Low | Medium | Document adapter pattern and keep stable interface |
| Security of sanitized HTML | Low | High | Use DOMPurify strict mode + allowlist |

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 16:34
