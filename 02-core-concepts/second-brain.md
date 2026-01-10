# Second Brain (Quack Brain)

Second Brain, powered by **Quack Brain**, is a Tana/Logseq-inspired knowledge management system built directly into Quack. It provides an outliner interface for organizing your thoughts, patterns, decisions, and learnings in a way that both you and AI can access.

## What is Second Brain?

Second Brain turns your knowledge into a **living graph** where every bullet point is an entity that can:
- Connect to other entities via `@mentions` and `[[WikiLinks]]`
- Be categorized with `#supertags`
- Store multiple observations (details)
- Be searched and filtered with natural language
- Be used by AI agents for context
- Sync bidirectionally with your Obsidian vault
- Be visualized in canvas diagrams

Think of it as your personal wiki that Claude can read and write to, synchronized with Obsidian for cross-device access and rich editing.

## Opening Second Brain

1. Click the **brain icon** in the header action bar
2. A new tab opens with the Second Brain outliner
3. You can have multiple Second Brain tabs open (each zoomed to different nodes)

## Understanding the Interface

```
+-------------------------------------------------------+
|  Home > Parent Node > Current Node                     |
+-------------------------------------------------------+
|  SUPERTAGS        |  MAIN OUTLINER                     |
|  #fact (12)       |                                    |
|  #pattern (8)     |  * Current Node Title  #pattern   |
|  #decision (5)    |                                    |
|  #project (3)     |  DETAILS (3)                       |
|                   |  - First observation               |
|  RECENT           |  - Second observation              |
|  * Latest item    |  - Third observation               |
|  * Another item   |  + [Add new detail...]             |
|                   |                                    |
|                   |  CHILDREN                          |
|                   |  * Child node 1                    |
|                   |  * Child node 2                    |
+-------------------------------------------------------+
```

### Main Components

| Component | Description |
|-----------|-------------|
| **Breadcrumbs** | Shows your navigation path (click to go back) |
| **Outliner** | The main bullet list where you create and edit |
| **Sidebar** | Filter by supertags and see recent items |
| **Details Section** | Shows observations when zoomed into a node |

## Creating Content

### At the Home Level

When you're at the home (root) level, typing creates **new entities**:

```
Type: My new thought #fact
Result: Creates entity "My new thought" with type "fact"
```

### Inside a Node (Zoomed)

When zoomed into a node, typing adds **observations** (details) to that entity:

```
Zoomed into: "React Patterns"
Type: Use custom hooks for reusable logic
Result: Adds observation to "React Patterns" entity
```

To create a NEW entity while zoomed, use a `#tag`:

```
Type: #pattern State management with Zustand
Result: Creates NEW entity "State management with Zustand" with type "pattern"
```

## Using Supertags

Supertags define the **type** of an entity. Each type determines where it's stored in your Obsidian vault and has a unique color:

:::callout[warning]
**One Tag Per Entity**: Each entity must have exactly ONE supertag. This determines its folder location in Obsidian. Choose the most specific tag that fits (e.g., prefer `#component` over `#note`).
:::

### Code & Documentation

| Supertag | Folder | Use For |
|----------|--------|---------|
| `#component` | `components/` | UI components, React/Vue elements |
| `#function` | `functions/` | Functions, methods, utilities |
| `#api` | `api/` | API endpoints, MCP tools, integrations |

### Patterns & Learning

| Supertag | Folder | Use For |
|----------|--------|---------|
| `#pattern` | `patterns/` | Code patterns, best practices, architectural patterns |
| `#bug` | `bugs/` | Bug fixes and solutions |
| `#decision` | `decisions/` | Architectural Decision Records (ADRs) |
| `#gotcha` | `patterns/` | Common pitfalls and how to avoid them |

### Work & Planning

| Supertag | Folder | Use For |
|----------|--------|---------|
| `#task` | `tasks/` | Completed tasks |
| `#todo` | `todos/` | Work in progress |
| `#idea` | `ideas/` | Ideas to explore |
| `#event` | Root | Events that happened |

### Organization

| Supertag | Folder | Use For |
|----------|--------|---------|
| `#project` | `projects/{name}/` | Projects you're working on |
| `#config` | `config/` | Configuration notes and setup guides |
| `#note` | `notes/` | Generic notes |
| `#glossary` | Root | Human→Technical term mappings |

### People & Context

| Supertag | Folder | Use For |
|----------|--------|---------|
| `#human` | `global/humans/` | People and contacts (always global) |
| `#preference` | Root | Your preferences and opinions |
| `#fact` | Root | General facts and information |
| `#diary` | `diary/` | Daily logs (always global) |

