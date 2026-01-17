---
applyTo: '**'
---

# ConPort Memory Strategy for PhaseGrid

## Overview

This project uses **ConPort (Context Portal)** as its memory bank - a database-backed MCP server for managing structured project context. ConPort replaces traditional file-based memory banks with a queryable SQLite database.

## Workspace Configuration

- **Workspace ID**: `/Users/cell/dev/PhaseGrid` (auto-detected)
- **Database Location**: `context_portal/context.db`
- **Project Brief**: `projectBrief.md` in root

## Initialization

At the start of each session:

1. Check if `context_portal/context.db` exists
2. If exists: Load context via `get_product_context`, `get_active_context`, `get_decisions` (limit 5), `get_progress` (limit 5), `get_system_patterns` (limit 5)
3. If not exists: Offer to initialize from `projectBrief.md`

## When to Update ConPort

Update ConPort throughout the session when:

- **Decisions are made**: Log via `log_decision` with summary, rationale, and tags
- **Progress changes**: Log via `log_progress` with status (TODO, IN_PROGRESS, DONE)
- **Patterns emerge**: Log via `log_system_pattern` with name and description
- **Custom data needed**: Log via `log_custom_data` with category/key/value

## Key ConPort Tools

### Context Management
- `get_product_context` / `update_product_context` - Project goals, features, architecture
- `get_active_context` / `update_active_context` - Current focus, recent changes, open issues

### Decision Logging
- `log_decision` - Log architectural/implementation decisions
- `get_decisions` - Retrieve past decisions
- `search_decisions_fts` - Full-text search decisions

### Progress Tracking
- `log_progress` - Log task status (description, status, linked_item_type, linked_item_id)
- `get_progress` - Retrieve progress entries
- `update_progress` - Update existing progress

### System Patterns
- `log_system_pattern` - Log coding/architectural patterns
- `get_system_patterns` - Retrieve patterns

### Custom Data
- `log_custom_data` - Store any structured data (category, key, value)
- `get_custom_data` - Retrieve custom data
- `search_custom_data_value_fts` - Search custom data

### Relationships
- `link_conport_items` - Create relationships between items
- `get_linked_items` - Explore the knowledge graph

### Batch and Utility
- `batch_log_items` - Log multiple items of same type at once
- `get_recent_activity_summary` - Catch up on recent changes
- `export_conport_to_markdown` / `import_markdown_to_conport` - Backup/restore

## PhaseGrid-Specific Categories

Use these custom data categories for PhaseGrid:

| Category | Purpose |
|----------|---------|
| `tech-stack` | Technology choices and versions |
| `technical-design` | DSP algorithms, audio quality specs |
| `functional-design` | Module specs, UI layout, features |
| `ProjectGlossary` | Domain terms and definitions |
| `critical_settings` | Important configuration values |
| `ErrorLogs` | Error tracking and debugging |

## Sync Routine

When user says "Sync ConPort" or "ConPort Sync":

1. Review the current chat session
2. Log new decisions, progress, patterns discovered
3. Update active context with current focus
4. Identify and create relationships between items
5. Confirm synchronization complete

## Best Practices

1. **Confirm before logging** - Ask user before storing significant information
2. **Use tags** - Tag decisions and patterns for easier retrieval
3. **Link items** - Connect related decisions, patterns, and progress
4. **Patch updates** - Use `patch_content` for partial context updates
5. **Search first** - Use FTS before asking user for info that may exist

## Migration from Memory Bank

The existing `memory-bank/` files map to ConPort as follows:

| File | ConPort Entity |
|------|----------------|
| `projectBrief.md` | Product Context |
| `activeContext.md` | Active Context |
| `progress.md` | Progress Entries |
| `systemPatterns.md` | System Patterns + Decisions (ADRs) |
| `techContext.md` | Custom Data (tech-stack) |
| `technicalDesignConcept.md` | Custom Data (technical-design) |
| `functionalDesignConcept.md` | Custom Data (functional-design) |
