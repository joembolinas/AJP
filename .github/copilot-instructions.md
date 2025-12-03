# GitHub Copilot Instructions

## Project Context

This file provides context and guidelines for GitHub Copilot when working on this project.

File index

| File name                  | abs                     | abc |
| -------------------------- | ----------------------- | --- |
| [README.md](D:\AJP\README.md) | Overall Project context |     |
|                            |                         |     |

**Sample Table Format:**

| Column 1 | Column 2 | Column 3 |
| -------- | -------- | -------- |
| Data 1   | Data 2   | Data 3   |
| Data 4   | Data 5   | Data 6   |

**Current Progress**: Phase 1

### General Guidelines

- No confirmation needed for `.github\prompt\commit.prompt.md`
- Always ask for clarification when encountering unclear or conflicting information across the project workspace
- It's always better to confirm than to guess
- always put footnote all files: "{Version} | {file status} | {**Last Updated**:MMM DD YYYY - HH:SS"


### ALWAYS REMEBER

commit is the only one log of all activities so always suggest git commit and provide message every end task or generate conventional commit messages. It provides instructions, examples, and formatting guidelines to help users write standardized, descriptive commit messages in accordance with the Conventional Commits specification if i forgot to use this `commit.prompt` 

### Environment Awareness for Commits

When generating commit messages, always include context about the environment and changes:

- **Repository Context**: Include branch name, repository state, and any relevant context from the workspace
- **Change Scope**: Clearly identify which files, directories, or components are affected
- **Environment State**: Note if changes affect configuration, dependencies, or development environment
- **Related Files**: Reference related files or components that may be impacted by the changes
- **Commit Body**: Use the body section for detailed explanations when changes span multiple areas or require additional context

Example commit with full context:
```
feat(docs): add sample table format and environment awareness guidelines

- Added sample table format under Project Context section
- Integrated environment awareness instructions for commit messages
- Updated file to include commit context best practices

Affects: .github/copilot-instructions.md
Branch: main
Environment: Documentation updates 



---

## Markdown Documentation Standards

This project enforces strict markdown standards for all documentation and content files.

### Content Rules

1. **Headings**: Use appropriate heading levels (H2, H3, etc.) to structure content. Do not use H1 headings, as these will be generated based on the title.
2. **Lists**: Use bullet points or numbered lists with proper indentation and spacing.
3. **Code Blocks**: Use fenced code blocks for code snippets with language specification for syntax highlighting.
4. **Links**: Use proper markdown syntax. Ensure links are valid and accessible.
5. **Images**: Use proper markdown syntax with alt text for accessibility.
6. **Tables**: Use markdown tables for tabular data with proper formatting and alignment.
7. **Line Length**: Limit line length to 400 characters for readability.
8. **Whitespace**: Use appropriate whitespace to separate sections and improve readability.
9. **Front Matter**: Include YAML front matter at the beginning of files with required metadata fields.

### Formatting Guidelines

#### Headings

- Use `##` for H2 and `###` for H3
- Maintain hierarchical structure
- Recommend restructuring if content includes H4
- Strongly recommend restructuring for H5 or deeper

#### Lists

- Use `-` for bullet points
- Use `1.` for numbered lists
- Indent nested lists with two spaces

#### Code Blocks

- Use triple backticks (```) to create fenced code blocks
- Specify language after opening backticks for syntax highlighting (e.g., ```csharp)

#### Links

- Format: `[link text](URL)`
- Ensure link text is descriptive
- Verify URLs are valid

#### Images

- Format: `![alt text](image URL)`
- Include brief description in alt text

#### Tables

- Use `|` to create tables
- Ensure columns are properly aligned
- Include headers

#### Line Length

- Break lines at 80 characters to improve readability
- Use soft line breaks for long paragraphs

#### Whitespace

- Use blank lines to separate sections
- Avoid excessive whitespace

### Front Matter Requirements

All markdown files must include YAML front matter with the following fields:

- `title`: The title of the post
- `source`: Leave blank
- `author`: The primary author of the post
- `post_slug`: The URL slug for the post
- `categories`: Categories for the post (must be from `/categories.txt`)
- `tags`: Tags for the post
- `ai_note`: Indicate if AI was used in the creation of the post
- `summary`: A brief summary of the post (recommend based on content when possible)
- `date`: The publication date of the post

### Validation

- Ensure content follows the markdown content rules specified above
- Verify proper formatting and structure according to guidelines
- Run validation tools to check for compliance with rules and guidelines

---

## Future Enhancements

The following features are planned for future implementation:

1. Table format enhancements
2. Obsidian link format support
3. Backlink functionality
