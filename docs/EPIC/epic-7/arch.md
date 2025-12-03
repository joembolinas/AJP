---
title: "Architecture: CI/CD & Deployment"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
artifact_id: EPIC-007-ARCH
status: Planned
summary: Architecture for GitHub Actions workflows, artifact handling, and deployment to GitHub Pages.
categories: [docs, architecture]
tags: [cicd, github-actions, automation]
ai_note: Assisted by AI (GitHub Copilot)
---

## Workflow Topology

```text
Push/PR Event
   │
   ├─ validate job (schema, links, a11y)
   │     └─ uploads validation report
   ├─ test job (unit, integration)
   │     └─ uploads coverage report
   ├─ build job (npm run build)
   │     └─ uploads Pages artifact
   └─ lighthouse job (post-deploy)
         └─ posts summary + budgets
```

Preview deployments branch off after build when event == `pull_request`.

## Key Components

| Component | Description |
|-----------|-------------|
| `ci.yml` | Runs on PR, executes validate/test/build, uploads artifacts, triggers preview deploy |
| `deploy.yml` | Runs on push to main, performs validate/test/build/deploy and Lighthouse |
| GitHub Pages environment | Stores production URL and enforces approvals if needed |
| Artifact store | Coverage, content reports, Lighthouse JSON |

## Implementation Details

- Use `actions/setup-node@v4` with npm cache keyed via `${{ runner.os }}-node-${{ hashFiles('package-lock.json') }}`.
- Validation/test runs reuse workspace by leveraging `actions/cache` and job outputs.
- Build job uploads `dist/` via `actions/upload-pages-artifact@v3`.
- Deploy job uses `actions/deploy-pages@v4` with environment protection rules.
- Preview deployments use `github-pages-deploy-action` or Pages preview API, with comment posted via `peter-evans/create-or-update-comment`.

## Observability & Alerts

- Enable GitHub Pages deployment protection logs.
- Use Lighthouse CI budget file stored at `lighthouse-budget.json`.
- Configure branch protection requiring `ci.yml` to pass before merging.

## Security

- Use GitHub OIDC to request temporary tokens if publishing to other services.
- Store tokens (e.g., `LIGHTHOUSE_GH_TOKEN`) as repository secrets.
- Limit workflow permissions to `contents: read` for CI, `contents: write` for deploy job only.

## Testing

- Validate workflows with `actionlint` locally.
- Use `act` for dry runs when editing YAML.
- Maintain integration tests for preview comment action via mocked API calls.

## Risks

| Risk | Mitigation |
|------|------------|
| Workflow drift (multiple files) | Consolidate shared steps via reusable workflow or composite action |
| Artifact size over quota | Prune old artifacts using retention policies |
| Preview deployments failing due to Pages restriction | Fallback to Surge/Netlify preview if needed |

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 17:18
