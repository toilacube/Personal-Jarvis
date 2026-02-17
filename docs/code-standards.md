# Code Standards

This document defines the conventions and standards for the Life System project.

## Philosophy

- **Plain text first**: Markdown as the universal format
- **Minimalism**: No apps, no subscriptions, no database
- **Automation with boundaries**: Scripts assist, human decides
- **Auditability**: Every decision traceable to context

## File Conventions

### Naming

| Type | Convention | Example |
|------|------------|---------|
| Daily journal | `YYYY-MM-DD.md` | `2026-02-17.md` |
| Weekly review | `week-WW.md` | `week-07.md` |
| Annual goals | `goals.md` | `journal/2026/goals.md` |
| Decision | Descriptive, kebab-case | `career-change-2026.md` |
| Book note | `{title-slug}.md` | `atomic-habits.md` |
| Course note | `{course-slug}.md` | `rust-for-rustaceans.md` |

### Directory Structure

```
life-system/
├── journal/              # All time-based content
│   └── YYYY/            # Year directory
│       ├── goals.md     # Annual goals (required)
│       └── MM/          # Month directory (required for daily)
├── decisions/           # Decision records
├── library/             # Books, courses, articles, learning
├── reference/           # Static reference material
├── scripts/             # Executable scripts
├── skills/              # Claude Code skills
└── templates/           # Reusable templates
```

### Markdown Standards

- Use ATX-style headers (`#`, `##`, `###`)
- Use fenced code blocks with language hints
- Use tables for structured data
- Use checkboxes (`- [ ]`, `- [x]`) for todos
- Use horizontal rules (`---`) to separate sections

### Checkbox Format

```markdown
## Morning Priorities
- [ ] Key outcome 1 (connects to: [goal reference])
- [x] Completed item
```

## Template Standards

### Daily Journal Template

Must include:
- Date header (`# YYYY-MM-DD`)
- Morning section with Franklin's question
- Log section for timestamped entries
- Evening section (optional)

### Decision Template

Must include:
- Status field
- Date opened
- Context section
- Options table (upsides, downsides, gut feel)
- Optimization criteria
- Decision section (written after)
- Review date

### Goals Template

Must include:
- Year header
- Area-based goals with checkboxes
- Anti-goals section
- "Becoming" section (identity-based)

## Script Standards (Bash)

### Required Elements

```bash
#!/bin/bash
# Description: One-line purpose
# Setup instructions in comments

# Constants at top (editable)
JOURNAL_DIR="$HOME/path/to/journal"
TEMPLATE="$HOME/path/to/template"
EDITOR_CMD="code"
```

### Best Practices

- Use `set -e` for error handling when appropriate
- Quote variables to handle spaces
- Check dependencies before execution
- Provide helpful error messages
- Support both macOS and Linux where possible

### Script Location

- User scripts: `~/.scripts/` (outside repo)
- Repo scripts: `scripts/` (shared/documented)

## Claude Code Skill Standards

### Skill File Structure

```markdown
---
name: skill-name
description: Clear description of when to use
user-invocable: true/false
allowed-tools: Read, Edit, Write, Glob, Grep, Bash, AskUserQuestion
---

# Skill Name

## Step 1: [Action]
[Details]

## Step 2: [Action]
[Details]
```

### Naming Convention

- Lowercase, kebab-case: `morning`, `weekly-review`
- One word or two hyphenated words max

### Documentation Standards

- Every skill needs a reference file
- Reference includes file locations and usage examples

## Values & Principles

### values.md Structure

1. **Mission**: One sentence, what you're here to do
2. **Core Values**: 3-5 descriptive (not aspirational) values
3. **Core Principles**: Rules from experience
4. **Work Principles**: How you do best work

### habits.md Structure

1. **Daily Schedule**: Time-blocked ideal day
2. **Morning Routine**: Ordered list of actions
3. **Core Habits**: Grouped by domain (Health, Mind, Financial, Relationships)

## Git Conventions

- Commit messages: Clear, imperative ("Add morning skill" not "Added")
- No merge rebasing (preserve history)
- Work in feature branches for experimental changes

## Search & Indexing

- QMD collections: Separate by content type (journal, reference, decisions, library)
- Rebuild index after adding 10+ new files
- Use context in collection definitions

### Collections

| Collection | Path | Description |
|------------|------|-------------|
| journal | `journal/**/*.md` | Daily entries, goals |
| reference | `reference/**/*.md` | Values, habits |
| decisions | `decisions/**/*.md` | Decision records |
| library | `library/**/*.md` | Books, courses, articles |
