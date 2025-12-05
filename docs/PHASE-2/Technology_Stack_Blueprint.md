---
title: Technology Stack Blueprint
source: ''
author: Portfolio Owner
post_slug: technology-stack-blueprint
categories: [architecture, docs, spec]
tags: [technology, stack, jamstack, nodejs, static-site, blueprint]
ai_note: Assisted by AI (GitHub Copilot)
summary: Comprehensive technology stack blueprint for the Academic Journey Portfolio, documenting all technologies, implementation patterns, and conventions.
date: 2025-12-04
---

## 1. Technology Identification Summary

This blueprint documents the complete technology stack for the Academic Journey Portfolio (AJP) - a JAMstack static site hosted on GitHub Pages. The analysis is based on project specifications, architecture documents, and planned implementation patterns.

### Project Type Detection

| Attribute             | Value                                              |
| --------------------- | -------------------------------------------------- |
| **Primary Type**      | JAMstack Static Site                               |
| **Architecture**      | Content-first, Component-based (Atomic Design)     |
| **Hosting**           | GitHub Pages (Static CDN)                          |
| **Build Environment** | Node.js 18+ LTS                                    |
| **Framework**         | Eleventy/Astro (SSG candidates)                    |
| **Content Format**    | Markdown with YAML front matter                    |
| **Interactivity**     | Progressive Enhancement (Vanilla JS)               |

---

## 2. Technology Stack Map

```text
┌─────────────────────────────────────────────────────────────────────────────┐
│                           TECHNOLOGY STACK                                   │
├─────────────────────────────────────────────────────────────────────────────┤
│  DELIVERY LAYER                                                              │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────────────────┐  │
│  │  GitHub Pages   │  │  HTTPS (Auto)   │  │  CDN Edge Caching           │  │
│  │  (PLT-001)      │  │  (SEC-003)      │  │  (NFR-013)                  │  │
│  └─────────────────┘  └─────────────────┘  └─────────────────────────────┘  │
├─────────────────────────────────────────────────────────────────────────────┤
│  PRESENTATION LAYER                                                          │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────────────────┐  │
│  │  HTML5 Semantic │  │  CSS3 / SCSS    │  │  Vanilla JavaScript (ES6+)  │  │
│  │  (GUD-005)      │  │  BEM Naming     │  │  Progressive Enhancement    │  │
│  └─────────────────┘  └─────────────────┘  └─────────────────────────────┘  │
├─────────────────────────────────────────────────────────────────────────────┤
│  BUILD LAYER                                                                 │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────────────────┐  │
│  │  Node.js 18+    │  │  Eleventy/Astro │  │  npm Scripts / CLI          │  │
│  │  (INF-002)      │  │  (PLT-002)      │  │  Task Runner                │  │
│  └─────────────────┘  └─────────────────┘  └─────────────────────────────┘  │
├─────────────────────────────────────────────────────────────────────────────┤
│  CONTENT LAYER                                                               │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────────────────┐  │
│  │  Markdown       │  │  YAML Front     │  │  JSON Schema Validation     │  │
│  │  (DAT-001)      │  │  Matter         │  │  (VAL-001 to VAL-010)       │  │
│  └─────────────────┘  └─────────────────┘  └─────────────────────────────┘  │
├─────────────────────────────────────────────────────────────────────────────┤
│  AUTOMATION LAYER                                                            │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────────────────┐  │
│  │  GitHub Actions │  │  Lighthouse CI  │  │  ESLint / Stylelint         │  │
│  │  (PLT-001)      │  │  (SVC-001)      │  │  Validation Pipeline        │  │
│  └─────────────────┘  └─────────────────┘  └─────────────────────────────┘  │
├─────────────────────────────────────────────────────────────────────────────┤
│  DEVELOPMENT LAYER                                                           │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────────────────┐  │
│  │  VS Code        │  │  GitHub Copilot │  │  Git 2.x+                   │  │
│  │  (INF-003)      │  │  (GUD-001)      │  │  (INF-001)                  │  │
│  └─────────────────┘  └─────────────────┘  └─────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────────┘
```

---

## 3. Core Technologies Analysis

### 3.1 Runtime & Build Environment

| Technology       | Version    | Purpose                              | License    | Requirement Ref |
| ---------------- | ---------- | ------------------------------------ | ---------- | --------------- |
| **Node.js**      | ≥18.x LTS | JavaScript runtime for build tools   | MIT        | INF-002         |
| **npm**          | ≥9.x      | Package management and task running  | Artistic-2 | INF-002         |
| **Git**          | ≥2.x      | Distributed version control          | GPL-2.0    | INF-001         |

