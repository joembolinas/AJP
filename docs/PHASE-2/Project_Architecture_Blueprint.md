---
title: Project Architecture Blueprint
source: ''
author: Portfolio Owner
post_slug: project-architecture-blueprint
categories: [architecture, docs]
tags: [blueprint, jamstack, portfolio, static-site]
ai_note: Assisted by AI (GitHub Copilot)
summary: Implementation-ready architecture blueprint for the Academic Journey Portfolio Phase 2 deliverable.
date: 2025-12-04
---
## Architecture Overview & Drivers

The Academic Journey Portfolio (AJP) is a JAMstack static site bound to GitHub Pages limits (CON-001, CON-004) and
atomic design ambitions (PAT-005). Architecture decisions focus on content-first pipelines, semantic presentation,
and automated validation so that functional requirements FR-001 to FR-014 can scale to 1,000+ entries without
architectural rework (NFR-010, NFR-011).

| Business Goal | Requirement IDs | Supporting Layers / Technologies |
| ------------- | --------------- | -------------------------------- |
| Capture 100% of academic artifacts per term | FR-001, FR-010, FR-014 | Content + Build layers using Markdown, gray-matter, checksum-based importers |
| Deliver modular, reusable UI at recruiter quality | FR-003, FR-004, PAT-005 | Presentation layer via Eleventy/Astro components, SCSS/BEM, Vanilla JS controllers |
| Enforce accessibility and validation by default | NFR-004, VAL-011 to VAL-020, AC-006 | Automation layer with AJV, axe-core, Lighthouse CI, html-proofer |
| Ship updates within 5 minutes of merge | FR-009, AC-005, VAL-021 | Automation + Delivery layers via GitHub Actions caching, artifact reuse, Pages deploy |
| Maintain GitHub Pages compliance while enabling future integrations | CON-001 to CON-006, NFR-014 | Development + Delivery layers with Node 18+, Git/GitHub workflows, AI-assisted prompts |

Drivers:

- JAMstack separation (PAT-001) keeps GitHub Pages CDN performant (NFR-003) while progressive enhancement satisfies
  CON-005 and Accessibility Guidelines (NFR-004).
- Atomic design and metadata-driven navigation align component growth with content growth, preventing layout rewrites
  when new terms or skills emerge (NFR-014, FR-011).

## Layered System Architecture

Each layer inherits responsibilities from the Technology Stack Blueprint while referencing Phase 1 requirements.

| Layer | Purpose | Key Technologies | Responsibilities | Requirements |
| ----- | ------- | ---------------- | ---------------- | ------------ |
| Delivery | Serve optimized static assets worldwide | GitHub Pages, HTTPS, CDN edge caching | Cache HTML/JS/CSS, enforce CSP/security headers | NFR-003, NFR-007, SEC series |
| Presentation | Render accessible UI | HTML5, SCSS (BEM), Vanilla JS (ESM) | Implement atomic templates, ARIA hooks, motion tokens | FR-003 to FR-006, NFR-004, VAL-011 to VAL-015 |
| Build | Transform and optimize content | Node.js 18+, Eleventy/Astro, esbuild, Sass | Parse markdown, compose layouts, minify assets, emit indexes | FR-002, FR-012, FR-013, NFR-002 |
| Content | Persist structured academic metadata | Markdown + YAML, JSON schema, checksum manifests | Capture term taxonomy, ensure schema alignment, stage assets | FR-001, FR-010, FR-014, DAT-001 |
| Automation | Enforce quality and deployments | GitHub Actions, Lighthouse CI, AJV, html-proofer | Lint, test, validate, deploy on merge | FR-007 to FR-009, VAL-001 to VAL-025, AC-005 |
| Development | Enable efficient authoring | VS Code, GitHub Copilot, npm scripts, docs | Provide scaffolds, prompts, instructions for contributors | GUD-001 to GUD-006, DOC standards |

ASCII dependency view (Technology Stack Blueprint naming, user-facing layer at the top):

