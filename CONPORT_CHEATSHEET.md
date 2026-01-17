# ConPort Cheatsheet

> Quick reference for using ConPort in PhaseGrid development

## Session Start

```
Workspace ID: /Users/cell/dev/PhaseGrid
```

### Load Context (do this first each session)
| Command | Purpose |
|---------|---------|
| `get_product_context` | Load project vision, goals, architecture |
| `get_active_context` | See current focus, recent changes, open issues |
| `get_decisions` (limit 5) | Recent architectural decisions |
| `get_progress` (limit 5) | Recent task status |
| `get_system_patterns` (limit 5) | Coding patterns in use |

---

## During Development

### When You Make a Decision
```
log_decision
  summary: "What was decided"
  rationale: "Why this approach"
  tags: ["dsp", "architecture", "ui"]
```

### When You Start/Finish a Task
```
log_progress
  description: "Task name"
  status: "TODO" | "IN_PROGRESS" | "DONE"

update_progress
  progress_id: <id>
  status: "DONE"
```

### When You Discover a Pattern
```
log_system_pattern
  name: "Pattern Name"
  description: "How and when to use it"
  tags: ["audio", "control", "ui"]
```

### When You Need Custom Data
```
log_custom_data
  category: "technical-design" | "functional-design" | "tech-stack"
  key: "unique-key"
  value: { any JSON object }
```

---

## Quick Lookups

| Need | Command | Filter Options |
|------|---------|----------------|
| Find a decision | `get_decisions` | `tags_filter_include_any: ["tag"]` |
| Check task status | `get_progress` | `status_filter: "IN_PROGRESS"` |
| Get module spec | `get_custom_data` | `category: "functional-design", key: "module-filter"` |
| Get DSP spec | `get_custom_data` | `category: "technical-design"` |
| Find pattern | `get_system_patterns` | `tags_filter_include_any: ["audio"]` |

---

## PhaseGrid Categories

### Custom Data Categories
| Category | Use For |
|----------|---------|
| `technical-design` | DSP algorithms, audio specs, CPU budgets |
| `functional-design` | Module specs, UI layout, features |
| `tech-stack` | Libraries, frameworks, versions |

### Common Tags
- **DSP**: `dsp`, `audio`, `filter`, `reverb`, `granular`, `spectral`
- **Architecture**: `architecture`, `performance`, `safety`
- **UI**: `ui`, `theme`, `accessibility`
- **Modules**: `gate`, `filter`, `spatial`, `glitch`, etc.

---

## Connecting Items

### Create Relationships
```
link_conport_items
  source_item_type: "decision"
  source_item_id: "3"
  target_item_type: "system_pattern"
  target_item_id: "1"
  relationship_type: "implements"
  description: "ADR implements pattern"
```

### Relationship Types
- `implements` - A implements B
- `uses` - A uses B
- `defines` - A defines B
- `relates_to` - General relationship

---

## Session End

### Update Active Context
```
update_active_context
  patch_content: {
    "current_focus": "What you're working on",
    "recent_changes": ["List of changes made"],
    "next_tasks": ["What's next"],
    "open_issues": ["Any blockers"]
  }
```

### Sync Phrase
Say **"Sync ConPort"** to have the assistant:
1. Review session activity
2. Log new decisions/progress/patterns
3. Update active context
4. Create relevant item links

---

## Batch Operations

### Log Multiple Items at Once
```
batch_log_items
  item_type: "custom_data" | "decision" | "progress_entry"
  items: [
    { category: "...", key: "...", value: {...} },
    { category: "...", key: "...", value: {...} }
  ]
```

---

## Search

| Command | Use Case |
|---------|----------|
| `search_decisions_fts` | Full-text search decisions |
| `search_custom_data_value_fts` | Search custom data values |
| `get_linked_items` | Find related items |
| `get_recent_activity_summary` | Catch up on changes |

---

## Current ConPort Stats

| Entity | Count |
|--------|-------|
| Custom Data | 41 entries |
| Progress | 19 tasks |
| Decisions | 11 ADRs |
| System Patterns | 8 patterns |
| Item Links | 11 relationships |

---

## Quick Examples

**"What's the Filter module spec?"**
```
get_custom_data category="functional-design" key="module-filter"
```

**"What CPU budgets are defined?"**
```
get_custom_data category="technical-design" key="cpu-budgets"
```

**"Show in-progress tasks"**
```
get_progress status_filter="IN_PROGRESS"
```

**"Find decisions about spatial audio"**
```
get_decisions tags_filter_include_any=["spatial", "mach1"]
```
