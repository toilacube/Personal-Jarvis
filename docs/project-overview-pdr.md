# Project Overview & PDR

## Project Overview

**Project Name**: Life System  
**Type**: Personal productivity/life management system  
**Core Functionality**: A plain-text personal operating system for life planning, journaling, decision-making, and task capture powered by Claude Code  
**Philosophy**: Files as source of truth, AI as accountability partner

## Problem Statement

Individuals struggle with:
- **Accountability drift**: Goals and values get forgotten in daily noise
- **Decision amnesia**: Past reasoning is lost or undocumented
- **Disconnected actions**: Daily tasks don't ladder up to long-term goals
- **Scattered capture**: Tasks and ideas live in multiple apps

## Solution

A minimal, file-based system where:
1. Plain markdown files store all life data
2. Claude Code reads your plan before every session
3. Automated morning/evening routines keep you aligned
4. Searchable archives preserve decision context

## Product Requirements

### Core Features

| Feature | Description | Priority |
|---------|-------------|----------|
| Life Plan | 10-year vision, chapters, non-negotiables | Required |
| Annual Goals | Yearly bets with progress tracking | Required |
| Daily Journal | Morning priorities + timestamped log + evening reflection | Required |
| Decision Records | Structured format for important decisions | Required |
| Inbox | Quick capture for tasks/ideas | Required |
| Values & Habits | Reference materials for Claude context | Required |
| Morning Skill | Claude Code skill for daily routine | Required |
| Search | QMD integration for cross-file search | Optional |

### User Interactions

1. **Morning Routine** (triggered by "morning" or "let's plan the day"):
   - Claude loads context (yesterday's journal, annual goals, life plan, inbox)
   - Reviews what happened yesterday
   - Creates today's journal from template
   - Challenges priorities against stated goals
   - Finalizes 1-3 key outcomes

2. **Throughout the Day**:
   - Auto-logging: Claude adds timestamped entries
   - Inbox capture: Tasks go to `inbox.md`
   - Decision support: Claude helps document important decisions

3. **Evening** (optional):
   - Franklin's closing question
   - Brief reflection on accomplished vs. planned

### Data Flow

```
User Input → Claude → File System (markdown)
                 ↓
           Context Files (plan, goals, values)
                 ↓
           Daily Alignment Check
                 ↓
           Journal Entry Updated
```

## Technical Specification

### File Structure

```
life-system/
├── CLAUDE.md              # Claude behavior instructions
├── plan.md                # 10-year vision
├── inbox.md               # Quick capture
├── decisions/             # Decision records
├── journal/
│   └── YYYY/
│       ├── goals.md       # Annual goals
│       └── MM/
│           └── YYYY-MM-DD.md  # Daily journals
├── reference/
│   ├── values.md         # Mission, values, principles
│   └── habits.md         # Daily routines
├── scripts/
│   └── journal.sh        # CLI for journal creation
├── skills/
│   └── morning/
│       ├── SKILL.md      # Morning routine skill
│       └── reference.md # Skill reference
└── templates/
    ├── daily-journal.md
    └── decision.md
```

### Dependencies

| Tool | Purpose | Required |
|------|---------|----------|
| Claude Code | AI assistant | Yes |
| Markdown editor | File editing | Yes |
| QMD | Search (optional) | No |
| icalBuddy | Calendar integration (macOS) | No |

## Acceptance Criteria

- [ ] Life plan template is customizable with 10-year vision
- [ ] Annual goals can be tracked with checkboxes
- [ ] Daily journal creates from template with date placeholders
- [ ] Morning skill loads all context files in parallel
- [ ] Decision records follow structured format
- [ ] Inbox captures tasks without disrupting flow
- [ ] Values and habits are readable by Claude
- [ ] Journal script creates/backfills entries
- [ ] QMD can search across all markdown files

## Future Considerations

- Weekly/monthly review templates
- Multiple goal tracks (work, personal, health)
- Project-specific sub-journals
- Backup/sync solutions
- Analytics on goal progress
