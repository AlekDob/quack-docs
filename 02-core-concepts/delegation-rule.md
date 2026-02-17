Quack agents follow a structured decision tree to determine the right level of delegation before implementing any task. This prevents both under-delegation (doing everything solo) and over-delegation (spawning teams for trivial work).

## The Three Levels

### Level 1: Agent Team (Parallel Full Sessions)

Use when **all** of these are true:

- Task touches more than one domain (e.g. frontend + backend + tests, or code + docs)
- Files do not overlap between workers
- No strict sequential dependency between subtasks
- Expected effort is more than 15 minutes per subtask

**Examples**: New feature with frontend + backend + tests, cross-layer refactor, parallel research and debugging.

Agent Teams use the Teammate tool to spawn full Claude Code sessions that communicate with each other. They are the most powerful but also the most expensive option in terms of tokens.

### Level 2: Subagent / Droid (Invisible Workers)

Use when **any** of these is true:

- Task is focused on one domain with a clear deliverable
- Requires a specific skill (code review, test generation, documentation)
- Result only needs to come back to the calling agent (no inter-worker communication)
- Task is research or exploration that feeds into a decision

**Examples**: Code review, test writing, documentation update, codebase search, single-file refactor.

Subagents use the Task tool or custom droids defined in `.claude/agents/`. They work invisibly and return results to the calling agent.

### Level 3: Single Agent (Do It Yourself)

Use when **all** of these are true:

- Task touches 3 or fewer files with interconnected logic
- Changes depend on understanding a single root cause
- Coordination overhead would exceed execution time

**Examples**: Bug fix on related files, small config change, quick UI tweak.

## The Checkpoint

Before starting implementation, the agent must:

1. State which delegation level was chosen (Team / Subagent / Single)
2. Explain why in one sentence
3. If Team: list who does what. If Subagent: list which droids or skills to use.

This makes delegation decisions transparent and reviewable.

## Cost Considerations

| Level | Token Cost | Best For |
|---|---|---|
| Agent Team | High (N separate context windows) | Multi-domain parallel work |
| Subagent/Droid | Medium (separate but ephemeral context) | Focused single-domain tasks |
| Single Agent | Low (one context window) | Small interconnected fixes |

## Installing from Marketplace

The Delegation Decision Rule is available as a standalone plugin in the Quack Marketplace under the name **delegation-rule**. Install it to add the rule to any agent.
