Branch per Session moves git branch management from the agent level to the session level. Instead of an agent being locked to one branch, each session can work on its own branch independently.

## Why Branch per Session?

In the previous model, each agent was tied to a single branch. If Agent Graydon was working on `main` and you needed a hotfix on `hotfix/crash-fix`, you had two bad options:

1. Create a **new agent** just for the different branch
2. Change the agent's branch, affecting **all** existing sessions

Branch per Session fixes this:

```
Agent Graydon
  - Session "Bug fix"          -> main
  - Session "Hotfix crash"     -> hotfix/crash-fix
  - Session "New feature"      -> feature/project-grouping
```

One agent. Multiple branches. Each session works in its own context.

## Creating a Session with a Branch

### Steps

1. Click the **+** button on an agent card to create a new session
2. Enter a session title
3. Expand the **Git Branch** section (click to open)
4. Choose your branch:

### Using an Existing Branch

Select the **Use existing** tab. You'll see a list of local branches:

```
  Use existing  |  Create new

  (*) main              <- current
  ( ) develop
  ( ) feature/auth
  ( ) hotfix/crash-fix
```

Select the branch you want this session to work on.

### Creating a New Branch

Select the **Create new** tab:

```
  Use existing  |  Create new

  Branch name: [feature/my-feature    ]
  [x] Branch from current (main)
```

Type the new branch name. Enable "Branch from current" to base it on the current branch.

## Dirty Working Tree Protection

If your working tree has uncommitted changes and you try to switch branches, Quack blocks the action:

```
  /!\ 12 uncommitted files detected.
  Commit or stash changes before switching
  branch, or enable worktree.

  [Continue]  <- disabled
```

The **Continue** button stays disabled until you either:

1. **Commit or stash** your changes first
2. **Enable worktree** to create an isolated copy (see below)

When you enable the worktree toggle, the warning turns green:

```
  Worktree will isolate changes.
  12 uncommitted files won't be affected.

  [Continue]  <- enabled
```

## Worktree Toggle

When you select a branch different from the current one, a **worktree toggle** appears:

```
  [x] Use worktree (isolated copy)
      Agent works in a separate directory
      without affecting your main workspace
```

When enabled:

- A git worktree is created at `{project}/.worktrees/session-{branch}-{id}`
- The Claude process runs in the worktree directory
- Changes in the worktree don't affect your main working directory
- You can have multiple sessions working on different branches simultaneously

When disabled:

- The session switches the main repo to the selected branch
- Only one branch can be active at a time in the main repo
- Blocked if there are uncommitted changes

See [Git Worktree Isolation](../03-advanced-techniques/git-worktree.md) for more details.

## Branch Display in the Sidebar

Sessions are grouped by branch under each agent:

```
Agent Graydon
  > main (2)
    * Bug fix              8s ago
    * Grouping projects    4m ago
  > feature/hotfix (1)
    * Fix crash            1h ago
```

Each branch group shows:

- **Branch icon and name**: The git branch
- **Session count**: Number of sessions on this branch
- **Sessions list**: Individual sessions with timestamps

### Branch Badge

Sessions with an explicit branch (different from the agent's default) show an **orange badge**. Sessions using the agent's default branch show a **gray badge**.

## How It Works Technically

### Session Metadata

Each session stores branch information:

```typescript
interface AgentSession {
  id: string;
  agentId: string;
  title: string;
  branch?: string;        // session-specific branch
  useWorktree?: boolean;  // whether using a worktree
  worktreePath?: string;  // path to the worktree
}
```

### Backward Compatibility

Sessions created before this feature have no `branch` field. They automatically inherit the agent's branch as their default. No migration needed.

### Working Directory Priority

When a session is active, the working directory resolves as:

1. `session.worktreePath` (if using a worktree)
2. `session.projectPath` (if set)
3. Agent's working directory (default)

This affects both the Claude process working directory and the git panel display.

## Agent vs Session Branch

Branches exist at two levels:

| Level | Set When | Purpose |
|-------|----------|---------|
| **Agent branch** | Creating a new agent (New Terminal modal) | Default branch for all sessions |
| **Session branch** | Creating a new session (New Session modal) | Override for this specific session |

The agent branch is the **default**. The session branch is the **override**. If no session branch is set, the agent's branch is used.

## Tips and Best Practices

### When to Use Session Branches

**Good use cases:**
- Working on a hotfix while a feature is in progress
- Testing a colleague's branch without disrupting your work
- Running parallel experiments on different branches

**Not needed:**
- All your sessions work on the same branch (just use the agent default)

### Branch + Worktree Combinations

| Scenario | Branch? | Worktree? | Result |
|----------|---------|-----------|--------|
| Same branch as agent | No | No | Uses agent's working directory |
| Different branch, clean tree | Yes | No | Switches main repo to new branch |
| Different branch, dirty tree | Yes | Yes | Creates isolated worktree |
| New feature branch | Yes | Yes | Creates branch + worktree |

### Naming Sessions

When using multiple branches, include the branch context in your session title:

**Good**: "Fix login bug (hotfix)", "Add pricing page (feature/pricing)"

**Bad**: "Session 1", "New session"

## Troubleshooting

### Session Shows Wrong Branch

**Problem**: The chat header shows `main` instead of the session's branch.

**Solution**: This can happen due to an async race condition. Switch to another session and back, or restart the app. The session's explicit branch takes priority over the git-detected branch.

### Branch Selector Not Loading

**Problem**: The branch list is empty in the New Session modal.

**Solution**: The branch selector requires the Tauri backend. Make sure you're running `npm run tauri dev` (not just `npm run dev`).

### Can't Switch Branch (Dirty Tree)

**Problem**: The Continue button is disabled when selecting a different branch.

**Solution**: You have uncommitted changes. Either commit/stash them first, or enable the **Use worktree** toggle to create an isolated copy.

## Related Features

- **[Project Grouping](./project-grouping)**: Group related projects and share context
- **[Git Worktree Isolation](../03-advanced-techniques/git-worktree.md)**: Deep dive into worktree mechanics
- **[Side Panel](./side-panel)**: Agent context showing current branch

---

**Previous**: [Project Grouping](./project-grouping)

**Next**: [Prompt Engineering](../03-advanced-techniques/prompt-engineering)
