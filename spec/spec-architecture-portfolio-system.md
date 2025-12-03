---
title: Academic Journey Portfolio - System Architecture Specification
version: 1.0
date_created: 2025-12-03
last_updated: 2025-12-03
owner: Portfolio Owner
tags: [architecture, design, infrastructure, github-pages, static-site]
---

## Introduction

This specification defines the comprehensive system architecture for the Academic Journey Portfolio, a scalable web-based platform designed to document and showcase academic learning, skills development, and growth over time through GitHub Pages. The system transforms raw academic content from multiple sources into a structured, component-based web presentation optimized for continuous content additions and term-based updates.

## 1. Purpose & Scope

This specification defines the architectural requirements, constraints, and interfaces for building a static portfolio website system that enables systematic documentation and presentation of academic work, reflections, and professional development. The architecture must support content extraction from multiple repositories, transformation into web-friendly formats, and deployment via GitHub Pages.

**Intended Audience**: AI code generation systems, developers, system architects, maintainers

**Assumptions**:

- GitHub Pages service availability and free tier access
- Content source directories maintain consistent structure across terms
- Regular quarterly updates aligned with academic term completion
- Static site generation only (no backend server)

## 2. Definitions

- **AJP**: Academic Journey Portfolio
- **GitHub Pages**: Static site hosting service provided by GitHub
- **MCP**: Model Context Protocol - integration system for VS Code
- **CI/CD**: Continuous Integration/Continuous Deployment
- **SSG**: Static Site Generator
- **Component**: Reusable, modular web UI element
- **Term**: Academic term (quarterly period)
- **Content Source**: Directory or repository containing raw academic materials
- **Deployment Target**: GitHub repository hosting the live portfolio site

## 3. Requirements, Constraints & Guidelines

### System Requirements

- **REQ-001**: System MUST support content import from multiple repositories and directories
- **REQ-002**: System MUST organize content by term, skill category, and project type
- **REQ-003**: System MUST provide component-based architecture for modular content display
- **REQ-004**: System MUST support expandable/collapsible UI components
- **REQ-005**: System MUST enable chronological content browsing
- **REQ-006**: System MUST support content filtering by category and skill
- **REQ-007**: System MUST provide automated content structure validation
- **REQ-008**: System MUST verify all internal and external links
- **REQ-009**: System MUST comply with web accessibility standards (WCAG 2.1)
- **REQ-010**: System MUST deploy via GitHub Pages automation

### Content Management Requirements

- **REQ-011**: System MUST extract content from primary source: `C:\Users\ADMIN\Desktop\School File\T3-AY2025`
- **REQ-012**: System MUST support future content sources from additional directories/repositories
- **REQ-013**: System MUST transform raw academic content into structured web formats
- **REQ-014**: System MUST preserve content metadata (dates, categories, tags, authors)
- **REQ-015**: System MUST support incremental content additions without full rebuild

### Performance Requirements

- **REQ-016**: System MUST provide responsive design for mobile and desktop viewports
- **REQ-017**: System MUST optimize asset delivery (images, scripts, styles)
- **REQ-018**: System MUST achieve minimum Google Lighthouse scores: Performance ≥90, Accessibility ≥95, Best Practices ≥90, SEO ≥90

### Security Requirements

- **SEC-001**: System MUST comply with school posting regulations
- **SEC-002**: System MUST NOT expose sensitive personal information
- **SEC-003**: System MUST use secure HTTPS deployment via GitHub Pages
- **SEC-004**: System MUST sanitize all user-provided content before rendering
- **SEC-005**: System MUST implement Content Security Policy (CSP) headers where possible

### Constraints

- **CON-001**: System is limited to GitHub Pages free tier capabilities
- **CON-002**: System MUST NOT require backend server or database
- **CON-003**: System MUST use static site generation only
- **CON-004**: System MUST comply with GitHub Pages supported frameworks
- **CON-005**: System is limited to client-side JavaScript for interactivity
- **CON-006**: System MUST minimize manual HTML/CSS coding requirement
- **CON-007**: System MUST NOT implement custom user authentication

