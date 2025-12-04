---
title: Git Branching Workflow
source: ''
author: Portfolio Owner
post_slug: git-workflow
categories: [docs, workflow, git]
tags: [git, branching, workflow, gitflow, development]
ai_note: Assisted by AI (GitHub Copilot)
summary: Comprehensive Git branching strategy and workflow for the AJP project lifecycle.
date: 2025-12-04
---
# Git Branching Workflow

> Complete Git Flow branching strategy for the Academic Journey Portfolio (AJP) project.

## Table of Contents

- [Branch Structure](#branch-structure)
- [Permanent Branches](#permanent-branches)
- [Temporary Branches](#temporary-branches)
- [Branch Lifecycle by Project Phase](#branch-lifecycle-by-project-phase)
- [Workflow Scenarios](#workflow-scenarios)
- [Merge Strategy](#merge-strategy)
- [Quick Reference](#quick-reference)

---



## Branch Examples

- `feature/component-library`
- `feature/content-ingestion-pipeline`
- `docs/agents-guide-update`
- `docs/readme-links-fix`
- `phase-2/repo-structure`
- `phase-3/config-content-sources`
- `hotfix/pages-build-error-#12`
- `release/v1.1.0`

## PR Targets

- Features/Docs/Phase → `develop`
- Release → `main` (after review)
- Hotfix → `main`, then back-merge to `develop`

## Commit Style

- `feat: add term-based content router`
- `docs: expand contributing guide with PR rules`
- `fix: correct broken site links`
- `chore: bump dependencies`

---



## Branch Structure

```text
┌─────────────────────────────────────────────────────────────┐
│                    PERMANENT BRANCHES                        │
├─────────────────────────────────────────────────────────────┤
│  main      → Production code (GitHub Pages deployment)      │
│  develop   → Integration branch (latest development)        │
└─────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────┐
│                    TEMPORARY BRANCHES                        │
├─────────────────────────────────────────────────────────────┤
│  feature/*     → New features and enhancements              │
│  epic/*        → Large features spanning multiple PRs       │
│  release/*     → Release preparation                        │
│  hotfix/*      → Critical production fixes                  │
│  bugfix/*      → Non-critical bug fixes                     │
│  docs/*        → Documentation updates                      │
│  refactor/*    → Code refactoring                           │
│  test/*        → Testing improvements                       │
│  chore/*       → Maintenance tasks                          │
└─────────────────────────────────────────────────────────────┘
```

---

## Permanent Branches

### `main`

**Purpose**: Production-ready code deployed to GitHub Pages

**Characteristics**:

- Every commit represents a stable release
- Protected branch (requires PR + review)
- Auto-deploys to https://joembolinas.github.io
- Tagged with version numbers (v1.0.0, v2.0.0, etc.)
- Never commit directly to main

**Accepts merges from**:

- `release/*` branches (for new releases)
- `hotfix/*` branches (for critical fixes)

**Example commits**:

```bash
v1.0.0 - Initial portfolio launch
v1.1.0 - Added project filtering feature
v1.1.1 - Hotfix: Fixed broken navigation links
```

---

### `develop`

**Purpose**: Integration branch for ongoing development

**Characteristics**:

- Contains latest development changes
- More stable than feature branches
- Base branch for all feature development
- Regularly merged to main via releases

**Accepts merges from**:

- `feature/*` branches
- `epic/*` branches
- `bugfix/*` branches
- `docs/*` branches
- `refactor/*` branches
- `test/*` branches
- `chore/*` branches
- `hotfix/*` branches (after merging to main)

**Merged to**:

- `main` (via release branches)

---

## Temporary Branches

### `feature/*`

**Purpose**: New features, enhancements, and improvements

**Branch from**: `develop`
**Merge to**: `develop`
**Naming**: `feature/<descriptive-name>` or `feature/<issue-number>-<description>`

**When to use**:

- Adding new UI components
- Implementing new functionality
- Performance improvements
- New content types or layouts
- Configuration additions

**Examples**:

```bash
feature/gitflow-workflow-setup
feature/term-navigation-component
feature/project-card-component
feature/skill-filter-system
feature/dark-mode-toggle
feature/search-functionality
feature/404-error-page
feature/rss-feed-generator
feature/social-share-buttons
feature/analytics-integration
```

**Lifecycle**:

```bash
# Create feature branch
git checkout develop
git pull origin develop
git checkout -b feature/new-feature

# Work on feature
git add .
git commit -m "feat: implement new feature"

# Keep updated with develop
git fetch origin
git rebase origin/develop

# Push to remote
git push -u origin feature/new-feature

# Merge via PR to develop
# Delete branch after merge
git branch -d feature/new-feature
```

---

### `epic/*`

**Purpose**: Large features that span multiple PRs or sub-features

**Branch from**: `develop`
**Merge to**: `develop`
**Naming**: `epic/<epic-number>-<epic-name>`

**When to use**:

- Major system overhauls
- Multi-component features
- Features with multiple sub-tasks
- Cross-cutting changes

**Examples**:

```bash
epic/1-content-pipeline-system
epic/2-component-architecture
epic/3-metadata-extraction
epic/4-content-integration
epic/5-ui-components
epic/6-testing-framework
epic/7-deployment-automation
epic/8-performance-optimization
epic/9-accessibility-compliance
```

**Sub-feature workflow**:

```bash
# Create epic branch
git checkout -b epic/1-content-pipeline-system develop

# Create sub-feature from epic
git checkout -b feature/content-parser epic/1-content-pipeline-system

# Merge sub-feature to epic
git checkout epic/1-content-pipeline-system
git merge --no-ff feature/content-parser

# Finally merge epic to develop
git checkout develop
git merge --no-ff epic/1-content-pipeline-system
```

---

### `release/*`

**Purpose**: Prepare for production release

**Branch from**: `develop`
**Merge to**: `main` AND `develop`
**Naming**: `release/v<version>`

**When to use**:

- Preparing for version release
- Version number updates
- Final bug fixes
- Documentation finalization
- Build configuration

**Examples**:

```bash
release/v1.0.0
release/v1.1.0
release/v2.0.0
release/v1.2.0-beta
```

**Release workflow**:

```bash
# Create release branch
git checkout -b release/v1.1.0 develop

# Bump version
# Update CHANGELOG.md
# Final testing and bug fixes
git commit -am "chore: prepare release v1.1.0"

# Merge to main
git checkout main
git merge --no-ff release/v1.1.0
git tag -a v1.1.0 -m "Release v1.1.0"

# Merge back to develop
git checkout develop
git merge --no-ff release/v1.1.0

# Push everything
git push origin main develop --tags

# Delete release branch
git branch -d release/v1.1.0
```

---

### `hotfix/*`

**Purpose**: Critical fixes for production issues

**Branch from**: `main`
**Merge to**: `main` AND `develop`
**Naming**: `hotfix/v<version>` or `hotfix/<critical-issue>`

**When to use**:

- Security vulnerabilities
- Critical production bugs
- Broken deployment
- Data corruption fixes
- Service outages

**Examples**:

```bash
hotfix/v1.1.1
hotfix/security-xss-patch
hotfix/broken-navigation
hotfix/image-loading-error
hotfix/deployment-failure
```

**Hotfix workflow**:

```bash
# Create hotfix from main
git checkout -b hotfix/v1.1.1 main

# Fix the issue
git commit -am "fix: critical navigation bug"

# Merge to main
git checkout main
git merge --no-ff hotfix/v1.1.1
git tag -a v1.1.1 -m "Hotfix v1.1.1"

# Merge to develop
git checkout develop
git merge --no-ff hotfix/v1.1.1

# Push and delete
git push origin main develop --tags
git branch -d hotfix/v1.1.1
```

---

### `bugfix/*`

**Purpose**: Non-critical bug fixes during development

**Branch from**: `develop`
**Merge to**: `develop`
**Naming**: `bugfix/<issue-description>`

**When to use**:

- UI glitches
- Minor functionality issues
- Non-blocking errors
- Development environment fixes

**Examples**:

```bash
bugfix/card-alignment-issue
bugfix/filter-button-state
bugfix/typo-in-footer
bugfix/broken-link-references
bugfix/css-overflow-mobile
```

---

### `docs/*`

**Purpose**: Documentation updates and improvements

**Branch from**: `develop`
**Merge to**: `develop`
**Naming**: `docs/<doc-topic>`

**When to use**:

- README updates
- Specification changes
- Guide creation
- Comment improvements
- API documentation

**Examples**:

```bash
docs/api-documentation
docs/readme-update
docs/contributing-guide
docs/architecture-diagram
docs/deployment-instructions
docs/component-guidelines
```

---

### `refactor/*`

**Purpose**: Code refactoring without changing functionality

**Branch from**: `develop`
**Merge to**: `develop`
**Naming**: `refactor/<area-being-refactored>`

**When to use**:

- Code cleanup
- Performance optimization
- Architecture improvements
- Removing technical debt
- Simplifying complex code

**Examples**:

```bash
refactor/component-structure
refactor/css-organization
refactor/content-parser
refactor/utility-functions
refactor/file-structure
```

---

### `test/*`

**Purpose**: Testing improvements and additions

**Branch from**: `develop`
**Merge to**: `develop`
**Naming**: `test/<test-scope>`

**When to use**:

- Adding test coverage
- Test framework setup
- Accessibility testing
- Performance testing
- Integration testing

**Examples**:

```bash
test/lighthouse-automation
test/accessibility-checks
test/component-unit-tests
test/e2e-navigation
test/performance-benchmarks
```

---

### `chore/*`

**Purpose**: Maintenance tasks and tooling

**Branch from**: `develop`
**Merge to**: `develop`
**Naming**: `chore/<task-description>`

**When to use**:

- Dependency updates
- Build configuration
- CI/CD pipeline changes
- Development tooling
- Git workflow setup

**Examples**:

```bash
chore/dependency-updates
chore/github-actions-setup
chore/eslint-configuration
chore/prettier-setup
chore/gitignore-update
```

---

## Branch Lifecycle by Project Phase

### Phase 1: Documentation (Current)

**Active branches**:

```bash
main                              # Empty/initial commit
develop                           # Integration
feature/gitflow-workflow-setup    # Current work
docs/project-specification        # Spec updates
docs/agents-reference            # Agent guide
docs/sdlc-overview               # SDLC documentation
```

**Expected activity**: Heavy documentation, planning, specification

---

### Phase 2: Design & Architecture

**Expected branches**:

```bash
epic/2-project-architecture       # Main epic
feature/component-structure       # Component design
feature/content-schema           # Content structure
feature/folder-organization      # File structure
docs/architecture-blueprint      # Architecture docs
refactor/initial-structure       # Structure refinement
```

**Expected activity**: Architecture setup, component design

---

### Phase 3: Development

**Expected branches**:

```bash
epic/3-content-extraction         # Content pipeline
epic/4-content-integration        # Integration system
epic/5-ui-components              # UI development
feature/markdown-parser           # Content parsing
feature/metadata-extractor        # Metadata handling
feature/term-component            # Term display
feature/project-card              # Project cards
feature/navigation-menu           # Navigation
feature/footer-component          # Footer
bugfix/*                          # Various fixes
test/component-testing            # Testing
```

**Expected activity**: Heavy feature development, testing

---

### Phase 4: Testing

**Expected branches**:

```bash
test/accessibility-audit          # A11y testing
test/performance-testing          # Performance
test/cross-browser-testing        # Compatibility
test/lighthouse-checks            # Quality metrics
bugfix/accessibility-issues       # A11y fixes
bugfix/performance-issues         # Performance fixes
refactor/optimization             # Code optimization
```

**Expected activity**: Testing, bug fixing, optimization

---

### Phase 5: Deployment

**Expected branches**:

```bash
release/v1.0.0                    # First release
chore/github-pages-setup          # Deployment config
chore/ci-cd-pipeline              # Automation
docs/deployment-guide             # Deploy docs
hotfix/deployment-issues          # Deploy fixes (if needed)
```

**Expected activity**: Release prep, deployment automation

---

### Phase 6: Maintenance

**Expected branches**:

```bash
feature/t4-ay2026-content         # New term content
feature/new-project-type          # New features
hotfix/broken-link                # Production fixes
bugfix/mobile-responsiveness      # Minor fixes
chore/dependency-updates          # Maintenance
docs/content-guidelines           # Documentation
```

**Expected activity**: Content updates, maintenance, enhancements

---

## Workflow Scenarios

### Scenario 1: Starting a New Feature

```bash
# 1. Update develop
git checkout develop
git pull origin develop

# 2. Create feature branch
git checkout -b feature/new-awesome-feature

# 3. Work on feature
# ... make changes ...
git add .
git commit -m "feat: add awesome feature"

# 4. Push to remote
git push -u origin feature/new-awesome-feature

# 5. Create Pull Request on GitHub
# 6. After approval, merge to develop
# 7. Delete branch
git branch -d feature/new-awesome-feature
```

---

### Scenario 2: Working on an Epic

```bash
# 1. Create epic branch
git checkout -b epic/5-ui-components develop

# 2. Create sub-features
git checkout -b feature/header-component epic/5-ui-components
# ... work on header ...
git checkout epic/5-ui-components
git merge --no-ff feature/header-component

git checkout -b feature/footer-component epic/5-ui-components
# ... work on footer ...
git checkout epic/5-ui-components
git merge --no-ff feature/footer-component

# 3. When epic is complete
git checkout develop
git merge --no-ff epic/5-ui-components
```

---

### Scenario 3: Preparing a Release

```bash
# 1. Create release branch from develop
git checkout -b release/v1.0.0 develop

# 2. Bump version in package.json, README, etc.
# 3. Update CHANGELOG.md
# 4. Final testing

# 5. Merge to main
git checkout main
git merge --no-ff release/v1.0.0
git tag -a v1.0.0 -m "Release version 1.0.0"

# 6. Merge back to develop
git checkout develop
git merge --no-ff release/v1.0.0

# 7. Push everything
git push origin main develop --tags

# 8. Cleanup
git branch -d release/v1.0.0
```

---

### Scenario 4: Emergency Hotfix

```bash
# 1. Create hotfix from main
git checkout -b hotfix/v1.0.1 main

# 2. Fix the critical issue
git commit -am "fix: critical security vulnerability"

# 3. Merge to main
git checkout main
git merge --no-ff hotfix/v1.0.1
git tag -a v1.0.1 -m "Hotfix v1.0.1 - Security patch"

# 4. Merge to develop
git checkout develop
git merge --no-ff hotfix/v1.0.1

# 5. Push and cleanup
git push origin main develop --tags
git branch -d hotfix/v1.0.1
```

---

### Scenario 5: Keeping Feature Branch Updated

```bash
# Option A: Rebase (cleaner history)
git checkout feature/my-feature
git fetch origin
git rebase origin/develop

# Option B: Merge (preserves history)
git checkout feature/my-feature
git fetch origin
git merge origin/develop
```

---

## Merge Strategy

### Merge Flags

**Always use `--no-ff` for important merges**:

```bash
git merge --no-ff feature/important-feature
```

This preserves branch history and makes it clear when features were merged.

### When to use `--no-ff`:

- ✅ Merging feature to develop
- ✅ Merging epic to develop
- ✅ Merging release to main
- ✅ Merging hotfix to main
- ✅ Merging release/hotfix back to develop

### When NOT to use `--no-ff`:

- ❌ Rebasing feature branches
- ❌ Fast-forward updates from develop

---

### Pull Request Requirements

**All merges to develop require**:

- Descriptive PR title
- Detailed description
- Linked issues (if applicable)
- Passing tests (when implemented)
- Code review (recommended)

**All merges to main require**:

- All of the above
- Version tag
- Updated CHANGELOG
- Deployment verification

---

## Quick Reference

### Branch Naming Cheat Sheet

| Type     | Format                   | Example                   |
| -------- | ------------------------ | ------------------------- |
| Feature  | `feature/<name>`       | `feature/search-bar`    |
| Epic     | `epic/<number>-<name>` | `epic/3-content-system` |
| Release  | `release/v<version>`   | `release/v1.2.0`        |
| Hotfix   | `hotfix/v<version>`    | `hotfix/v1.2.1`         |
| Bugfix   | `bugfix/<issue>`       | `bugfix/broken-link`    |
| Docs     | `docs/<topic>`         | `docs/readme-update`    |
| Refactor | `refactor/<area>`      | `refactor/css-cleanup`  |
| Test     | `test/<scope>`         | `test/unit-tests`       |
| Chore    | `chore/<task>`         | `chore/deps-update`     |

---

### Common Commands

```bash
# List all branches
git branch -a

# Delete local branch
git branch -d branch-name

# Delete remote branch
git push origin --delete branch-name

# Rename current branch
git branch -m new-name

# See branch merge status
git branch --merged
git branch --no-merged

# Clean up deleted remote branches
git fetch --prune

# View branch graph
git log --graph --oneline --all
```

---

### Estimated Branch Count Over Project Lifecycle

| Phase   | Estimated Branches | Types                                   |
| ------- | ------------------ | --------------------------------------- |
| Phase 1 | 5-10               | docs/*, feature/*                     |
| Phase 2 | 10-15              | epic/*, feature/*, refactor/*         |
| Phase 3 | 30-50              | epic/*, feature/*, bugfix/*, test/* |
| Phase 4 | 15-25              | test/*, bugfix/*, refactor/*          |
| Phase 5 | 5-10               | release/*, hotfix/*, chore/*          |
| Phase 6 | 10-20/year         | feature/*, bugfix/*, hotfix/*         |

**Total estimated**: 75-130 temporary branches across full project lifecycle

---

### Branch Protection Rules (Recommended)

**For `main`**:

- Require pull request reviews
- Require status checks to pass
- Require branches to be up to date
- Include administrators
- Restrict who can push

**For `develop`**:

- Require pull request reviews (optional)
- Require status checks to pass (when available)
- Allow force pushes (only if needed)

---

## Commit Message Convention

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```bash
<type>(<scope>): <subject>

<body>

<footer>
```

**Types**:

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting, missing semicolons, etc.
- `refactor`: Code refactoring
- `test`: Adding tests
- `chore`: Maintenance tasks

**Examples**:

```bash
feat(components): add project card component
fix(navigation): resolve mobile menu toggle issue
docs(readme): update installation instructions
refactor(parser): simplify markdown processing
test(accessibility): add WCAG 2.1 compliance tests
chore(deps): update dependencies to latest versions
```

---

## Resources

- [Git Flow Model](https://nvie.com/posts/a-successful-git-branching-model/)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [Project SDLC](../SDLC.md)
- [Contributing Guide](../CONTRIBUTING.md)

---

v1.0.0 | Active | Last Updated: Dec 04 2025 - 15:30
