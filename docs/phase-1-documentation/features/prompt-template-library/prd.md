---
title: "Feature PRD: Prompt Template Library"
version: 1.0
date_created: 2025-12-04
last_updated: 2025-12-04
owner: Portfolio Owner
feature_id: F1-002
epic_id: EPIC-001
status: Draft
author: Portfolio Owner
ai_note: Assisted by AI (GitHub Copilot)
summary: PRD for creating a comprehensive library of reusable prompt templates for AI-assisted development tasks in the AJP project.
---

## 1. Feature Name: Prompt Template Library

---

## 2. Epic

- **Parent Epic**: [Documentation & Planning Foundation](../epic.md)
- **Architecture**: [Phase 1 Architecture Specification](../arch.md)
- **Related Requirements**: FR-018, GUD-001, TE4

---

## 3. Goal

### Problem

AI-assisted development with GitHub Copilot produces inconsistent results when prompts are ad-hoc:

- **Inconsistent outputs**: Same task requested differently yields varying code quality and style
- **Lost context**: Each new session requires re-explaining project conventions
- **Repeated effort**: Common tasks require crafting similar prompts repeatedly
- **Quality variance**: Without structured prompts, AI may miss project-specific requirements (accessibility, BEM naming, JSDoc)
- **Onboarding friction**: New users don't know how to effectively prompt for project-compliant code

### Solution

Create a Prompt Template Library containing standardized, reusable prompts for common development tasks:

- **Task-specific templates**: Component creation, content generation, documentation writing, debugging
- **Context injection**: Templates include project-specific requirements automatically
- **Output formatting**: Templates specify expected output structure
- **Validation hooks**: Templates include acceptance criteria for self-checking
- **Usage documentation**: Clear instructions on when and how to use each template

### Impact

| Metric | Expected Outcome |
|--------|------------------|
| Prompt Reuse Rate | 80%+ of AI interactions use templates |
| Code Compliance | 95%+ generated code follows project standards |
| Development Velocity | 40% reduction in prompt iteration cycles |
| Consistency | Uniform output structure across sessions |
| Onboarding Time | New users productive with AI in <30 minutes |

---

## 4. User Personas

### Primary: Portfolio Owner (Developer)

- **Role**: Student developer using Copilot for code and content generation
- **Goals**: Get project-compliant code on first prompt; reduce time spent refining AI outputs
- **Pain Points**: Forgetting to include project requirements in prompts; inconsistent results
- **Needs**: Ready-to-use templates, clear usage instructions, customization guidance

### Secondary: AI Development Assistant (GitHub Copilot)

- **Role**: AI receiving prompts and generating outputs
- **Goals**: Produce accurate, complete, project-compliant outputs
- **Pain Points**: Incomplete context leads to generic or incorrect outputs
- **Needs**: Explicit requirements, output format specifications, examples

### Tertiary: Future Maintainer

- **Role**: Anyone extending the portfolio or adding new AI workflows
- **Goals**: Understand existing prompt patterns; create new templates following conventions
- **Pain Points**: Inconsistent template formats make extension difficult
- **Needs**: Template structure documentation, naming conventions, contribution guidelines

---

## 5. User Stories

### Template Usage

- **US-001**: As a Portfolio Owner, I want a prompt template for creating new content files so that the output includes valid front matter.
- **US-002**: As a Portfolio Owner, I want a prompt template for generating UI components so that the code follows BEM naming and accessibility standards.
- **US-003**: As a Portfolio Owner, I want a prompt template for writing documentation so that it follows markdown.instructions.md standards.
- **US-004**: As a Portfolio Owner, I want a prompt template for debugging issues so that the AI considers project context.

### Template Discovery

- **US-005**: As a Portfolio Owner, I want an index of all available templates so that I can find the right one quickly.
- **US-006**: As a Portfolio Owner, I want templates organized by category so that I can browse by task type.
- **US-007**: As a Portfolio Owner, I want usage examples for each template so that I understand how to customize them.

### Template Management

- **US-008**: As a maintainer, I want a standard template format so that new templates are consistent.
- **US-009**: As a maintainer, I want templates versioned with the project so that changes are tracked.
- **US-010**: As a maintainer, I want templates to reference project requirements by ID so that they stay aligned with specifications.

---

## 6. Requirements

### Functional Requirements

#### Core Templates

- [ ] **FR-PT-001**: Create content generation template for each content type:
  - Project content template
  - Reflection content template
  - Assignment content template
  - Achievement content template
- [ ] **FR-PT-002**: Create component development templates:
  - HTML component template (semantic, accessible)
  - CSS component template (BEM naming)
  - JavaScript component template (progressive enhancement)
- [ ] **FR-PT-003**: Create documentation templates:
  - Feature PRD template (this document format)
  - Technical specification template
  - README section template
- [ ] **FR-PT-004**: Create utility templates:
  - Code review prompt
  - Debugging assistance prompt
  - Refactoring prompt
  - Test case generation prompt

#### Template Structure