```text
+------------------------------------------------------------------+
| Delivery: GitHub Pages + HTTPS + CDN Edge (NFR-003, NFR-007)      |
+------------------------------------------------------------------+
            ^
            |
+------------------------------------------------------------------+
| Presentation: HTML5 + SCSS/BEM + Vanilla JS PE (FR-003, NFR-004) |
+------------------------------------------------------------------+
            ^
            |
+------------------------------------------------------------------+
| Build: Node.js 18+, Eleventy/Astro, esbuild, Sass (FR-012)       |
+------------------------------------------------------------------+
            ^
            |
+------------------------------------------------------------------+
| Content: Markdown + YAML FM + JSON Schema (FR-001, FR-013)       |
+------------------------------------------------------------------+
            ^
            |
+------------------------------------------------------------------+
| Automation: GitHub Actions, Lighthouse CI, AJV, Pa11y (VAL-*)    |
+------------------------------------------------------------------+
            ^
            |
+------------------------------------------------------------------+
| Development: VS Code, Git, Copilot prompts (GUD-001 to GUD-006)  |
+------------------------------------------------------------------+
```

Runtime dependencies flow downward (Development tooling enables Automation, which gates Content → Delivery), while
feedback flows upward (e.g., Lighthouse alerts Development via Automation reports).

## Content & Build Pipelines

Content acquisition, validation, transformation, and deployment operate as a deterministic conveyor referencing
FR-001, FR-010, FR-012, VAL-001 to VAL-025.

ASCII sequence (simplified):

```text
Content Author -> Import Adapter -> Schema Validator -> Markdown Parser -> Component Builder
      |                  |                 |                   |                    |
      v                  v                 v                   v                    v
  Term folders      Source manifest    AJV reports       Eleventy data        _site artifact
                                            |                                     |
                                            v                                     v
                                      QA dashboards                      GitHub Pages Deploy
```

| Stage | Inputs | Actions & Tooling | Outputs | Requirement Links |
| ----- | ------ | ----------------- | ------- | ----------------- |
| Ingest | Term directories, repository mirrors | File adapters, checksum cache, `npm run ingest` | Normalized manifest with relative asset paths | FR-001, FR-010, NFR-014 |
| Validate | Manifest, Markdown | AJV (`lib/validators/front-matter.js`), markdownlint, html-proofer dry runs | Pass/fail report with VAL IDs | FR-007, VAL-001 to VAL-010 |
| Transform | Validated Markdown, schema-approved metadata | gray-matter, remark/rehype, Eleventy/Astro templates | HTML fragments, JSON indexes, RSS feeds | FR-002, FR-003, NFR-002 |
| Optimize | HTML/CSS/JS bundles, media assets | esbuild, Sass, Sharp (optional), asset hashing | Minified bundles, responsive images | NFR-001, NFR-002, VAL-016 to VAL-020 |
| Deploy | `_site` artifact | GitHub Actions Deploy Pages step, cache restore | Live HTTPS site, artifact retention | FR-009, AC-005, VAL-021 to VAL-025 |

Verification hooks surface warnings to `docs/PHASE-2/GIT_WORKFLOW.md` as required by AC-001.

## Component & Presentation Architecture

Atomic design hierarchy (PAT-005) ensures FR-003, FR-004, FR-006 and GUD-005 compliance:

- **Atoms**: badges, tags, buttons; accessible focus rings baked in.
- **Molecules**: `content-card`, `skill-list`, expand toggles with ARIA states (NFR-004, VAL-011-VAL-015).
- **Organisms**: `term-section`, navigation, filter bar binding molecules via semantic `<section>` wrappers.
- **Templates**: `home`, `term`, `project-detail` controlling layout flow.
- **Pages**: static Eleventy outputs per term, category, or highlight.

Sample directory outline (mirrors Technology Stack Blueprint):

```text
src/
  components/
    atoms/badge.njk
    molecules/content-card.njk
    organisms/term-section.njk
  styles/
    components/_content-card.scss
  scripts/
    controllers/filter-controller.js
```

Coding conventions:

- Semantic HTML headings never skip levels (VAL-012) and pair with ARIA attributes for icon buttons (VAL-015).
- BEM naming (`.content-card__header`, `.content-card--featured`) keeps selectors predictable (GUD-002).
- Progressive enhancement ensures toggles degrade gracefully if JavaScript fails (CON-005).

## Data & Metadata Architecture

Front matter schema excerpt (AJV enforced):

```json
{
  "$id": "content-schema.json",
  "required": ["title", "date", "category", "term", "type"],
  "properties": {
    "term": { "type": "string", "pattern": "^T[1-4]-AY\\d{4}$" },
    "skills": { "type": "array", "items": { "type": "string" } }
  }
}
```

