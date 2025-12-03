
# 🏔️Epic Breakdown for AJP

Based on your comprehensive specification documents, here's a refined epic breakdown that maps directly to your requirements:

---

## Epic 1: Foundation & Project Infrastructure

**Priority:** 🔴 Critical (Must be first)
**Size:** Small (3-5 days)
**Phase Alignment:** Phase 2 - Structure
**Related Requirements:** CON-001 to CON-007, PAT-001 to PAT-005, GUD-001 to GUD-006

### Description

Establish the repository structure, development environment, tooling configuration, and foundational architecture.  This includes setting up the Node.js toolchain, configuring the static site generator (Eleventy or Astro), and establishing the atomic design component structure.

### User Value

- Portfolio owner has a well-organized, maintainable project structure
- Clear separation of concerns (content, presentation, behavior) per PAT-003
- Scalable architecture ready for 1,000+ content files (NFR-010)

### Key Features

| Feature              | Requirement Ref | Description                                                                |
| -------------------- | --------------- | -------------------------------------------------------------------------- |
| Directory Structure  | PAT-005         | Create `content/`, `components/`, `scripts/`, `_data/` directories |
| Node.js Toolchain    | INF-002         | Configure Node.js ≥18. x with npm scripts                                 |
| SSG Setup            | PLT-002         | Initialize Eleventy or Astro with base configuration                       |
| Copilot Instructions | GUD-001         | Configure `. github/copilot-instructions.md` for AI-assisted dev         |
| Component Scaffolds  | PAT-005         | Create atomic design structure (atoms, molecules, organisms)               |
| Configuration Files  | DAT-002         | Setup `site.config.json`, `. editorconfig`, linting configs            |
| Git Workflow         | GUD-003         | Branch strategy, PR templates, contribution guidelines                     |

### Dependencies

- None (foundation epic)

### Acceptance Criteria

- [ ] Repository follows documented folder structure
- [ ] `npm install` and `npm run build` execute without errors
- [ ] Copilot instructions configured and tested
- [ ] Base layout template renders successfully
- [ ] ESLint/Stylelint pass with zero errors

### Technical Notes

- Use Node.js 18+ LTS (INF-002)
- Follow JAMstack architecture (PAT-001)
- Implement declarative configuration (PAT-004)

---

## Epic 2: Content Schema & Validation System

**Priority:** 🔴 Critical
**Size:** Medium (1 week)
**Phase Alignment:** Phase 3 - Configuration
**Related Requirements:** VAL-001 to VAL-010, FR-007, FR-008, FR-013

### Description

Define and implement the content schema, metadata validation, and automated quality checks.  This ensures all content meets the required front matter structure before being processed.

### User Value

- Content errors caught before deployment (VAL-001)
- Consistent metadata across all content files
- Automated validation reduces manual review burden

### Key Features

| Feature                | Requirement Ref    | Description                                        |
| ---------------------- | ------------------ | -------------------------------------------------- |
| Front Matter Schema    | VAL-001            | JSON Schema for required YAML front matter         |
| Date Validation        | VAL-007            | ISO 8601 format enforcement (YYYY-MM-DD)           |
| Category Validation    | VAL-008            | Validate against allowed categories list           |
| Term Format Validation | VAL-009            | Enforce T[1-4]-AY[YYYY] format                     |
| Type Validation        | VAL-010            | Validate content types (project, reflection, etc.) |
| Link Checker           | FR-008, VAL-002    | Verify internal and external links                 |
| Accessibility Lint     | VAL-011 to VAL-015 | Alt text, heading hierarchy, ARIA checks           |
| Validation CLI         | VAL-006            | npm script for running all validations             |

### Dependencies

- Epic 1 (Foundation) - needs Node.js toolchain

### Acceptance Criteria

- [ ] Invalid front matter fails build with clear error messages
- [ ] All date formats validated against ISO 8601
- [ ] Categories restricted to predefined list
- [ ] Term formats validated with regex
- [ ] Link checker reports broken links with URLs
- [ ] Validation runs in <30 seconds for 100 files

