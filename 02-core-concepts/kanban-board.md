The Kanban Board is a visual task management system that helps you organize and track AI-assisted work across multiple projects. It provides an intuitive drag-and-drop interface for managing tasks through their lifecycle.

## Opening the Kanban Board

There are two ways to access the Kanban Board:

1. **Keyboard Shortcut**: Press `Cmd+K` (macOS) or `Ctrl+K` (Windows/Linux)
2. **Toolbar Button**: Click the board icon in the top toolbar

The Kanban Board replaces the standard chat view, giving you a full-screen workspace for task management.

## Understanding the Layout

```
+------------------+------------------------------------------+
|    AGENTS        |           KANBAN BOARD                   |
|   SIDEBAR        |  [TODO]    [IN PROGRESS]    [DONE]       |
+------------------+------------------------------------------+
|  [Agent 1]       |  [Card]      [Card]         [Card]       |
|  [Agent 2]       |  [Card]      [Card]         [Card]       |
|  [Agent 3]       |              [Card]                      |
|  + New Agent     |                                          |
+------------------+------------------------------------------+
```

### Three Columns

| Column | Purpose |
|--------|---------|
| **TODO** | Tasks waiting to be started |
| **In Progress** | Tasks currently being worked on by AI agents |
| **Done** | Completed tasks |

### Agents Sidebar

The left sidebar shows all available AI agents from your terminals. You can:
- See which agents are available
- Drag an agent onto the board to create a task
- Click "+ New Agent" to create a new terminal with an agent

## Creating Tasks

### Method 1: Add Task Button

1. Click the **+ Add Task** button in the top-right corner
2. Fill in the task details:
   - **Title**: A short name for the task
   - **Prompt**: The full instructions for the AI agent
   - **Project**: Select which project this task belongs to
   - **Branch**: Choose the Git branch (if applicable)
   - **Agent**: Assign an agent to work on the task
3. Click **Create Task**

### Method 2: Drag an Agent

1. Find an agent in the left sidebar
2. Drag the agent onto any column
3. A modal will appear with the agent pre-selected
4. Fill in the task details and create

## Working with Tasks

### Moving Tasks

Drag and drop task cards between columns:
- **TODO to In Progress**: Starts the task - the chat drawer opens automatically with your prompt
- **In Progress to Done**: Marks the task as complete
- **Done to TODO**: Re-opens the task for more work

### Task Cards

Each task card displays:
- **Title**: The task name
- **Project/Branch**: Where the task runs
- **Agent Avatar**: Who's assigned to the task
- **Token Usage**: How many tokens have been used (if applicable)

### Chat Drawer

When you click on a task card, a chat drawer opens on the right side:

- **Active Tasks**: Continue the conversation with the AI agent
- **Completed Tasks**: Review the chat history and results
- **Controls**: Send messages, clear conversation, or abort streaming

The chat uses the same powerful Claude integration as the main terminal, but isolated to this specific task.

## Cross-Project View

The Kanban Board shows tasks from **all your projects** in one place. This makes it easy to:
- See your total workload across projects
- Move between different projects without switching contexts
- Track progress on multiple features simultaneously

Each task card shows its project name, so you always know where it belongs.

## Tips and Best Practices

### Effective Task Prompts

Write clear, specific prompts for better results:

**Good prompt:**
```
Review the authentication module in src/auth/ and identify
any security vulnerabilities. Focus on:
1. Input validation
2. Token handling
3. Session management
```

**Vague prompt:**
```
Check the auth code
```

### Organizing Work

- **Break large tasks into smaller pieces**: Create separate tasks for research, implementation, and testing
- **Use descriptive titles**: "Add user validation" is better than "Fix bug"
- **Assign the right agent**: Use specialized agents (code reviewer, test engineer) for specific tasks

### Managing Agents

- **One task per agent**: Each agent works on one task at a time
- **Review before completing**: Always check the results before moving to Done
- **Clear completed tasks**: Periodically archive done tasks to keep the board clean

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `Cmd+K` | Toggle Kanban Board on/off |
| `Escape` | Close chat drawer |
| `Enter` | Send message in chat drawer |

## Related Features

- **Background Tasks**: Run long operations without blocking the board
- **Terminal Sessions**: Each agent is backed by a full terminal
- **Chat History**: All conversations are saved per task

---

**Previous**: [Side Panel](./side-panel)

**Next**: [Second Brain](./second-brain)
