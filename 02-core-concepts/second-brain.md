# Second Brain

Second Brain is a Tana/Logseq-inspired knowledge management system built directly into Quack. It provides an outliner interface for organizing your thoughts, patterns, decisions, and learnings in a way that both you and AI can access.

## What is Second Brain?

Second Brain turns your knowledge into a **living graph** where every bullet point is an entity that can:
- Connect to other entities via `@mentions`
- Be categorized with `#supertags`
- Store multiple observations (details)
- Be searched and filtered
- Be used by AI agents for context

Think of it as your personal wiki that Claude can read and write to.

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

Supertags define the **type** of an entity. Each type has a unique color:

| Supertag | Color | Use For |
|----------|-------|---------|
| `#fact` | Green | General facts and information |
| `#preference` | Blue | Your preferences and opinions |
| `#pattern` | Orange | Code patterns and best practices |
| `#decision` | Purple | Architectural or technical decisions |
| `#project` | Rose | Projects you're working on |
| `#person` | Rose | People you interact with |
| `#technology` | Cyan | Technologies and tools |
| `#mistake` | Red | Lessons learned from mistakes |
| `#context` | Gray | General context |

### Custom Tags

Any tag not in the list becomes a **custom type**:

```
#meeting - Creates a custom "meeting" type
#idea - Creates a custom "idea" type
```

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

Claude agents can **read and write** to your Second Brain:

### Reading
- Agents search for relevant patterns before answering
- Context from your memories improves responses
- Previous solutions help solve similar problems

### Writing
- Agents can save bug fixes they discover
- New patterns get documented automatically
- Decisions are recorded for future reference

You'll see AI-created entities appear in your Second Brain with their supertag.

## Best Practices

### Organize by Topic

Use supertags consistently:
- `#pattern` for code patterns
- `#decision` for architectural choices
- `#mistake` for lessons learned

### Add Context to Observations

When zoomed into a node, add multiple observations:

```
React Custom Hooks  #pattern
  DETAILS:
  - Use for reusable stateful logic
  - Prefix with "use" (e.g., useAuth)
  - Keep hooks focused on single purpose
  - Can call other hooks
```

### Link Related Items

Use `@mentions` liberally:
- `@project-name` to scope memories to projects
- `@person-name` for attribution
- `@technology` to connect related tech

### Regular Review

- Check the "Recent" section to review new entries
- Clean up duplicates or outdated information
- Add observations to existing entities instead of creating duplicates

## Project-Scoped Memories

Memories can be **global** (visible everywhere) or **project-scoped** (visible only in a specific project).

### How It Works

1. **Global memories**: Facts about you, general preferences
2. **Project memories**: Patterns, decisions specific to one project

The sidebar shows a scope selector dropdown to filter views.

### Automatic Scoping

When working in a project, new memories are automatically scoped to that project using the `belongs_to_project` relation.

---

**Previous**: [Kanban Board](./kanban-board)

**Next**: [Background Tasks](./background-tasks)