### Technical Notes

```javascript
// Example validation schema structure
const contentSchema = {
  required: ['title', 'date', 'category', 'term', 'type'],
  properties: {
    title: { type: 'string', minLength: 1 },
    date: { type: 'string', pattern: '^\\d{4}-\\d{2}-\\d{2}$' },
    category: { type: 'array', items: { enum: ['academic', 'reflection', 'extracurricular', 'achievement'] }},
    term: { type: 'string', pattern: '^T[1-4]-AY\\d{4}$' },
    type: { type: 'string', enum: ['project', 'reflection', 'assignment', 'achievement'] }
  }
};
```

---

## Epic 3: Content Extraction & Transformation Pipeline

**Priority:** 🔴 Critical
**Size:** Medium (1-2 weeks)
**Phase Alignment:** Phase 3 - Content Extraction
**Related Requirements:** FR-001, FR-010, FR-011, FR-012, FR-013, FR-014

### Description

Create the system to extract academic content from source directories, transform Markdown into structured data, and generate the content graph for downstream processing.

### User Value

- Content from Term 3 successfully imported (FR-010)
- Raw academic work transformed into web-ready format (FR-012)
- Metadata preserved for filtering and navigation (FR-013)
- Future terms can be added without code changes (FR-011)

### Key Features

| Feature                   | Requirement Ref | Description                                          |
| ------------------------- | --------------- | ---------------------------------------------------- |
| Content Source Manager    | FR-001          | Aggregate content from multiple directories/repos    |
| Directory Manifest        | FR-010          | Configure primary source path for T3-AY2025          |
| Markdown Parser           | FR-012          | Convert Markdown → AST → sanitized HTML            |
| Metadata Extractor        | FR-013          | Extract and normalize YAML front matter              |
| Content Graph Builder     | FR-002          | Build relationships (Term → Items, Items ↔ Skills) |
| Incremental Build         | FR-014          | Checksum-based cache for unchanged files             |
| Content Adapter Interface | FR-011          | Extensible adapter pattern for new sources           |

### Dependencies

- Epic 1 (Foundation) - needs toolchain
- Epic 2 (Validation) - content must pass validation

### Acceptance Criteria

- [ ] Content extracted from `C:\Users\ADMIN\Desktop\School File\T3-AY2025`
- [ ] All valid Markdown files transformed to HTML components
- [ ] Metadata normalized (dates to ISO, categories to slugs)
- [ ] Content graph JSON generated with term/skill indexes
- [ ] Incremental build skips unchanged files
- [ ] New term can be added by config change only

### Technical Notes

```text
Content Pipeline Flow:
┌─────────────┐     ┌──────────────┐     ┌─────────────────┐
│ Source Dir  │ --> │ Front Matter │ --> │ Content Graph   │
│ (Markdown)  │     │ Validator    │     │ Builder         │
└─────────────┘     └──────────────┘     └─────────────────┘
                           │                      │
                           v                      v
                    ┌──────────────┐     ┌─────────────────┐
                    │ Error Report │     │ Term/Skill      │
                    │ (if invalid) │     │ Index JSON      │
                    └──────────────┘     └─────────────────┘
```

### Edge Cases Handled

- Missing required front matter → Validation error (Edge Case 1)
- Overlapping dates → Secondary sort by title (Edge Case 2)
- Special characters in filenames → URL slug sanitization (Edge Case 3)
- Large files → Warning with optimization suggestions (Edge Case 4)

---

## Epic 4: Component-Based Presentation Layer

**Priority:** 🟡 High
**Size:** Medium (1-2 weeks)
**Phase Alignment:** Phase 4 - Integration
**Related Requirements:** FR-003, FR-004, NFR-001, NFR-004, PAT-005

### Description

Develop the reusable UI component library following atomic design methodology. Components must be accessible, responsive, and support progressive enhancement.

### User Value

- Professional, consistent content presentation
- Expandable sections for detailed exploration (FR-004)
- Mobile-responsive design for all devices (NFR-001)
- WCAG 2. 1 AA accessible (NFR-004)