- [ ] **FR-PT-005**: Each template MUST include:
  - Template name and ID
  - Purpose/use case description
  - Required context inputs (placeholders)
  - Expected output format
  - Project requirements to enforce
  - Usage example
- [ ] **FR-PT-006**: Templates MUST use consistent placeholder syntax: `{PLACEHOLDER_NAME}`
- [ ] **FR-PT-007**: Templates MUST reference relevant requirement IDs (REQ-XXX, PAT-XXX, etc.)

#### Template Organization

- [ ] **FR-PT-008**: Create template index file listing all available templates
- [ ] **FR-PT-009**: Organize templates by category in subdirectories:
  - `.github/prompt/content/`
  - `.github/prompt/component/`
  - `.github/prompt/documentation/`
  - `.github/prompt/utility/`
- [ ] **FR-PT-010**: Use consistent naming: `{category}-{action}.prompt.md`

#### Integration

- [ ] **FR-PT-011**: Reference Prompt Template Library in copilot-instructions.md
- [ ] **FR-PT-012**: Include template usage guidance in AGENTS.md quick reference

### Non-Functional Requirements

- **NFR-PT-001**: Templates MUST be usable without modification for common cases
- **NFR-PT-002**: Templates MUST be customizable for edge cases
- **NFR-PT-003**: Template file size MUST be ≤2KB for quick reading
- **NFR-PT-004**: Templates MUST work with both chat and inline Copilot modes
- **NFR-PT-005**: Templates MUST produce outputs that pass project validation

---

## 7. Acceptance Criteria

### Template Quality

- **AC-PT-001**: Given the project content template, when used with Copilot, then the generated file includes valid front matter matching the Content Standards Guide.
- **AC-PT-002**: Given the HTML component template, when used with Copilot, then the generated code uses semantic elements and includes ARIA attributes where needed.
- **AC-PT-003**: Given the CSS component template, when used with Copilot, then the generated code follows BEM naming convention.

### Template Usability

- **AC-PT-004**: Given the template index, when a user searches for a template by task, then they find the relevant template within 30 seconds.
- **AC-PT-005**: Given any template, when the placeholder syntax is reviewed, then all placeholders are clearly labeled with expected input type.
- **AC-PT-006**: Given a template usage example, when followed exactly, then the output is production-ready.

### Template Consistency

- **AC-PT-007**: Given all templates, when reviewed for structure, then 100% follow the defined template format (FR-PT-005).
- **AC-PT-008**: Given template file names, when listed, then all follow the naming convention (FR-PT-010).

### AC: Integration

- **AC-PT-009**: Given copilot-instructions.md, when read by Copilot, then it references the Prompt Template Library location.
- **AC-PT-010**: Given a template with requirement references, when cross-checked with AGENTS.md, then all referenced IDs exist.

---

## 8. Out of Scope

| Item | Reason | Future Consideration |
|------|--------|---------------------|
| Automated template validation | Enhancement, not core feature | Post-Phase 5 |
| Template versioning beyond git | Git history sufficient | N/A |
| Interactive template builder | Overhead not justified | N/A |
| Templates for non-AJP projects | Project-specific scope | N/A |
| Multi-AI provider support | GitHub Copilot only per GUD-001 | Future if needed |
| Template analytics/usage tracking | Privacy concern, not needed | N/A |

---

## 9. Dependencies

### Internal Dependencies

| Dependency | Type | Status |
|------------|------|--------|
| copilot-instructions.md | Integration point | ✅ Complete |
| markdown.instructions.md | Documentation standards | ✅ Complete |
| Content Standards Guide | Content template requirements | ⏳ Pending (F1-001) |
| Project Specification | Requirement IDs to reference | ✅ Complete |

### External Dependencies

| Dependency | Type | Impact |
|------------|------|--------|
| GitHub Copilot | AI provider | Required for template usage |
| VS Code | IDE integration | Required for prompt file support |

---

## 10. Success Metrics

| KPI | Target | Measurement Method |
|-----|--------|-------------------|
| Template Coverage | All common tasks have templates | Checklist audit |
| Template Usage | 80%+ of AI interactions use templates | Self-reported during development |
| Output Compliance | 95%+ outputs pass validation | Validation script results |
| Template Discoverability | Found in <30 seconds | Timed self-test |

---

## 11. Deliverables

| Deliverable | Format | Location |
|-------------|--------|----------|
| Template Index | Markdown | `.github/prompt/README.md` |
| Content Templates | Prompt files | `.github/prompt/content/*.prompt.md` |
| Component Templates | Prompt files | `.github/prompt/component/*.prompt.md` |
| Documentation Templates | Prompt files | `.github/prompt/documentation/*.prompt.md` |
| Utility Templates | Prompt files | `.github/prompt/utility/*.prompt.md` |

---

## 12. Related Documents

- [Epic PRD](../epic.md)
- [Copilot Instructions](../../../.github/copilot-instructions.md)
- [Existing Commit Prompt](../../../commit.prompt.md)
- [Existing Epic Prompt](../../../.github/prompt/3-breakdown-epic-pm.prompt.md)

---

v1.0 | Draft | **Last Updated**: Dec 04 2025 - 16:00
