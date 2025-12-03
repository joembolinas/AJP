---
title: Academic Journey Portfolio
source: ''
author: Portfolio Owner
post_slug: readme
categories: [docs, portfolio]
tags: [portfolio, academic, github-pages, static-site]
ai_note: Assisted by AI (GitHub Copilot)
summary: Main README for the Academic Journey Portfolio - a scalable, component-based portfolio system for academic content.
date: 2025-12-04
---

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live-blue?style=flat-square&logo=github)](https://joembolinas.github.io)
[![Current Phase](https://img.shields.io/badge/Phase-1%20Documentation-orange?style=flat-square)](./SDLC.md)
[![Term](https://img.shields.io/badge/Term-T3--AY2025-green?style=flat-square)](https://joembolinas.github.io)

> A scalable, component-based portfolio system to document and showcase academic learning, skills development, and growth through GitHub Pages.

[Overview](#overview) • [Features](#features) • [Architecture](#architecture) • [Getting Started](#getting-started) • [Project Status](#project-status)

## Overview

The Academic Journey Portfolio (AJP) is a static web platform designed to systematically document and present academic work, reflections, and professional development throughout an educational journey. Built with a content-first approach, it transforms raw academic materials into a structured, navigable web experience.

**Live Site**: [https://joembolinas.github.io](https://joembolinas.github.io)

### Why Build This?

- **Showcases Growth**: Provides a narrative of development, demonstrating how skills and knowledge evolve over time
- **Encourages Self-Reflection**: Reviewing work helps identify what strategies work best and tracks improvement
- **Demonstrates Preparedness**: Offers a complete picture beyond grades for admissions committees and potential employers
- **Builds Essential Skills**: Improves time management, self-assessment, and digital citizenship

## Features

- **Multi-Source Content Import** — Pull academic content from multiple repositories and directories
- **Term-Based Organization** — Content organized chronologically by academic term
- **Component-Based Architecture** — Modular, reusable UI components for content display
- **Expandable Content Elements** — Interactive components for detailed exploration
- **Category & Skill Filtering** — Browse content by category, skill, or project type
- **Automated Deployment** — CI/CD via GitHub Actions for seamless updates
- **Accessibility Compliant** — WCAG 2.1 standards with minimum Lighthouse score targets

## Architecture

```text
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│  Content        │────▶│  Transformation  │────▶│  GitHub Pages   │
│  Sources        │     │  Pipeline        │     │  Deployment     │
└─────────────────┘     └──────────────────┘     └─────────────────┘
     T3-AY2025               Components              Static Site
     Future Terms            Metadata                 HTTPS
```

### Tech Stack

| Category | Technology |
|----------|------------|
| Hosting | GitHub Pages (Static) |
| Version Control | Git + GitHub |
| CI/CD | GitHub Actions |
| Development | VS Code + GitHub Copilot |
| Architecture | JAMstack (JavaScript, APIs, Markup) |

### Content Structure

```text
content/
├── projects/           # Academic projects and case studies
├── reflections/        # Learning reflections and insights
├── assignments/        # Course assignments and submissions
└── achievements/       # Awards, certificates, and honors
```

> [!NOTE]
> The system supports content from multiple source directories and scales to 1,000+ content files without configuration changes.

## Getting Started

### Prerequisites

- Git and GitHub account
- Node.js LTS (for local development)
- VS Code with GitHub Copilot (recommended)

### Quick Start

1. **Clone the repository**

   ```bash
   git clone https://github.com/joembolinas/joembolinas.github.io.git
   cd joembolinas.github.io
   ```

2. **Review the specification**

   ```bash
   cat spec/Project_Specification.md
   ```

3. **Understand the development phases**

   ```bash
   cat SDLC.md
   ```

> [!TIP]
> Check the `docs/AGENTS.md` file for a quick reference of all system requirements, constraints, and guidelines.

## Project Status

| Phase | Description | Status |
|-------|-------------|--------|
| Phase 1 | Documentation & Planning | 🔄 In Progress |
| Phase 2 | Project Structure & Architecture | ⏳ Pending |
| Phase 3 | Configuration & Content Extraction | ⏳ Pending |
| Phase 4 | Content Integration & Components | ⏳ Pending |
| Phase 5 | Testing & Deployment | ⏳ Pending |

### Development Roadmap

- [x] Project initialization and requirements gathering
- [x] Architecture planning and technical specification
- [ ] Repository structure and component architecture
- [ ] Content extraction pipeline
- [ ] Component development
- [ ] Production deployment

## Portfolio Components

The portfolio showcases various types of academic content:

| Component | Description |
|-----------|-------------|
| **Academic Work** | Papers, projects, presentations, and case studies |
| **Reflections** | Written pieces discussing growth, challenges, and lessons |
| **Extracurriculars** | Sports, clubs, internships, and activities |
| **Achievements** | Awards, certificates, and honors |
| **Technical Learning** | GitHub, VS Code, and development tool experience |

## Performance Targets

| Metric | Target |
|--------|--------|
| Performance | ≥ 90 |
| Accessibility | ≥ 95 |
| Best Practices | ≥ 90 |
| SEO | ≥ 90 |

Scores measured via Google Lighthouse.

## Resources

- [Project Specification](./spec/Project_Specification.md) — Detailed system architecture and requirements
- [Agent Reference Guide](./spec/AGENTS.md) — Quick reference for specifications
- [SDLC Overview](./SDLC.md) — Development lifecycle phases

---

v1.1 | Active Development | **Last Updated**: Dec 04 2025 - 12:00
