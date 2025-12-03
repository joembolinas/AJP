---
title: "Feature PRD: Content Standards Guide"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
feature_id: F1-001
epic_id: EPIC-001
status: Draft
author: Portfolio Owner
ai_note: Assisted by AI (GitHub Copilot)
summary: PRD for establishing comprehensive content standards including front matter validation rules, markdown formatting guidelines, and content quality criteria.
---

## 1. Feature Name: Content Standards Guide

---

## 2. Epic

- **Parent Epic**: [Documentation & Planning Foundation](../epic.md)
- **Architecture**: [Phase 1 Architecture Specification](../arch.md)
- **Related Requirements**: FR-003, FR-014, NFR-001, NFR-002, VAL-001 through VAL-010

---

## 3. Goal

### Problem

Without defined content standards, the Academic Journey Portfolio faces several challenges:

- **Inconsistent front matter**: Content files lack uniform metadata structure, causing validation failures and broken filtering/categorization
- **Formatting ambiguity**: Contributors (including AI assistants) produce markdown with varying styles, reducing readability and maintainability
- **Quality gaps**: No clear criteria for what constitutes "complete" or "publishable" content leads to incomplete entries reaching production
- **Validation failures**: Build processes reject content without clear guidance on how to fix issues

### Solution

Create a comprehensive Content Standards Guide that defines:

- **Front matter schema**: Required and optional fields with validation rules
- **Markdown formatting conventions**: Heading hierarchy, code blocks, lists, links, images
- **Content quality checklist**: Minimum requirements for each content type (project, reflection, assignment, achievement)
- **Examples**: Valid and invalid content samples for reference
- **Error resolution**: Common validation errors and how to fix them

### Impact

| Metric | Expected Outcome |
|--------|------------------|
| Validation Pass Rate | 95%+ first-time pass rate for new content |
| Content Consistency | 100% compliance with front matter schema |
| Contributor Efficiency | 50% reduction in content revision cycles |
| AI Generation Quality | Copilot produces valid content on first attempt |
| Build Stability | Zero build failures from malformed content |

---

## 4. User Personas

### Primary: Portfolio Owner (Content Author)

- **Role**: Student creating and maintaining portfolio content
- **Goals**: Write content that passes validation on first submission; understand exactly what metadata is required
- **Pain Points**: Unclear which front matter fields are mandatory; inconsistent error messages from validation
- **Needs**: Clear examples, copy-paste templates, validation error explanations

### Secondary: AI Development Assistant (GitHub Copilot)

- **Role**: AI generating content scaffolding and documentation
- **Goals**: Produce valid front matter and properly formatted markdown automatically
- **Pain Points**: Without explicit rules, generates generic or invalid metadata
- **Needs**: Machine-readable schema definitions, explicit formatting rules

### Tertiary: Future Maintainer

- **Role**: Anyone updating content after initial development
- **Goals**: Quickly understand content requirements without reading entire specification
- **Pain Points**: Standards scattered across multiple documents
- **Needs**: Single-source reference for all content rules

---

## 5. User Stories

### Content Creation

- **US-001**: As a Portfolio Owner, I want a front matter template for each content type so that I can create valid content quickly.
- **US-002**: As a Portfolio Owner, I want clear examples of valid and invalid front matter so that I understand the requirements.
- **US-003**: As a Portfolio Owner, I want a content quality checklist so that I know when my content is ready to publish.

### Validation & Error Handling

- **US-004**: As a Portfolio Owner, I want validation error messages that explain how to fix issues so that I can resolve problems independently.
- **US-005**: As a Portfolio Owner, I want to validate content locally before committing so that I avoid failed builds.

### AI-Assisted Development

- **US-006**: As a Portfolio Owner using Copilot, I want the AI to generate valid front matter automatically so that I can focus on content.
- **US-007**: As a Portfolio Owner, I want prompt templates that produce standards-compliant content so that AI assistance is reliable.

### Reference & Learning

- **US-008**: As a new contributor, I want a single document explaining all content rules so that I can onboard quickly.
- **US-009**: As a maintainer, I want the standards guide to be versioned so that I can track changes over time.

---

## 6. Requirements

### Functional Requirements

#### Front Matter Standards

- [ ] **FR-CS-001**: Define required front matter fields for all content types:
  - `title` (string, required)
  - `date` (YYYY-MM-DD, required)
  - `category` (string[], required)
  - `term` (T[1-4]-AY[YYYY], required)
  - `type` (enum: project|reflection|assignment|achievement, required)
- [ ] **FR-CS-002**: Define optional front matter fields:
  - `skills` (string[])
  - `tags` (string[])
  - `summary` (string, max 200 characters)
  - `author` (string, defaults to Portfolio Owner)
  - `ai_note` (string, for AI-assisted content disclosure)
- [ ] **FR-CS-003**: Provide copy-paste templates for each content type
- [ ] **FR-CS-004**: Document field validation rules (format, allowed values, constraints)

#### Markdown Formatting Standards

- [ ] **FR-CS-005**: Define heading hierarchy rules (H2 for sections, H3 for subsections, no H1)
- [ ] **FR-CS-006**: Define code block conventions (language specification, max width)
- [ ] **FR-CS-007**: Define list formatting (bullet vs numbered, indentation)
- [ ] **FR-CS-008**: Define link conventions (relative paths for internal, descriptive text)
- [ ] **FR-CS-009**: Define image requirements (alt text mandatory, size limits, formats)
- [ ] **FR-CS-010**: Define table formatting (alignment, header requirements)