### Key Features

| Feature             | Requirement Ref | Description                                    |
| ------------------- | --------------- | ---------------------------------------------- |
| **Atoms**     | PAT-005         | Skill tags, date badges, category labels       |
| **Molecules** | PAT-005         | Content cards, metadata groups, expand buttons |
| **Organisms** | PAT-005         | Term sections, navigation menu, filter panel   |
| **Templates** | PAT-005         | Page layouts, content list views               |
| Expand/Collapse     | FR-004          | Accessible expandable content with ARIA        |
| Responsive Grid     | NFR-001         | CSS Grid/Flexbox for mobile/desktop            |
| Keyboard Navigation | VAL-014         | All interactive elements keyboard accessible   |
| Skip Links          | NFR-004         | Skip to main content for screen readers        |

### Dependencies

- Epic 1 (Foundation) - needs component scaffolds
- Epic 2 (Validation) - accessibility requirements defined

### Acceptance Criteria

- [ ] Components render across all supported browsers
- [ ] Expand/collapse works with click and keyboard (Enter/Space)
- [ ] ARIA attributes properly implemented (`aria-expanded`, etc.)
- [ ] Mobile layout functional at 320px width (AC-007)
- [ ] Color contrast ≥4.5:1 for text (VAL-013)
- [ ] Lighthouse Accessibility ≥95 (NFR-003)

### Component Examples

```html
<!-- Atom: Skill Tag -->
<span class="skill-tag" data-skill="database">database</span>

<!-- Molecule: Content Card Header -->
<header class="card-header">
  <h3 class="card-title">{{ title }}</h3>
  <time datetime="{{ date }}">{{ formattedDate }}</time>
  <ul class="skills-list">
    {% for skill in skills %}
    <li class="skill-tag">{{ skill }}</li>
    {% endfor %}
  </ul>
</header>

<!-- Organism: Expandable Content Card -->
<article class="content-card" data-term="{{ term }}">
  {% include "molecules/card-header.njk" %}
  <button class="expand-toggle" aria-expanded="false" aria-controls="content-{{ id }}">
    View Details
  </button>
  <div class="card-content" id="content-{{ id }}" hidden>
    {{ content | safe }}
  </div>
</article>
```

---

## Epic 5: Navigation & Content Filtering

**Priority:** 🟡 High
**Size:** Small-Medium (1 week)
**Phase Alignment:** Phase 4 - Integration
**Related Requirements:** FR-005, FR-006, NFR-012

### Description

Implement chronological browsing, category/skill filtering, and navigation systems.  Client-side filtering must be performant and accessible.

### User Value

- Users can browse content chronologically (FR-005)
- Content filterable by category and skill (FR-006)
- Responsive filtering under 100ms (NFR-012)

### Key Features

| Feature           | Requirement Ref | Description                                        |
| ----------------- | --------------- | -------------------------------------------------- |
| Term Navigation   | FR-005          | Browse by academic term (T1, T2, T3.. .)           |
| Category Filters  | FR-006          | Filter by academic, reflection, achievement, etc.  |
| Skill Filters     | FR-006          | Filter by skills (database, SQL, presentation.. .) |
| Search (Optional) | FR-006          | Text search across content titles/tags             |
| URL State         | FR-005          | Filter state reflected in URL for sharing          |
| No-JS Fallback    | GUD-006         | Progressive enhancement - works without JS         |

### Dependencies

- Epic 3 (Content Pipeline) - needs content indexes
- Epic 4 (Components) - needs filter UI components

### Acceptance Criteria

- [ ] Term navigation displays all terms with content counts
- [ ] Filter changes update display within 100ms (NFR-012)
- [ ] Multiple filters can be combined (AND logic)
- [ ] Filter state persists in URL query params
- [ ] Works with JavaScript disabled (shows all content)
- [ ] Keyboard accessible filter controls

### Technical Notes