### 3.2 Static Site Generator (SSG)

| Technology  | Version | Purpose                            | License | Requirement Ref |
| ----------- | ------- | ---------------------------------- | ------- | --------------- |
| **Eleventy** | 2.x     | Template-based static site generation | MIT     | PLT-002         |
| **Astro**   | 4.x     | Alternative: Component-based SSG   | MIT     | PLT-002         |

**Selection Rationale**: Both candidates satisfy GitHub Pages constraints (CON-004). Eleventy offers simpler configuration; Astro provides modern component patterns. Final selection deferred to Epic 1 implementation.

### 3.3 Content Processing

| Technology          | Version | Purpose                             | License | Requirement Ref |
| ------------------- | ------- | ----------------------------------- | ------- | --------------- |
| **gray-matter**     | 4.x     | YAML front matter parsing           | MIT     | FR-013          |
| **remark/rehype**   | 15.x    | Markdown to HTML transformation     | MIT     | FR-012          |
| **markdown-it**     | 14.x    | Alternative Markdown parser         | MIT     | FR-012          |
| **ajv**             | 8.x     | JSON Schema validation              | MIT     | VAL-001         |

### 3.4 Frontend Technologies

| Technology       | Version | Purpose                              | License | Requirement Ref |
| ---------------- | ------- | ------------------------------------ | ------- | --------------- |
| **HTML5**        | -       | Semantic markup structure            | -       | GUD-005         |
| **CSS3/SCSS**    | -       | Styling with preprocessor            | MIT     | NFR-001         |
| **JavaScript**   | ES6+    | Client-side interactions             | -       | CON-005         |

### 3.5 Development Tooling

| Technology         | Version | Purpose                           | License | Requirement Ref |
| ------------------ | ------- | --------------------------------- | ------- | --------------- |
| **VS Code**        | Latest  | Primary development environment   | MIT     | INF-003         |
| **GitHub Copilot** | Latest  | AI-assisted development           | Prop.   | GUD-001         |
| **ESLint**         | 8.x     | JavaScript linting                | MIT     | VAL-006         |
| **Stylelint**      | 16.x    | CSS/SCSS linting                  | MIT     | VAL-005         |
| **Prettier**       | 3.x     | Code formatting                   | MIT     | GUD-002         |

### 3.6 Testing Frameworks

| Technology          | Version | Purpose                          | License | Requirement Ref |
| ------------------- | ------- | -------------------------------- | ------- | --------------- |
| **Vitest**          | 1.x     | Unit and integration testing     | MIT     | Section 7       |
| **Playwright**      | 1.x     | End-to-end browser testing       | Apache  | Section 7       |
| **axe-core**        | 4.x     | Accessibility testing            | MPL-2.0 | VAL-011-015     |
| **html-proofer**    | 5.x     | Link validation                  | MIT     | FR-008          |
| **Lighthouse CI**   | 0.13.x  | Performance auditing             | Apache  | VAL-016-020     |

### 3.7 CI/CD & Deployment

| Technology          | Version | Purpose                          | License | Requirement Ref |
| ------------------- | ------- | -------------------------------- | ------- | --------------- |
| **GitHub Actions**  | -       | CI/CD automation                 | -       | PLT-001         |
| **GitHub Pages**    | -       | Static site hosting              | -       | CON-001         |

---

## 4. Dependency Architecture

### 4.1 Production Dependencies

```json
{
  "dependencies": {
    "@11ty/eleventy": "^2.0.0",
    "gray-matter": "^4.0.3",
    "remark": "^15.0.0",
    "remark-html": "^16.0.0",
    "rehype-sanitize": "^6.0.0"
  }
}
```

### 4.2 Development Dependencies

```json
{
  "devDependencies": {
    "ajv": "^8.12.0",
    "eslint": "^8.56.0",
    "stylelint": "^16.2.0",
    "prettier": "^3.2.0",
    "vitest": "^1.2.0",
    "playwright": "^1.41.0",
    "axe-core": "^4.8.0",
    "@lhci/cli": "^0.13.0",
    "npm-run-all": "^4.1.5"
  }
}
```

### 4.3 Dependency Flow Diagram

