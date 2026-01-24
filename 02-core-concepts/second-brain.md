# Second Brain

Quack's Second Brain is a file-based knowledge store that helps AI assistants remember patterns, bug fixes, and decisions. It uses simple markdown files in `~/.quack/brain/` - no database, no complexity.

## Overview

Your AI assistants automatically learn from conversations and save knowledge for future reference. After each significant task, Claude evaluates what was learned and decides if it's worth saving.

## Architecture: Three Pillars

The Second Brain works through three core components:

### 1. Storage - Plain Markdown Files

Knowledge is stored as markdown files with YAML frontmatter. No database means:
- Zero corruption risk
- Git-friendly versioning
- Works with any markdown editor
- Easy backup and sync

### 2. AI Access - Smart File Operations

Claude accesses your brain using standard file tools (Grep, Read, Write). A rule called `use-quack-brain.md` is always in context, teaching Claude:
- When to search the brain (before answering questions, investigating bugs)
- When to save to the brain (bug fixes, patterns, decisions)
- How to name files descriptively
- Search priority: map.md → project files → inbox → global

### 3. Auto-learn - Claudeception Evaluation

After completing significant tasks, Claude self-evaluates with four questions:

1. Was this a genuine discovery? (not a docs lookup)
2. Would it help someone in 6 months hitting the same problem?
3. Is the solution verified to work?
4. Does it have clear trigger conditions?

If ALL four are true, Claude saves it. If any is false, it doesn't. This works in any language - no regex needed.

## Directory Structure

```
~/.quack/brain/
├── global/
│   ├── patterns/     # Cross-project patterns
│   ├── preferences/  # User preferences
│   ├── people/       # People & contacts
│   └── tools/        # Tool configurations
└── projects/
    └── {project-name}/
        ├── map.md        # Architecture glossary (Component | Path | Purpose)
        ├── inbox/        # Quick ideas from mobile (Obsidian Sync)
        ├── patterns/     # Project-specific patterns
        ├── bugs/         # Bug fixes
        ├── decisions/    # Architecture decisions
        ├── gotchas/      # Pitfalls to avoid
        └── diary/        # Daily logs (YYYY-MM-DD.md)
```

## Knowledge Types

| Type | Folder | When Saved |
|------|--------|------------|
| `pattern` | patterns/ | Reusable code patterns and techniques |
| `bug_fix` | bugs/ | Non-trivial bug solutions |
| `decision` | decisions/ | Architecture and design choices |
| `gotcha` | gotchas/ | Pitfalls and caveats to remember |
| `preference` | preferences/ | User preferences and settings |
| `person` | people/ | People and contacts |
| `tool` | tools/ | Tool configurations |
| `diary` | diary/ | Daily logs (YYYY-MM-DD.md) |
| `inbox` | inbox/ | Quick captures from mobile (ephemeral) |

## Special Folders

### map.md - Architecture Glossary

Each project can have a `map.md` file - a single-page navigation guide that helps AI assistants quickly understand where components live.

**Purpose:**
- Fast orientation in the codebase
- Reduces need for grep searches
- Always read FIRST before exploring code

**Format:**
```markdown
---
type: map
project: quack-app
updated: 2025-01-24
---

# Architecture Map - Quack

## Core Components

| Component | Path | Purpose |
|-----------|------|---------|
| Agent Management | `src/services/unifiedAgentStorage.ts` | CRUD for agents |
| Chat Session | `src/hooks/useClaudeChat.ts` | Claude SDK integration |
| Kanban Board | `src/components/kanban/` | Task management UI |
| Second Brain | `src/services/brainFileService.ts` | File-based knowledge |

## State Management

| Store | File | Manages |
|-------|------|---------|
| Session Store | `src/stores/sessionStore.ts` | Active agents & tabs |
| Kanban Store | `src/stores/kanbanStore.ts` | Tasks & assignments |
```

**Rules:**
- One `map.md` per project
- Keep it concise and scannable
- Use tables for clarity
- Update when significant components are added/moved

### inbox/ - Mobile-First Capture

The inbox folder is a temporary collection point for quick ideas captured on mobile via Obsidian Sync.

**Use Case:**
You're out and about with just your iPhone. An idea strikes for Quack. Open Obsidian, drop a note in the inbox, and Quack's AI will process it when relevant.

**Workflow:**
1. **Capture** (mobile): Quick note in `inbox/idea-title.md`
2. **Process** (desktop): AI checks inbox when starting work
3. **Action**: Delete or promote to proper folder (bugs/, patterns/, etc.)

**File Format:**
```markdown
---
type: inbox
created: 2025-01-24
---

# Quick idea title

Brief description or todo item...
```

**Rules:**
- Minimal frontmatter: only `type: inbox` and `created`
- No tags needed - inbox is ephemeral
- Process relevant items, then delete or promote
- AI doesn't auto-process all items - only when contextually relevant

:::callout[info]
**Why inbox?** Inspired by GTD methodology. Your brain shouldn't hold ideas - capture them fast, process them later when you have context.
:::

## File Format

Each brain entry is a markdown file with YAML frontmatter:

```markdown
---
type: pattern
project: my-project
created: 2025-01-23
tags: [react, hooks, performance]
---

# Pattern: Memoize expensive list operations

Use useMemo for filtered/sorted lists to avoid re-computation on every render...
```

### Diary Format (Special Rules)

Diary entries have simpler frontmatter - NO tags allowed:

```markdown
---
type: diary
project: my-project
date: 2025-01-23
---

# Daily Log - Jan 23, 2025

Today I worked on...
```

:::callout[info]
**Why no tags in diary?** Diary is temporal, not categorical. Tags belong only on knowledge files (bugs, patterns, decisions, gotchas).
:::

## File Naming Convention

File names MUST be explicit and self-descriptive. Someone should understand the content from the title alone.

**Good examples:**
- `fix-white-screen-after-standby.md`
- `pattern-error-boundary-per-provider.md`
- `decision-file-based-brain-over-sqlite.md`
- `gotcha-tauri-shell-plugin-limitations.md`

**Bad examples:**
- `bug-fix-1.md` (too vague)
- `pattern-react.md` (not specific enough)
- `note.md` (meaningless)

## Accessing Your Brain

### From Quack

- **Sidebar**: Click the "Brain" button to open in Finder or Obsidian
- **Settings**: Go to Settings > Second Brain to view and change brain location
- **AI**: Claude automatically searches the brain for relevant context when needed

### From External Tools

Since brain files are standard markdown, you can use:

- **Obsidian**: Open `~/.quack/brain/` as a vault subfolder
- **VS Code**: Browse and edit files directly
- **Git**: Version control your knowledge
- **Any markdown editor**: Files are plain text

## Configuration

### Change Brain Location

1. Open Settings > Second Brain
2. Click "Change Brain Location"
3. Select a new directory
4. Brain path is saved to `~/.quack/brain-path` for AI discovery

:::callout[warning]
Changing the brain location doesn't move existing files. You'll need to manually copy files from the old location to the new one.
:::

## How Claude Uses the Brain

### When Searching (Read)

Claude searches the brain during the Analysis phase using a priority order:

**Search Priority Order:**

1. **Read map.md first** - Understand architecture quickly
2. **List project files** - File names are self-descriptive
3. **Check inbox/** - Process relevant pending items
4. **Search globally** - Only if nothing in project folder
5. **Read specific files** - Only when title matches need

**Example workflow:**
```bash
# 1. Orient with map
Read "~/.quack/brain/projects/quack-app/map.md"

# 2. List project files (names tell you what's inside)
Glob "~/.quack/brain/projects/quack-app/**/*.md"

# 3. Check inbox for relevant items
Glob "~/.quack/brain/projects/quack-app/inbox/*.md"

# 4. Only if needed, search globally
Grep pattern="dropdown" path="~/.quack/brain/"

# 5. Read specific files that match
Read file_path="~/.quack/brain/projects/quack-app/bugs/fix-dropdown-z-index.md"
```

This approach minimizes unnecessary grep searches and maximizes contextual understanding.

### When Saving (Write)

Claude saves to the brain after completing tasks:

1. **Evaluates** using the four questions above
2. **Chooses type** (bug, pattern, decision, gotcha)
3. **Names descriptively** following naming conventions
4. **Writes file** with proper frontmatter and content

## Testing the Brain

Try these prompts to see the brain in action:

**Save knowledge:**
> "Save in the brain that I prefer to use Tailwind for styling"

**Search knowledge:**
> "Search the brain for any patterns related to React hooks"

**Check configuration:**
> Go to Settings > Second Brain to verify the path

## What Changed from Old System

The new file-first architecture replaced:

- ❌ SQLite database
- ❌ MCP server (brain-mcp-server.js)
- ❌ In-app outliner/graph views
- ❌ Memory indicator badges
- ❌ Obsidian bidirectional sync
- ❌ FTS5 search
- ❌ Embeddings

With:

- ✅ Plain markdown files
- ✅ Direct file access (Grep/Read/Write)
- ✅ Zero setup required
- ✅ No corruption possible
- ✅ Git-friendly
- ✅ Works with any markdown editor

## Best Practices

### For Users

- Keep brain location in a backed-up folder (Dropbox, iCloud, etc.)
- Use Obsidian for rich viewing and linking experience
- Review diary entries weekly to track progress
- Don't manually edit frontmatter unless you know what you're doing
- **Use inbox/ for mobile captures** - Quick ideas on iPhone sync via Obsidian
- **Keep map.md updated** - Help AI navigate your codebase faster

### For AI Assistants

- **Read map.md FIRST** before grepping the codebase
- Always search project folder first before global search
- **Check inbox/** when starting work - process relevant items only
- Use descriptive file names - no generic names
- Evaluate carefully before saving - quality over quantity
- Write in the same language the user communicates in
- No tags in diary or inbox frontmatter - keep it simple
- Update map.md when significant components are added/moved

---

**Next**: [Background Tasks](./background-tasks) - Run long operations without blocking

**Previous**: [Kanban Board](./kanban-board) - Visual task management