### Technology

| Supertag | Folder | Use For |
|----------|--------|---------|
| `#technology` | Root | Technologies, tools, and frameworks |
| `#tool` | Root | Tools and their configurations |
| `#document` | Root | Documentation references |

**Note**: `#human` and `#diary` are always placed in global folders, regardless of project scope. All other types respect project scoping.

## Creating Relations with @mentions

Use `@` to link entities together:

```
Alek prefers dark mode @Alek
```

This creates:
- Entity: "Alek prefers dark mode"
- Relation: Links to "Alek" entity

### Autocomplete

When you type `@`, an autocomplete dropdown appears:
- Shows existing entities that match
- Press `Tab` or `Enter` to select
- Press `Escape` to close

The same works for `#` tags.

## Navigating the Outliner

### Zooming In

Click the **bullet point** (colored circle) to zoom into a node:
- The node becomes the page title
- You see its observations (details)
- You can add more details or child nodes

### Zooming Out

Use the **breadcrumbs** at the top:
- Click "Home" to go to the root
- Click any parent to go to that level

### Expanding/Collapsing

If a node has children:
- Click the **arrow** to expand/collapse
- Children appear indented below

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Enter` | Create new bullet / Save edit |
| `Backspace` (empty) | Delete current bullet |
| `Shift+Enter` | New line within bullet |
| `Arrow Up/Down` | Navigate between bullets |
| `Tab` (in autocomplete) | Select suggestion |
| `Escape` | Close autocomplete / Cancel edit |

## The Sidebar

### Supertags Section

Shows all entity types with counts:
- Click a tag to **filter** the list
- Numbers show how many entities of each type

### Recent Section

Shows recently modified entities:
- Click to jump directly to that entity
- Helps you find recent work quickly

### Scope Filter

Filter by visibility:
- **All**: Show everything
- **Global**: Memories visible everywhere
- **Project**: Memories specific to current project

## Integration with Knowledge Graph

Second Brain and the Knowledge Graph are **two views of the same data**:

| Aspect | Second Brain | Knowledge Graph |
|--------|--------------|-----------------|
| View | Hierarchical outliner | Force-directed graph |
| Editing | Full create/edit/delete | View only |
| Focus | One node at a time | All nodes visible |
| Relations | Via @mentions | Visual lines |

**Click a node** in the Knowledge Graph to open it in Second Brain.

## How AI Uses Second Brain

Claude agents can **read and write** to your Second Brain through the Brain MCP server, which provides powerful tools for knowledge management.

:::callout[info]
**Automatic Context**: When you work in Quack, Claude automatically searches your Brain for relevant patterns, past decisions, and solutions during the analysis phase. You don't need to explicitly tell Claude to check your Brain - it's built into the workflow.
:::

### Available MCP Tools

| Tool | Purpose |
|------|---------|
| `search` | Full-text search across entities and observations |
| `smart_search` | Natural language semantic search |
| `create_entity` | Create new entities with observations |
| `add_observation` | Add observations to existing entities |
| `get_graph` | Retrieve the entire knowledge graph |
| `create_relation` | Create relations between entities |
| `list_entities` | List entities with optional filters |
| `get_backlinks` | Get entities that link TO a given entity |
| `get_wikilinks` | Get all WikiLinks FROM a given entity |
| `read_canvas` | Read canvas diagrams |
| `create_canvas` | Create new canvas diagrams |
| `update_canvas` | Update existing canvas diagrams |

### Reading (AI to Brain)

Agents search for relevant context before answering:
- **Before starting work**: Search for patterns, past decisions, and gotchas
- **During debugging**: Find similar bugs that were fixed before
- **When making decisions**: Review past architectural choices
- **For context**: Understand project-specific conventions

Example: When you ask about authentication, Claude searches for `#pattern` and `#decision` entities related to auth.

### Writing (AI to Brain)

Agents save discoveries automatically:
- **Bug fixes**: Document tricky solutions for future reference
- **Patterns**: Record effective code patterns as they emerge
- **Decisions**: Log architectural choices with rationale
- **Gotchas**: Save lessons learned from mistakes
- **Canvas diagrams**: Visualize complex systems

Example: After fixing a complex bug, Claude creates a `#bug` entity with observations about the root cause and solution.

### Automatic Context

When you work in Quack, Claude automatically:
1. **Searches** your Brain for relevant context during the analysis phase
2. **Saves** important discoveries after completing tasks
3. **Links** new entities to your current project
4. **Updates** existing entities with new observations

You'll see AI-created entities appear in your Second Brain with their appropriate supertag and project scope.