```text
┌──────────────────────────────────────────────────────────────────────────┐
│                        DEPENDENCY FLOW                                    │
├──────────────────────────────────────────────────────────────────────────┤
│                                                                           │
│   ┌─────────────┐                                                         │
│   │  Markdown   │──────────────────────────────────────────────┐          │
│   │  Content    │                                              │          │
│   └──────┬──────┘                                              │          │
│          │                                                     │          │
│          v                                                     v          │
│   ┌─────────────┐     ┌─────────────┐     ┌─────────────────────────┐    │
│   │ gray-matter │────>│    ajv      │────>│  Validation Reports     │    │
│   │ (parse)     │     │ (validate)  │     │  (Pass/Fail)            │    │
│   └──────┬──────┘     └─────────────┘     └─────────────────────────┘    │
│          │                                                               │
│          v                                                               │
│   ┌─────────────┐     ┌─────────────┐     ┌─────────────────────────┐    │
│   │  remark     │────>│   rehype    │────>│  Sanitized HTML         │    │
│   │ (parse MD)  │     │ (to HTML)   │     │  Components             │    │
│   └──────┬──────┘     └─────────────┘     └───────────┬─────────────┘    │
│          │                                            │                   │
│          v                                            v                   │
│   ┌─────────────┐     ┌─────────────┐     ┌─────────────────────────┐    │
│   │  Eleventy   │────>│  Templates  │────>│  Static HTML/CSS/JS     │    │
│   │ (build)     │     │  (Nunjucks) │     │  Output                 │    │
│   └─────────────┘     └─────────────┘     └───────────┬─────────────┘    │
│                                                       │                   │
│                                                       v                   │
│                                           ┌─────────────────────────┐    │
│                                           │  GitHub Pages Deploy    │    │
│                                           └─────────────────────────┘    │
│                                                                           │
└──────────────────────────────────────────────────────────────────────────┘
```

---

## 5. Implementation Patterns & Conventions

### 5.1 Naming Conventions

#### File Naming

| Type                | Pattern                              | Example                           |
| ------------------- | ------------------------------------ | --------------------------------- |
| Content files       | `kebab-case.md`                      | `database-design-project.md`      |
| Component templates | `kebab-case.njk`                     | `content-card.njk`                |
| JavaScript modules  | `kebab-case.js` or `camelCase.js`   | `filter-controller.js`            |
| SCSS files          | `_kebab-case.scss`                   | `_content-card.scss`              |
| Config files        | `kebab-case.config.json`             | `site.config.json`                |
| Test files          | `*.test.js` or `*.spec.js`          | `validator.test.js`               |

#### CSS/BEM Naming

```scss
// Block: content-card
// Element: content-card__header
// Modifier: content-card--expanded

.content-card {
  // Block styles
  
  &__header {
    // Element styles
  }
  
  &__content {
    // Element styles
  }
  
  &--expanded {
    // Modifier styles
  }
  
  &--featured {
    // Modifier styles
  }
}
```

#### JavaScript Naming

```javascript
// Classes: PascalCase
class FilterController { }
class ContentCard { }

// Functions: camelCase
function parseMarkdown() { }
function validateFrontMatter() { }

// Constants: SCREAMING_SNAKE_CASE
const MAX_FILE_SIZE = 10485760;
const ALLOWED_CATEGORIES = ['academic', 'reflection'];

// Variables: camelCase
let currentFilter = 'all';
const contentItems = [];
```

### 5.2 Directory Structure

```text
AJP/
├── .github/
│   ├── workflows/
│   │   └── deploy.yml              # CI/CD pipeline (PLT-001)
│   ├── copilot-instructions.md     # AI development guidance (GUD-001)
│   ├── instructions/               # File-specific instructions
│   └── prompt/                     # Prompt templates
│
├── content/                        # Content source directory (DAT-001)
│   ├── projects/                   # Academic projects
│   ├── reflections/                # Learning reflections
│   ├── assignments/                # Course assignments
│   └── achievements/               # Awards and honors
│
├── src/
│   ├── components/                 # Atomic design components (PAT-005)
│   │   ├── atoms/                  # Smallest UI elements
│   │   │   ├── badge.njk
│   │   │   ├── button.njk
│   │   │   └── tag.njk
│   │   ├── molecules/              # Composed elements
│   │   │   ├── content-card.njk
│   │   │   ├── skill-list.njk
│   │   │   └── date-display.njk
│   │   └── organisms/              # Complex sections
│   │       ├── term-section.njk
│   │       ├── navigation.njk
│   │       └── content-grid.njk
│   │
│   ├── layouts/                    # Page layouts
│   │   ├── base.njk
│   │   ├── home.njk
│   │   └── term.njk
│   │
│   ├── scripts/                    # Client-side JavaScript
│   │   ├── controllers/
│   │   │   ├── filter-controller.js
│   │   │   └── expand-controller.js
│   │   ├── utils/
│   │   │   └── event-bus.js
│   │   └── main.js
│   │
│   └── styles/                     # SCSS stylesheets
│       ├── base/
│       │   ├── _reset.scss
│       │   ├── _typography.scss
│       │   └── _variables.scss
│       ├── components/
│       │   ├── _content-card.scss
│       │   └── _navigation.scss
│       └── main.scss
│
├── _data/                          # Global data files
│   ├── site.json                   # Site metadata
│   ├── navigation.json             # Navigation structure
│   └── categories.json             # Allowed categories
│
├── lib/                            # Build-time utilities
│   ├── validators/
│   │   ├── front-matter.js
│   │   ├── link-checker.js
│   │   └── schema.js
│   ├── transforms/
│   │   ├── markdown-parser.js
│   │   └── content-graph.js
│   └── adapters/
│       └── file-adapter.js
│
├── tests/                          # Test files
│   ├── unit/
│   ├── integration/
│   └── fixtures/
│
├── docs/                           # Documentation
│   ├── PHASE-1/
│   ├── PHASE-2/
│   └── AGENTS.md
│
├── .eleventy.js                    # Eleventy configuration
├── package.json                    # Dependencies and scripts
├── site.config.json                # Site configuration
├── .eslintrc.json                  # ESLint configuration
├── .stylelintrc.json               # Stylelint configuration
├── .prettierrc                     # Prettier configuration
└── README.md
```

