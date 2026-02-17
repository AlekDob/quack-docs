# Brain Migration

If you've been using Quack for a while, you might have knowledge scattered across different locations — the old `~/.quack/brain/` folder, loose markdown files in your project root, or docs in `.claude/docs/`. The **Brain Migrate** skill consolidates everything into the new Brain v2 structure automatically.

## Do I Need to Migrate?

You need to migrate if **any** of these are true:

- You have files in `{project}/.quack/brain/` (the old per-project brain)
- You have documentation in `{project}/.claude/docs/`
- You have loose `.md` files in your project root that contain project knowledge
- You have a `docs/` folder with unstructured documentation
- You **don't** have a `{project}/documentation/` folder yet

You **don't** need to migrate if:
- Your project already has a `documentation/` folder with `bugs/`, `patterns/`, `decisions/`, etc.
- You're starting a new project from scratch (Brain v2 is the default for new projects)

## What the Migration Does

The Brain Migrate skill performs a **6-step process**, asking for your approval before making any changes:

### Step 1: Scan

The skill searches these locations for existing documentation:

| Location | What it finds |
|----------|--------------|
| `{project}/documentation/` | Already migrated content (skipped) |
| `{project}/.quack/brain/` | Old project brain files |
| `{project}/.claude/docs/` | Claude-specific documentation |
| `~/.quack/brain/projects/{name}/` | Global brain mirror |
| `{project}/*.md` (root) | Loose markdown files |
| `{project}/docs/` | Generic docs folder |

It reports what was found with file counts per location.

### Step 2: Classify

Each file is categorized by:

- **Type**: bug fix, pattern, decision, gotcha, diary, guide, or skip
- **Audience**: AI (structured, with frontmatter) or Human (narrative, tutorial-style)
- **Action**: move, copy, merge, skip, or delete

The classification uses smart rules — files named `fix-*` go to `bugs/`, files in `patterns/` stay as patterns, narrative docs become human guides, and `.mmd` files are preserved as Mermaid diagrams.

### Step 3: Plan

Before touching any files, the skill shows you a **complete migration plan**:

```
Migration Plan for my-project
==================================

Sources found:
- .quack/brain/: 86 files
- .claude/docs/: 31 files
- Root: 3 files

Actions:
- Move to documentation/patterns/: 15 files
- Move to documentation/bugs/: 12 files
- Move to documentation/gotchas/: 7 files
- Move to documentation/decisions/: 8 files
- Move to documentation/diary/: 20 files
- Convert to documentation/guide/: 5 files
- Move to inbox/ (needs review): 10 files
- Skip (global/wrong scope): 6 files
- Delete (empty/duplicate): 3 files
```

**Nothing happens until you approve.** You can ask to change the plan before proceeding.

### Step 4: Execute

After approval, the skill:

1. Creates the `documentation/` folder structure
2. Moves files according to the plan (using `git mv` when possible to preserve history)
3. Fixes file naming to kebab-case
4. Adds missing YAML frontmatter to AI knowledge files
5. Converts narrative docs to guide format
6. Creates an architecture `map.md`

### Step 5: Update CLAUDE.md

The skill updates your project's `CLAUDE.md` to reference the new documentation structure:

- Adds a **Knowledge Base** section with links to critical gotchas and patterns
- Lists all human guide features
- Removes old references to `.quack/brain/` or `.claude/docs/`
- Adds the Brain breadcrumbs convention reference

It only touches the Knowledge Base section — agent headers, group context, and other sections are preserved.

### Step 6: Verify

Finally, the skill verifies the result:
- Lists the `documentation/` tree
- Confirms `map.md` exists and is populated
- Counts files per category
- Reports any orphaned files

## How to Run the Migration

### Option A: Using the Skill Directly

In any Quack chat session, just ask:

> "Migrate my project documentation to Brain v2 format"

or

> "Run the brain-migrate skill on this project"

The AI will use the Brain Migrate skill automatically.

### Option B: Installing from the Marketplace

If you don't have the skill installed:

1. Open Quack **Marketplace** (from the sidebar or settings)
2. Search for **"brain-migrate"**
3. Click **Install**
4. Start a new chat and ask to migrate

## What About My Global Brain?

The migration only touches **project-level** documentation. Your global brain at `~/.quack/brain/` is left untouched — it's managed separately and contains cross-project knowledge that doesn't belong in any single repo.

## After Migration: Cleanup

After verifying the migration was successful, the skill will suggest cleaning up old source locations:

| Old location | Recommendation |
|-------------|----------------|
| `.quack/brain/` | Can be deleted after verification |
| `.claude/docs/` | Can be deleted after verification |
| `~/.quack/brain/projects/{name}/` | Leave as-is (global brain, managed separately) |

**The skill never auto-deletes** — it always asks first.

## Converting Existing Diagrams

If your project has architecture diagrams in any format (ASCII art, draw.io, PlantUML), the migration can convert them to **Mermaid diagrams** (`.mmd` files) that render interactively in the Brain UI.

Mermaid diagrams are placed in `documentation/guide/{feature}/` alongside the human guide pages, making them part of the feature documentation.

## FAQ

**Q: Will the migration break my git history?**
A: No. The skill uses `git mv` when possible to preserve file history. The files are moved, not copied-and-deleted.

**Q: What if I have files in multiple old locations?**
A: The skill scans all locations and merges everything into one unified structure. Duplicates are detected and handled.

**Q: Can I run the migration multiple times?**
A: Yes. The skill detects already-migrated content and skips it. You can safely run it again after adding new files.

**Q: What if a file doesn't fit any category?**
A: It goes to `documentation/inbox/` — a safety net for files that need manual review. You can reclassify them later.

**Q: Do I need to migrate before using the Brain UI?**
A: The Brain UI works with both old and new structures. But migrating gives you the best experience — proper categorization, audience badges, and guide rendering.

---

**Next**: [Brain Store Setup](./brain-store-setup) — Install the Brain plugins from the Quack Store

**Previous**: [Brain Timeline](./brain-timeline) — Activity feed with search and multi-user tracking