#### Content Quality Standards

- [ ] **FR-CS-011**: Define minimum content requirements per type:
  - Project: Overview, Key Learnings, at least 2 sections
  - Reflection: Context, Insights, minimum 300 words
  - Assignment: Description, Approach, Outcome
  - Achievement: Description, Date, Evidence (if applicable)
- [ ] **FR-CS-012**: Provide quality checklist for self-review before submission
- [ ] **FR-CS-013**: Document content length guidelines (minimum and recommended)

#### Examples & Templates

- [ ] **FR-CS-014**: Provide valid examples for each content type
- [ ] **FR-CS-015**: Provide invalid examples with explanations of what's wrong
- [ ] **FR-CS-016**: Include edge case examples (special characters, long titles, etc.)

#### Error Resolution

- [ ] **FR-CS-017**: Document common validation errors with resolution steps
- [ ] **FR-CS-018**: Provide troubleshooting decision tree for validation failures

### Non-Functional Requirements

- **NFR-CS-001**: Guide MUST be accessible from root `docs/` directory
- **NFR-CS-002**: Guide MUST follow its own formatting standards (dogfooding)
- **NFR-CS-003**: Guide MUST be readable in under 15 minutes for overview
- **NFR-CS-004**: Templates MUST be copy-paste ready (no placeholder syntax that breaks validation)
- **NFR-CS-005**: Guide MUST be referenced in `.github/copilot-instructions.md` for AI context

---

## 7. Acceptance Criteria

### AC: Front Matter Standards

- **AC-CS-001**: Given the Content Standards Guide, when a user creates a project content file using the provided template, then the file passes front matter validation on first attempt.
- **AC-CS-002**: Given the field validation rules, when a user enters an invalid date format, then the validation error clearly states the expected format (YYYY-MM-DD).
- **AC-CS-003**: Given the category field documentation, when a user selects categories, then only predefined allowed values are accepted.

### Markdown Formatting

- **AC-CS-004**: Given the heading hierarchy rules, when content uses H4 or deeper, then the guide recommends restructuring to H3 maximum.
- **AC-CS-005**: Given the image requirements, when an image lacks alt text, then validation fails with a clear accessibility-focused error message.

### Content Quality

- **AC-CS-006**: Given a project content file, when it contains fewer than 2 sections, then the quality checklist flags it as incomplete.
- **AC-CS-007**: Given the quality checklist, when all items are checked, then the content meets minimum publishing standards.

### Examples & Usability

- **AC-CS-008**: Given the provided templates, when copied into a new file, then no placeholder text remains that would cause validation errors.
- **AC-CS-009**: Given an invalid example, when reviewed, then the explanation clearly identifies all violations.

### Integration

- **AC-CS-010**: Given the Content Standards Guide, when referenced by Copilot via custom instructions, then AI-generated content follows the defined standards.

---

## 8. Out of Scope

| Item | Reason | Future Consideration |
|------|--------|---------------------|
| Automated validation tooling | Phase 3 deliverable | Content Pipeline Epic |
| VS Code extension for live validation | Enhancement, not core feature | Post-Phase 5 |
| Multi-language content support | Not required for initial portfolio | Future internationalization |
| Content approval workflow | No multi-user collaboration planned | N/A per CON-007 |
| SEO optimization guidelines | Phase 4/5 concern | Deployment Epic |
| Accessibility testing procedures | Separate from content standards | Accessibility Epic |

---

## 9. Dependencies

### Internal Dependencies

| Dependency | Type | Status |
|------------|------|--------|
| Project Specification (Section 4) | Content schema definition | ✅ Complete |
| AGENTS.md | VAL requirements reference | ✅ Complete |
| markdown.instructions.md | Base formatting rules | ✅ Complete |

### External Dependencies

| Dependency | Type | Impact |
|------------|------|--------|
| categories.txt | Allowed category values | Must exist for category validation |

---

## 10. Success Metrics

| KPI | Target | Measurement Method |
|-----|--------|-------------------|
| Template Usage | 100% of new content uses templates | Manual review of commits |
| First-Pass Validation | ≥95% pass rate | Validation script output |
| Guide Comprehension | No clarifying questions needed | Self-assessment during Phase 2 |
| Copilot Compliance | AI-generated content valid | Sample review of 5 generated files |

---

## 11. Deliverables

| Deliverable | Format | Location |
|-------------|--------|----------|
| Content Standards Guide | Markdown | `docs/content-standards.md` |
| Front Matter Templates | YAML snippets | Embedded in guide |
| Quality Checklists | Markdown checklists | Embedded in guide |
| Example Files | Markdown | `docs/examples/` directory |

---

## 12. Related Documents

- [Project Specification - Section 4](../../Project_Specification.md#4-interfaces--data-contracts)
- [Project Specification - Section 10](../../Project_Specification.md#10-validation-criteria)
- [Markdown Standards](../../../.github/instructions/markdown.instructions.md)
- [Epic PRD](../epic.md)

---

v1.0 | Draft | **Last Updated**: Dec 04 2025 - 16:00