### Guidelines

- **GUD-001**: Prefer AI-assisted development using GitHub Copilot with custom instructions
- **GUD-002**: Use component-based architecture for maintainability
- **GUD-003**: Implement automated workflows to minimize manual intervention
- **GUD-004**: Document all content transformation processes
- **GUD-005**: Follow semantic HTML5 markup patterns
- **GUD-006**: Implement progressive enhancement for JavaScript features

### Architectural Patterns

- **PAT-001**: Use JAMstack architecture (JavaScript, APIs, Markup)
- **PAT-002**: Implement content-first design approach
- **PAT-003**: Follow separation of concerns (content, presentation, behavior)
- **PAT-004**: Use declarative configuration over imperative code
- **PAT-005**: Implement atomic design methodology for components

## 4. Interfaces & Data Contracts

### Content Source Interface

**Input Directory Structure**:

```text
T3-AY2025/
├── projects/
│   ├── project-name/
│   │   ├── README.md
│   │   ├── documentation/
│   │   └── assets/
├── reflections/
│   └── reflection-YYYY-MM-DD.md
├── assignments/
│   └── subject-assignment-name.md
└── achievements/
    └── achievement-name.md
```

**Content File Metadata Schema**:

```yaml
---
title: string (required)
date: YYYY-MM-DD (required)
category: string[] (required) # ["academic", "reflection", "extracurricular", "achievement"]
skills: string[] (optional)
tags: string[] (optional)
term: string (required) # "T3-AY2025"
type: string (required) # ["project", "reflection", "assignment", "achievement"]
---
```

### Component Interface

**Component Definition Schema**:

```javascript
{
  "componentName": string,
  "props": {
    "title": string,
    "content": string | markdown,
    "metadata": {
      "date": "YYYY-MM-DD",
      "category": string[],
      "skills": string[],
      "tags": string[]
    },
    "expandable": boolean,
    "defaultExpanded": boolean
  }
}
```

### Deployment Configuration

**GitHub Pages Configuration** (`_config.yml`):

```yaml
title: string
description: string
baseurl: string
url: string
theme: string | null
plugins: string[]
exclude: string[]
include: string[]
markdown: string
```

**GitHub Actions Workflow** (`.github/workflows/deploy.yml`):

```yaml
name: Deploy to GitHub Pages
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
      - name: Build
      - name: Test
      - name: Deploy
```

### Navigation Data Contract

**Site Navigation Structure**:

```json
{
  "navigation": [
    {
      "label": string,
      "path": string,
      "children": [
        {
          "label": string,
          "path": string,
          "metadata": {
            "term": string,
            "category": string
          }
        }
      ]
    }
  ]
}
```

## 5. Acceptance Criteria

- **AC-001**: Given a content source directory with valid markdown files, When the content extraction process runs, Then all files with correct front matter are successfully imported and transformed into web components
- **AC-002**: Given term-based content organization, When a user navigates the portfolio, Then content is grouped by term with clear chronological ordering
- **AC-003**: Given multiple content categories, When a user applies category filters, Then only content matching the selected category is displayed
- **AC-004**: Given expandable content components, When a user clicks an expand/collapse control, Then the component transitions smoothly and maintains state
- **AC-005**: Given the deployment workflow, When changes are pushed to the main branch, Then GitHub Actions automatically builds and deploys the updated site within 5 minutes
- **AC-006**: Given accessibility requirements, When tested with automated tools, Then the site achieves minimum WCAG 2.1 AA compliance
- **AC-007**: Given responsive design requirements, When viewed on mobile devices (≥320px width), Then all content is readable and navigable without horizontal scrolling
- **AC-008**: Given link validation requirements, When the validation process runs, Then all internal and external links return successful responses (200-299 status codes)
- **AC-009**: Given content from multiple repositories, When content is added from a new repository, Then the system successfully imports and displays the content without manual configuration changes
- **AC-010**: Given performance requirements, When tested with Google Lighthouse, Then all core metrics meet or exceed minimum thresholds

## 6. Test Automation Strategy

### Test Levels

