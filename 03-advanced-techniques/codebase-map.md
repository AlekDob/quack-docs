# Codebase Map

Automatically generate a compact index of your entire TypeScript codebase that AI assistants can read in one shot instead of making dozens of exploratory Read calls.

## Overview

When Claude explores your codebase, it typically needs to Read multiple files just to understand what exports are available. For a 400+ file project, this can mean 20+ Read calls, consuming significant context.

The Codebase Map solves this by generating a single, compact markdown file (~300 lines) that indexes all TypeScript/TSX exports in your project. AI assistants read this map first, then jump directly to the files they need.

**Result:** Faster analysis, reduced token consumption, better context utilization.

## What Gets Indexed

The map scans `.ts` and `.tsx` files and extracts:

- **Exported functions**: `export function createSession()`
- **Exported types**: `export type User = { id: string }`
- **Exported interfaces**: `export interface KanbanTask { ... }`
- **Exported classes**: `export class SessionManager { ... }`
- **Exported enums**: `export enum TaskStatus { ... }`
- **Exported constants**: `export const API_URL = '...'`

## How It Works

### 1. Generation Script

A lightweight Node.js script (`scripts/generate-codebase-map.mjs`) scans your project:

```bash
# Full scan (first time or manual refresh)
node scripts/generate-codebase-map.mjs [projectPath] [outputPath]

# Incremental update (auto-triggered on file save)
node scripts/generate-codebase-map.mjs --update-file <path>
```

**Performance:**
- Full scan: 478 files in ~123ms
- Incremental: Single file in ~2ms
- Zero external dependencies

### 2. Output Format

The map is saved to `.quack/codebase-map.md`:

```markdown
---
type: codebase-map
project: quack-app
generated: 2026-01-31T17:51:35Z
files: 400
exports: 1166
---

# Codebase Map

## src/stores/kanbanStore.ts
- export fn `useKanbanStore()`
- export type `KanbanTask { id, title, status }`
- export type `KanbanColumn { ... }`

## src/services/claudeSDK.ts
- export fn `createSession(agentId: string)`
- export fn `streamMessage(sessionId: string, prompt: string)`
- export fn `stopSession(sessionId: string)`

## src/components/settings/categories/CodebaseMapSettings.tsx
- export fn `CodebaseMapSettings()`
```

### 3. Auto-Update Hook

A PostToolUse hook automatically updates the map when Claude writes TypeScript files:

- Detects Write tool calls to `.ts` or `.tsx` files
- Runs incremental update in background (~2ms)
- Zero impact on workflow

## Using the Map

### Settings UI

Go to **Settings > Codebase Map** to:

- **Toggle auto-generation** on/off
- **Generate Now** - Manually trigger full scan
- **View Map** - Open `.quack/codebase-map.md` in editor
- **See stats** - Files indexed, exports found, last generated

### For AI Assistants

Claude automatically reads the map when exploring your codebase:

**Without map:**
```
1. Read src/stores/ directory
2. Read sessionStore.ts
3. Read kanbanStore.ts
4. Read agentStore.ts
5. Read settingsStore.ts
... 15+ Read calls later ...
```

**With map:**
```
1. Read .quack/codebase-map.md (one call, full overview)
2. Read specific file needed (direct jump)
```

## When to Use

### Perfect For:

- **Large codebases** (100+ TypeScript files)
- **Frequent refactoring** - AI needs to understand structure quickly
- **New AI assistants** - Fast onboarding to project architecture
- **Code reviews** - Quick overview of what's exported where

### Skip If:

- **Small projects** (<50 files) - Overhead outweighs benefit
- **Non-TypeScript projects** - Map only indexes TS/TSX files
- **Static codebases** - If code rarely changes, manual map works fine

## Configuration

### Auto-Generation

By default, auto-generation is **enabled**. The map updates automatically when you save TypeScript files.

**To disable:**
1. Go to Settings > Codebase Map
2. Toggle "Auto-generate on file save" off

### Custom Output Location

The map is always saved to `.quack/codebase-map.md` in your project root. This location is hardcoded to ensure AI assistants know where to find it.

## Technical Details

### File Scanning Strategy

The script uses regex-based extraction (no AST parsing) for maximum speed:

