---
title: Project Architecture Blueprint
source: ''
author: Portfolio Owner
post_slug: project-architecture-blueprint
categories: [architecture, docs]
tags: [blueprint, jamstack, portfolio, static-site]
ai_note: Assisted by AI (GitHub Copilot)
summary: Comprehensive architecture blueprint for the Academic Journey Portfolio derived from Phase 1 specifications.
date: 2025-12-04
---
## 1. Architecture Detection and Analysis

- **Project type**: Jamstack static site hosted on GitHub Pages (REQ-001, PAT-001).
- **Framework candidates**: Eleventy or Astro for build automation, Markdown content with YAML front matter, minimal vanilla JS for progressive enhancement.
- **Architecture pattern**: Content-first layered architecture blending atomic design for UI, pipeline pattern for transformation, and CI/CD automation (PAT-002, PAT-005).
- **Dependency flow**: Content sources feed a transformation pipeline that emits pre-rendered HTML, CSS, and JSON indexes consumed by the GitHub Pages runtime; no server-side execution (CON-002, CON-003).
- **Communication mechanisms**: Mostly file-based during build, client-side interactions via DOM events, and optional fetch requests for JSON archives (REQ-005, REQ-006).

## 2. Architectural Overview

- **Guiding principles**: Separation of content, presentation, and behavior; single source of truth per requirement; automation-first validation; accessibility by default (REQ-007, NFR-004).
- **Boundaries**: Content acquisition isolated from UI rendering; reusable component library decoupled from term data; deployment scripts operate only on build outputs.
- **Hybrid patterns**: Static generation for deterministic pages combined with client-side micro-interactions (expand/collapse, filtering) implemented through progressive enhancement to remain usable without JS (CON-005).
- **Enforcement**: Directory conventions (`content/`, `components/`, `scripts/`, `_data/`) and lint/validation pipelines guard cross-layer violations (VAL-001 to VAL-006).

## 3. Architecture Visualization

### 3.1 High-Level System Topology

```text
+---------------+     +--------------------+     +-----------------+
| Content       | --> | Transformation      | --> | GitHub Pages    |
| Sources       |     | Pipeline (Node.js)  |     | CDN + HTTPS     |
+---------------+     +--------------------+     +-----------------+
       ^                        |                          |
       |                        v                          v
       |                +-----------------+        +---------------+
       +--------------  | Validation & QA |        | End Users     |
                         +-----------------+        +---------------+
```

### 3.2 Component Interaction View

```text
+-----------------+
| Content Catalog |
+-----------------+
          |
          v
+-----------------+     +--------------------+     +----------------------+
| Parser &        | --> | Component Templates | --> | Static Site Shell    |
| Metadata Loader |     | (Atomic Design)     |     | (Layouts + Routing)  |
+-----------------+     +--------------------+     +----------------------+
                                               \
                                                \---> Client Enhancers
```

### 3.3 Data Flow View

```text
Markdown + Assets --> Front Matter Validator --> Content Graph Builder
            |                                         |
            v                                         v
        Metadata JSON --------------------------> Term/Skill Index
                                                   |
                                                   v
                                         Client Filters & Search
```

## 4. Core Architectural Components

### 4.1 Content Source Manager

- **Purpose**: Aggregate Markdown from local directories and future repositories (REQ-001, REQ-012).
- **Structure**: Directory manifests, import adapters, checksum cache for incremental builds (REQ-014).
- **Interaction**: Emits normalized content graph for downstream parsing; receives configuration from `content.config.{json|yaml}`.
- **Evolution**: Add adapters for new storage (ZIP, remote repo) without touching parser via adapter interface.

### 4.2 Transformation & Validation Pipeline

- **Purpose**: Convert Markdown into HTML components, enforce schema, and generate derivative data (REQ-003, REQ-007).
- **Structure**: Sequential stages (lint -> validate -> transform -> optimize) orchestrated by npm scripts or custom CLI.
- **Interaction**: Consumes content graph, outputs build artifacts and validation reports consumed by CI (VAL-021).
- **Evolution**: Pluggable stage registry to insert new validators (e.g., AI-based quality checks) with minimal churn.

### 4.3 Component Library (Atomic Design)

- **Purpose**: Provide reusable UI fragments (atoms: badges, molecules: cards, organisms: term sections) (PAT-005).
- **Structure**: Templating engine partials with shared data contracts and SCSS modules.
- **Interaction**: Bound to JSON payloads produced by pipeline; progressive enhancement scripts subscribe to data attributes.
- **Evolution**: Add new component variations via modifier classes, keep BEM naming consistent (GUD-002).

### 4.4 Client Enhancement Layer

- **Purpose**: Offer filtering, expand/collapse, and accessible interactions while keeping static fallbacks (REQ-004 to REQ-006).
- **Structure**: ES modules compiled to one small bundle (<50KB) with feature detection gates.
- **Interaction**: Reads DOM data attributes, publishes custom events for analytics hooks.
- **Evolution**: New features implemented as opt-in controllers registered through a central initializer.