```javascript
// Client-side filter controller example
class FilterController {
  constructor(contentGrid, filterPanel) {
    this.grid = contentGrid;
    this.filters = new Map();
  }
  
  applyFilters() {
    const start = performance.now();
    this.grid.querySelectorAll('.content-card').forEach(card => {
      const visible = this.matchesAllFilters(card. dataset);
      card.hidden = !visible;
    });
    console.log(`Filter applied in ${performance.now() - start}ms`);
  }
  
  matchesAllFilters(dataset) {
    for (const [key, value] of this.filters) {
      if (dataset[key] !== value) return false;
    }
    return true;
  }
}
```

---

## Epic 6: Content Integration & Population

**Priority:** 🟡 High
**Size:** Medium (1-2 weeks)
**Phase Alignment:** Phase 4 - Integration
**Related Requirements:** FR-002, AC-001 to AC-003

### Description

Integrate extracted Term 3 content into the component-based presentation layer, populating the portfolio with actual academic work organized by term, category, and skills.

### User Value

- Portfolio displays real Term 3 academic content
- All work properly categorized and navigable
- Content grouped by term with chronological ordering (AC-002)

### Key Features

| Feature            | Requirement Ref | Description                                    |
| ------------------ | --------------- | ---------------------------------------------- |
| Academic Projects  | FR-002          | Papers, presentations, case studies            |
| Reflections        | FR-002          | Learning journal entries, growth documentation |
| Achievements       | FR-002          | Awards, certificates, honors                   |
| Assignments        | FR-002          | Coursework and assessments                     |
| Technical Learning | FR-002          | GitHub, VS Code, Copilot documentation         |
| Skills Showcase    | OBJ-002         | Filterable skills with progression tracking    |
| Goals Section      | FR-002          | Future aspirations and objectives              |

### Dependencies

- Epic 3 (Content Pipeline) - needs extracted content
- Epic 4 (Components) - needs display components
- Epic 5 (Navigation) - needs filtering system

### Acceptance Criteria

- [ ] All Term 3 content files displayed correctly (AC-001)
- [ ] Content grouped by term with chronological ordering (AC-002)
- [ ] Category filtering works correctly (AC-003)
- [ ] No sensitive information exposed (NFR-006)
- [ ] All internal links resolve (VAL-002)
- [ ] Images have alt text (VAL-011)

---

## Epic 7: CI/CD & Deployment Pipeline

**Priority:** 🟢 Medium
**Size:** Small (3-5 days)
**Phase Alignment:** Phase 5 - Deployment
**Related Requirements:** FR-009, OBJ-004, VAL-021 to VAL-025, PLT-001

### Description

Set up GitHub Actions for automated validation, building, testing, and deployment to GitHub Pages. Includes quality gates and performance monitoring.

### User Value

- Automatic deployment within 5 minutes of push (OBJ-004)
- Consistent, error-free deployments
- Quality gates prevent broken deployments

### Key Features

| Feature          | Requirement Ref | Description                       |
| ---------------- | --------------- | --------------------------------- |
| Build Workflow   | FR-009          | GitHub Actions workflow for build |
| Validation Stage | VAL-021         | Run all validators before build   |
| Test Stage       | VAL-021         | Run unit and integration tests    |
| Lighthouse CI    | NFR-003         | Automated performance auditing    |
| Link Checker     | FR-008          | Verify all links post-build       |
| Deploy Stage     | VAL-022         | Deploy to GitHub Pages            |
| Preview Deploys  | PLT-001         | PR preview environments           |

### Dependencies

- Epic 1 (Foundation) - needs build scripts
- Epic 2 (Validation) - needs validators
- Epic 4-6 (Content) - needs content to deploy

### Acceptance Criteria

- [ ] Workflow triggers on push to main (AC-005)
- [ ] Build completes within 10 minutes for 1000 files (NFR-011)
- [ ] Failed validation blocks deployment
- [ ] Site accessible at joembolinas.github.io (VAL-022)
- [ ] HTTPS certificate valid (VAL-023)
- [ ] Lighthouse scores meet thresholds (VAL-020)

### Workflow Structure

