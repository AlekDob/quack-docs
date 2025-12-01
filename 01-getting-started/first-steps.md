# First Steps with Quack

Now that you have Quack installed, let's explore the basic features and get you productive quickly.

## The Quack Interface

Quack is organized into several key areas:

### 1. Tab Bar (Top)
- **Chat Tab**: Main conversation with Claude
- **Terminal Tabs**: Each open terminal appears as a tab
- **File Tabs**: Opened files for quick reference
- **Browser Tabs**: Integrated web browser for localhost apps

### 2. Sidebar (Left)
- **Chat**: AI conversation interface
- **File Explorer**: Navigate your project files
- **Git**: Version control operations
- **Agents**: Manage available agents
- **Skills**: Browse and use Claude skills
- **Commands**: Quick access to slash commands

### 3. Main Content Area
- **Terminal**: XTerm.js-powered terminal
- **Editor**: Code viewer (coming soon)
- **Browser**: Embedded web view for local apps

### 4. Status Bar (Bottom)
- Connection status
- Current working directory
- Active model information

## Opening Your First Terminal

Let's start by opening a terminal:

1. Click the **+** button in the tab bar (or press `Cmd/Ctrl + T`)
2. A new terminal tab will appear
3. The terminal starts in your home directory by default

Try running some basic commands:

```bash
# Check current directory
pwd

# List files
ls -la

# Navigate to a project
cd ~/projects/my-app

# Run a dev server
npm run dev
```

## Having Your First Conversation

Claude is always ready in the Chat tab:

1. Click the **Chat** tab (or press `Cmd/Ctrl + 1`)
2. Type a question or request
3. Press `Enter` to send

**Try these prompts**:

```
Explain the difference between let and const in JavaScript
```

```
How do I create a React component with TypeScript?
```

```
Show me best practices for error handling in async functions
```

## Using File References

One of Quack's most powerful features is **file context**:

You can reference files in your prompts using the `@` symbol:

```
Explain what this file does @src/App.tsx
```

```
Find bugs in @src/components/Terminal.tsx
```

```
Analyze all components in @src/components/*.tsx
```

## Working with Multiple Terminals

Quack supports multiple terminals running simultaneously:

1. Open a new terminal: `Cmd/Ctrl + T`
2. Each terminal maintains its own session
3. Switch between terminals by clicking their tabs
4. Color indicators help distinguish terminals
5. Close terminals with the × button

**Use case example**:
- Terminal 1: Running `npm run dev`
- Terminal 2: Running `npm test --watch`
- Terminal 3: Git operations

## Exploring Agents

Agents are specialized AI assistants for specific tasks:

1. Click **Agents** in the sidebar
2. Browse available agents (git-flow-manager, test-engineer, etc.)
3. Click an agent to learn what it does
4. Use agents via chat: `/agent-name task description`

## Using Skills

Skills provide domain-specific knowledge:

1. Click **Skills** in the sidebar
2. Browse skills (xterm-terminal-expert, tauri-build-expert, etc.)
3. Click a skill to read its documentation
4. Skills are automatically available to Claude

## Slash Commands

Slash commands are **custom prompts** you can create and manage. They allow you to define frequently-used prompts that Claude can execute.

### Managing Commands

1. Click the **Commands** icon in the right sidebar
2. Browse your existing project and personal commands
3. Search commands using the search bar
4. Click any command to view or edit it

### Creating a Command

1. Open the **Commands** panel in the right sidebar
2. Click the **+ New Command** button (top right)
3. Fill in the command details:
   - **Name**: The command name (e.g., `review`)
   - **Description**: What the command does
   - **Content**: The prompt instructions
4. Save your command

Your new command will be available immediately as `/your-command-name`.

### Example Commands

Here are some useful commands you might create:

- `/review` - Review code for bugs and improvements
- `/explain` - Explain code in simple terms
- `/optimize` - Analyze code for performance issues
- `/document` - Generate documentation for code

Type `/` in the chat to see all available commands.

## Next Steps

Now that you're familiar with the basics:

- Explore the [Side Panel](../02-core-concepts/side-panel) in depth
- Learn [Advanced Techniques](../03-advanced-techniques/prompt-engineering) for better AI interactions
- Discover [Best Practices](../04-best-practices/prompting-patterns) for power users

**Previous**: [Installation](./installation)

**Next**: [The Side Panel](../02-core-concepts/side-panel)
