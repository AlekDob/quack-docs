# Second Brain

Quack's Second Brain stores knowledge as simple markdown files in `~/.quack/brain/`. Your AI assistants automatically learn from conversations and save patterns, bug fixes, and decisions for future reference.

## How It Works

1. **Auto-learn**: After each AI conversation, Quack evaluates the response for knowledge worth saving
2. **AI Skill**: Claude can read and search your brain files for relevant context
3. **Obsidian Compatible**: Brain files are standard markdown - open them in Obsidian or any editor

## What Gets Saved

The system automatically detects and saves:

- **Bug fixes** - Solutions to tricky problems
- **Patterns** - Best practices and techniques discovered
- **Gotchas** - Pitfalls and caveats to remember
- **Decisions** - Architecture and design choices

## Where Files Live

```
~/.quack/brain/
├── global/          # Knowledge that applies everywhere
│   ├── patterns/
│   ├── preferences/
│   └── tools/
└── projects/        # Project-specific knowledge
    └── my-project/
        ├── patterns/
        ├── bugs/
        ├── decisions/
        └── gotchas/
```

## Accessing Your Brain

- **Sidebar**: Click the brain button to open in Finder
- **Settings**: Second Brain section shows the path and quick actions
- **Obsidian**: Files work as a standard Obsidian vault subfolder
- **AI**: Claude automatically searches brain for relevant context

## File Format

Each file uses standard markdown with YAML frontmatter:

```markdown
---
type: pattern
project: my-project
created: 2025-01-15
tags: [react, performance]
---

# Pattern: Virtualize large lists

Use react-window for lists over 100 items to maintain 60fps scrolling...
```