```yaml
name: Build and Deploy
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '18'
      - run: npm ci
      - run: npm run validate  # Front matter, links, a11y
    
  test:
    needs: validate
    runs-on: ubuntu-latest
    steps:
      - run: npm test
      - run: npm run test:coverage
    
  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - run: npm run build
      - uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist
        
  deploy:
    needs: build
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps. deployment.outputs.page_url }}
    steps:
      - uses: actions/deploy-pages@v4
        id: deployment
      
  lighthouse:
    needs: deploy
    runs-on: ubuntu-latest
    steps:
      - uses: treosh/lighthouse-ci-action@v10
        with:
          urls: https://joembolinas.github.io
          budgetPath: ./lighthouse-budget.json
```

---

## Epic 8: Testing & Quality Assurance

**Priority:** 🟢 Medium
**Size:** Medium (1 week)
**Phase Alignment:** Phase 5 - Testing
**Related Requirements:** Section 7 (Test Automation Strategy)

### Description

Implement comprehensive testing infrastructure including unit tests, integration tests, visual regression, accessibility tests, and E2E tests.

### User Value

- Confidence in code changes (no regressions)
- Automated quality enforcement
- 80%+ code coverage on business logic

### Key Features

| Feature             | Requirement Ref | Description                                  |
| ------------------- | --------------- | -------------------------------------------- |
| Unit Tests          | Section 7       | Jest/Vitest for parsers, helpers, validators |
| Integration Tests   | Section 7       | Content pipeline end-to-end tests            |
| E2E Tests           | Section 7       | Playwright for critical user journeys        |
| Visual Regression   | Section 7       | Percy/Chromatic for UI consistency           |
| Accessibility Tests | Section 7       | axe-core automated checks                    |
| Coverage Reports    | Section 7       | 80% minimum coverage threshold               |

### Dependencies

- Epic 1-6 (All code must exist to test)

### Acceptance Criteria

- [ ] Unit tests cover all validators and helpers
- [ ] Integration tests verify content pipeline
- [ ] E2E tests cover: navigation, filtering, expand/collapse
- [ ] Accessibility tests pass (zero critical violations)
- [ ] Coverage ≥80% for statements, functions, lines
- [ ] Tests complete in <5 minutes

---

## Epic 9: Scalability & Documentation

**Priority:** 🟢 Medium
**Size:** Small (3-5 days)
**Phase Alignment:** Phase 5 - Documentation
**Related Requirements:** OBJ-006, NFR-010, NFR-014

### Description

Document processes for adding future terms, ensure architecture supports growth, and create maintainer documentation.

### User Value

- Easy to add Term 4, 5, etc.  without code changes
- Portfolio grows sustainably (NFR-014)
- Clear documentation for future maintenance

### Key Features

| Feature             | Requirement Ref | Description                              |
| ------------------- | --------------- | ---------------------------------------- |
| Term Addition Guide | NFR-014         | Step-by-step for adding new terms        |
| Content Templates   | OBJ-006         | Markdown templates for each content type |
| Runbook             | GUD-003         | Operational procedures for updates       |
| Architecture Docs   | Section 16      | Keep blueprint current                   |
| ADR Updates         | Section 15      | Document new decisions                   |
| Performance Guide   | NFR-010         | Scaling recommendations for 1000+ files  |

### Dependencies

- All previous epics (documents complete process)

### Acceptance Criteria

- [ ] Adding Term 4 documented with clear steps
- [ ] Content templates available for all types
- [ ] CONTRIBUTING. md updated with workflow
- [ ] Architecture blueprint reflects current state
- [ ] All ADRs documented and linked

---

## 📅 Implementation Timeline

