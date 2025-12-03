---
title: "Architecture: Foundation & Project Infrastructure"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
source: ''
author: Portfolio Owner
post_slug: epic-1-foundation-arch
categories: [architecture, docs]
tags: [infrastructure, tooling, scaffolding]
ai_note: Assisted by AI (GitHub Copilot)
summary: High-level architecture describing the foundational tooling, repository structure, and automation for Epic 1.
date: 2025-12-04
epic_id: EPIC-001
status: In Progress
---

## 1. Epic Architecture Overview

Epic 1 delivers the scaffolding that every other phase depends on. The architecture focuses on reproducible local environments, deterministic builds, and strong project guardrails. A single source of truth `package.json` exposes scripts that orchestrate linting, validation, and static site generation. Directory conventions match the content pipeline defined in the specification, enabling Copilot and humans to locate assets consistently.

---

## 2. System Architecture Diagram

```text
+------------------+        +-------------------+
| Contributors     |        | GitHub Copilot    |
| (VS Code + Git)  |        | (AI Pair)         |
+---------+--------+        +---------+---------+
		  |                           |
		  | git clone / commits       | reads guidance
		  v                           v
+-----------------------------------------------+
| Local Workspace                              |
|  - scripts/bootstrap.(ps1|sh)                 |
|  - package.json (lint, build, validate)       |
|  - content/, components/, _data/, docs/       |
|  - .github/copilot-instructions.md            |
+------------------------+----------------------+
						 |
						 | CI trigger (push/PR)
						 v
+-----------------------------------------------+
| GitHub Actions Runner                         |
|  - npm ci                                     |
|  - npm run lint, test:types, validate         |
|  - npm run build -> dist/                     |
+------------------------+----------------------+
						 |
						 | artifact
						 v
+-----------------------------------------------+
| GitHub Pages Preview (staging artifact)       |
+-----------------------------------------------+
```

This ASCII diagram highlights how local tooling, scripts, and CI workflows interact to provide a consistent foundation.

---

## 3. High-Level Features & Technical Enablers

### Features

- Repository bootstrap script that provisions canonical folders and placeholder files.
- Baseline Eleventy/Astro project with default layout, data loaders, and sample content.
- Linting, formatting, and validation npm scripts surfaced through `npm run lint`, `npm run style`, `npm run validate`.
- Conventional commit helper plus Husky pre-commit pipeline.
- Documentation touchpoints (README, CONTRIBUTING draft, Copilot instructions) referencing requirement IDs.

### Technical Enablers

- Node.js 18+ runtime plus Volta or Corepack pinning for consistent versions.
- ESLint shareable config capturing accessibility and BEM linting.
- EditorConfig + Prettier to ensure cross-editor consistency.
- GitHub repository templates: issue template, PR template, codeowners.

---

## 4. Technology Stack

- Node.js 18 LTS, npm 10, optional pnpm via Corepack.
- Eleventy 3.x (preferred) or Astro 4.x for static site generation.
- ESLint, Stylelint, Prettier, markdownlint for quality gates.
- Husky + lint-staged for pre-commit enforcement.
- GitHub Actions for continuous validation.
- VS Code devcontainer (optional) for environment parity.

---

## 5. Technical Value

**Value: High.** A reliable foundation avoids cascading failures in later phases, reduces onboarding time, and ensures Copilot generates conformant code. Toolchain automation also enforces architectural conventions without manual review overhead.

---

## 6. T-Shirt Size Estimate

**Size: S (3-5 days).** Work is configuration-heavy with minimal coding but requires careful validation across environments.

---

## 7. Deployment Considerations

- GitHub Actions workflow templates should live under `.github/workflows/validate.yml` even before deployment-specific logic exists, enabling incremental hardening.
- Use environment variables via `.env.example` for paths (e.g., `CONTENT_ROOT`) while keeping secrets out of scope for this static phase.
- Document fallback instructions for developers without WSL by providing PowerShell mirror scripts.

---

## 8. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Toolchain drift between contributors | Medium | Medium | Use Volta/Corepack pinning plus lockfile commits |
| Eleventy vs Astro decision churn | Low | Medium | Document selection criteria and keep adapter interface thin |
| Copilot ignoring custom instructions | Medium | Low | Add reminders in templates and README, include references in prompts |
| Windows path issues in scripts | Medium | High | Provide dual `.ps1` and `.sh` scripts and rely on Node-based tooling |

---

v1.0 | Active | Last Updated: Dec 04 2025 - 16:00
