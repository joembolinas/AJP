# Agent Reference Guide

This file provides quick reference tables for all specifications defined in `spec-architecture-portfolio-system.md`, which serves as the single source of truth for the Academic Journey Portfolio system architecture.

## System Requirements (REQ)

| ID      | Description                                                                                                               |
| ------- | ------------------------------------------------------------------------------------------------------------------------- |
| REQ-001 | System MUST support content import from multiple repositories and directories                                             |
| REQ-002 | System MUST organize content by term, skill category, and project type                                                    |
| REQ-003 | System MUST provide component-based architecture for modular content display                                              |
| REQ-004 | System MUST support expandable/collapsible UI components                                                                  |
| REQ-005 | System MUST enable chronological content browsing                                                                         |
| REQ-006 | System MUST support content filtering by category and skill                                                               |
| REQ-007 | System MUST provide automated content structure validation                                                                |
| REQ-008 | System MUST verify all internal and external links                                                                        |
| REQ-009 | System MUST comply with web accessibility standards (WCAG 2.1)                                                            |
| REQ-010 | System MUST deploy via GitHub Pages automation                                                                            |
| REQ-011 | System MUST extract content from primary source:`C:\Users\ADMIN\Desktop\School File\T3-AY2025`                          |
| REQ-012 | System MUST support future content sources from additional directories/repositories                                       |
| REQ-013 | System MUST transform raw academic content into structured web formats                                                    |
| REQ-014 | System MUST preserve content metadata (dates, categories, tags, authors)                                                  |
| REQ-015 | System MUST support incremental content additions without full rebuild                                                    |
| REQ-016 | System MUST provide responsive design for mobile and desktop viewports                                                    |
| REQ-017 | System MUST optimize asset delivery (images, scripts, styles)                                                             |
| REQ-018 | System MUST achieve minimum Google Lighthouse scores: Performance ≥90, Accessibility ≥95, Best Practices ≥90, SEO ≥90 |

## Security Requirements (SEC)

| ID      | Description                                                                |
| ------- | -------------------------------------------------------------------------- |
| SEC-001 | System MUST comply with school posting regulations                         |
| SEC-002 | System MUST NOT expose sensitive personal information                      |
| SEC-003 | System MUST use secure HTTPS deployment via GitHub Pages                   |
| SEC-004 | System MUST sanitize all user-provided content before rendering            |
| SEC-005 | System MUST implement Content Security Policy (CSP) headers where possible |

## Constraints (CON)

| ID      | Description                                                   |
| ------- | ------------------------------------------------------------- |
| CON-001 | System is limited to GitHub Pages free tier capabilities      |
| CON-002 | System MUST NOT require backend server or database            |
| CON-003 | System MUST use static site generation only                   |
| CON-004 | System MUST comply with GitHub Pages supported frameworks     |
| CON-005 | System is limited to client-side JavaScript for interactivity |
| CON-006 | System MUST minimize manual HTML/CSS coding requirement       |
| CON-007 | System MUST NOT implement custom user authentication          |

## Guidelines (GUD)

| ID      | Description                                                                  |
| ------- | ---------------------------------------------------------------------------- |
| GUD-001 | Prefer AI-assisted development using GitHub Copilot with custom instructions |
| GUD-002 | Use component-based architecture for maintainability                         |
| GUD-003 | Implement automated workflows to minimize manual intervention                |
| GUD-004 | Document all content transformation processes                                |
| GUD-005 | Follow semantic HTML5 markup patterns                                        |
| GUD-006 | Implement progressive enhancement for JavaScript features                    |

## Architectural Patterns (PAT)

| ID      | Description                                                     |
| ------- | --------------------------------------------------------------- |
| PAT-001 | Use JAMstack architecture (JavaScript, APIs, Markup)            |
| PAT-002 | Implement content-first design approach                         |
| PAT-003 | Follow separation of concerns (content, presentation, behavior) |
| PAT-004 | Use declarative configuration over imperative code              |
| PAT-005 | Implement atomic design methodology for components              |

## Acceptance Criteria (AC)

| ID     | Description                                                                                                                                                                                                  |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| AC-001 | Given a content source directory with valid markdown files, When the content extraction process runs, Then all files with correct front matter are successfully imported and transformed into web components |
| AC-002 | Given term-based content organization, When a user navigates the portfolio, Then content is grouped by term with clear chronological ordering                                                                |
| AC-003 | Given multiple content categories, When a user applies category filters, Then only content matching the selected category is displayed                                                                       |
| AC-004 | Given expandable content components, When a user clicks an expand/collapse control, Then the component transitions smoothly and maintains state                                                              |
| AC-005 | Given the deployment workflow, When changes are pushed to the main branch, Then GitHub Actions automatically builds and deploys the updated site within 5 minutes                                            |
| AC-006 | Given accessibility requirements, When tested with automated tools, Then the site achieves minimum WCAG 2.1 AA compliance                                                                                    |
| AC-007 | Given responsive design requirements, When viewed on mobile devices (≥320px width), Then all content is readable and navigable without horizontal scrolling                                                 |
| AC-008 | Given link validation requirements, When the validation process runs, Then all internal and external links return successful responses (200-299 status codes)                                                |
| AC-009 | Given content from multiple repositories, When content is added from a new repository, Then the system successfully imports and displays the content without manual configuration changes                    |
| AC-010 | Given performance requirements, When tested with Google Lighthouse, Then all core metrics meet or exceed minimum thresholds                                                                                  |

## External Systems (EXT)

