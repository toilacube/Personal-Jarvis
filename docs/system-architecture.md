# System Architecture

## Overview

The Life System is a minimalist, file-based personal operating system. It has no backend, no database, and no external services. Everything lives in markdown files on disk, edited through Claude Code or a text editor.

## Architecture Layers

```
┌─────────────────────────────────────┐
│         User Interaction            │
│   (CLI, Claude Code, Editor)        │
└─────────────────┬───────────────────┘
                  │
┌─────────────────▼───────────────────┐
│        Claude Code Agent            │
│   (Skills, Context Loading)         │
└─────────────────┬───────────────────┘
                  │
┌─────────────────▼───────────────────┐
│         File System Layer           │
│    (Markdown Files, Templates)      │
└─────────────────────────────────────┘
```

## Core Components

### 1. Context Layer

Claude reads these files at session start to understand the user's context:

| File | Purpose | Claude Access |
|------|---------|---------------|
| `plan.md` | 10-year vision, life chapters | Every session |
| `journal/YYYY/goals.md` | Annual goals | Every session |
| `reference/values.md` | Mission, values, principles | Every session |
| `reference/habits.md` | Daily routines | Every session |
| `inbox.md` | Quick capture | Every session |
| `CLAUDE.md` | Behavior instructions | Every session |

### 2. Journal Layer

Time-based content organized by year/month:

```
journal/
└── 2026/
    ├── goals.md      # Annual goals (one file per year)
    └── 02/
        ├── 2026-02-17.md   # Daily entries
        └── 2026-02-16.md
```

**Daily Entry Flow**:
1. Morning skill creates entry from template
2. User fills in priorities
3. During-day logging appends to "Log" section
4. Evening reflection adds "Evening" section

### 3. Decision Layer

```
decisions/
├── career-change-2026.md
├── tool-selection.md
└── ...
```

Each decision is a structured markdown file with:
- Status (Open → Active → Closed)
- Context
- Options evaluated
- Decision rationale
- Review date

### 4. Automation Layer

**Scripts**:
- `scripts/journal.sh`: CLI for journal creation
  - Creates daily entries from template
  - Backfills missing days
  - Integrates calendar (optional)
  - Carries over incomplete todos

**Skills**:
- `skills/morning/SKILL.md`: Morning routine automation
  - Loads context files
  - Reviews yesterday
  - Aligns today to goals
  - Creates journal entry

### 5. Search Layer

QMD (optional) provides search across all markdown files:

```
┌─────────────────────────────────────┐
│           QMD Collections           │
├──────────────┬──────────────────────┤
│ journal      │ Daily entries         │
│ reference    │ Values, habits        │
│ decisions   │ Decision records      │
│ root         │ Plans, templates      │
└──────────────┴──────────────────────┘
```

## Data Flow

### Morning Routine

```
1. User: "morning"
       ↓
2. Skill: Load plan.md, goals.md, values.md, inbox.md
       ↓
3. Skill: Read yesterday's journal
       ↓
4. Skill: Create today's journal from template
       ↓
5. Skill + User: Review yesterday, set priorities
       ↓
6. Skill: Alignment check (to-dos → goals → plan)
       ↓
7. Skill: Write today's journal with priorities
       ↓
8. Skill: Summary of 1-3 key outcomes
```

### Decision Documentation

```
1. User: "I need to think through X"
       ↓
2. Skill: Ask clarifying questions
       ↓
3. Skill: Create decision.md from template
       ↓
4. Skill + User: Fill in context, options, criteria
       ↓
5. User: Makes decision
       ↓
6. Skill: Document decision + rationale
       ↓
7. Skill: Set review date
```

### Search

```
1. User: "What have I decided about X?"
       ↓
2. Claude: Uses QMD MCP
       ↓
3. QMD: Searches across collections
       ↓
4. Claude: Presents results with context
```

## Integration Points

### Claude Code

- Reads `CLAUDE.md` for behavior instructions
- Uses skills for structured interactions
- MCP servers provide tool access (QMD)

### Editor Integration

- `journal.sh` opens entries in configured editor
- Default: VS Code (`code`)
- Configurable: vim, Cursor, Obsidian, etc.

### Calendar Integration (macOS)

- Optional: icalBuddy for calendar events
- Pulls today's events into journal
- Filters by calendar name

## Scalability Considerations

### Current Limitations

- Single-user only
- No concurrent editing (git handles this)
- Manual backup required

### When to Consider Changes

| Growth | Change |
|--------|--------|
| Multiple years | Archive old years to separate directory |
| Many decisions | Add subdirectories by category |
| Large journals | Add monthly/weekly summaries |
| Multiple devices | Add sync solution (iCloud, Dropbox, etc.) |

## Security

- Local-only: No cloud services
- `.gitignore`: Excludes `.DS_Store`
- Sensitive info: Keep outside repo (credentials, etc.)

## Future Architecture

Potential enhancements (not implemented):

- Git-based sync across devices
- Backup automation
- Analytics on goal progress
- Multiple journals (work/personal)