```text
┌──────────────────────────────────────────────────────────────────────────┐
│                     AJP Implementation Timeline                           │
├──────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│  Phase 1: Documentation ✅ COMPLETE                                       │
│  ════════════════════════════════                                        │
│  - README.md, SDLC.md                                                    │
│  - Project_Specification.md                                              │
│  - Project_Architecture_Blueprint. md                                     │
│                                                                           │
│  Phase 2: Structure (Week 1)                                             │
│  ──────────────────────────────                                          │
│  └── Epic 1: Foundation & Infrastructure                                 │
│                                                                           │
│  Phase 3: Configuration & Extraction (Weeks 2-3)                         │
│  ────────────────────────────────────────────────                        │
│  ├── Epic 2: Content Schema & Validation                                 │
│  └── Epic 3: Content Extraction Pipeline                                 │
│                                                                           │
│  Phase 4: Integration (Weeks 4-6)                                        │
│  ─────────────────────────────────                                       │
│  ├── Epic 4: Component Presentation Layer                                │
│  ├── Epic 5: Navigation & Filtering                                      │
│  └── Epic 6: Content Integration                                         │
│                                                                           │
│  Phase 5: Deployment & QA (Weeks 7-8)                                    │
│  ─────────────────────────────────────                                   │
│  ├── Epic 7: CI/CD Pipeline                                              │
│  ├── Epic 8: Testing & QA                                                │
│  └── Epic 9: Scalability & Documentation                                 │
│                                                                           │
└──────────────────────────────────────────────────────────────────────────┘
```

---

## 📊 Epic Dependency Map

```text
                    Epic 1: Foundation
                           │
              ┌────────────┼────────────┐
              ▼            ▼            ▼
        Epic 2:      Epic 4:      Epic 7:
        Validation   Components   CI/CD (partial)
              │            │
              ▼            │
        Epic 3:            │
        Content Pipeline   │
              │            │
              └─────┬──────┘
                    ▼
              Epic 5: Navigation
                    │
                    ▼
              Epic 6: Content Integration
                    │
         ┌──────────┼──────────┐
         ▼          ▼          ▼
    Epic 7:    Epic 8:    Epic 9:
    CI/CD      Testing    Scalability
   (complete)
```

---

## 📋 Requirements Traceability Matrix

| Epic   | Key Requirements Covered                                                       |
| ------ | ------------------------------------------------------------------------------ |
| Epic 1 | CON-001 to CON-007, PAT-001 to PAT-005, GUD-001 to GUD-006, INF-001 to INF-003 |
| Epic 2 | VAL-001 to VAL-010, FR-007, FR-008, FR-013                                     |
| Epic 3 | FR-001, FR-010, FR-011, FR-012, FR-013, FR-014                                 |
| Epic 4 | FR-003, FR-004, NFR-001, NFR-004, PAT-005, VAL-011 to VAL-015                  |
| Epic 5 | FR-005, FR-006, NFR-012, GUD-006                                               |
| Epic 6 | FR-002, OBJ-001, OBJ-002, AC-001 to AC-003                                     |
| Epic 7 | FR-009, OBJ-004, VAL-021 to VAL-025, PLT-001, NFR-011                          |
| Epic 8 | Section 7 (Test Automation), VAL-016 to VAL-020                                |
| Epic 9 | OBJ-006, NFR-010, NFR-014, Section 16                                          |

---

## 🎯 Next Steps

Now that you have a comprehensive epic breakdown aligned with your specifications, here's what to do next:

### 1. Save the Epic Breakdown

```bash
# Create/update the file
touch docs/EPICS.md
# Copy this epic breakdown into the file
```

### 2.  Commit to Repository

```bash
git add docs/EPICS.md
git commit -m "docs: Add comprehensive epic breakdown aligned with specifications

- 9 epics mapped to 5 development phases
- Requirements traceability matrix included
- Dependencies and acceptance criteria defined
- Timeline estimated at 8 weeks

Refs: Project_Specification.md, Project_Architecture_Blueprint.md"
```

### 3. Proceed to Phase 2

You're ready to start **Epic 1: Foundation & Infrastructure**!

Would you like me to:

1. **Create detailed task breakdown** for Epic 1 (Step 5. 2)?
2. **Generate GitHub Issues** from these epics for tracking?
3. **Create the `docs/EPICS. md` file content** ready to paste?
4. **Start Epic 1 implementation** with specific setup instructions?