| ID      | Name         | Description                                                                                                                                |
| ------- | ------------ | ------------------------------------------------------------------------------------------------------------------------------------------ |
| EXT-001 | GitHub       | Version control, repository hosting, and collaboration platform. Required for source control, pull requests, issues, and Actions workflows |
| EXT-002 | GitHub Pages | Static site hosting service. Required for production deployment and public accessibility                                                   |

## Third-Party Services (SVC)

| ID      | Name                   | Description                                                                                                                     |
| ------- | ---------------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| SVC-001 | Google Lighthouse      | Performance and accessibility auditing. Required for automated quality monitoring. SLA: Best-effort availability (free service) |
| SVC-002 | CDN (via GitHub Pages) | Content delivery network for asset distribution. Required for optimal performance globally                                      |

## Infrastructure Dependencies (INF)

| ID      | Name    | Description                                                                                                   |
| ------- | ------- | ------------------------------------------------------------------------------------------------------------- |
| INF-001 | Git     | Distributed version control system. Required version ≥2.x for all contributors and automation                |
| INF-002 | Node.js | JavaScript runtime for build tools and testing frameworks. Required version ≥18.x LTS for consistent tooling |
| INF-003 | VS Code | Development environment. Required for AI-assisted development with Copilot integration                        |

## Data Dependencies (DAT)

| ID      | Name                    | Description                                                                                                                                                                           |
| ------- | ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| DAT-001 | Academic Content Source | Term-based directories containing markdown files with front matter. Format: Markdown with YAML front matter. Frequency: Quarterly updates. Access: Local filesystem or Git repository |
| DAT-002 | Site Configuration      | YAML-based configuration files defining site metadata and build parameters. Format: YAML. Frequency: As needed for configuration changes                                              |

## Technology Platform Dependencies (PLT)

| ID      | Name                  | Description                                                                                                                                                                                 |
| ------- | --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| PLT-001 | GitHub Actions        | CI/CD automation platform. Constraint: Free tier limits (2000 minutes/month). Rationale: Integrated workflow automation without external services                                           |
| PLT-002 | Static Site Generator | Framework for transforming markdown to HTML. Constraint: Must be supported by GitHub Pages (Jekyll, Hugo, or custom build). Rationale: Automates content transformation and site generation |
| PLT-003 | Modern Web Browsers   | Client environment for site viewing. Constraint: Support for ES6+ JavaScript, CSS Grid, Flexbox. Rationale: Required for interactive features and responsive design                         |

## Compliance Dependencies (COM)

| ID      | Name                          | Description                                                                                                                           |
| ------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| COM-001 | School Content Posting Policy | Institutional guidelines for public sharing of academic work. Impact: Content review and approval process required before publication |
| COM-002 | WCAG 2.1 Level AA             | Web accessibility standards. Impact: Design and development must follow accessibility guidelines                                      |
| COM-003 | GitHub Terms of Service       | Platform usage policies. Impact: Content must comply with GitHub acceptable use policies                                              |

## Validation Criteria (VAL)

| ID      | Category                 | Description                                                                |
| ------- | ------------------------ | -------------------------------------------------------------------------- |
| VAL-001 | Build Validation         | All markdown files MUST have valid YAML front matter with required fields  |
| VAL-002 | Build Validation         | All internal links MUST resolve to existing pages or anchors               |
| VAL-003 | Build Validation         | All images MUST be accessible and properly sized                           |
| VAL-004 | Build Validation         | Generated HTML MUST pass W3C validation                                    |
| VAL-005 | Build Validation         | CSS MUST pass CSS validation                                               |
| VAL-006 | Build Validation         | JavaScript MUST pass linting (ESLint) without errors                       |
| VAL-007 | Content Validation       | All dates MUST follow ISO 8601 format (YYYY-MM-DD)                         |
| VAL-008 | Content Validation       | All categories MUST match predefined allowed categories                    |
| VAL-009 | Content Validation       | All terms MUST follow format: T[1-4]-AY[YYYY]                              |
| VAL-010 | Content Validation       | Content types MUST be one of: project, reflection, assignment, achievement |
| VAL-011 | Accessibility Validation | All images MUST have alt text                                              |
| VAL-012 | Accessibility Validation | Heading hierarchy MUST be logical (no skipped levels)                      |
| VAL-013 | Accessibility Validation | Color contrast MUST meet WCAG AA standards (4.5:1 for normal text)         |
| VAL-014 | Accessibility Validation | Interactive elements MUST be keyboard accessible                           |
| VAL-015 | Accessibility Validation | ARIA labels MUST be present for icon-only buttons                          |
| VAL-016 | Performance Validation   | Total page weight MUST be ≤2MB per page                                   |
| VAL-017 | Performance Validation   | Critical rendering path MUST complete ≤1.5s on 3G connection              |
| VAL-018 | Performance Validation   | Images MUST be optimized (WebP/AVIF with fallbacks)                        |
| VAL-019 | Performance Validation   | CSS/JS MUST be minified in production                                      |
| VAL-020 | Performance Validation   | Lighthouse Performance score MUST be ≥90                                  |
| VAL-021 | Deployment Validation    | GitHub Actions workflow MUST complete successfully                         |
| VAL-022 | Deployment Validation    | Deployed site MUST be accessible at configured URL                         |
| VAL-023 | Deployment Validation    | HTTPS certificate MUST be valid                                            |
| VAL-024 | Deployment Validation    | All pages MUST return HTTP 200 status                                      |
| VAL-025 | Deployment Validation    | No console errors on any page                                              |

---

**Reference**: See [spec-architecture-portfolio-system.md](./Project_Specification.md) for complete details and context.

**Link**: 

**Last Updated**: December 3, 2025
