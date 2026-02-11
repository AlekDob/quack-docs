# Code Graph MCP

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

### Prerequisites

- Python 3.12 or higher
- pipx (recommended) or pip

### Step 1: Install the Package

```bash
# Install pipx if you don't have it
brew install pipx
pipx ensurepath

# Install code-graph-mcp with Python 3.12
pipx install --python python3.12 code-graph-mcp
```

### Step 2: Find the Absolute Path

Tauri apps don't always inherit your shell PATH, so you need the absolute path:

```bash
which code-graph-mcp
# Example output: /Users/yourname/.local/bin/code-graph-mcp
```

### Step 3: Configure in Quack

Open the MCP panel in Quack, click "Edit JSON" > "Global .mcp.json", and add:

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

Replace `/Users/yourname/.local/bin/code-graph-mcp` with your actual path from Step 2.

### Step 4: Verify

After saving, the MCP panel should show `code-graph-mcp` with a green "Running" status under Global Servers.

## How Agents Use It

Once installed, agents automatically use Code Graph MCP when the `use-code-graph` rule is active (installed from the Quack Store). The rule instructs agents to:

1. Use `find_definition` instead of Grep when looking for where something is defined
2. Use `find_references` before modifying a function to check impact
3. Use `dependency_analysis` to understand module relationships
4. Use `complexity_analysis` to identify refactoring targets

You don't need to do anything special -- agents will prefer Code Graph queries over manual file searches whenever the tools are available.

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