### 4.5 Deployment & Observability Tooling

- **Purpose**: Automate build, test, deploy, and monitor budgets (REQ-009, REQ-010).
- **Structure**: GitHub Actions workflow with build/test/deploy jobs, Lighthouse CI, link checker.
- **Interaction**: Pulls repo, caches node_modules, uploads artifact to Pages, posts status badges.
- **Evolution**: Additional environments (preview branches) plug into same workflow by parameterizing targets.

## 5. Architectural Layers and Dependencies

1. **Content Layer**: Markdown, assets, metadata schema (DAT-001).
2. **Build Layer**: Node.js tooling, validators, template renderers (PAT-004).
3. **Presentation Layer**: Generated HTML/CSS/JS served statically.
4. **Delivery Layer**: GitHub Pages CDN, HTTPS, caching (NFR-013).

**Rules**:

- Downstream layers only depend on outputs of upstream layers; no Presentation -> Build coupling at runtime.
- Shared contracts expressed as JSON schema types to prevent circular dependencies.
- DI pattern through configuration injection at build time; runtime uses data attributes rather than direct imports.

## 6. Data Architecture

- **Domain model**: `Term` aggregates `ContentItem`; each item has `metadata`, `body`, `assets`, linking to `SkillTag` and `Category` taxonomies.
- **Relationships**: Many-to-many between items and skills, one-to-many between terms and items, derived indexes for categories.
- **Access patterns**: Build-time repository queries (file globbing), runtime client fetch for optional JSON indexes.
- **Transformation**: Markdown -> AST -> sanitized HTML -> component props; metadata normalized to ISO 8601 and controlled vocabularies (VAL-007 to VAL-010).
- **Caching**: Incremental builds store content digests; CDN caches assets with hash-based filenames (NFR-012).
- **Validation**: JSON Schema + remark/rehype plugins enforce structure and accessible HTML.

## 7. Cross-Cutting Concerns Implementation

- **Authentication & Authorization**: Not required (static site); repo permissions and GitHub Pages controls guard writes (SEC-002).
- **Error Handling & Resilience**: Pipeline fails fast on schema violations, surfaces actionable diagnostics; client enhancements wrap logic in try/catch with aria-live announcements for degraded states (REQ-015).
- **Logging & Monitoring**: GitHub Actions logs, Lighthouse trend reports, optional privacy-friendly analytics for runtime event capture.
- **Validation**: Multi-stage validators (front matter, link checking, accessibility) with machine-readable reports for gating merges (VAL-001 to VAL-019).
- **Configuration Management**: `.env` for local overrides, `site.config.json` for shared settings, GitHub secrets for tokens; configuration merged via precedence rules (REQ-015).

## 8. Service Communication Patterns

- **Service boundaries**: Content pipeline vs. hosting vs. analytics; integrate via artifacts not live RPC.
- **Protocols**: HTTPS for GitHub APIs, REST for optional analytics, fetch-based JSON retrieval for client filters.
- **Sync vs async**: Build pipeline synchronous; runtime enhancements asynchronous but only for non-critical paths.
- **API versioning**: Data exports versioned through file names (`term-index.v1.json`); breaking changes require new suffix.
- **Service discovery**: Static configuration; no runtime discovery needed.
- **Resilience**: Optional JSON fetch guarded by timeout fallback to static experience.

## 9. Technology-Specific Architectural Patterns

### Static Site Stack (Detected)

- Node.js 18+ orchestrates npm scripts, Eleventy/Astro handles templating and data cascade.
- Layout inheritance ensures consistent chrome; global data files expose site metadata.
- Shortcodes encapsulate repeated fragments (badges, timeline markers).

#### .NET Architectural Patterns

- Not detected; repository contains no .NET assets. Section reserved for future integrations.

#### Java Architectural Patterns

- Not detected; build and runtime do not rely on JVM technologies.

#### React Architectural Patterns

- Not currently used; client layer sticks to framework-agnostic controllers to meet CON-005.

#### Angular Architectural Patterns

- Not detected; SPA frameworks would breach static hosting constraints.

#### Python Architectural Patterns

- Not detected; pipeline favors Node.js for tooling consistency, though data audits could adopt Python scripts later.

## 10. Implementation Patterns

- **Interface Design**: Define TypeScript-style typedefs (even in JS docs) for `ContentItem`, `TermIndex`, and component props; keep prop bags flattened to avoid deep destructuring.
- **Service Implementations**: Treat build stages as idempotent services invoked via npm scripts; compose them using a task runner (e.g., `npm-run-all`).
- **Repository Pattern**: Content repository abstracts file system with methods like `listByTerm(termId)` returning hydrated objects; enables unit testing with in-memory fixtures.
- **Controller/API Pattern**: Client controllers expose `init(el)` functions that attach behavior to DOM nodes; responses normalized to `Result<T>` objects for consistent error handling.
- **Domain Model Implementation**: Use value objects for `TermCode`, `SkillTag`, `CategorySlug` to enforce normalization and guard invalid strings.

