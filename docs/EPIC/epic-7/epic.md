---
title: "Epic PRD: Phase 5 - CI/CD & Deployment Pipeline"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
epic_id: EPIC-007
status: Planned
source: ''
author: Portfolio Owner
post_slug: epic-7-cicd
categories: [docs, project]
tags: [cicd, deployment, automation]
ai_note: Assisted by AI (GitHub Copilot)
summary: Epic PRD describing the automated validation, build, test, and deployment workflow for the Academic Journey Portfolio.
date: 2025-12-04
---

## 1. Epic Name

CI/CD & Deployment Pipeline

---

## 2. Goal

### Problem

Manual builds are slow, error-prone, and make it difficult to enforce validation gates before publishing to GitHub Pages. There is no clear chain of custody for artifacts.

### Solution

Design a GitHub Actions pipeline that runs validation, testing, build, Lighthouse checks, and deployment to GitHub Pages. Include preview deployments for pull requests and enforce quality gates.

### Impact

| Metric | Target | Measurement |
|--------|--------|-------------|
| Deployment time | ≤5 minutes from merge to live | Actions logs |
| Pipeline success rate | ≥98% success across rolling 30 days | Actions metrics |
| Lighthouse performance | ≥90 per budget file | lhci report |
| Validation coverage | 100% of validators executed each run | CI summary |

---

## 3. Personas

- **Portfolio owner**: Wants worry-free deployments with consistent quality.
- **Reviewer**: Needs preview environments to review PR changes.
- **Automation**: Requires structured metadata to generate release notes.

---

## 4. Journeys

1. Owner pushes to `main`, pipeline runs validate → test → build → deploy in <10 minutes.
2. Reviewer opens PR, preview deploy link posts as comment for QA.
3. Failure in validation blocks downstream stages and posts actionable logs.

---

## 5. Business Requirements

### Functional

- FR-CICD-001: Provide workflows for push and pull requests.
- FR-CICD-002: Run validation scripts (schema, links, accessibility) before build.
- FR-CICD-003: Execute unit/integration tests with coverage gating (≥80%).
- FR-CICD-004: Build static site artifact and attach to workflow.
- FR-CICD-005: Deploy to GitHub Pages automatically on main.
- FR-CICD-006: Generate preview deployments for PRs.
- FR-CICD-007: Run Lighthouse CI with performance budgets.

### Non-Functional

- NFR-CICD-001: Pipeline completes within 15 minutes for 1000 files.
- NFR-CICD-002: Secrets stored in GitHub encrypted storage.
- NFR-CICD-003: Workflows documented in `docs/automation.md`.

---

## 6. Success Metrics

| KPI | Target | Method |
|-----|--------|--------|
| Mean deployment duration | ≤10 min | GitHub Actions metrics |
| Preview availability | 100% PRs include preview link | Bot comment audit |
| Quality gate adherence | 0 builds skip validation/test steps | Workflow logs |

---

## 7. Out of Scope

| Item | Reason |
|------|--------|
| Multi-environment deployments | GitHub Pages only |
| Canary releases | Not applicable to static site |
| Self-hosted runners | Hosted runners sufficient |

---

## 8. Business Value

High. Automation improves reliability, enforces compliance, and communicates status to stakeholders, freeing the owner to focus on content.

---

## 9. Dependencies

| Dependency | Type | Notes |
|------------|------|-------|
| Build scripts (Epic 1) | Internal | Provide `npm run build`, `npm run validate` |
| Tests (Epic 8) | Internal | Provide automated suites |
| Content (Epics 3-6) | Internal | Provide real site artifacts |

---

## 10. Risks & Mitigation

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Long pipeline duration | Medium | Medium | Cache npm deps, parallelize jobs |
| Lighthouse flakiness | Medium | Low | Retry once, use median score |
| Preview deploy limits | Low | Medium | Use feature branches only for critical previews |

---

## 11. Acceptance Criteria

- AC-EPIC-007-01: Workflow triggered on push to `main` automatically deploys to GitHub Pages.
- AC-EPIC-007-02: Pull request workflow posts preview URL comment.
- AC-EPIC-007-03: Pipeline fails if validation/test steps fail.
- AC-EPIC-007-04: Lighthouse job enforces budget thresholds.

---

## 12. References

- [Epic Breakdown](../PHASE-2/Epic-breakdown.md#epic-7-cicd--deployment-pipeline)
- [Project Specification - Section 14](../PHASE-1/Project_Specification.md#deployment)

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 17:18
