# Academic Journey Portfolio

> A scalable web-based portfolio system to document and showcase academic learning, skills development, and growth over time through GitHub Pages.

## Table of Contents

- [Overview](#overview)
- [Project Vision](#project-vision)
- [Portfolio Components](#portfolio-components)
- [Project Goals](#project-goals)
- [Project Scope](#project-scope)
- [Stakeholders](#stakeholders)
- [Technical Architecture](#technical-architecture)
- [Development Phases](#development-phases)
- [Requirements](#requirements)
- [Constraints and Assumptions](#constraints-and-assumptions)
- [Risks](#risks)
- [Getting Started](#getting-started)

## Overview

The Academic Journey Portfolio is a simple, scalable web platform designed to document and present academic work, reflections, and personal development throughout your educational journey. Starting with Term 3 (AY2025), this portfolio serves as a comprehensive showcase for teachers, admissions committees, and future employers.

**Live Site**: [https://joembolinas.github.io](https://joembolinas.github.io)

**Current Term**: Term 3 - AY2025

## Project Vision

An academic journey portfolio is a collection of a student's work that documents their learning, skills, and growth over time. It includes academic projects, reflections, and extracurricular activities to showcase progress, achievements, and personal development to others, such as teachers, admissions committees, or future employers.

### Benefits

- **Showcases Growth**: Provides a narrative of development, showing how skills and knowledge have evolved over time
- **Encourages Self-Reflection**: Reviewing your portfolio allows you to see what strategies work best and how you've improved
- **Promotes Ownership**: Taking an active role in education by curating work and articulating learning meaningfully
- **Demonstrates Preparedness**: Offers a complete picture of potential beyond grades for college or graduate school applications
- **Builds Essential Skills**: Improves time management, self-assessment, and digital citizenship

## Portfolio Components

### What to Include

- **Academic Work**: Papers, projects, presentations, case studies, and assignments demonstrating learning
- **Reflections**: Written pieces or videos discussing growth, challenges, and lessons learned
- **Extracurriculars**: Involvement in sports, clubs, internships, or activities showing well-rounded development
- **Achievements**: Awards, certificates, and honors received
- **Goals**: Statements of future aspirations and objectives
- **Personal Interests**: Creative or personal work such as artwork, videos, or recommendations
- **Technical Learning**: Practical experience with tools and platforms, including:
  - GitHub fundamentals (repositories, commits, staging, push)
  - Collaboration workflows (issues, pull requests, branching strategies)
  - GitHub products (Actions, Codespaces, Pages, MCP)
  - Development tools (VS Code, GitHub Copilot)

## Project Goals

### Primary Objectives

1. Build a simple GitHub Pages site for Academic Journey Portfolio starting with Term 3
2. Create a scalable system to accommodate future terms
3. Transform raw academic content into structured, web-friendly formats

### Stakeholder Alignment

- **Content Development**: Transform content from various directories/repositories into structured web design
- **Structured Presentation**: Organize content by sections with components that display information clearly
- **Chronological Organization**: Present content using chronological order, skills categorization, or project grouping
- **Interactive Elements**: Enable expandable/clickable components for detailed content exploration
- **Scalability**: Support content addition and updates at the end of each term from any repository

### Success Criteria

- ✅ Successfully deploy a GitHub Page displaying academic content
- ✅ Scalable architecture allowing content additions/updates every term from any repository
- ✅ Structured, navigable interface for content presentation

## Project Scope

### In Scope

**Features and Functionalities:**

- Easy content addition from various repositories each term
- Expandable content elements for detailed information
- Transform raw content into structured web design
- Component-based architecture for modular content display

**Deliverables:**

- **Phase 1**: Documentation and planning
- **Phase 2**: Project structure and architecture
- **Phase 3**: Configuration, setup, prompts, and Term 3 content extraction
- **Phase 4**: Content integration and component development
- **Phase 5**: Testing, deployment, and documentation

### Out of Scope

**Excluded Features:**

- Custom UI design (HTML/CSS frameworks may be revised if needed)
- Complex interactive features beyond basic expandable elements
- Backend database systems
- User authentication systems

**Limitations:**

- Preference for minimal manual HTML/CSS coding
- Constraint to GitHub Pages deployment capabilities

## Stakeholders

### Key Stakeholders

#### User (Portfolio Owner)

- **Role**: Content creator and maintainer
- **Responsibilities**: Update content at the end of each term, curate academic work, maintain portfolio accuracy

#### Visitor (Audience)

- **Role**: Portfolio viewer
- **Responsibilities**: Browse content, assess academic progress, explore projects and achievements
- **Audience Types**: Teachers, admissions committees, potential employers, peers

### Input Management

- Stakeholder feedback gathered through GitHub issues
- Content updates managed through pull requests
- Regular review cycles at term completion

## Technical Architecture

### Tech Stack

**Development Tools:**

- **AI-Assisted Development**: GitHub Copilot with custom instructions, agent.md, and prompt.md configurations
- **Version Control**: Git and GitHub
- **Automation**: GitHub Actions for CI/CD workflows
- **Deployment**: GitHub Pages
- **Development Environment**: VS Code with MCP integration

**Content Source:**

- Primary: `C:\Users\ADMIN\Desktop\School File\T3-AY2025`
- Future terms from additional directories/repositories

**Deployment Target:**

- Repository: `https://github.com/joembolinas/joembolinas.github.io`

### Development Workflow

1. Content extraction from term directories
2. Structured data transformation
3. Component-based presentation layer
4. Automated deployment via GitHub Actions
5. Continuous integration through pull requests and issues

## Development Phases

### Phase 1: Documentation

- Project requirements gathering
- Architecture planning
- Technical specifications

### Phase 2: Structure

- Repository setup
- Directory organization
- Component architecture design

### Phase 3: Configuration & Content Extraction

- Development environment setup
- Prompt engineering for content transformation
- Term 3 content extraction and processing

### Phase 4: Integration

- Component development
- Content integration
- Feature implementation

### Phase 5: Deployment

- Testing and quality assurance
- Production deployment
- Documentation finalization

## Requirements

### Functional Requirements

**Content Management:**

- System must support content import from multiple repositories
- Content must be organizable by term, skill, and project type
- Components must support expandable/collapsible functionality

**Navigation:**

- Users must be able to browse content chronologically
- Content must be filterable by category or skill
- Each content item must link to detailed information

**Validation:**

- Content structure validation through automated checks
- Link verification for all references
- Accessibility compliance testing

### Non-Functional Requirements

**Performance:**

- Page load time < 3 seconds
- Responsive design for mobile and desktop
- Optimized asset delivery

**Security:**

- Compliance with school posting regulations
- No sensitive personal information exposure
- Secure GitHub Pages deployment

**Usability:**

- Intuitive navigation structure
- Clear content organization
- Accessible to all user types

**Measurement:**

- Google Lighthouse scores for performance monitoring
- GitHub Pages analytics for visitor tracking
- User feedback through GitHub issues

## Constraints and Assumptions

### Constraints

**Resources:**

- Limited to GitHub Pages free tier capabilities
- No backend server or database
- Static site generation only

**Technology:**

- Must comply with GitHub Pages supported frameworks
- Limited to client-side JavaScript for interactivity

**Compliance:**

- Must adhere to school rules regarding content posting
- Privacy considerations for academic work sharing

### Assumptions

**Environment:**

- GitHub Pages remains available and free
- Content source directories maintain consistent structure
- Regular term-end updates (approximately quarterly)

**Impact:**

- Assumption changes may require architecture modifications
- Content source changes may need transformation script updates

## Risks

### Potential Risks

| Risk | Impact | Probability | Mitigation Strategy |
|------|--------|-------------|---------------------|
| Content source structure changes | High | Medium | Flexible extraction scripts, documented content format |
| GitHub Pages service changes | High | Low | Alternative static hosting backup plan |
| Content privacy concerns | High | Medium | Content review process, compliance checks |
| Scalability limitations | Medium | Medium | Modular architecture, performance monitoring |
| Maintenance burden | Medium | High | Automated workflows, clear documentation |

### Risk Management

**Identification:**

- Regular architecture reviews
- Monitoring GitHub Pages updates
- Stakeholder feedback collection

**Assessment:**

- Impact and probability evaluation
- Risk priority matrix
- Regular risk register updates

**Mitigation:**

- Preventive measures in architecture
- Contingency plans for critical risks
- Regular backup and version control

## Getting Started

### Prerequisites

- Git installed and configured
- GitHub account with access to deployment repository
- VS Code with GitHub Copilot (recommended)
- Node.js (if using build tools)

### Initial Setup

```bash
# Clone this repository
git clone https://github.com/joembolinas/AJP.git
cd AJP

# Configure deployment repository
git remote add pages https://github.com/joembolinas/joembolinas.github.io.git

# Review project structure
cat SDLC.md
```

### Contributing

1. Create a feature branch for each term or major update
2. Follow the established content structure
3. Submit pull requests for review
4. Address feedback before merging

### Documentation

- See `SDLC.md` for detailed development lifecycle information
- Check `.github/instructions/` for contribution guidelines
- Review prompt files for AI-assisted development patterns

---

**Last Updated**: December 3, 2025
**Current Phase**: Phase 1 - Documentation
**Next Milestone**: Phase 2 - Structure Development