### 5.3 Code Organization Patterns

#### Component Structure (Atomic Design)

```text
ATOMS (Smallest, standalone elements)
├── badge          - Skill/category badges
├── button         - Interactive buttons
├── icon           - SVG icons
└── tag            - Content tags

MOLECULES (Combinations of atoms)
├── content-card   - Card with header, content, badges
├── skill-list     - List of skill badges
├── date-display   - Formatted date with icon
└── expand-toggle  - Expandable section control

ORGANISMS (Complex UI sections)
├── term-section   - Full term with cards
├── navigation     - Site navigation
├── content-grid   - Filterable grid of cards
└── filter-bar     - Category/skill filters
```

---

## 6. JavaScript Implementation Patterns

### 6.1 Module Structure

```javascript
/**
 * Filter Controller - Manages content filtering interactions
 * @module controllers/filter-controller
 * @requires utils/event-bus
 */

import { eventBus } from '../utils/event-bus.js';

/**
 * @class FilterController
 * @description Handles filter UI interactions and publishes filter events
 */
export class FilterController {
  /**
   * @param {EventBus} bus - Event bus for inter-component communication
   */
  constructor(bus = eventBus) {
    this.bus = bus;
    this.activeFilters = new Set();
  }

  /**
   * Initialize controller on DOM element
   * @param {HTMLElement} root - Root element containing filter controls
   * @returns {void}
   */
  init(root) {
    if (!root) {
      console.warn('FilterController: No root element provided');
      return;
    }

    root.addEventListener('change', this.handleFilterChange.bind(this));
    root.addEventListener('keydown', this.handleKeyboard.bind(this));
  }

  /**
   * Handle filter checkbox changes
   * @param {Event} event - Change event
   * @private
   */
  handleFilterChange(event) {
    const { target } = event;
    if (!target.matches('[data-filter]')) return;

    const filterValue = target.dataset.filter;
    
    if (target.checked) {
      this.activeFilters.add(filterValue);
    } else {
      this.activeFilters.delete(filterValue);
    }

    this.bus.publish('filter:change', {
      filters: Array.from(this.activeFilters),
      source: 'FilterController'
    });
  }

  /**
   * Handle keyboard navigation for accessibility
   * @param {KeyboardEvent} event - Keyboard event
   * @private
   */
  handleKeyboard(event) {
    // Keyboard navigation implementation
  }
}
```

### 6.2 Event Bus Pattern

```javascript
/**
 * Simple pub/sub event bus for component communication
 * @module utils/event-bus
 */

class EventBus {
  constructor() {
    this.listeners = new Map();
  }

  /**
   * Subscribe to an event
   * @param {string} event - Event name
   * @param {Function} callback - Callback function
   * @returns {Function} Unsubscribe function
   */
  subscribe(event, callback) {
    if (!this.listeners.has(event)) {
      this.listeners.set(event, new Set());
    }
    this.listeners.get(event).add(callback);

    return () => this.listeners.get(event).delete(callback);
  }

  /**
   * Publish an event
   * @param {string} event - Event name
   * @param {*} data - Event data
   */
  publish(event, data) {
    if (!this.listeners.has(event)) return;

    for (const callback of this.listeners.get(event)) {
      try {
        callback(data);
      } catch (error) {
        console.error(`EventBus: Error in ${event} handler`, error);
      }
    }
  }
}

export const eventBus = new EventBus();
```

