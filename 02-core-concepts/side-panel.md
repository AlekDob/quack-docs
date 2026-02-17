The Side Panel is your command center in Quack. Located on the right side of the interface, it provides quick access to all the tools and information you need while working with AI agents.

## Overview

The Side Panel contains 8 sections, accessible via icon tabs:

| Icon | Section | Description |
|------|---------|-------------|
| Person | Agent Context | Current agent info and context |
| Folder | File Explorer | Navigate project files |
| Terminal | Commands | Manage slash commands |
| Robot | Droids | Browse and create specialized agents |
| Star | Skills | View available skills |
| Chip | MCP Servers | Configure Model Context Protocol |
| Hook | Hooks | Automation triggers |
| Clock | Sessions | Conversation history |

## Agent Context

The Agent Context panel shows information about your currently active agent.

### What You'll See

- **Agent Name and Avatar**: The active agent's identity
- **Working Directory**: Current project path
- **Project Name**: Detected from package.json or folder name
- **Git Branch**: Current branch if in a git repository
- **Personality**: Agent's communication style and notes

### Actions

- **Edit Agent**: Modify the current agent's configuration
- **View Context Files**: See CLAUDE.md and other context files
- **Browse Skills**: Quick access to assigned skills
- **Browse Droids**: Quick access to assigned droids

## File Explorer

Navigate your project files without leaving Quack.

### Features

- **Tree View**: Collapsible folder structure
- **File Icons**: Visual indicators for file types
- **Modified Indicators**: Shows files with unsaved changes
- **Quick Actions**: Right-click menu for file operations

### Usage

1. Click folders to expand/collapse
2. Click files to open in a new tab
3. Use the mention button (@) to reference files in chat
4. Modified files show a colored indicator

## Commands

Create and manage custom slash commands for frequently-used prompts.

### Viewing Commands

Commands are organized by scope:
- **Project Commands**: Stored in `.claude/commands/` (shared with team)
- **Personal Commands**: Stored in `~/.claude/commands/` (your own)

### Creating a Command

1. Click the **+ New Command** button
2. Fill in the command details:
   - **Name**: The command name (e.g., `review`)
   - **Description**: What the command does
   - **Content**: The prompt instructions
3. Save your command

Your new command will be available as `/your-command-name`.

### Using Commands

- Type `/` in chat to see available commands
- Click a command in the panel to insert it
- Commands can include arguments using `$ARGUMENTS`

## Droids

Droids are specialized subagents that handle specific tasks in isolation.

### How Droids Work

- They run as **separate agents** with their own context
- Results are returned to the main conversation
- They don't pollute your primary chat history
- Perfect for focused, specialized tasks

### Browsing Droids

The panel shows:
- **Droid Name**: The identifier
- **Description**: What the droid specializes in
- **Model**: Which Claude model it uses
- **Scope**: Project or Personal

### Creating a Droid

1. Click **+ New Droid** button
2. Choose a template or start from scratch
3. Configure:
   - **Name**: Unique identifier
   - **Description**: What it does
   - **Model**: Claude model to use
   - **Color**: Visual identifier
   - **Instructions**: Detailed guidance
4. Save to project or personal scope

### Using Droids

Claude automatically discovers droids based on your request. You can also explicitly invoke them in prompts:

```
Use the code-reviewer droid to analyze this file
```

## Skills

Skills are modular capabilities that extend what Claude can do.

### Understanding Skills

- Skills are **folders** containing instructions and resources
- Claude **automatically discovers** relevant skills
- They provide domain-specific knowledge and workflows
- Can include scripts, templates, and reference docs

### Viewing Skills

The panel shows:
- **Skill Name**: The identifier
- **Description**: What capability it provides
- **Source**: Personal, Project, or Plugin
- **Files**: Number of resources included

### Skill Sources

| Source | Location | Sharing |
|--------|----------|---------|
| Personal | `~/.claude/skills/` | Only you |
| Project | `.claude/skills/` | Team via git |
| Plugin | Installed plugins | Plugin-dependent |

## MCP Servers

Model Context Protocol servers extend Claude's capabilities with external tools and data sources.

### What is MCP?

MCP allows Claude to:
- Access external APIs and services
- Use custom tools you define
- Connect to databases and filesystems
- Integrate with third-party applications

### Viewing MCP Servers

The panel shows:
- **Server Name**: The identifier
- **Status**: Connected, Disconnected, or Error
- **Tools**: Available tools from this server
- **Prompts**: Available prompts from this server

### Configuring MCP

MCP servers are configured in your settings:

1. Open Settings (Cmd/Ctrl + ,)
2. Navigate to MCP section
3. Add server configuration:
   - **Name**: Server identifier
   - **Command**: How to start the server
   - **Args**: Command arguments
   - **Environment**: Environment variables

### Common MCP Servers

- **Filesystem**: Read/write local files
- **GitHub**: Interact with repositories
- **Memory**: Persistent knowledge graph
- **Database**: Query SQL databases

## Hooks

Hooks are automation triggers that run before or after Claude actions.

### How Hooks Work

Hooks intercept tool usage:
- **PreToolUse**: Runs before a tool executes
- **PostToolUse**: Runs after a tool completes

### Viewing Hooks

The panel shows:
- **Hook Name**: The identifier
- **Event**: PreToolUse or PostToolUse
- **Matcher**: Which tools trigger this hook
- **Enabled**: Whether the hook is active

### Creating a Hook

1. Click **+ New Hook** button
2. Configure:
   - **Name**: Unique identifier
   - **Event**: When to trigger
   - **Matcher**: Tool pattern (e.g., `Bash`, `Edit:*`)
   - **Command**: Script to run
3. Save to project or personal scope

### Hook Use Cases

- **Pre-commit checks**: Validate before git commit
- **Auto-formatting**: Format code after edits
- **Logging**: Track all tool usage
- **Notifications**: Alert on specific actions

## Sessions

View and resume previous conversations.

### Session List

The panel shows recent sessions with:
- **Timestamp**: When the session occurred
- **Preview**: First message or topic
- **Duration**: How long the session lasted
- **Agent**: Which agent was used

### Resuming a Session

1. Click a session to preview
2. Click **Resume** to continue the conversation
3. All context and history will be restored

### Session Management

- Sessions are stored locally
- Each project maintains its own session history
- Older sessions are automatically archived

## Tips and Best Practices

### Efficient Navigation

- Use keyboard shortcuts to toggle panels
- The panel remembers your last active tab
- Collapse the panel when you need more space

### Context Awareness

- Keep Agent Context visible to monitor your agent
- Use File Explorer to quickly reference files
- Check Sessions to resume previous work

### Organization

- Create project-specific commands for team workflows
- Use personal droids for your unique use cases
- Organize skills by domain in subfolders

**Previous**: [First Steps](../01-getting-started/first-steps)

**Next**: [Kanban Board](./kanban-board)
