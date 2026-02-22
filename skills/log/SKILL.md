---
name: log
description: "Quick logging, todo management, and inbox capture. Use when user says 'log', 'note', 'add todo', 'capture', or wants to add entries to today's journal or inbox."
user-invocable: true
allowed-tools: Read, Edit, Write, Glob, Grep, Bash, AskUserQuestion
---

# Log - Quick Logging & Todo Management

Streamline daily workflow with quick commands to interact with the journal without manually editing files.

**Tone:** Direct, concise. Keep the conversation flowing — say "Added to log: [summary]" without asking permission when adding log entries.

---

## Step 1: Get Today's Journal

Calculate today's date (YYYY-MM-DD format) and check if the journal exists at `/home/toilacube/dreamer/jarvis/journal/YYYY/MM/YYYY-MM-DD.md`.

If it doesn't exist:
- Read `/home/toilacube/dreamer/jarvis/templates/daily-journal.md`
- Create today's journal from the template (replace `{{DATE}}` with today's date)

---

## Step 2: Determine Action

Use AskUserQuestion to clarify what the user wants to do:

**Options:**
1. **Add a log entry** — Add a timestamped entry to the Log section
2. **Add a todo** — Add a task to Morning Priorities
3. **Add to inbox** — Quick capture to inbox.md
4. **View today** — Show Morning Priorities and Log sections
5. **Mark complete** — Mark a task as done
6. **View past incomplete tasks** — Show incomplete todos from previous days

---

## Step 3: Add Log Entry

1. Get current timestamp in HH:MM format (use 24-hour format)
2. Read today's journal
3. Append to the Log section: `- HH:MM — [user's entry]`
4. Say: "Added to log: [brief summary of entry]"

**Never ask permission** for log entries — just do it and notify.

---

## Step 4: Add Todo

### 4a: Show Past Incomplete Tasks First

Before adding a new todo, read the previous day's journal and extract incomplete tasks:
- Look for `- [ ]` items in the Morning Priorities section
- Present these to the user first: "Incomplete from yesterday: [list]"

Use AskUserQuestion: "Add a new task or select from incomplete past tasks?"
- Option 1: Add new task
- Option 2: Carry over a past task (then show the list to choose from)

### 4b: Add New Task

1. Get the task text from the user
2. Read today's journal
3. Append to Morning Priorities section: `- [ ] [user's task]`
4. Support sub-tasks (numbered or indented list items)
5. Say: "Added todo: [task text]"

**Do not auto-complete** — leave the checkbox unchecked unless the user explicitly says to mark it done.

---

## Step 5: Add to Inbox

1. Read `/home/toilacube/dreamer/jarvis/inbox.md`
2. Ask user which section using AskUserQuestion:
   - **To Do** — Actionable items
   - **Ideas** — Concepts to develop
   - **Someday / Not Now** — Deferred items
3. Append to the chosen section with proper checkbox or bullet point
4. Say: "Added to inbox: [brief summary]"

**For actionable items:** Use `- [ ] [item]`
**For ideas/someday:** Use `- [item]`

---

## Step 6: View Today

1. Read today's journal
2. Present the Morning Priorities and Log sections
3. Format cleanly — don't just dump the file, extract and present the relevant sections

---

## Step 7: Mark Complete

1. Read today's journal
2. Show Morning Priorities with numbered list for selection
3. Use AskUserQuestion to identify which task to mark complete
4. Change `- [ ]` to `- [x]` for the selected task
5. **CRITICAL:** Never auto-complete without explicit confirmation
6. Say: "Marked complete: [task text]"

---

## Step 8: View Past Incomplete Tasks

1. Look back up to 7 days from today's journal
2. For each journal file, extract `- [ ]` items from Morning Priorities
3. Present grouped by day with the date
4. Use AskUserQuestion to ask if the user wants to carry any over to today

---

## File Paths

**All paths are absolute and fixed:**

```
/home/toilacube/dreamer/jarvis/journal/YYYY/MM/YYYY-MM-DD.md
/home/toilacube/dreamer/jarvis/inbox.md
/home/toilacube/dreamer/jarvis/templates/daily-journal.md
```

---

## Rules from CLAUDE.md

- **Never auto-complete checkboxes** — Only mark `[x]` when user explicitly confirms
- **"Note" ≠ "Do"** — When user says "note this" or "remember this", capture information but leave checkbox unchecked
- **Distinguish learning from doing** — "Researching X" or "learning about X" goes in Log or Reading/Learning, not as a completed task
- **Ask before marking complete** — If unsure, don't guess
- **Log what happens, not intentions** — Future intentions go in inbox or as unchecked items

---

## Examples

### User: "log: finished the project"
- Get timestamp
- Append: `- 14:32 — Finished the project`
- Say: "Added to log: Finished the project"

### User: "add todo: write proposal"
- First show incomplete from yesterday
- Ask: new or carry over?
- If new: append `- [ ] Write proposal`
- Say: "Added todo: Write proposal"

### User: "capture: idea for new app"
- Ask: To Do, Ideas, or Someday?
- If Ideas selected: append `- Idea for new app: [details]`
- Say: "Added to inbox: Idea for new app"