| Field | Usage in Components | Validation & Errors |
| ----- | ------------------- | ------------------- |
| `title` | Rendered in `content-card` header and `<title>` tags | Missing title blocks build (VAL-001) |
| `date` | ISO string used for chronological sorting and `<time>` | Regex validation (VAL-007); bad values raise AJV error |
| `category` | Data attributes for filtering and navigation menus | Must match `categories.txt`; mismatches flagged (VAL-008) |
| `skills` | Skill badges and filter chips | Optional; duplicates removed during build |
| `term` | Creates term sections, anchors, navigation | Format `T#-AY####`; invalid codes stop pipeline |
| `type` | Drives template selection and icons | Enumerated values guard new layout requirements |

Error reporting: AJV emits JSON, CLI prints summarized table, GitHub Actions uploads artifact for review (VAL-001 to
VAL-003). Build halts on schema violations; warnings (e.g., large image) tag GitHub issue via workflow automation.

## Cross-Cutting Concerns

- **Accessibility**: ARIA patterns, focus management, keyboard traps prevention (NFR-004, VAL-011 to VAL-015).
- **Performance**: 2 MB/page budget (VAL-016) enforced via Lighthouse CI and asset hashing; lazy loading for media
  satisfies NFR-002 and NFR-015.
- **Security**: CSP + `Permissions-Policy` headers described in Technology Stack Blueprint; GitHub Pages enforces
  HTTPS and integrates with AC-005 (NFR-007, SEC series).
- **Caching**: `Cache-Control` strategies align with NFR-013; hashed filenames keep CDN immutable.
- **Validation notes**: Every edit must pass markdown lint, schema validation, link checks, Lighthouse budgets, and
  README instructions before merge, including front matter completeness, heading structure, and ≤400-character lines.
- **Diagram policy**: Architecture diagrams stay ASCII-only per validator guidance; mermaid or rich-media diagrams
  require an explicit stakeholder request before inclusion.

## CI/CD, Testing, and Quality Gates

Pipeline (Section 7 of spec) runs lint → validate → unit/integration tests → accessibility/performance audits → deploy.

| Stage | Tools | Purpose | Requirement IDs | Pass / Fail Criteria |
| ----- | ----- | ------- | --------------- | ------------------- |
| Lint | ESLint, Stylelint, markdownlint | Enforce coding and doc style | VAL-005, VAL-006 | Zero errors; warnings allowed only if justified |
| Schema Validation | AJV, custom CLI | Guarantee metadata completeness | VAL-001 to VAL-010 | Any failure blocks build |
| Unit & Integration Tests | Vitest, fixture FS, snapshot tests | Validate parsers, controllers, build pipeline | Section 7, AC-001 | ≥80% coverage, no failing tests |
| Accessibility & Performance | axe-core, Pa11y CI, Lighthouse CI | Uphold WCAG + Lighthouse budgets | NFR-003, NFR-004, VAL-011 to VAL-020 | Scores ≥ targets, zero critical axe findings |
| Link & Deploy | html-proofer, GitHub Actions deploy-pages | Ensure output integrity and ship artifact | FR-009, VAL-021 to VAL-025 | HTTP 200 for all pages; deploy job success |

Test alignment matrix:

| Validation Focus | Pipeline Stage | Requirement IDs | Evidence |
| ---------------- | -------------- | --------------- | -------- |
| Metadata schema | Schema Validation | VAL-001 to VAL-004, FR-013 | `npm run validate:schema` logs attached to workflow |
| Accessibility | Accessibility & Performance | NFR-004, AC-006 | axe-core + Pa11y reports stored as artifacts |
| Performance budgets | Accessibility & Performance | NFR-003, VAL-016 to VAL-020 | Lighthouse CI assertions ≥ 0.9/0.95/0.9/0.9 |
| Functional completeness | Unit & Integration tests | FR-002 to FR-006, AC-001 to AC-004 | Vitest summary + coverage report |
| Deployment readiness | Link & Deploy | FR-009, AC-005, VAL-021 to VAL-025 | GitHub Pages deployment log and status badge |

## Extension & Evolution Strategy

- **New terms**: Drop term folders under `content/` following naming convention; schema auto-picks up (NFR-014). No
  pipeline change required provided metadata conforms to `content-schema.json`.
- **New components**: Extend atomic directories, register SCSS partial, update `src/scripts/main.js` for behavior. All
  additions must cite relevant FR/NFR IDs in PR description per `.github/copilot-instructions.md`.
