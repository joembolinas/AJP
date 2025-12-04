---
title: Contributing Guide
post_slug: contributing
categories: [process]
tags: [git, workflow, branching]
ai_note: Assisted by AI (GitHub Copilot)
summary: Contribution workflow and branching strategy for AJP.
date: 2025-12-04
---

## Contributing to AJP

This guide describes the Git Flow branching strategy adapted for a static-site, documentation-first project.

## Branches

- `main`: Production branch; source for GitHub Pages deployment.
- `develop`: Integration branch; all work merges here before release.
- `feature/[short-description]`: Feature or enhancement work.
- `docs/[section-or-topic]`: Documentation-only changes.
- `phase-N/[task]`: Work aligned to SDLC phases (e.g., `phase-2/structure`).
- `hotfix/[issue-slug]`: Urgent fixes for production (`main`).
- `release/vX.Y.Z`: Release preparation branches.

## Naming Conventions

- Use kebab-case for descriptions: `feature/content-pipeline`, `docs/agents-guide`.
- Keep names concise and specific; prefer nouns over verbs.
- Reference issue numbers when applicable: `feature/content-pipeline-#23`.

## Workflow

1. Branch off `develop` for regular work (features, docs, phases).
2. Commit with Conventional Commits (e.g., `feat: add content parser`).
3. Open a Pull Request targeting `develop`.
4. Keep PRs small, focused, and linked to issues.
5. After review, squash-merge into `develop`.
6. For releases: create `release/vX.Y.Z`, stabilize, then merge to `main` and tag.
7. For urgent production fixes: `hotfix/*` branches from `main`, then merge back to `main` and `develop`.

## Pull Requests

- Required checks: lint/docs build if configured.
- Template: clear scope, screenshots (if UI), and links to spec.
- Labels: `enhancement`, `docs`, `phase`, `hotfix`, `release` as applicable.

## Protection & Settings (GitHub)

- Protect `main` and `develop`: require PRs, dismiss stale reviews, and enforce linear history if desired.
- Link `main` to GitHub Pages (Pages settings).
- Enable branch naming rules via repository policies where available.

## References

- Git Flow model: [nvie.com: A successful Git branching model](https://nvie.com/posts/a-successful-git-branching-model/)
- Project Spec: `docs/PHASE-1/Project_Specification.md`
- SDLC: `SDLC.md`

---

v1.0.0 | Active | Last Updated: Dec 04 2025 - 14:45