- **Unit Testing**: Component-level tests for individual UI elements and transformation functions
- **Integration Testing**: Content pipeline tests from source to rendered output
- **End-to-End Testing**: Full user journey tests including navigation, filtering, and content interaction
- **Performance Testing**: Lighthouse CI for automated performance monitoring
- **Accessibility Testing**: Automated WCAG 2.1 compliance checks

### Testing Tools & Frameworks

- **JavaScript Testing**: Jest or Vitest for unit and integration tests
- **E2E Testing**: Playwright or Cypress for browser automation
- **Visual Regression**: Percy or Chromatic for UI consistency
- **Performance**: Lighthouse CI in GitHub Actions
- **Accessibility**: axe-core or Pa11y for automated checks
- **Link Validation**: html-proofer or broken-link-checker

### Test Data Management

- **Approach**: Use fixture files with sample content matching production structure
- **Test Content**: Create mock term directories with representative markdown files
- **Cleanup**: Automated cleanup of test artifacts after test runs
- **Isolation**: Each test suite uses isolated content fixtures

### CI/CD Integration

- **GitHub Actions Pipeline**:
  - Run unit tests on all pull requests
  - Execute integration tests before merge
  - Deploy to preview environment for PR review
  - Run full E2E suite on main branch
  - Execute Lighthouse audit post-deployment
- **Test Reports**: Generate and publish test coverage reports
- **Quality Gates**: Require minimum 80% code coverage for merges

### Coverage Requirements

- **Minimum Thresholds**:
  - Statements: 80%
  - Branches: 75%
  - Functions: 80%
  - Lines: 80%
- **Critical Paths**: 100% coverage for content transformation and validation logic

### Performance Testing

- **Approach**: Automated Lighthouse audits on every deployment
- **Benchmarks**: Track performance metrics over time
- **Alerts**: Notify on performance regression > 5 points
- **Load Testing**: Not applicable (static site, GitHub Pages handles scaling)

## 7. Rationale & Context

### Architectural Decisions

**Static Site Generation**: Chosen to eliminate server costs, reduce attack surface, and leverage GitHub Pages free hosting while maintaining simplicity and performance.

**Component-Based Architecture**: Enables modular development, reusability across terms, easier maintenance, and AI-assisted component generation.

**JAMstack Pattern**: Provides better performance, improved security, cost-effectiveness, and developer experience through pre-rendering and CDN distribution.

**GitHub-Centric Workflow**: Leverages existing version control, enables collaborative content management through pull requests, and integrates seamlessly with GitHub Pages deployment.

**AI-Assisted Development**: Reduces manual coding effort, accelerates development cycles, and maintains consistency through custom instructions and prompt engineering.

### Design Trade-offs

**No Backend Database**:

- **Pro**: Zero infrastructure costs, enhanced security, simplified deployment
- **Con**: Limited dynamic features, manual content updates required
- **Justification**: Portfolio updates are infrequent (quarterly), static content is sufficient

**Client-Side Interactivity Only**:

- **Pro**: Fast load times, no server dependency, works offline after initial load
- **Con**: Limited to JavaScript capabilities, SEO considerations for dynamic content
- **Justification**: Required interactivity (expand/collapse, filtering) achievable client-side

**GitHub Pages Dependency**:

- **Pro**: Free hosting, automatic HTTPS, integrated with GitHub workflow
- **Con**: Vendor lock-in, limited to supported frameworks and configurations
- **Justification**: Benefits outweigh risks; migration path available via Netlify/Vercel if needed

### Content Strategy

**Term-Based Organization**: Aligns with academic calendar, enables clear chronological narrative, simplifies content addition workflow.

**Multi-Repository Support**: Accommodates diverse content sources, enables separation of concerns (portfolio vs. course work), supports collaborative projects.

**Metadata-Driven**: Enables flexible filtering and categorization, supports automated content processing, facilitates content discovery.

## 8. Dependencies & External Integrations

### External Systems

- **EXT-001**: GitHub - Version control, repository hosting, and collaboration platform. Required for source control, pull requests, issues, and Actions workflows.
- **EXT-002**: GitHub Pages - Static site hosting service. Required for production deployment and public accessibility.

