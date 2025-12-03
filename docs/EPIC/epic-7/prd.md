---
title: "Feature PRD: Automated Build & Deploy"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
feature_id: EPIC-007-F1
status: Planned
summary: Feature plan for GitHub Actions workflows covering validation, testing, build, deployment, and preview environments.
categories: [docs, project]
tags: [cicd, github-actions]
ai_note: Assisted by AI (GitHub Copilot)
---

## Overview

Implements end-to-end automation for the Academic Journey Portfolio using GitHub Actions. Two workflows will exist: `ci.yml` for PRs and `deploy.yml` for main branch deployments.

---

## Objectives

- Run validation, tests, and build on every push/PR.
- Deploy to GitHub Pages automatically when `main` succeeds.
- Provide preview deployment URLs on PRs for UX review.
- Capture artifacts (coverage, content report, Lighthouse) for traceability.

---

## Functional Requirements

| ID | Description | Priority |
|----|-------------|----------|
| FR-007-01 | Checkout repo, setup Node 18, cache npm. | Must |
| FR-007-02 | Run `npm run validate` (schema, links, a11y). | Must |
| FR-007-03 | Run `npm run test -- --coverage` with ≥80% gate. | Must |
| FR-007-04 | Build static site via `npm run build`. | Must |
| FR-007-05 | Upload `dist/` as Pages artifact. | Must |
| FR-007-06 | Deploy via `actions/deploy-pages@v4`. | Must |
| FR-007-07 | Run Lighthouse CI against deployed URL. | Should |
| FR-007-08 | Add PR comment summarizing status + preview link. | Should |

---

## Non-Functional Requirements

- Pipeline runtime ≤12 minutes under nominal load.
- Workflows linted via `actionlint` to prevent syntax issues.
- Sensitive env vars (e.g., GH_TOKEN) stored as GitHub secrets.

---

## User Stories

1. As a maintainer, when I open a PR I receive a comment with validation/test results and a preview URL.
2. As a maintainer, deployment to production requires no manual steps beyond merging to `main`.
3. As a reviewer, I can access Lighthouse reports from the workflow summary.

---

## Release Plan

1. Author workflow yaml files, test locally via `act` (optional).
2. Create GitHub Pages environment + secrets.
3. Merge to main with feature flag disabled (dry run).
4. Enable deployment to production after validation.
5. Document pipeline in `docs/automation.md` with troubleshooting steps.

---

## Metrics

- Track workflow duration via GitHub Insights.
- Alert on failures >2 consecutive runs (manual review).
- Store coverage reports as build artifacts for 30 days.

---

## Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| npm cache corruption | Build failures | Use cache key with lockfile hash |
| Lighthouse rate limits | Missing report | Schedule job nightly if needed |
| Preview link missing due to permissions | Reviewer blocked | Use workflow bot token with comment access |

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 17:18