### 6.3 Progressive Enhancement Pattern

```javascript
/**
 * Main application entry point
 * Initializes all controllers with progressive enhancement
 */

import { FilterController } from './controllers/filter-controller.js';
import { ExpandController } from './controllers/expand-controller.js';

/**
 * Initialize application when DOM is ready
 */
function init() {
  // Feature detection before initialization
  if (!('querySelector' in document)) {
    console.warn('Browser does not support required features');
    return;
  }

  // Initialize filter controller
  const filterRoot = document.querySelector('[data-controller="filter"]');
  if (filterRoot) {
    new FilterController().init(filterRoot);
  }

  // Initialize expand controllers
  const expandElements = document.querySelectorAll('[data-controller="expand"]');
  expandElements.forEach(el => {
    new ExpandController().init(el);
  });
}

// Wait for DOM ready
if (document.readyState === 'loading') {
  document.addEventListener('DOMContentLoaded', init);
} else {
  init();
}
```

---

## 7. Content Schema & Validation

### 7.1 Front Matter Schema (JSON Schema)

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "$id": "content-schema.json",
  "title": "AJP Content Schema",
  "description": "Schema for validating content file front matter",
  "type": "object",
  "required": ["title", "date", "category", "term", "type"],
  "properties": {
    "title": {
      "type": "string",
      "minLength": 1,
      "maxLength": 200,
      "description": "Content title"
    },
    "date": {
      "type": "string",
      "pattern": "^\\d{4}-\\d{2}-\\d{2}$",
      "description": "Publication date in ISO 8601 format (YYYY-MM-DD)"
    },
    "category": {
      "type": "array",
      "items": {
        "type": "string",
        "enum": ["academic", "reflection", "extracurricular", "achievement"]
      },
      "minItems": 1,
      "description": "Content categories"
    },
    "skills": {
      "type": "array",
      "items": {
        "type": "string",
        "minLength": 1
      },
      "description": "Related skills"
    },
    "tags": {
      "type": "array",
      "items": {
        "type": "string",
        "minLength": 1
      },
      "description": "Content tags for search and filtering"
    },
    "term": {
      "type": "string",
      "pattern": "^T[1-4]-AY\\d{4}$",
      "description": "Academic term (e.g., T3-AY2025)"
    },
    "type": {
      "type": "string",
      "enum": ["project", "reflection", "assignment", "achievement"],
      "description": "Content type"
    }
  },
  "additionalProperties": true
}
```

### 7.2 Validation Implementation

```javascript
/**
 * Front matter validator using JSON Schema
 * @module validators/front-matter
 */

import Ajv from 'ajv';
import contentSchema from './schemas/content-schema.json';

const ajv = new Ajv({ allErrors: true, verbose: true });
const validate = ajv.compile(contentSchema);

/**
 * Validate content front matter
 * @param {Object} frontMatter - Parsed front matter object
 * @param {string} filePath - File path for error reporting
 * @returns {ValidationResult}
 */
export function validateFrontMatter(frontMatter, filePath) {
  const valid = validate(frontMatter);

  if (!valid) {
    return {
      valid: false,
      filePath,
      errors: validate.errors.map(err => ({
        field: err.instancePath || err.params.missingProperty,
        message: err.message,
        value: err.data
      }))
    };
  }

  return { valid: true, filePath, errors: [] };
}

/**
 * @typedef {Object} ValidationResult
 * @property {boolean} valid - Whether validation passed
 * @property {string} filePath - Path to validated file
 * @property {ValidationError[]} errors - List of validation errors
 */

/**
 * @typedef {Object} ValidationError
 * @property {string} field - Field that failed validation
 * @property {string} message - Error message
 * @property {*} value - Invalid value
 */
```

---

## 8. Build Configuration

### 8.1 Eleventy Configuration

```javascript
// .eleventy.js
const markdownIt = require('markdown-it');
const markdownItAnchor = require('markdown-it-anchor');

