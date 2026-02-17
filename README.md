

# Personal Jarvis

Personal Jarvis to manage my life. Powered by Claude Code. Inspired by Carmack's .plan files and Franklin's systematic self-improvement.

Forked from: https://github.com/davidhariri/life
## What This Is

A plain-text system for life planning, daily journaling, decision-making, and task capture — with Claude Code as your thinking partner. No apps, no subscriptions. Just markdown files, a terminal, and an AI that pushes back.

## What You Get

- **Life plan** — 10-year vision, life chapters, what you're optimizing for
- **Annual goals** — Yearly bets, anti-goals, who you're becoming
- **Daily journal** — Franklin's morning question + Carmack-style timestamped log + evening reflection
- **Decision records** — Structured docs for important decisions so you can trace your reasoning later
- **Inbox** — Quick capture for tasks, ideas, and things to process later
- **Values & habits** — Your principles and daily routines, written down so Claude can hold you to them

## Quick Start

```bash
cd /home/toilacube/dreamer/life-system
claude
```

Say "morning" or "let's plan the day" — Claude will run the full routine.

## Structure

```
life-system/
├── CLAUDE.md              # Claude configuration
├── plan.md                # 10-year life vision
├── inbox.md               # Quick capture
├── decisions/             # Decision records
├── journal/
│   └── 2026/goals.md     # Annual goals
├── reference/
│   ├── values.md          # Mission, values, principles
│   └── habits.md          # Daily routines
├── scripts/journal.sh     # Journal CLI tool
├── skills/morning/        # Morning routine skill
└── templates/             # Journal, decision templates
```

## Key Files

| File | Purpose |
|------|---------|
| `plan.md` | 10-year vision, life chapters, non-negotiables |
| `journal/2026/goals.md` | Annual goals with checkboxes |
| `skills/morning/SKILL.md` | Morning routine automation |
| `CLAUDE.md` | How Claude behaves |

## Daily Flow

### Morning
- Claude reviews yesterday's journal, goals, and life plan
- Creates today's journal from template
- Asks Franklin's question: "What good shall I do this day?"
- Challenges your priorities against stated goals

### During the Day
- Auto-logging: Claude adds timestamped entries
- Inbox capture: Tasks go to `inbox.md`
- Decision records: Claude helps document important decisions

### Evening
- Franklin's question: "What good have I done today?"
- Brief reflection on what happened vs. what was planned

## Setup (Optional)

### Journal Script

```bash
cp scripts/journal.sh ~/.scripts/journal.sh
chmod +x ~/.scripts/journal.sh
echo "alias jrn='~/.scripts/journal.sh'" >> ~/.zshrc
source ~/.zshrc
```

Then customize `JOURNAL_DIR` and `TEMPLATE` in the script.

### QMD Search

```bash
npm install -g @tobilu/qmd
cd /home/toilacube/dreamer/life-system
qmd update && qmd embed
```

## Customizing

Everything is a starting point:
- Remove Franklin's questions if you don't want them
- Add weekly reviews with a `week-WW.md` template
- Update `reference/habits.md` for your routine
- Modify `CLAUDE.md` to change how Claude behaves

## The Key Insight

Claude reads your plan, goals, and values before every session. It holds you accountable to what you said matters. When your daily actions drift from your annual goals, it names it.

The files are the source of truth. Claude is the accountability partner who never forgets.

## Documentation

See the `docs/` directory for detailed documentation:
- `project-overview-pdr.md` — Product requirements
- `code-standards.md` — Conventions
- `system-architecture.md` — How it works
- `project-roadmap.md` — Future plans
