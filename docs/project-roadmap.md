# Project Roadmap

This document outlines the current state and potential future enhancements for the Life System.

## Current State

### Completed Features

| Feature | Status | Notes |
|---------|--------|-------|
| Life plan template | Done | plan.md with chapters, vision, non-priorities |
| Annual goals | Done | Template with checkboxes, anti-goals, becoming |
| Daily journal | Done | Template with morning/log/evening sections |
| Decision records | Done | Structured format with status tracking |
| Inbox | Done | Quick capture with To Do / Someday / Ideas |
| Values & habits | Done | Mission, principles, daily schedule |
| Morning skill | Done | Claude Code skill for daily routine |
| Journal script | Done | Bash script with backfill + calendar |
| QMD integration | Done | MCP server configured, 3 collections |

### Usage Flow

1. User starts Claude in the project directory
2. Claude loads CLAUDE.md, plan, goals, values, inbox
3. User says "morning" or "let's plan the day"
4. Morning skill runs full routine
5. Throughout the day: logging, capture, decisions
6. Evening: optional reflection

## Short-Term Improvements

### Priority 1: Documentation

- [ ] Fix duplicate install instructions in README.md
- [ ] Add troubleshooting section
- [ ] Document how to customize templates
- [ ] Create quick-start guide

### Priority 2: Template Refinement

- [ ] Improve goal tracking format
- [ ] Add weekly review template
- [ ] Create project-specific sub-journal template

### Priority 3: Script Enhancement

- [ ] Support Linux (date commands differ from macOS)
- [ ] Add dry-run mode
- [ ] Support custom template variables

## Medium-Term Enhancements

### Automation

- [ ] Add weekly review skill
- [ ] Create monthly review skill
- [ ] Add goal progress tracking script

### Organization

- [ ] Decision categorization (folders by type)
- [ ] Project journals (subdirectories in decisions/)
- [ ] Archive system for old years

### Search & Discovery

- [ ] Add decision collection to QMD
- [ ] Document search patterns
- [ ] Create saved queries

## Long-Term Possibilities

### Multi-Device

- [ ] Git sync setup
- [ ] Backup automation
- [ ] Conflict resolution guide

### Analytics

- [ ] Goal completion tracking
- [ ] Habit streak tracking
- [ ] Time allocation analysis

### Extensions

- [ ] Multiple journals (work, personal)
- [ ] Integration with task managers
- [ ] Calendar sync (beyond icalBuddy)

## Not Planned

The following are intentionally out of scope:

- **Cloud sync services**: Keep local-only for privacy
- **Mobile apps**: Terminal + editor is the interface
- **Database**: Files are the database
- **Web interface**: Plain text is the interface
- **AI-generated goals**: Human decides, AI helps execute

## Contributing

This is a personal system, but ideas are welcome:

1. Fork the repo
2. Make changes
3. Test the morning skill
4. Share what works

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 1.0 | Feb 2026 | Initial release with all core features |
