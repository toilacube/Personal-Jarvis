# Log Skill Reference

Quick reference for using the `/log` command in your Personal Jarvis system.

---

## Usage

Invoke with `/log` or use natural language triggers:
- "log: [entry]"
- "note: [something]"
- "add todo: [task]"
- "capture: [item]"
- "add to inbox: [item]"

---

## File Paths

All paths are absolute (no `~` expansion needed):

| File | Path |
|------|------|
| Daily journal | `/home/toilacube/dreamer/jarvis/journal/YYYY/MM/YYYY-MM-DD.md` |
| Inbox | `/home/toilacube/dreamer/jarvis/inbox.md` |
| Template | `/home/toilacube/dreamer/jarvis/templates/daily-journal.md` |

---

## Actions

### Add Log Entry
Adds a timestamped entry to today's Log section.

**Example:**
```
log: finished the backend API
```

**Result:**
```markdown
- 14:32 — Finished the backend API
```

---

### Add Todo
Adds a task to Morning Priorities. Shows incomplete tasks from previous days first.

**Example:**
```
add todo: review PR #123
```

**Result:**
```markdown
- [ ] Review PR #123
```

---

### Add to Inbox
Quick capture to inbox.md. Asks which section.

**Example:**
```
capture: idea for automated backup system
```

**Result in Ideas section:**
```markdown
- Idea for automated backup system
```

---

### View Today
Shows Morning Priorities and Log sections from today's journal.

---

### Mark Complete
Marks a task as done in Morning Priorities.

**Example:**
```
mark complete: review PR #123
```

**Result:**
```markdown
- [x] Review PR #123
```

---

### View Past Incomplete Tasks
Shows incomplete todos from the past 7 days, grouped by day.

---

## Rules

1. **Never auto-complete checkboxes** — Only `[x]` when user explicitly confirms
2. **"Note" ≠ "Do"** — "Note this" captures info but leaves checkbox unchecked
3. **Learning ≠ Doing** — "Researching X" goes in Log/Reading, not as completed task
4. **Log what happens, not intentions** — Future plans go to inbox

---

## Daily Journal Structure

```markdown
# YYYY-MM-DD

## Morning (Franklin: "What good shall I do this day?")
- [ ] Task 1
- [ ] Task 2

## Reading / Learning
- [ ] Book/article

## Log
- HH:MM — Entry 1
- HH:MM — Entry 2

## Evening (Franklin: "What good have I done today?")
```
