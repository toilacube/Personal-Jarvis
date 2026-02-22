# Codebase Summary

This document provides an overview of the Life System codebase. It is auto-generated from the repomix compaction and serves as a quick reference for understanding the project structure and contents.

## Project Overview

- **Project Name**: Life System
- **Type**: Personal productivity/life management system
- **Core Functionality**: A plain-text personal operating system for life planning, journaling, decision-making, and task capture powered by Claude Code
- **Total Files**: 16 files
- **Total Tokens**: ~8,349 tokens

## Directory Structure

```
/home/toilacube/dreamer/jarvis/
├── .claude/
│   ├── .mcp.json              # QMD MCP server configuration
│   ├── settings.json          # Claude settings
│   └── settings.local.json    # Local permissions
├── decisions/                 # Decision records (empty directory)
├── journal/
│   └── 2026/
│       └── goals.md           # Annual goals template
├── reference/
│   ├── habits.md             # Daily habits template
│   └── values.md             # Core values template
├── scripts/
│   └── journal.sh            # Bash script for journal creation
├── skills/
│   └── morning/
│       ├── reference.md      # Morning skill reference
│       └── SKILL.md           # Morning routine skill definition
├── templates/
│   ├── daily-journal.md      # Daily journal template
│   └── decision.md           # Decision record template
├── .gitignore
├── CLAUDE.md                 # Claude configuration
├── inbox.md                  # Quick capture inbox
├── plan.md                   # 10-year life vision
└── README.md                 # Project documentation
```

## Key Files

| File | Purpose | Tokens |
|------|---------|--------|
| `scripts/journal.sh` | Journal CLI tool with calendar integration | 1,759 |
| `README.md` | Project documentation | 1,579 |
| `skills/morning/SKILL.md` | Morning routine skill | 1,535 |
| `CLAUDE.md` | Claude configuration | 1,401 |
| `plan.md` | 10-year life vision | 341 |

## Technology Stack

- **Languages**: Markdown, Bash
- **Tools**: Claude Code, QMD (search), icalBuddy (optional calendar)
- **No backend/database** - purely file-based

## Core Components

### 1. Life Planning (`plan.md`)
- Life chapters (past, present, future)
- Enduring insights (self-knowledge)
- Critical aspects (non-negotiables)
- 10-year vision
- Deliberate non-priorities

### 2. Daily Journal System
- Morning: Franklin's question "What good shall I do this day?"
- Log: Timestamped Carmack-style entries
- Evening: "What good have I done today?"
- Template: `templates/daily-journal.md`

### 3. Decision Records (`decisions/`)
- Structured format for important decisions
- Context, options, criteria, decision, review date
- Template: `templates/decision.md`

### 4. Reference Materials
- `reference/values.md`: Mission, core values, principles
- `reference/habits.md`: Daily schedule, routines, habits

### 5. Claude Integration
- `CLAUDE.md`: Instructions for Claude behavior
- `skills/morning/SKILL.md`: Morning routine automation
- MCP server: QMD for searching markdown files

## File Statistics

```
Top 5 Files by Token Count:
1. scripts/journal.sh     (1,759 tokens, 21.1%)
2. README.md              (1,579 tokens, 18.9%)
3. skills/morning/SKILL.md (1,535 tokens, 18.4%)
4. CLAUDE.md             (1,401 tokens, 16.8%)
5. plan.md               (341 tokens, 4.1%)
```

## Philosophy

The Life System is inspired by:
- **Carmack's .plan files**: Public personal logs with timestamped entries
- **Franklin's systematic self-improvement**: Morning/evening questions, deliberate goal-setting
- **Plain text**: Files as the single source of truth
- **AI accountability**: Claude as a thinking partner that holds you to your stated values

## Getting Help

- Full documentation: See `README.md`
- Claude configuration: See `CLAUDE.md`
- Morning routine: See `skills/morning/SKILL.md`
- Search across all files: Use QMD (`qmd search`, `qmd query`)