module.exports = function(eleventyConfig) {
  // Passthrough copy for static assets
  eleventyConfig.addPassthroughCopy('src/styles');
  eleventyConfig.addPassthroughCopy('src/scripts');
  eleventyConfig.addPassthroughCopy('content/**/assets');

  // Markdown configuration
  const md = markdownIt({
    html: true,
    breaks: true,
    linkify: true
  }).use(markdownItAnchor);

  eleventyConfig.setLibrary('md', md);

  // Custom filters
  eleventyConfig.addFilter('dateFormat', (date) => {
    return new Date(date).toLocaleDateString('en-US', {
      year: 'numeric',
      month: 'long',
      day: 'numeric'
    });
  });

  eleventyConfig.addFilter('byTerm', (collection, term) => {
    return collection.filter(item => item.data.term === term);
  });

  eleventyConfig.addFilter('byCategory', (collection, category) => {
    return collection.filter(item => 
      item.data.category && item.data.category.includes(category)
    );
  });

  // Custom collections
  eleventyConfig.addCollection('content', (collectionApi) => {
    return collectionApi
      .getFilteredByGlob('content/**/*.md')
      .sort((a, b) => new Date(b.data.date) - new Date(a.data.date));
  });

  eleventyConfig.addCollection('terms', (collectionApi) => {
    const items = collectionApi.getFilteredByGlob('content/**/*.md');
    const terms = [...new Set(items.map(item => item.data.term))];
    return terms.sort().reverse();
  });

  // Shortcodes
  eleventyConfig.addShortcode('badge', (text, type = 'default') => {
    return `<span class="badge badge--${type}">${text}</span>`;
  });

  eleventyConfig.addPairedShortcode('expandable', (content, title) => {
    return `
      <details class="expandable">
        <summary class="expandable__toggle">${title}</summary>
        <div class="expandable__content">${content}</div>
      </details>
    `;
  });

  return {
    dir: {
      input: 'content',
      includes: '../src/components',
      layouts: '../src/layouts',
      data: '../_data',
      output: '_site'
    },
    markdownTemplateEngine: 'njk',
    htmlTemplateEngine: 'njk'
  };
};
```

### 8.2 npm Scripts Configuration

```json
{
  "scripts": {
    "dev": "eleventy --serve --watch",
    "build": "npm-run-all clean build:*",
    "build:eleventy": "eleventy",
    "build:styles": "sass src/styles/main.scss:_site/css/main.css --style=compressed",
    "build:scripts": "esbuild src/scripts/main.js --bundle --minify --outfile=_site/js/main.js",
    "clean": "rimraf _site",
    "lint": "npm-run-all lint:*",
    "lint:js": "eslint src/scripts/**/*.js lib/**/*.js",
    "lint:css": "stylelint src/styles/**/*.scss",
    "lint:md": "markdownlint content/**/*.md",
    "validate": "npm-run-all validate:*",
    "validate:schema": "node lib/validators/run-validation.js",
    "validate:links": "html-proofer _site --check-html --allow-hash-href",
    "test": "vitest run",
    "test:watch": "vitest",
    "test:coverage": "vitest run --coverage",
    "test:e2e": "playwright test",
    "lighthouse": "lhci autorun",
    "a11y": "pa11y-ci",
    "ci": "npm-run-all lint validate build test lighthouse"
  }
}
```

---

## 9. CI/CD Pipeline Configuration

### 9.1 GitHub Actions Workflow

```yaml
# .github/workflows/deploy.yml
name: Build and Deploy

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

jobs:
  validate:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Lint
        run: npm run lint

      - name: Validate content
        run: npm run validate:schema

  build:
    needs: validate
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Build site
        run: npm run build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: _site

  test:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Run unit tests
        run: npm run test

      - name: Download artifact
        uses: actions/download-artifact@v4
        with:
          name: github-pages
          path: _site

      - name: Validate links
        run: npm run validate:links

  lighthouse:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '18'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Download artifact
        uses: actions/download-artifact@v4
        with:
          name: github-pages
          path: _site

      - name: Run Lighthouse CI
        run: npm run lighthouse
        env:
          LHCI_GITHUB_APP_TOKEN: ${{ secrets.LHCI_GITHUB_APP_TOKEN }}

  deploy:
    if: github.ref == 'refs/heads/main'
    needs: [test, lighthouse]
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

### 9.2 Lighthouse CI Configuration

```json
{
  "ci": {
    "collect": {
      "staticDistDir": "_site",
      "url": [
        "http://localhost/index.html",
        "http://localhost/terms/t3-ay2025/index.html"
      ]
    },
    "assert": {
      "assertions": {
        "categories:performance": ["error", { "minScore": 0.9 }],
        "categories:accessibility": ["error", { "minScore": 0.95 }],
        "categories:best-practices": ["error", { "minScore": 0.9 }],
        "categories:seo": ["error", { "minScore": 0.9 }]
      }
    },
    "upload": {
      "target": "temporary-public-storage"
    }
  }
}
```

---

## 10. Testing Architecture

### 10.1 Test Structure