### Third-Party Services

- **SVC-001**: Google Lighthouse - Performance and accessibility auditing. Required for automated quality monitoring. SLA: Best-effort availability (free service).
- **SVC-002**: CDN (via GitHub Pages) - Content delivery network for asset distribution. Required for optimal performance globally.

### Infrastructure Dependencies

- **INF-001**: Git - Distributed version control system. Required version ≥2.x for all contributors and automation.
- **INF-002**: Node.js - JavaScript runtime for build tools and testing frameworks. Required version ≥18.x LTS for consistent tooling.
- **INF-003**: VS Code - Development environment. Required for AI-assisted development with Copilot integration.

### Data Dependencies

- **DAT-001**: Academic Content Source - Term-based directories containing markdown files with front matter. Format: Markdown with YAML front matter. Frequency: Quarterly updates. Access: Local filesystem or Git repository.
- **DAT-002**: Site Configuration - YAML-based configuration files defining site metadata and build parameters. Format: YAML. Frequency: As needed for configuration changes.

### Technology Platform Dependencies

- **PLT-001**: GitHub Actions - CI/CD automation platform. Constraint: Free tier limits (2000 minutes/month). Rationale: Integrated workflow automation without external services.
- **PLT-002**: Static Site Generator - Framework for transforming markdown to HTML. Constraint: Must be supported by GitHub Pages (Jekyll, Hugo, or custom build). Rationale: Automates content transformation and site generation.
- **PLT-003**: Modern Web Browsers - Client environment for site viewing. Constraint: Support for ES6+ JavaScript, CSS Grid, Flexbox. Rationale: Required for interactive features and responsive design.

### Compliance Dependencies

- **COM-001**: School Content Posting Policy - Institutional guidelines for public sharing of academic work. Impact: Content review and approval process required before publication.
- **COM-002**: WCAG 2.1 Level AA - Web accessibility standards. Impact: Design and development must follow accessibility guidelines.
- **COM-003**: GitHub Terms of Service - Platform usage policies. Impact: Content must comply with GitHub acceptable use policies.

## 9. Examples & Edge Cases

### Content Transformation Example

**Input** (Source Markdown):

```markdown
---
title: Database Design Project
date: 2025-10-15
category: [academic, project]
skills: [database, SQL, ERD]
tags: [database-design, normalization, relational-model]
term: T3-AY2025
type: project
---

## Overview

This project demonstrates database normalization principles...

## Key Learnings

- Third Normal Form (3NF) application
- Entity-Relationship Diagram (ERD) creation
```

**Output** (Rendered Component):

```html
<article class="content-card" data-term="T3-AY2025" data-category="academic project">
  <header class="card-header">
    <h3>Database Design Project</h3>
    <time datetime="2025-10-15">October 15, 2025</time>
    <ul class="skills-list">
      <li class="skill-tag">database</li>
      <li class="skill-tag">SQL</li>
      <li class="skill-tag">ERD</li>
    </ul>
  </header>
  <button class="expand-toggle" aria-expanded="false">View Details</button>
  <div class="card-content" hidden>
    <section>
      <h4>Overview</h4>
      <p>This project demonstrates database normalization principles...</p>
    </section>
    <section>
      <h4>Key Learnings</h4>
      <ul>
        <li>Third Normal Form (3NF) application</li>
        <li>Entity-Relationship Diagram (ERD) creation</li>
      </ul>
    </section>
  </div>
</article>
```

### Edge Cases

#### Edge Case 1: Missing Required Front Matter

```markdown
---
title: Incomplete Post
date: 2025-10-15
# Missing: category, term, type
---
Content here...
```

**Expected Behavior**: Validation fails, content excluded from build with detailed error message identifying missing fields.

#### Edge Case 2: Multiple Content Sources with Overlapping Dates

```text
Repository A: project-x (date: 2025-10-15)
Repository B: project-y (date: 2025-10-15)
```

**Expected Behavior**: Both displayed chronologically, secondary sort by title alphabetically, unique identifiers prevent conflicts.