```javascript
// Detects: export function createSession(...)
/export\s+(async\s+)?function\s+(\w+)/g

// Detects: export type User = { ... }
/export\s+type\s+(\w+)/g

// Detects: export interface Session { ... }
/export\s+interface\s+(\w+)/g
```

**Why regex instead of TypeScript AST?**
- **Speed**: 10-100x faster than AST parsing
- **Simplicity**: No TypeScript compiler dependency
- **Good enough**: Captures 95% of exports accurately

### Excluded Patterns

The script ignores:

- `node_modules/` and `.next/` directories
- `.d.ts` declaration files (too noisy)
- Test files (`*.test.ts`, `*.spec.ts`)
- Build output (`dist/`, `build/`)

### Key Files

| File | Purpose |
|------|---------|
| `scripts/generate-codebase-map.mjs` | Generation script (Node.js) |
| `src/services/codebaseMapService.ts` | Service layer (Tauri integration) |
| `src/components/settings/categories/CodebaseMapSettings.tsx` | Settings UI |
| `.quack/codebase-map.md` | Output file (gitignored) |

## Performance Impact

### Storage

- **Map size**: ~10-30 KB for 400-file project
- **Disk writes**: Only on file save (incremental) or manual refresh (full)

### CPU

- **Full scan**: ~100-150ms for 400-500 files
- **Incremental**: ~2ms per file save
- **Negligible** impact on UI responsiveness

### Token Consumption

- **Without map**: ~50-100K tokens for exploratory reads
- **With map**: ~1-2K tokens to read map once
- **Savings**: 95%+ reduction in discovery phase tokens

## Limitations

### What It Doesn't Index

- **JavaScript files** (`.js`, `.jsx`) - TypeScript only
- **Internal functions** - Only exports are indexed
- **Function signatures** - Simplified to `functionName()`
- **Comments/docs** - Not included in map

### Edge Cases

- **Dynamic exports** (`export * from './...'`) - Not followed
- **Conditional exports** - May not be detected accurately
- **Minified code** - Regex may miss obfuscated exports

:::callout[info]
The map is a **discovery aid**, not a complete reference. AI assistants still need to Read actual files for implementation details.
:::

## Best Practices

### For Users

- **Enable auto-generation** if you work on TypeScript projects daily
- **Run manual refresh** after major refactoring or git pulls
- **Check map stats** if AI seems confused about project structure
- **Add `.quack/codebase-map.md` to `.gitignore`** - This is project-specific and auto-generated

### For AI Assistants

- **Read map FIRST** before exploring TypeScript codebases
- **Use map for discovery** (what exists) then Read files for details (how it works)
- **Verify map freshness** - Check `generated` timestamp in frontmatter
- **Fall back to direct reads** if map is missing or outdated

## Example Workflow

### Scenario: Add Authentication

**User prompt:**
> "Add JWT authentication to the API"

**Claude's approach WITH map:**

1. **Read** `.quack/codebase-map.md` (1 call, full overview)
2. **Identify** `src/services/api.ts` has `fetchWithAuth()`
3. **Read** `src/services/api.ts` (direct jump to relevant file)
4. **Implement** authentication using existing patterns

**Claude's approach WITHOUT map:**

1. **List** `src/` directory
2. **Read** `src/services/` directory
3. **Read** `api.ts`, `auth.ts`, `session.ts`, `user.ts`...
4. **Read** `src/types/` directory
5. **Read** various type files...
... 10+ exploratory reads later ...

## Troubleshooting

### Map Not Generating

**Check:**
- Is auto-generation enabled? (Settings > Codebase Map)
- Is the project path valid?
- Are there TypeScript files to index?

**Fix:** Click "Generate Now" to force full scan

### Map Outdated

**Symptoms:**
- AI refers to files that don't exist
- Missing recent exports

**Fix:**
- Click "Generate Now" for full refresh
- Verify auto-generation is enabled

### Map Too Large

**Symptoms:**
- Map file exceeds 50 KB
- AI struggles to process it

**Fix:**
- Review excluded patterns in `generate-codebase-map.mjs`
- Consider excluding test files or vendor code

---

**Previous**: [Prompt Engineering](./prompt-engineering) - Write better prompts for Claude

**Next**: [Best Practices](../04-best-practices/prompting-patterns) - Proven workflows and patterns
