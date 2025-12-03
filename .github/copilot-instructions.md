# GitHub Copilot Custom Instructions for AJP

SEE HERE THE CONTEXT OF MY PROMPT: `docs/Project_Specification.md`

## Project Context

This is the **Academic Journey Portfolio (AJP)** project - a GitHub Pages portfolio system for documenting academic learning and growth.

**Current Progress**: Phase 1 (Documentation)

### Project Files Reference

| File                                                               | Description                             |
| ------------------------------------------------------------------ | --------------------------------------- |
| [`README.md`](../README.md)                                         | Overall project context and overview    |
| [`docs/Project_Specification.md`](../spec/Project_Specification.md) | Complete system specification           |
| [`docs/AGENTS.md`](../spec/AGENTS.md)                               | Agent reference guide with requirements |

---

## Available Agents

### @mentor

Use the mentor agent for:

- Learning new concepts
- Understanding project architecture
- Getting guided help with debugging
- Code review with educational feedback

**Invoke with**: "As my mentor, help me understand..."

---

## Development Standards

### Code Style

- Use semantic HTML5 elements
- Follow BEM naming convention for CSS
- Write accessible, WCAG 2.1 compliant code
- Include meaningful comments for learning
- Implement progressive enhancement for JavaScript features

### Documentation

- All functions should have JSDoc comments
- Explain the "why" not just the "what"
- Link to relevant project specifications
- Always put footnote on files: `{Version} | {file status} | {Last Updated: MMM DD YYYY - HH:MM}`

### Git Workflow

- Write descriptive commit messages
- Reference issues in commits
- Use conventional commit format
- Commit is the primary log of all activities

---

## General Guidelines

- No confirmation needed for `.github\prompt\commit.prompt.md`
- Always ask for clarification when encountering unclear or conflicting information
- It's always better to confirm than to guess
- Follow requirements defined in `docs/AGENTS.md` (REQ, SCL, SEC, CON, GUD, PAT, AC)

### Commit Reminder

Always suggest git commit and provide a message at the end of each task. Generate conventional commit messages following the Conventional Commits specification. Use `commit.prompt` for detailed guidance.

---

*v1.1.0 | Active | Last Updated: Dec 04 2025 - 14:30*
