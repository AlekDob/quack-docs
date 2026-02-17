# Background Tasks

Background Tasks allow you to run long-running operations without blocking your main workflow. Whether you're running builds, tests, or AI agents, background tasks keep Quack responsive while work happens in the background.

## Why Use Background Tasks?

When you run a command like `npm run build` in a regular terminal, you have to wait for it to finish. Background Tasks solve this by:

- **Non-blocking execution**: Continue working while tasks run
- **Progress tracking**: See real-time progress and logs
- **Notifications**: Get notified when tasks complete
- **Queue management**: Run multiple tasks with priority control

## Using the /background Command

The `/background` command is the easiest way to run background tasks.

### Running Shell Commands

```bash
# Run a build
/background npm run build

# Run tests
/background npm test

# Run linting
/background npm run lint

# Run any shell command
/background ./scripts/deploy.sh
```

### Running AI Agents

Use `@agent-name` to run an AI agent in the background:

```bash
# Run code reviewer agent
/background @code-reviewer Review the authentication module

# Run test engineer agent
/background @test-engineer Write unit tests for the API endpoints

# Run documentation agent
/background @doc-writer Update the README with new features
```

## Task Types

The system automatically detects the type of task based on your command:

| Type | Keywords | Default Timeout |
|------|----------|-----------------|
| **Build** | `build`, `compile`, `dev` | 10 minutes |
| **Test** | `test`, `vitest`, `jest` | 10 minutes |
| **Analysis** | `lint`, `analyze`, `audit` | 10 minutes |
| **Agent** | Commands starting with `@` | 5 minutes |
| **Custom** | Everything else | 10 minutes |

## Monitoring Tasks

### Background Tasks Panel

Access the Background Tasks panel from the sidebar. It shows:

- **Task list**: All current and recent tasks
- **Status indicators**: Queued, Running, Completed, Failed
- **Progress bars**: Real-time progress for each task
- **Logs**: Expandable log output with ANSI color support

### Task Cards

Each task card displays:

```
+--------------------------------------------------+
|  Build Project                           RUNNING  |
|  npm run build                                    |
|  [=========>                      ] 45%           |
|  Building components...                           |
|  Duration: 0:45                                   |
|  [Pause] [Cancel] [Expand Logs]                   |
+--------------------------------------------------+
```

### Status Indicators

| Status | Description |
|--------|-------------|
| **Queued** | Waiting to start (max concurrent tasks reached) |
| **Running** | Currently executing |
| **Completed** | Finished successfully |
| **Failed** | Finished with errors |
| **Paused** | Temporarily stopped |
| **Cancelled** | Manually stopped |

## Priority Levels

Tasks can have three priority levels:

| Priority | Weight | Use For |
|----------|--------|---------|
| **High** | 3 | Critical tasks that need immediate execution |
| **Medium** | 2 | Normal development tasks |
| **Low** | 1 | Background maintenance tasks |

Higher priority tasks run first. Within the same priority, older tasks run first.

## Managing the Queue

### Concurrent Tasks

By default, Quack runs up to **5 tasks simultaneously**. You can adjust this in settings.

### Queue Operations

From the Background Tasks panel, you can:

- **Pause Queue**: Stop starting new tasks
- **Resume Queue**: Continue starting queued tasks
- **Change Priority**: Move tasks up or down in the queue
- **Clear Completed**: Remove finished tasks from the list

### Task Controls

For individual tasks:

- **Pause**: Temporarily stop the task
- **Resume**: Continue a paused task
- **Cancel**: Stop and terminate the task
- **Retry**: Re-run a failed task

## Real-time Features

### Log Streaming

Logs appear in real-time as the task runs:

- **stdout**: Normal output in white
- **stderr**: Error output in red
- **ANSI colors**: Full color support for formatted output

Click **Expand Logs** on a task card to see the full output.

### Progress Tracking

Some commands report progress:
- Percentage complete
- Current stage (e.g., "Compiling TypeScript")
- Estimated time remaining

### Desktop Notifications

When a task completes, you receive a desktop notification:

- **Success**: "Task Completed" with green styling
- **Failure**: "Task Failed" with error message

You also hear a "quack" sound on successful completion!

## Integration with Kanban

Background tasks integrate seamlessly with the Kanban Board:

1. **Create a Kanban task** with a prompt
2. The task can spawn **background operations**
3. Monitor progress in the Background Tasks panel
4. Get notified when everything completes

This is especially useful for long-running AI tasks like code reviews or test generation.

## Best Practices

### When to Use Background Tasks

**Use for:**
- Builds that take more than a few seconds
- Full test suites
- Code analysis and linting
- AI agent tasks (code review, test writing)
- Git operations on large repositories

**Don't use for:**
- Quick commands (less than 2 seconds)
- Interactive prompts that need input
- Debugging sessions

### Effective Commands

**Be specific with prompts:**

```bash
# Good - clear instructions
/background @test-engineer Write unit tests for src/auth/login.ts focusing on error handling

# Vague - may produce poor results
/background @test-engineer write tests
```

### Managing Resources

- **Limit concurrent tasks**: Don't run too many at once
- **Clear completed tasks**: Keep the panel clean
- **Set appropriate timeouts**: Long tasks should have longer timeouts
- **Monitor logs**: Check for errors early

## Troubleshooting

### Task Stuck in Queued

**Cause**: Maximum concurrent tasks reached

**Solution**:
- Wait for running tasks to complete
- Cancel unnecessary running tasks
- Increase the concurrent task limit in settings

### Task Fails Immediately

**Cause**: Command not found or invalid

**Solution**:
1. Check the task logs for error messages
2. Verify the command works in a regular terminal
3. Check the working directory is correct

### No Logs Appearing

**Cause**: Real-time logs may be disabled

**Solution**:
1. Click "Expand Logs" on the task card
2. Check if the command produces any output
3. Some commands buffer output until completion

### Notifications Not Working

**Cause**: System notification permissions

**Solution**:
1. Check macOS/Windows notification permissions
2. Ensure Quack has permission to send notifications
3. Check that notifications aren't set to Do Not Disturb

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `/background` | Start typing background command |
| `Escape` | Close Background Tasks panel |

---

**Previous**: [Brain Store Setup](./brain-store-setup) — Installa i plugin Brain dal Quack Store

**Next**: [Task Progress Tracking](./task-progress-tracking)
