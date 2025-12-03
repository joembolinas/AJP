---
title: "Architecture: Content Integration"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
artifact_id: EPIC-006-ARCH
status: Planned
summary: Architecture blueprint for binding extracted content, metadata, and presentation templates.
categories: [docs, architecture]
tags: [content, pipeline, integration]
ai_note: Assisted by AI (GitHub Copilot)
---

## System Context

```text
Source Markdown -> Validation -> Extraction Pipeline -> Content Graph
                                                |-> HTML partials
                                                |-> Analytics JSON
```

Epic 6 consumes the finalized content graph and HTML partials to hydrate front-end templates.

## Modules

| Module | Description |
|--------|-------------|
| `content-manifest` | JSON describing source files, categories, visibility |
| `content-integrator` | Node script that maps manifest entries to components |
| `term-aggregator` | Creates chronological groupings and summaries |
| `skill-matrix` | Tallies skill usage per term for progression visual |
| `redaction-guard` | Removes or masks flagged content before render |

## Rendering Strategy

1. Load manifest and content graph via Eleventy data files (`_data/content.js`).
2. Build derived collections: per term, per category, featured items.
3. Pass derived data to Nunjucks/Astro templates for cards and highlights.
4. Emit JSON snapshots (`dist/data/content-report.json`) for QA + analytics.

## Data Contracts

- Manifest entry

```json
{
  "id": "t3-2025-sql-project",
  "path": "content/t3-ay2025/projects/sql.md",
  "category": "academic",
  "skills": ["sql", "data-modeling"],
  "term": "T3-AY2025",
  "hidden": false
}
```

- Derived card props (simplified)

```json
{
  "title": "Relational Modeling Workshop",
  "summary": "Designed and optimized a student services database...",
  "date": "2025-10-12",
  "term": "T3-AY2025",
  "skills": ["sql", "leadership"],
  "category": "academic",
  "slug": "relational-modeling-workshop"
}
```

## Security & Compliance

- Run redaction guard to ensure no private info or grades appear.
- Sanitize HTML snippets with DOMPurify running in Node (JSDOM) to remove inline scripts.
- Adopt content QA checklist requiring manual review of sensitive sections.

## Observability

- Integration script outputs `content-report.json` with counts and checksum per item.
- GitHub Actions uploads report as artifact for auditing.
- Optional Slack/webhook notification summarizing new/changed entries.

## Risks & Mitigation

| Risk | Mitigation |
|------|------------|
| Manifest drift vs filesystem | Generate manifest via script and diff |
| Broken relative media paths | Normalize and copy assets to `/assets/content` |
| Accessibility regression due to long content | Use `<details>` components to collapse |

## Testing Strategy

- Unit: Jest tests for manifest loader and slug generator.
- Integration: CLI run in CI verifying counts, metadata parity, redaction guard.
- Visual: Storybook snapshot for each category page after data binding.

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 17:05
