# Task Progress Tracking

The Task Progress Bar gives you real-time visibility into your agent's work. Located in the status bar at the bottom of Quack, it shows exactly where you stand in any multi-step task - no more wondering how much is left or if the agent is still working.

## How It Works

When an AI agent creates a plan with multiple steps, Quack automatically tracks progress:

- **Percentage**: Visual progress indicator (e.g., 75%)
- **Counter**: Completed vs total tasks (e.g., 6/8)
- **Live Updates**: Progress updates as the agent completes each step
- **Always Visible**: Status bar remains visible during work

```
Status Bar: [Building features...] ████████░░ 75% (6/8)
```

## What You'll See

### During Active Work

When an agent is executing a plan:

```
┌─────────────────────────────────────────────────────┐
│  Analyzing authentication flow... 🔄 25% (2/8)       │
└─────────────────────────────────────────────────────┘
```

The status bar shows:
- **Current Task**: What the agent is working on right now
- **Progress Bar**: Visual indicator of completion
- **Percentage**: Numeric progress (0-100%)
- **Counter**: Steps completed out of total (e.g., 2/8)

### Real-time Updates

As the agent moves through its plan:

```
Step 1: Reading authentication files... ✓
Step 2: Analyzing security patterns...  ← Currently here (25%)
Step 3: Checking token handling...
Step 4: Testing session logic...
...
```

The progress bar updates immediately when each step completes.

### On Completion

When all tasks finish:

```
┌─────────────────────────────────────────────────────┐
│  Authentication review complete ✓ 100% (8/8)        │
└─────────────────────────────────────────────────────┘
```

## Understanding Task Plans

Agents create structured plans for complex requests. The progress tracker shows these as countable steps.

### Example: Feature Implementation

**Prompt:**
```
Add user authentication to the dashboard
```

**Agent Plan (8 steps):**
1. Read current authentication setup → 12.5%
2. Create login component → 25%
3. Add authentication hooks → 37.5%
4. Implement session management → 50%
5. Add protected route guards → 62.5%
6. Write unit tests → 75%
7. Update documentation → 87.5%
8. Final review and cleanup → 100%

Each completed step advances the progress bar.

### Example: Code Review

**Prompt:**
```
Review the API endpoints for security issues
```

**Agent Plan (5 steps):**
1. List all endpoint files → 20%
2. Check input validation → 40%
3. Verify authentication → 60%
4. Test error handling → 80%
5. Generate security report → 100%

## Benefits

### Always Know Where You Stand

No more uncertainty:
- **Clear expectations**: See total number of steps upfront
- **Estimated completion**: Gauge how much work remains
- **Confidence**: Know the agent is making progress

### Better Planning

The counter helps you:
- **Schedule work**: Know if you have time for coffee or need to wait
- **Identify bottlenecks**: See when the agent gets stuck on a step
- **Track efficiency**: Compare actual vs expected task counts

### Multi-agent Awareness

When running multiple agents:
- Each agent's progress is tracked independently
- Switch between terminals to check different task statuses
- Kanban tasks show their own progress in the drawer

## Tips and Best Practices

### Understanding Progress

**Linear progress doesn't mean linear time:**
- Some steps are fast (reading files) - 5 seconds
- Some steps are slow (running tests) - 2 minutes
- A task at 50% might be 25% complete in time

**Progress resets between conversations:**
- Each new prompt starts fresh at 0%
- Multi-turn conversations maintain progress within that session

### When Progress Isn't Shown

Progress tracking requires the agent to create an explicit plan. You won't see progress for:

- **Single-step tasks**: "What is 2+2?" doesn't need a plan
- **Exploratory questions**: "What files are in this project?"
- **Streaming responses**: Long text outputs without discrete steps

In these cases, the status bar shows activity without percentages:

```
┌─────────────────────────────────────────────────────┐
│  Generating response... 🔄                           │
└─────────────────────────────────────────────────────┘
```

### Maximizing Progress Visibility

**Ask for structured work:**

Good prompt (generates plan):
```
Refactor the authentication module:
1. Extract reusable functions
2. Add TypeScript types
3. Write unit tests
4. Update imports
```

Vague prompt (may not show progress):
```
Make the auth code better
```

**Break large tasks into stages:**

Instead of:
```
Build the entire dashboard feature
```

Try:
```
Build the dashboard feature. Start by:
1. Creating the layout
2. Adding data fetching
3. Implementing charts
4. Writing tests
```

## Integration with Other Features

### Kanban Board

Tasks in the Kanban Board show progress in the chat drawer:
- Drag a task to "In Progress"
- The chat drawer opens with the agent's plan
- Progress updates appear in both the drawer and status bar

### Background Tasks

Background agents also report progress:
- Check the Background Tasks panel for progress
- Desktop notifications show final percentage on completion
- Long-running tasks maintain accurate counts

### Multiple Terminals

Each terminal maintains its own progress:
- Switch terminals to see different agent progress
- Progress persists when switching tabs
- Status bar always shows the active terminal's progress

## Troubleshooting

### Progress Stuck at Same Percentage

**Cause**: Agent is working on a long-running step

**What to check**:
- Look at the current task description in status bar
- Watch the chat stream for ongoing output
- Some steps (like running tests) take minutes

**Not stuck if you see**:
- Chat messages still streaming
- Terminal output continuing
- Status bar shows "🔄" activity indicator

### Progress Goes Backward

**Cause**: Agent revised its plan mid-execution

**What happened**:
- Agent realized more steps were needed
- Total step count increased (e.g., 5/6 became 5/8)
- Percentage recalculated based on new total
- This is normal adaptive behavior

### No Progress Shown

**Cause**: Task doesn't have a structured plan

**Examples**:
- Simple questions: "What does this function do?"
- File searches: "Find all TypeScript files"
- Single operations: "Format this code"

**Solution**: These tasks complete quickly without needing progress tracking.

## Related Features

- **Background Tasks**: Run long operations without blocking your workflow
- **Kanban Board**: Visual task management with progress per card
- **Chat Streaming**: Real-time response rendering

---

**Previous**: [Background Tasks](./background-tasks)

**Next**: [Interactive Questions](./interactive-questions)
