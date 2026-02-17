Code Graph MCP is an AST-powered code intelligence server that gives your AI agents deep understanding of your codebase structure. Instead of scanning flat file lists, it builds a real code graph with definitions, references, call chains, and complexity metrics.

## What It Does

Code Graph MCP runs as an MCP (Model Context Protocol) server alongside your Quack sessions. When an agent needs to understand your code, it queries the graph instead of doing multiple Glob/Grep searches.

### Available Tools

| Tool | What It Does | Speed |
|------|-------------|-------|
| `find_definition` | Locates where a symbol is defined | Fast (<1s) |
| `find_references` | Finds all usages of a symbol | Fast (<3s) |
| `find_callers` | Shows which functions call a target | Fast (<2s) |
| `find_callees` | Shows what a function calls internally | Fast (<2s) |
| `complexity_analysis` | Identifies complex/risky code | Moderate (5-15s) |
| `dependency_analysis` | Maps module import relationships | Moderate (3-10s) |
| `analyze_codebase` | Full project overview with metrics | Slow (10-60s) |

### Before vs After

**Without Code Graph MCP:**
1. Agent runs Glob to find files matching a pattern
2. Agent runs Grep to search for function name
3. Agent reads 3-4 files to understand context
4. Agent runs more Grep to find who calls the function
5. 8-10 tool calls, high token usage

**With Code Graph MCP:**
1. Agent calls `find_definition("myFunction")`
2. Agent calls `find_callers("myFunction")`
3. 2 tool calls, low token usage

This is how the [Medium article](https://medium.com/@me_82386/i-cut-my-claude-code-api-costs-by-40-with-one-tool-12cf4306a1ab) reports a 40% reduction in API costs.

## Installation

There are two parts: installing the Python package on your system, and configuring Quack to use it.

### Part 1: Install the Python Package

Code Graph MCP requires Python 3.12+. Install it with pipx (recommended):

```bash
# Install pipx if you don't have it
brew install pipx
pipx ensurepath

# If you don't have Python 3.12+, install it first
brew install python@3.12

# Install code-graph-mcp
pipx install --python python3.12 code-graph-mcp
```

Find the absolute path (needed for Quack configuration):

```bash
which code-graph-mcp
# Example output: /Users/yourname/.local/bin/code-graph-mcp
```

### Part 2: Configure in Quack (Two Options)

**Option A: Install from Quack Store (Recommended)**

1. Open the Quack Store (sidebar)
2. Go to the "MCP Servers" category
3. Find "Code Graph MCP" and click Install
4. Choose "Global" when prompted for scope

This automatically:
- Adds the server to your `~/.mcp.json`
- Installs the `use-code-graph` rule in `~/.claude/rules/` (tells agents to use Code Graph tools)

After installing from the Store, open "Edit JSON" > "Global .mcp.json" and replace the command with your absolute path from Part 1:

```json
{
  "mcpServers": {
    "code-graph-mcp": {
      "command": "/Users/yourname/.local/bin/code-graph-mcp",
      "type": "stdio"
    }
  }
}
```

**Option B: Manual Configuration**

Open the MCP panel, click "Edit JSON" > "Global .mcp.json", and add the config above manually. Then copy the rule file from the [Quack Marketplace repo](https://github.com/AlekDob/quack-marketplace/blob/main/plugins/code-graph-mcp/rules/use-code-graph.md) to `~/.claude/rules/use-code-graph.md`.

### Verify

After configuration, the MCP panel should show `code-graph-mcp` with a green "Running" status under Global Servers.

## How Agents Use It

Once installed, agents **automatically** use Code Graph MCP in every session. No need to ask them. This works because:

1. The `use-code-graph` rule in `~/.claude/rules/` is loaded at the start of every Claude Code session
2. The rule instructs agents to prefer Code Graph tools over manual Glob/Grep searches
3. The MCP server runs in the background, providing tools like `find_definition`, `find_references`, etc.

Agents will:
- Use `find_definition` instead of Grep when looking for where something is defined
- Use `find_references` before modifying a function to check impact
- Use `dependency_analysis` to understand module relationships
- Use `complexity_analysis` to identify refactoring targets

You don't need to do anything special -- it just works.

## Language Support

Code Graph MCP uses [ast-grep](https://ast-grep.github.io/) for parsing, which supports 25+ languages including:

- TypeScript / JavaScript / JSX / TSX
- Rust
- Python
- Go, Java, C, C++, C#
- Ruby, PHP, Swift, Kotlin
- And many more

This is a significant improvement over the previous codebase map which only supported TypeScript/JavaScript.

## Limitations

- **No visual graph UI** -- Code Graph MCP is a headless query server. It doesn't generate visual diagrams. A visual graph explorer may be added to Quack in a future release.
- **First analysis is slow** -- The initial `analyze_codebase` call takes 10-60 seconds depending on project size. Results are cached after that.
- **Python dependency** -- Requires Python 3.12+ installed on the system.

## Troubleshooting

### "Command not found" Error

The server shows "Error" status with "Command not found":
- Make sure you used the **absolute path** in `.mcp.json`
- Verify the binary exists: `ls -la /Users/yourname/.local/bin/code-graph-mcp`
- If using pipx, run `pipx ensurepath` and restart your terminal

### "Connection test failed"

- Check that Python 3.12+ is installed: `python3.12 --version`
- Reinstall: `pipx install --python python3.12 code-graph-mcp --force`

### Empty Results from find_definition

Some symbol names may not be indexed. Try:
- Running `analyze_codebase` with `rebuild_graph=true` first
- Using partial symbol names (e.g., "MyComponent" instead of "export default MyComponent")

---

Previous: [Prompt Engineering](./prompt-engineering.md) | Next: [Git Worktree](./git-worktree.md)