```text
tests/
├── unit/
│   ├── validators/
│   │   ├── front-matter.test.js
│   │   └── link-checker.test.js
│   ├── transforms/
│   │   ├── markdown-parser.test.js
│   │   └── content-graph.test.js
│   └── controllers/
│       ├── filter-controller.test.js
│       └── expand-controller.test.js
├── integration/
│   ├── build-pipeline.test.js
│   └── content-extraction.test.js
├── e2e/
│   ├── navigation.spec.js
│   ├── filtering.spec.js
│   └── accessibility.spec.js
└── fixtures/
    ├── valid-content/
    ├── invalid-content/
    └── mock-data.json
```

### 10.2 Unit Test Example

```javascript
// tests/unit/validators/front-matter.test.js
import { describe, it, expect } from 'vitest';
import { validateFrontMatter } from '../../../lib/validators/front-matter.js';

describe('validateFrontMatter', () => {
  describe('valid content', () => {
    it('should pass validation for complete front matter', () => {
      const frontMatter = {
        title: 'Database Design Project',
        date: '2025-10-15',
        category: ['academic', 'project'],
        term: 'T3-AY2025',
        type: 'project',
        skills: ['database', 'SQL']
      };

      const result = validateFrontMatter(frontMatter, 'test.md');

      expect(result.valid).toBe(true);
      expect(result.errors).toHaveLength(0);
    });
  });

  describe('invalid content', () => {
    it('should fail for missing required fields', () => {
      const frontMatter = {
        title: 'Incomplete Post'
        // Missing: date, category, term, type
      };

      const result = validateFrontMatter(frontMatter, 'test.md');

      expect(result.valid).toBe(false);
      expect(result.errors.length).toBeGreaterThan(0);
    });

    it('should fail for invalid date format', () => {
      const frontMatter = {
        title: 'Test',
        date: '15-10-2025', // Wrong format
        category: ['academic'],
        term: 'T3-AY2025',
        type: 'project'
      };

      const result = validateFrontMatter(frontMatter, 'test.md');

      expect(result.valid).toBe(false);
      expect(result.errors.some(e => e.field.includes('date'))).toBe(true);
    });

    it('should fail for invalid term format', () => {
      const frontMatter = {
        title: 'Test',
        date: '2025-10-15',
        category: ['academic'],
        term: 'Term3-2025', // Wrong format
        type: 'project'
      };

      const result = validateFrontMatter(frontMatter, 'test.md');

      expect(result.valid).toBe(false);
      expect(result.errors.some(e => e.field.includes('term'))).toBe(true);
    });
  });
});
```

### 10.3 E2E Test Example

```javascript
// tests/e2e/filtering.spec.js
import { test, expect } from '@playwright/test';

test.describe('Content Filtering', () => {
  test.beforeEach(async ({ page }) => {
    await page.goto('/');
  });

  test('should filter content by category', async ({ page }) => {
    // Click academic category filter
    await page.click('[data-filter="academic"]');

    // Verify only academic content is visible
    const cards = await page.locator('.content-card:visible');
    await expect(cards).toHaveCount(await page.locator('.content-card[data-category*="academic"]').count());
  });

  test('should filter content by skill', async ({ page }) => {
    // Click database skill filter
    await page.click('[data-filter="database"]');

    // Verify filtered results
    const visibleCards = page.locator('.content-card:visible');
    for (const card of await visibleCards.all()) {
      await expect(card).toHaveAttribute('data-skills', /database/);
    }
  });

  test('should combine multiple filters', async ({ page }) => {
    await page.click('[data-filter="academic"]');
    await page.click('[data-filter="SQL"]');

    // Verify combined filter results
    const visibleCards = page.locator('.content-card:visible');
    for (const card of await visibleCards.all()) {
      await expect(card).toHaveAttribute('data-category', /academic/);
      await expect(card).toHaveAttribute('data-skills', /SQL/);
    }
  });

  test('should be keyboard accessible', async ({ page }) => {
    // Tab to first filter
    await page.keyboard.press('Tab');
    await page.keyboard.press('Tab');

    // Activate filter with Space
    await page.keyboard.press('Space');

    // Verify filter was applied
    await expect(page.locator('[data-filter]:first-child')).toBeChecked();
  });
});
```

---

## 11. Accessibility Implementation

### 11.1 WCAG 2.1 Compliance Patterns