## 11. Testing Architecture

- **Strategies**: Unit tests for parsers and helpers, integration tests for pipeline, visual regression for templates, accessibility tests (axe-core) (Phase 4 scope).
- **Boundaries**: Unit (helpers/validators) -> integration (build pipeline) -> system (deployed site) -> smoke (post-deploy health).
- **Test doubles**: Virtual file systems, stubbed fetch, fixture markdown directories.
- **Data strategy**: Fixture packs per term with golden outputs; auto-generated snapshots for HTML fragments.
- **Tooling**: Vitest/Jest, Playwright for E2E, Lighthouse CI, html-proofer for links.

## 12. Deployment Architecture

- **Topology**: Single GitHub repository, main branch triggers build and deploy to Pages; artifact stored in Pages environment.
- **Environment adaptations**: Preview branches deploy to staging URLs; config toggles (analytics) keyed by environment variables.
- **Runtime dependencies**: Only static files served via CDN; service workers optional for caching.
- **Configuration management**: GitHub environment secrets store tokens; `_config` or `site.config` selects environment-specific metadata.
- **Cloud integration**: Optional third-party analytics loaded via async script respecting CSP (SEC-005).

## 13. Extension and Evolution Patterns

- **Feature addition**: Create content types by extending JSON schema, add templates under appropriate atomic level, map to navigation metadata (GUD-002).
- **Modification**: Use feature flags (config-based) for risky changes; maintain backwards-compatible data fields and mark deprecations in schema changelog.
- **Integration**: Wrap external data feeds in adapters that sanitize payloads before merging with content graph; introduce anti-corruption layer to prevent schema pollution.

## 14. Architectural Pattern Examples

### Layer Separation Example

```markdown
---
title: Capstone Presentation
date: 2025-11-12
category: [academic, project]
skills: [presentation, research]
term: T3-AY2025
type: project
---
Summary paragraph...
```

Build step converts this into JSON props consumed by a component template:

```js
export const contentCard = ({ title, date, categories, body }) => `
  <article class="content-card" data-term="${categories.term}">
    <header>
      <h3>${title}</h3>
      <time datetime="${dateISO(date)}">${formatDate(date)}</time>
    </header>
    ${body}
  </article>`;
```

### Component Communication Example

```js
class FilterController {
  constructor(bus) {
    this.bus = bus;
  }

  init(root) {
    root.addEventListener('change', event => {
      this.bus.publish('filter.change', event.target.value);
    });
  }
}

bus.subscribe('filter.change', value => updateGrid({ value }));
```

### Extension Point Example

```js
registerAdapter('notion', async (config) => {
  const rows = await fetchNotionExport(config.token);
  return rows.map(toContentItem);
});
```

## 15. Architectural Decision Records

| Decision                          | Context                                        | Alternatives                       | Consequences                                   |
| --------------------------------- | ---------------------------------------------- | ---------------------------------- | ---------------------------------------------- |
| Static generation on GitHub Pages | Meets CON-001/CON-003, leverages free CDN      | Netlify/Vercel, custom server      | Zero runtime costs, limited server-side logic  |
| Atomic design component library   | Need reusable UI aligned with PAT-005          | Page-level templates only          | Higher upfront planning, easier future scaling |
| Node.js toolchain                 | Align with Jamstack ecosystem, reuse JS skills | Python static tooling, Ruby Jekyll | Unified language, dependency on npm ecosystem  |
| Progressive enhancement JS        | Accessibility + offline-first (NFR-004)        | SPA frameworks                     | Smaller bundles, but more manual wiring        |

## 16. Architecture Governance

- **Compliance checks**: Front matter validator, ESLint/stylelint, accessibility lint, link checker.
- **Automated enforcement**: GitHub Actions gates merges unless validation + tests pass (VAL-021).
- **Review process**: Architecture-affecting PRs require blueprint reference updates and mention in ADR table.
- **Documentation practice**: Significant changes documented in `docs/Project_Architecture_Blueprint.md` and summarized in release notes.

## 17. Blueprint for New Development

- **Workflow**: Identify requirement (e.g., REQ-006), update blueprint if architecture changes, implement in feature branch, run validation/test suites, submit PR referencing requirements.
- **Implementation templates**: Duplicate component scaffolds (`components/molecules/content-card.njk` + `content/examples/*.md`), update schema/test fixtures, register JS controller if needed.
- **Integration steps**: Wire content config, regenerate indexes, ensure navigation metadata updated, document feature in README or release notes.
- **Common pitfalls**: Skipping schema update when adding metadata, introducing blocking JS, bypassing accessibility review, forgetting to regenerate indexes leading to stale filters.
- **Currency**: Regenerate blueprint per phase milestone or after structural change; include timestamp in footnote to track freshness.

*v1.0.0 | Draft | Last Updated: Dec 04 2025 - 16:45*