#### Edge Case 3: Special Characters in File Names

```text
reflection - "my thoughts" & learning (10-15).md
```

**Expected Behavior**: File processed successfully, URL slug sanitized to `reflection-my-thoughts-learning-10-15`, special characters escaped in HTML.

#### Edge Case 4: Very Large Content Files (>10MB)

```text
project-with-many-images.md (contains 50+ embedded images)
```

**Expected Behavior**: Build process warns about size, suggests optimization, provides image compression recommendations, build continues with warning.

#### Edge Case 5: Content with External Dependencies

```markdown
![External Image](https://example.com/image.jpg)
[External Link](https://external-site.com)
```

**Expected Behavior**: Link validation checks external resources, warns on broken links, continues build, marks content with external dependencies for review.

#### Edge Case 6: Empty Term Directory

```text
T4-AY2025/
  (no content files)
```

**Expected Behavior**: Term section created but displays "No content available for this term" message, navigation includes term for future additions.

## 10. Validation Criteria

### Build Validation

- **VAL-001**: All markdown files MUST have valid YAML front matter with required fields
- **VAL-002**: All internal links MUST resolve to existing pages or anchors
- **VAL-003**: All images MUST be accessible and properly sized
- **VAL-004**: Generated HTML MUST pass W3C validation
- **VAL-005**: CSS MUST pass CSS validation
- **VAL-006**: JavaScript MUST pass linting (ESLint) without errors

### Content Validation

- **VAL-007**: All dates MUST follow ISO 8601 format (YYYY-MM-DD)
- **VAL-008**: All categories MUST match predefined allowed categories
- **VAL-009**: All terms MUST follow format: T[1-4]-AY[YYYY]
- **VAL-010**: Content types MUST be one of: project, reflection, assignment, achievement

### Accessibility Validation

- **VAL-011**: All images MUST have alt text
- **VAL-012**: Heading hierarchy MUST be logical (no skipped levels)
- **VAL-013**: Color contrast MUST meet WCAG AA standards (4.5:1 for normal text)
- **VAL-014**: Interactive elements MUST be keyboard accessible
- **VAL-015**: ARIA labels MUST be present for icon-only buttons

### Performance Validation

- **VAL-016**: Total page weight MUST be ≤2MB per page
- **VAL-017**: Critical rendering path MUST complete ≤1.5s on 3G connection
- **VAL-018**: Images MUST be optimized (WebP/AVIF with fallbacks)
- **VAL-019**: CSS/JS MUST be minified in production
- **VAL-020**: Lighthouse Performance score MUST be ≥90

### Deployment Validation

- **VAL-021**: GitHub Actions workflow MUST complete successfully
- **VAL-022**: Deployed site MUST be accessible at configured URL
- **VAL-023**: HTTPS certificate MUST be valid
- **VAL-024**: All pages MUST return HTTP 200 status
- **VAL-025**: No console errors on any page

## 11. Related Specifications / Further Reading

### Internal Documentation

- [README.md](../README.md) - Project overview and goals
- [SDLC.md](../SDLC.md) - Software development lifecycle phases
- [.github/copilot-instructions.md](../.github/copilot-instructions.md) - AI-assisted development guidelines
- [.github/instructions/markdown.instructions.md](../.github/instructions/markdown.instructions.md) - Markdown content standards

### External Resources

- [GitHub Pages Documentation](https://docs.github.com/en/pages) - Official hosting platform documentation
- [JAMstack Architecture](https://jamstack.org/) - Modern web development architecture
- [WCAG 2.1 Guidelines](https://www.w3.org/WAI/WCAG21/quickref/) - Web accessibility standards
- [Web.dev Performance](https://web.dev/performance/) - Performance optimization best practices
- [Atomic Design Methodology](https://atomicdesign.bradfrost.com/) - Component design patterns
- [GitHub Actions Documentation](https://docs.github.com/en/actions) - CI/CD automation
- [Markdown Guide](https://www.markdownguide.org/) - Markdown syntax reference
- [YAML Specification](https://yaml.org/spec/1.2/spec.html) - YAML format documentation