## Best Practices

### Organize by Topic

Use supertags consistently for better organization:
- `#pattern` for code patterns and best practices
- `#decision` for architectural choices (ADRs)
- `#bug` for bug fixes and solutions
- `#gotcha` for common pitfalls
- `#component` for UI component documentation
- `#api` for API endpoints and integrations

### Add Context to Observations

When zoomed into a node, add multiple observations with timestamps:

```
React Custom Hooks  #pattern
  DETAILS:
  - [2026-01-08] Use for reusable stateful logic
  - Prefix with "use" (e.g., useAuth, useUser)
  - Keep hooks focused on single purpose
  - Can call other hooks
  - [2026-01-09] Prefer custom hooks over HOCs
```

Timestamps help you track when observations were added and see evolution over time.

### Link Related Items

Use `[[WikiLinks]]` and `@mentions` liberally:
- `[[project-name]]` to scope memories to projects
- `[[person-name]]` for attribution
- `[[technology-name]]` to connect related tech
- `[[pattern-name]]` to reference other patterns

Example:
```markdown
This component uses [[React Query]] for data fetching.
Based on the pattern described in [[API Client Design]].
Implemented by [[Alek]] for [[quack-app]].
```

### Use Canvas for Complex Concepts

When explaining complex systems or flows:
1. Ask Claude to create a canvas diagram
2. Review and refine the diagram in Obsidian
3. Link the canvas in related notes: `![[diagram-name.canvas]]`

Canvas diagrams help visualize:
- Architecture overviews
- Authentication flows
- Component hierarchies
- Bug investigation trails

### Leverage Obsidian Sync

Take advantage of bidirectional sync:
- **Quick capture in Quack**: Fast inline editing, AI assistance
- **Deep editing in Obsidian**: Rich formatting, plugins, mobile sync
- **Graph View**: Visualize connections between notes
- **Templates**: Use Obsidian templates for consistent note structure

### Regular Review

- Check the "Recent" section to review new AI-created entries
- Clean up duplicates or outdated information
- Add observations to existing entities instead of creating duplicates
- Review your diary entries weekly to track progress
- Use Obsidian's search and filters to find stale notes

### Tag Hierarchy

Follow this hierarchy for better organization:
1. **Use specific tags**: Prefer `#component` over `#note`
2. **Project scope**: Use `[[project-name]]` WikiLink in project notes
3. **Temporal context**: Add date prefixes to observations `[YYYY-MM-DD]`
4. **Link related concepts**: Connect patterns, bugs, and decisions with WikiLinks

## Project-Scoped Memories

Memories can be **global** (visible everywhere) or **project-scoped** (visible only in a specific project).

### How It Works

1. **Global memories**: Facts about you, general preferences
2. **Project memories**: Patterns, decisions specific to one project

The sidebar shows a scope selector dropdown to filter views.

### Automatic Scoping

When working in a project, new memories are automatically scoped to that project using the `belongs_to_project` relation.

## Obsidian Sync

Quack Brain can sync bidirectionally with your Obsidian vault, giving you the best of both worlds: a fast, AI-integrated interface in Quack and a rich markdown editor in Obsidian.

:::callout[info]
**Sync Architecture**: Quack Brain uses SQLite as the primary storage for fast queries and AI operations. Obsidian sync is optional and designed for human editing, mobile access, and cross-device workflows.
:::

### How It Works

- **Primary Storage**: SQLite database in `~/.quack/brain/brain.db` (fast queries, relations, embeddings)
- **Vault Sync**: Markdown files in your Obsidian vault at `QuackBrain/` folder
- **Bidirectional**: Changes in either place sync to the other
- **Automatic**: Sync happens when you create/edit entities (if auto-sync is enabled)

### Vault Folder Structure

```
YourVault/QuackBrain/
├── diary/                    # Daily notes (#diary)
│   └── 2026-01-08.md
├── global/                   # Notes without project scope
│   ├── patterns/
│   ├── humans/
│   ├── ideas/
│   └── glossary.md
└── projects/                 # Project-scoped notes
    └── quack-app/
        ├── components/
        ├── functions/
        ├── api/
        ├── patterns/
        ├── bugs/
        ├── decisions/
        ├── tasks/
        └── glossary.md
```

### Enabling Obsidian Sync

1. Open **Settings** in Quack
2. Navigate to **Brain** section
3. Configure:
   - **Enable Sync**: Toggle on
   - **Vault Path**: Select your Obsidian vault folder
   - **Auto Sync**: Enable automatic sync on create/edit
   - **Conflict Resolution**: Choose policy (brain_wins, obsidian_wins, or ask)