- **External integrations**: Add adapters in `lib/adapters/`; sanitize payloads to avoid violating CON-002. Document
  addition in `docs/AGENTS.md` (REQ, CON compliance) before merging.
- **AI-assisted updates**: Use prompt templates in `.github/prompt/`, capture rationale in ADR log, and link blueprint
  section to maintain traceability per GUD-001.

## Architectural Decision Log

| ID | Decision | Context & Drivers | Status | Consequences |
| -- | -------- | ----------------- | ------ | ------------ |
| ADR-001 | Prefer Eleventy with optional Astro fallback | GitHub Pages support (CON-004) and rapid prototyping | Proposed; finalize in Epic 1 | Minimizes config, but dual-path documentation required |
| ADR-002 | Enforce atomic design across presentation assets | PAT-005, FR-003 | Accepted | Requires shared design tokens and linting for BEM naming |
| ADR-003 | Use Vanilla JS progressive enhancement vs SPA | CON-005, NFR-004 | Accepted | Manual state management; JS bundle kept <30 KB |
| ADR-004 | Centralize validation via AJV + npm scripts | FR-007, VAL-001 | Accepted | Contributors must run `npm run validate` locally |
| ADR-005 | Store navigation metadata in `_data` JSON files | FR-002, FR-005 | Accepted | Navigation updates require JSON edit + schema check |
| ADR-006 | Run Lighthouse CI on every merge to main | NFR-003, AC-010 | Accepted | Longer pipeline runtime; ensures budget awareness |

## Risk & Mitigation Register

| Risk | Impact | Likelihood | Mitigation | Owners |
| ---- | ------ | ---------- | ---------- | ------ |
| Eleventy vs Astro decision delay | Blocks component scaffolding | Medium | Deliver POC comparing build time + Pages compatibility by Epic 1 retro | Architecture squad |
| Content schema drift across terms | Broken filters, failed builds | High | Lock schema versioning, require schema PR review, add schema tests | Data maintainers |
| Performance regression due to media bloat | Lighthouse failure (VAL-016) | Medium | Enforce image compression script + GitHub check | Frontend lead |
| Accessibility regressions | AC-006 failure, user impact | Medium | Automate Pa11y + manual spot checks; add checklist to PR template | QA lead |
| GitHub Actions minute limits exceeded | Slower deploys | Low | Cache dependencies, split workflows per branch, monitor usage monthly | DevOps |

## Requirement Coverage Matrix

| Blueprint Section | Requirement IDs | Coverage Status | Notes / Evidence |
| ----------------- | --------------- | --------------- | ---------------- |
| Architecture Overview & Drivers | FR-001 to FR-014, NFR-001 to NFR-015, CON series | Covered | Summaries cite IDs and tie to stack map |
| Layered System Architecture | FR-002 to FR-006, NFR-002 to NFR-004 | Covered | Layer table traces responsibilities to requirements |
| Content & Build Pipelines | FR-001, FR-007 to FR-010, VAL-001 to VAL-025 | Covered | Pipeline table + ASCII flow references spec Sec. 7 |
| Component & Presentation Architecture | FR-003 to FR-006, PAT-005, VAL-011 to VAL-015 | Covered | Atomic hierarchy, directory outline, BEM guidance |
| Data & Metadata Architecture | FR-013, VAL-001 to VAL-010 | Covered | Schema excerpt + field mapping |
| Cross-Cutting Concerns | NFR-003, NFR-004, SEC-001 to SEC-005, VAL-016 to VAL-020 | Covered | Budgets, CSP, caching documented |
| CI/CD, Testing, Quality Gates | VAL-001 to VAL-025, AC-001 to AC-010 | Covered | Stage table + alignment matrix |
| Extension & Evolution Strategy | NFR-014, CON-002, GUD-001 to GUD-006 | Covered | Guidelines reference `.github` instructions |
| ADR + Risk Registers | CON-001 to CON-006, PAT-001 to PAT-005 | Covered | ADR decisions cite constraints and patterns |

## Next Steps

- Run `npm run validate` locally to confirm schema, lint, and test suites before committing updates to this blueprint.
- Attach workflow evidence (Lighthouse, Pa11y, AJV logs) to future PRs to maintain traceability with VAL and AC IDs.

{v1.0.0 | Draft | Last Updated: Dec 04 2025 - 21:30}
