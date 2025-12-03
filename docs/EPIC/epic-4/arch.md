---
title: "Architecture: Component-Based Presentation Layer"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
source: ''
author: Portfolio Owner
post_slug: epic-4-presentation-arch
categories: [architecture, docs]
tags: [components, accessibility, design]
ai_note: Assisted by AI (GitHub Copilot)
summary: Architecture description for the atomic component system powering Epic 4.
date: 2025-12-04
epic_id: EPIC-004
status: Planned
---

## 1. Architecture Overview

The presentation layer is a component library built on semantic HTML, SCSS modules (or CSS), and Eleventy templates. Atomic units live under `src/components/{atoms|molecules|organisms}` with paired README files and Storybook stories. Tokens and utilities are centralized, keeping the build deterministic and portable to other static generators.

---

## 2. Component Stack Diagram

```text
Design Tokens -> Utilities -> Atoms -> Molecules -> Organisms -> Templates -> Pages
       |             |          |           |             |             |
       |             |          |           |             |             v
       |             |          |           |             |      Eleventy Layouts
       |             |          |           |             v
       |             |          |           v      Storybook / Docs
       |             |          v
       |             v    Accessible Behaviors (JS enhancement)
       v
Stylelint + Accessibility Tests
```

---

## 3. Key Components & Enablers

- **Token Layer**: JSON/SCSS variables for color, typography, spacing, shadow, z-index.
- **Utility Layer**: Mixins/helpers for media queries, focus outlines, fluid type scales.
- **Atoms**: Buttons, skill tags, badges, icon-only buttons, heading wrappers.
- **Molecules**: Metadata stack, expandable card body, filter pill groups, CTA rows.
- **Organisms/Templates**: Term grid, achievements carousel (with no-JS fallback), hero header, filter side panel.
- **Docs Tooling**: Storybook or Eleventy component gallery, plus mdx/markdown usage notes.

---

## 4. Technology Stack

- Eleventy (Nunjucks/Liquid) components or Astro islands (decision final during build).
- SCSS modules compiled via PostCSS + autoprefixer.
- Stylelint w/ BEM rules, Prettier for formatting.
- Storybook 8 (optional) or Eleventy component gallery for documentation.
- Lighthouse CI + axe for accessibility validation.

---

## 5. Deployment & Ops

- Components compiled into `dist/assets/css` with hashed filenames.
- JS enhancements (accordion, skip-link focus fix) bundled via Vite/ESBuild.
- A11y and visual regression tests executed in CI prior to publishing to GitHub Pages.
- Component docs deployed with site or kept under `/docs/components/` for contributors.

---

## 6. Technical Value & Size

Value: High — enables consistent UX and drastically reduces future dev time.

T-Shirt Size: M (approx. 1.5 weeks) assuming design tokens are defined.

---

## 7. Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| CSS bloat | Medium | Medium | Enforce tree-shaking via PostCSS purge + component scoping |
| Accessibility regressions | Low | High | Add axe tests + manual keyboard audits per release |
| Storybook maintenance overhead | Low | Medium | Automate story scaffolding from component folders |
| Lack of design tokens | Medium | Medium | Derive from spec immediate requirements, iterate later |

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 16:44