### Markdown Format

Each entity becomes a markdown file with YAML frontmatter:

```markdown
---
id: uuid-here
name: React Error Boundaries
entityType: pattern
projectId: quack-app
createdAt: 2026-01-08T10:00:00Z
updatedAt: 2026-01-08T15:30:00Z
diary: "[[2026-01-08]]"
---

#pattern

[[quack-app]]

## Observations

- Wrap providers individually with ErrorBoundary for graceful degradation
- [2026-01-08] Added global unhandledrejection handler for Promise errors
- Test error boundaries in development mode
```

### WikiLinks and Graph View

Use `[[NoteName]]` syntax to create links between notes:

```markdown
This pattern is used in [[Authentication Flow]] and [[User Dashboard]].
See also [[React Best Practices]].
```

These links:
- Work in both Quack and Obsidian
- Appear in Obsidian's Graph View
- Can be queried via backlinks

### Daily Diary Integration

Every note automatically links to its creation day via `[[YYYY-MM-DD]]` in frontmatter. Temporal events (bugs, tasks, decisions) are also appended to the diary entry:

:::callout[info]
**Smart Diary Filtering**: Only temporal events (bugs, tasks, decisions, gotchas, events) appear in diary entries. Structural documentation (patterns, components, ideas) is excluded to keep your diary focused on "what happened today."
:::

**Diary Entry (2026-01-08.md):**
```markdown
# 2026-01-08

## Bug Fixes
- **Fixed dropdown positioning** - Dropdown was cut off in modal dialogs

## Tasks Completed
- **Implement Obsidian sync** - Bidirectional sync between Brain and vault

## Decisions Made
- **Use SQLite as primary storage** - Faster queries and better relations
```

**Temporal entities added to diary:**
- `#bug` / `#bug_fix`
- `#task`
- `#decision`
- `#todo` (when completed)
- `#gotcha`
- `#event`

**Structural entities NOT in diary:**
- `#pattern`, `#component`, `#function`, `#api`
- `#idea`, `#config`, `#note`
- `#human`, `#preference`, `#fact`

This keeps your diary focused on "what happened today" rather than documentation.

## Canvas Diagrams

Create visual diagrams, mind maps, and flowcharts using Obsidian Canvas format.

### What Are Canvas Diagrams?

Canvas files (`.canvas`) let you:
- Create text cards with markdown content
- Embed vault files (notes, images, other canvases)
- Add external resources (GIFs, URLs, images)
- Connect nodes with arrows and lines
- Use colors to categorize nodes

### Where Are Canvases Stored?

Canvas files are always stored in the project folder:
- `QuackBrain/projects/{project-name}/*.canvas`

### Creating a Canvas via AI

Ask Claude to create diagrams for you:

```
Create a canvas diagram showing the authentication flow in quack-app
```

Claude will use the `create_canvas` tool to generate a visual diagram with nodes and connections.

### Canvas Colors

Use colors to categorize nodes:

| Color | Use For |
|-------|---------|
| Red | Important, warnings, blockers |
| Orange | Needs attention, questions |
| Yellow | Ideas, notes |
| Green | Done, approved, success |
| Cyan | Info, reference |
| Purple | Special, creative |

### Node Types

- **Text**: Markdown text cards (titles, descriptions, notes)
- **File**: Embedded vault files (notes, images, other canvases)
- **Link**: External URLs (GIFs from Giphy, web images, documentation)

### Example Use Cases

- **Architecture diagrams**: Visualize system components and connections
- **Feature planning**: Map out user flows and requirements
- **Bug investigation**: Connect related issues and solutions
- **Learning maps**: Organize concepts and their relationships

### Canvas-in-Canvas

You can embed canvas files inside other canvases, creating nested diagrams for complex systems.

## Natural Language Search

Quack Brain includes a smart search feature that understands natural language queries.

### Using Smart Search

In the search bar, type questions or descriptions instead of exact keywords:

```
Show me all React patterns we use
What bug fixes were done last week?
Find decisions about authentication
```

### How It Works

Smart search uses:
- **Full-text search** across entity names and observations
- **Semantic understanding** to match intent
- **Project context** to prioritize relevant results
- **Entity type filtering** based on your query

### Search Tips

- Use natural language: "Show me..." or "Find all..."
- Mention entity types: "patterns", "bugs", "decisions"
- Include time references: "last week", "recent", "today"
- Add project names for scoped searches

---

**Previous**: [Kanban Board](./kanban-board)

**Next**: [Background Tasks](./background-tasks)
