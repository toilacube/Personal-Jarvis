# Research Report: Markdown-Based Reading Log & Library Journal Systems

**Date:** 2026-02-17

## Executive Summary

Obsidian with Dataview is the dominant approach for markdown-based book tracking. The pattern of "one book, one file" with YAML frontmatter provides the most flexibility. Key community consensus: use a `shelf` or `status` property for reading state, tags for genre/category, and Dataview queries to generate dynamic views.

---

## 1. Templates for Tracking Books

### Standard Status Values (Shelves)

Based on multiple sources, the most common status workflow:

| Status | Meaning |
|--------|---------|
| `noted` | Book added to list, not yet read |
| `to-read` | Intend to read |
| `reading` | Currently reading |
| `read` | Finished |

Some users add: `rereading`, `held` (paused), `dnf` (did not finish)

### Book Note Template Structure

```markdown
---
title: 
author: 
status: to-read
rating: 
genre: 
tags: []
date_added: <% tp.date.now("YYYY-MM-DD") %>
date_started: 
date_finished: 
pages: 
publisher: 
isbn: 
series: 
series_num: 
cover_url: 
goodreads_url: 
library: 
kindle: 
---

# Notes

## Key Takeaways


## Quotes


## Connected Notes
```

---

## 2. Data Structure (YAML Frontmatter)

### Minimal Viable Fields

```yaml
---
title: "The Pragmatic Programmer"
author: "David Thomas, Andrew Hunt"
status: read
rating: 5
date_finished: 2024-03-15
genre: Programming
tags: [#software-development, #best-practices]
---
```

### Extended Fields (from community templates)

```yaml
---
# Core
title: 
author: 
status: reading  # noted | to-read | reading | read | rereading | held | dnf
rating: 4       # 1-5 scale
genre:          # broad category
tags: []        # granular topics

# Dates
date_added: 2024-01-01    # auto-populated
date_started: 2024-02-01
date_finished: 2024-03-15

# Book Metadata
pages: 352
publisher: 
pub_year: 2020
isbn: 
series: 
series_num: 

# Locations
library: true/false
kindle: true/false
cover_url: 

# Social
goodreads_url: 
review_url: 
---
```

### Key Design Decision: Status as Field vs Tag

- **Field (recommended):** `status: reading` — queryable, sortable, explicit
- **Tag:** `#shelf/reading` — works but less clean for filtering

Consensus: Use a `shelf` or `status` YAML property for primary state.

---

## 3. Organizing by Category/Genre

### Three-Layer Approach (from Obsidian forum best practices)

| Layer | Use | Example |
|-------|-----|---------|
| **Genre** | Broad categories | `Fiction`, `Non-Fiction`, `Programming` |
| **Tags** | Granular topics | `#philosophy`, `#startup`, `#react` |
| **Folder** | Physical organization | `library/fiction/`, `library/tech/` |

### Recommended Implementation

```yaml
---
genre: Science Fiction
tags: [#space-opera, #dystopian, #award-winner]
---
```

### Query by Genre (Dataview)

```dataview
TABLE author, rating, date_finished
FROM "library"
WHERE genre = "Science Fiction"
SORT date_finished DESC
```

### Query by Tag

```dataview
TABLE author, rating
FROM "library"
WHERE contains(tags, "#philosophy")
```

---

## 4. Integration with Daily Journal

### Pattern 1: Link Books in Daily Notes

In daily journal entries:

```markdown
## Reading

Started reading [[The Pragmatic Programmer]] today.

## Finished

Finished [[Clean Code]] - highly recommend for beginners.
```

### Pattern 2: Reading Progress in Daily Notes

```dataview
TABLE WITHOUT ID
  file.link as "Currently Reading",
  progress as "Progress"
FROM "library"
WHERE status = "reading"
```

### Pattern 3: Weekly/Monthly Reading Log

```dataview
TABLE WITHOUT ID
  file.link as Book,
  author as Author,
  rating as Rating
FROM "library"
WHERE status = "read" AND date_finished >= date(today) - dur(1 month)
SORT date_finished DESC
```

### Pattern 4: Books Started This Year

```dataview
TABLE author, genre, rating
FROM "library"
WHERE date_started >= date("2026-01-01")
SORT date_started DESC
```

### Integration Points

| Daily Journal Section | Content |
|---------------------|---------|
| Morning | Today's reading goal |
| Log | Books started/finished, page counts |
| Evening | Reflection on what was read |

---

## 5. Recommended File Structure

```
/library/
  /books/
    /fiction/
    /non-fiction/
    /technical/
  /templates/
    book-note.md
    book-reading.md
  index.md          # Master library view
  to-read.md        # Query: status = "to-read"
  reading.md        # Query: status = "reading"
  read.md           # Query: status = "read"
```

---

## 6. Sample Dataview Queries

### All Books Table

```dataview
TABLE WITHOUT ID
  file.link as Book,
  author as Author,
  status as Status,
  rating as Rating,
  genre as Genre
FROM "library"
SORT status ASC, author ASC
```

### Currently Reading with Progress

```dataview
TABLE WITHOUT ID
  file.link as Book,
  author as Author,
  pages as "Total Pages",
  date_started as "Started"
FROM "library"
WHERE status = "reading"
SORT date_started ASC
```

### Read This Year, Grouped by Genre

```dataview
TABLE genre, rows.file.link as Books, rows.rating as Ratings
FROM "library"
WHERE status = "read" AND date_finished >= date("2026-01-01")
GROUP BY genre
```

---

## 7. Tools & Plugins Referenced

- **Obsidian** — primary tool
- **Dataview** — query engine for dynamic views
- **Book Search Plugin** — auto-populate book metadata from Google Books API
- **Templater** — advanced template variable insertion

---

## Resources

- [Obsidian Book Templates (joschua.io)](https://joschua.io/posts/2023/04/30/obsidian-book-templates/)
- [Sample Vault - Obsidian Forum](https://forum.obsidian.md/t/sample-vault-for-tracking-your-reading/53684)
- [Tracking Reading with Obsidian Bases (tamarisk.it)](https://tamarisk.it/tracking-reading-in-obsidian)
- [Book Tracking with Dataview (ajy.co)](https://ajy.co/how-i-track-books-and-reading-with-obsidian/)

---

## Unresolved Questions

1. How to handle physical vs Kindle vs library book tracking — separate fields or single `format` field?
2. Should series be a separate metadata note or embedded in each book?
3. Best approach for rereads — new note or versioned fields?
