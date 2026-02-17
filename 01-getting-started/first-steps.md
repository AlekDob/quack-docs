Now that you have Quack installed, let's explore the basic features and get you productive quickly.

## The Quack Interface

Quack is organized into three main areas:

### 1. Agents Panel (Left)
The left sidebar shows your **AI agents**:
- Each agent can work on one or multiple projects
- Agents maintain their own conversation history
- Click an agent to start or resume a conversation
- Create new agents with the **+** button

### 2. Chat Area (Center)
The main workspace where you interact with your agent:
- **Chat Tab**: Conversation with the active agent
- **Terminal Tabs**: XTerm.js-powered terminals
- **File Tabs**: Opened files for quick reference
- **Browser Tabs**: Integrated web browser for localhost apps
- **Docs Tab**: Built-in documentation viewer

### 3. Side Panel (Right)
Project context and tools:
- **Project Context**: Current agent info, working directory, git branch
- **File Explorer**: Navigate your project files
- **Commands**: Create and manage slash commands
- **Droids**: Specialized subagents for focused tasks
- **Skills**: Modular capabilities Claude can use
- **MCP Servers**: Model Context Protocol integrations
- **Hooks**: Automation triggers for tool events
- **Sessions**: Previous conversation history

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

## Working with Agents

Agents are your AI assistants in the left panel:

1. Click an agent in the **left sidebar** to select it
2. Each agent has its own conversation history
3. Agents can work on one or multiple projects
4. Create a new agent with the **+** button at the top

### Agent Features
- **Color coding**: Each agent has a unique color for easy identification
- **Project assignment**: Assign agents to specific projects
- **Persistent memory**: Agents remember context across sessions

## Using Droids

Droids are specialized subagents in the **right sidebar**:

1. Click **Droids** in the Side Panel (right)
2. Browse available droids (code-reviewer, test-engineer, etc.)
3. Droids work in isolation and return focused results
4. Claude automatically invokes droids when appropriate

## Using Skills

Skills are modular capabilities in the **right sidebar**:

1. Click **Skills** in the Side Panel (right)
2. Browse available skills
3. Skills are automatically discovered by Claude
4. They provide domain-specific knowledge and workflows

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
