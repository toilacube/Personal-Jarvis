# Research Report: PKM Systems for Learning & Reading

**Date:** 2026-02-17  
**Sources:** 5 web searches (Reddit, Obsidian Forum, Medium, GitHub, blogs)

---

## Executive Summary

Markdown-based PKM systems can effectively track learning progress, capture notes from books/articles, integrate spaced repetition, and implement Zettelkasten patterns. Key tools: Obsidian, Logseq. Core principle: atomic notes with bidirectional links.

---

## 1. Learning Progress Tracking

### Patterns

| Component | Implementation |
|-----------|----------------|
| **Course tracker** | YAML frontmatter with `status: in-progress | completed | paused` + `progress: 0-100` + `started: YYYY-MM-DD` |
| **Video/article tracker** | Frontmatter: `type: video | article | book`, `source: URL`, `completed: YYYY-MM-DD`, `rating: 1-5` |
| **Dataview queries** | List all `in-progress` items, show completion rate by month |

### Example Note Template

```markdown
---
type: course
title: "Rust for Rustaceans"
source: https://example.com/course
status: in-progress
progress: 45
started: 2026-01-15
tags: [learning, rust]
---

## Progress Log
- [x] Module 1: Ownership
- [ ] Module 2: Borrowing
```

---

## 2. Note-Taking Patterns for Books/Articles

### Three Note Types (Luhmann-inspired)

1. **Fleeting notes** — Raw capture, no structure. Process within 24-48h.
2. **Literature notes** — Summaries with source citation. One note per source.
3. **Permanent/Atomic notes** — Single idea, own words, linked to other notes.

### Literature Note Template

```markdown
---
type: literature
title: "Atomic Habits"
author: James Clear
year: 2018
source: book
rating: 5
---

## Core Ideas
- 1% better every day
- Habit loops: cue → routine → reward

## My Takeaways
- Applied to: [[daily-routine-improvement]]

## Quotes
> "You do not rise to the level of your goals. You fall to the level of your systems."
```

### Key Rules
- Always cite source + page number
- Write in your own words (no copy-paste)
- Link to existing atomic notes, not create new ones unless original idea

---

## 3. Spaced Repetition Integration

### Options

| Approach | Tool | Markdown Support |
|----------|------|------------------|
| **Export to Anki** | Obsidian_to_Anki plugin | ✓ Cloze deletions |
| **Sync** | Yanki Obsidian | ✓ Pure markdown |
| **Native** | Obsidian Spaced Repetition plugin | ✓ Review queue |

### Simple Flashcard Format (Markdown-compatible)

```markdown
---
type: flashcard
deck: programming
tags: [sr, rust]
---

Q: What is the ownership rule in Rust?
A: Each value has exactly one owner. When owner goes out of scope, value is dropped.

<!-- Cloze style -->
Rust ownership: {{c1::Only one owner}} at a time. When {{c2::owner goes out of scope}}, value is dropped.
```

### Integration Workflow
1. Create flashcard notes in dedicated `/flashcards/` folder
2. Plugin syncs to Anki via AnkiConnect
3. Review in Anki; changes reflect back in Obsidian

### Alternative: Passive Review
- Use Dataview to list notes last modified >30 days ago
- Prompt: "Review this note and add to Anki if valuable"

---

## 4. Zettelkasten / Second Brain Patterns

### Core Principles

| Principle | Description |
|-----------|-------------|
| **Atomicity** | One idea per note |
| **Linking** | Every note links to ≥1 other note |
| **Unique IDs** | Sequential (2026011701) or slug-based |
| **No folders** | Prefer tags + links over hierarchy |

### Note Structure

```
/zettelkasten/
  2026011701-rust-ownership.md
  2026011702-borrowing-basics.md
  2026011703-lifetime-syntax.md
```

### Linking Patterns

```markdown
<!-- Bidirectional -->
Related: [[2026011701-rust-ownership]]

<!-- Outgoing from this note -->
See also: [[memory-management]], [[programming-languages]]

<!-- Incoming: shown via backlinks panel -->
"{{title}}" is referenced by [[other-note]]
```

### PARA Adaptation (Tiago Forte)

| Folder | Content |
|--------|---------|
| **P**rojects | Active work |
| **A**reas | Responsibilities (e.g., "rust-learning") |
| **R**esources | Topics, references |
| **A**rchives | Completed |

### Network Growth Metrics
- Track: "Orphan notes" (no incoming links) — aim for <10%
- Obsidian graph view shows connectivity

---

## 5. Unified System Architecture

```
/learning/
  /inbox/           # Fleeting notes (capture anything)
  /sources/         # Literature notes (books, articles, videos)
  /atomic/          # Permanent notes (Zettelkasten)
  /flashcards/      # Anki-ready cards
  /tracks/          # Progress dashboards (Dataview)
```

### Workflow

```
Book/Article → Source Note → Extract Atomic Ideas → Link to Existing + Flashcards
                                        ↓
                              Spaced Repetition Review
```

---

## 6. Tools & Plugins

| Function | Tool |
|----------|------|
| Markdown editor | Obsidian, Logseq, Neovim |
| Spaced repetition | Obsidian_to_Anki, Yanki, Spaced Repetition plugin |
| Query/dashboard | Dataview (Obsidian), DataScript (Logseq) |
| Sync | Git (any markdown editor) |

---

## 7. Anti-Patterns to Avoid

- ❌ Copy-pasting without rephrasing
- ❌ Creating notes without links
- ❌ Over-tagging (more than 5 tags/note)
- ❌ Folder depth >2 levels
- ❌ Abandoning system for complexity

---

## Unresolved Questions

1. How to handle video course notes differently from book notes? (Timestamp references vs page numbers)
2. What's optimal atomic note length? (150-300 words suggested, but varies)
3. Should flashcards live in same vault or separate? (Same preferred for context)

---

## References

- [Obsidian Spaced Repetition Plugins (Reddit)](https://reddit.com/r/ObsidianMD/comments/1kc84rx)
- [Zettelkasten Method Guide (Atlas Workspace)](https://atlasworkspace.ai/blog/zettelkasten-method-guide)
- [The Learning Journey (GitHub)](https://github.com/the-taggart-institute/the-learning-journey)
- [Yanki Obsidian Plugin](https://github.com/kitschpatrol/yanki-obsidian)
- [Obsidian for PKM (Isaac Wyatt)](https://www.isaacwyatt.com/using-obsidian-for-pkm)