```html
<!-- Accessible expand/collapse component -->
<div class="content-card" data-controller="expand">
  <header class="content-card__header">
    <h3 id="card-title-1">Database Design Project</h3>
    <button 
      class="content-card__toggle"
      aria-expanded="false"
      aria-controls="card-content-1"
      aria-labelledby="card-title-1"
    >
      <span class="visually-hidden">Toggle details for</span>
      <svg aria-hidden="true" class="icon icon--chevron"><!-- SVG --></svg>
    </button>
  </header>
  
  <div 
    id="card-content-1"
    class="content-card__content"
    hidden
    role="region"
    aria-labelledby="card-title-1"
  >
    <!-- Content -->
  </div>
</div>
```

### 11.2 Accessibility Testing Configuration

```javascript
// axe-core configuration
const axeConfig = {
  rules: {
    'color-contrast': { enabled: true },
    'heading-order': { enabled: true },
    'image-alt': { enabled: true },
    'link-name': { enabled: true },
    'button-name': { enabled: true },
    'aria-allowed-attr': { enabled: true },
    'aria-required-attr': { enabled: true },
    'aria-valid-attr': { enabled: true }
  },
  tags: ['wcag2a', 'wcag2aa', 'wcag21aa']
};
```

---

## 12. Performance Optimization

### 12.1 Asset Optimization Strategy

| Asset Type | Optimization                              | Target           |
| ---------- | ----------------------------------------- | ---------------- |
| Images     | WebP/AVIF with fallbacks, srcset          | < 100KB per image |
| CSS        | Minification, critical CSS inlining       | < 50KB total     |
| JavaScript | Tree-shaking, minification, ES modules    | < 30KB total     |
| Fonts      | Subset, font-display: swap                | < 100KB total    |

### 12.2 Caching Strategy

```text
Cache-Control Headers (via GitHub Pages):
├── HTML files:     no-cache (revalidate)
├── CSS/JS:         max-age=31536000 (immutable with hash)
├── Images:         max-age=2592000 (30 days)
└── Fonts:          max-age=31536000 (1 year)
```

---

## 13. Security Implementation

### 13.1 Content Security Policy

```html
<meta http-equiv="Content-Security-Policy" content="
  default-src 'self';
  script-src 'self';
  style-src 'self' 'unsafe-inline';
  img-src 'self' data: https:;
  font-src 'self';
  connect-src 'self';
  frame-ancestors 'none';
  base-uri 'self';
  form-action 'self';
">
```

### 13.2 Security Headers

| Header                      | Value                          | Purpose                    |
| --------------------------- | ------------------------------ | -------------------------- |
| `X-Content-Type-Options`   | `nosniff`                      | Prevent MIME sniffing      |
| `X-Frame-Options`          | `DENY`                         | Prevent clickjacking       |
| `Referrer-Policy`          | `strict-origin-when-cross-origin` | Control referrer info   |
| `Permissions-Policy`       | `geolocation=(), camera=()`    | Disable unnecessary APIs   |

---

## 14. Technology Decision Records

| Decision                        | Context                                     | Alternatives                  | Consequences                          |
| ------------------------------- | ------------------------------------------- | ----------------------------- | ------------------------------------- |
| Eleventy over Astro             | Simpler config, mature ecosystem            | Astro, Hugo, Jekyll           | Less framework overhead, more manual  |
| Vanilla JS over frameworks      | CON-005 constraint, bundle size             | Alpine.js, Petite-Vue         | More manual wiring, full control      |
| SCSS over CSS-in-JS             | Static site, no runtime overhead            | CSS Modules, Tailwind         | Build step required, BEM discipline   |
| Vitest over Jest                | Faster, ESM native, Vite-compatible         | Jest, Mocha                   | Smaller community, newer tool         |
| Playwright over Cypress         | Cross-browser, faster, headless default     | Cypress, Puppeteer            | Steeper learning curve                |

---

## 15. Related Documentation

### Internal References

| Document                          | Purpose                                    |
| --------------------------------- | ------------------------------------------ |
| `Project_Specification.md`        | Complete system requirements               |
| `Project_Architecture_Blueprint.md` | Architectural patterns and decisions     |
| `Epic-breakdown.md`               | Development epic definitions               |
| `AGENTS.md`                       | Quick reference for requirements           |

### External Resources

| Resource                                                         | Purpose                          |
| ---------------------------------------------------------------- | -------------------------------- |
| [Eleventy Docs](https://www.11ty.dev/docs/)                      | SSG reference                    |
| [WCAG 2.1 Quick Reference](https://www.w3.org/WAI/WCAG21/quickref/) | Accessibility guidelines      |
| [Lighthouse Docs](https://developer.chrome.com/docs/lighthouse/) | Performance auditing             |
| [Atomic Design](https://atomicdesign.bradfrost.com/)             | Component methodology            |

---

v1.0.0 | Draft | **Last Updated**: Dec 04 2025 - 18:00
