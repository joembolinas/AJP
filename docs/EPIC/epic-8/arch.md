---
title: "Architecture: Quality & Testing Stack"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
artifact_id: EPIC-008-ARCH
status: Planned
summary: Architecture outline for automated testing layers supporting the Academic Journey Portfolio.
categories: [docs, architecture]
tags: [testing, qa]
ai_note: Assisted by AI (GitHub Copilot)
---

## Layered Architecture

```text
Unit (Vitest)
  ↑  feeds
Integration (Pipeline fixtures)
  ↑  feeds
E2E (Playwright)
  ↘
   Accessibility (axe/Pa11y)
   Visual Regression (Chromatic/Percy)
```

Each layer builds upon lower layers to detect regressions early and cheaply.

## Toolchain Details

| Layer | Tooling | Responsibilities |
|-------|---------|------------------|
| Unit | Vitest + Testing Library | Validate schema validators, utility functions, component logic |
| Integration | Node scripts + fixtures | Run extraction pipeline end-to-end with mock directories |
| E2E | Playwright | Simulate user flows (navigation, filtering, expand) in headless browsers |
| Accessibility | axe-core + Pa11y | Scan rendered pages and Storybook stories |
| Visual | Chromatic/Percy | Snapshot core templates and detect UI diffs |

## Data Fixtures

- `tests/fixtures/content-small/` (5 files) for unit/integration.
- `tests/fixtures/content-full/` (subset of Term 3) for nightly suite.
- `tests/fixtures/graph.json` for deterministic Playwright assertions.

## Reporting Pipeline

1. Vitest generates `coverage/coverage-final.json`.
2. Integration tests emit `reports/pipeline-report.json` (counts, timings).
3. Playwright outputs traces + videos for failures.
4. axe-core results stored as SARIF uploaded to GitHub Security tab.
5. Visual diff statuses reported via Chromatic GitHub check.
6. `npm run qa:report` compiles results into `docs/reports/qa-status.md`.

## CI Integration

- Unit/integration tests run on every push/PR.
- E2E runs on PR + nightly scheduled job.
- Visual regressions triggered on PR when components change.
- Accessibility scans run nightly and on release branches.

## Governance

- Quality gates defined in `vitest.config.ts` and `.lighthouserc.js`.
- Owners documented in `CODEOWNERS` for test directories.
- Flaky test process: quarantine file, open issue, track in `qa-status.md`.

## Risks & Mitigations

| Risk | Mitigation |
|------|------------|
| Fixture rot as real content evolves | Regenerate fixtures via CLI weekly |
| Playwright environment mismatch (fonts, locale) | Use Docker container with pinned fonts/locales |
| Visual baseline drift | Require manual approval + note in PR |

---

v1.0 | Planned | Last Updated: Dec 04 2025 - 17:28
