# Git Worktree Isolation

Git worktrees let you work on multiple branches simultaneously without switching your main repository. Each worktree is a separate directory with its own working tree, sharing the same git history as the main repo. In Quack, worktrees are created per session, giving each AI agent session its own isolated workspace.

## Why Use Worktrees?

### The Problem

In a multi-agent environment, you often need sessions working on different branches at the same time. Without worktrees:

- Switching branches in the main repo affects all sessions
- Uncommitted changes block branch switching
- You can't have two sessions on different branches simultaneously

### The Solution

Worktrees create separate directories for each branch:

```
/path/to/project/                     <- main repo (main branch)
/path/to/project/.worktrees/
  session-feature-auth-a1b2/          <- worktree (feature/auth)
  session-hotfix-crash-c3d4/          <- worktree (hotfix/crash)
```

Each session works in its own directory. No conflicts. No switching.

## How Worktrees Work in Quack

### Creation

When you create a new session and enable the worktree toggle:

1. Quack checks if a worktree for that branch already exists
2. If it exists, the session **reuses** the existing worktree
3. If it doesn't, Quack calls `git worktree add` to create one

The worktree path follows the pattern:
```
{projectPath}/.worktrees/session-{sanitized-branch}-{short-id}
```

For example:
```
/Users/you/project/.worktrees/session-feature-auth-a1b2c3d4
```

### Reuse

If you already have a worktree for `feature/auth` and create a new session on the same branch, Quack detects the existing worktree and reuses it. No duplicate worktrees are created.

### What Runs in the Worktree

When a session uses a worktree:

- **Claude process**: Starts with `cwd` set to the worktree directory
- **Git panel**: Shows the worktree's status (not the main repo)
- **File operations**: All reads and writes happen in the worktree
- **Commits**: Go to the worktree's branch

When you switch to a different session, the git panel and Claude process automatically switch to that session's directory.

## Worktree vs Branch Switch

| Aspect | Branch Switch | Worktree |
|--------|--------------|----------|
| **Working directory** | Same (main repo) | Separate directory |
| **Parallel branches** | No (one at a time) | Yes (multiple) |
| **Dirty tree** | Must commit/stash first | Not affected |
| **Disk space** | Minimal | Extra copy of files |
| **Speed** | Instant | Seconds (copies files) |

### When to Use Each

**Branch switch** (no worktree):
- Working tree is clean
- You only need one branch at a time
- Quick context switch

**Worktree**:
- You have uncommitted changes you don't want to stash
- You need multiple branches running simultaneously
- You want full isolation between sessions

## Working With the Git Panel

The git panel automatically follows the active session. When you click on a session that uses a worktree:

1. The git panel root path updates to the worktree directory
2. Status shows files changed in the worktree (not the main repo)
3. Branch name shows the worktree's branch
4. Commit, stage, and push operations target the worktree

Switching between sessions triggers an automatic git status refresh.

## Directory Structure

A typical setup with worktrees:

```
~/Projects/quack-app/                  <- main repo
  .git/                                <- shared git data
  .worktrees/
    session-feature-auth-a1b2/         <- worktree 1
      .git                             <- file pointing to main .git
      src/                             <- separate working tree
      package.json
    session-hotfix-crash-c3d4/         <- worktree 2
      .git
      src/
      package.json
```

Each worktree has its own copy of the working files but shares the same `.git` database. This means commits, branches, and history are shared across all worktrees.

## Tips and Best Practices

### Naming Branches

Use clear, descriptive branch names. They become part of the worktree directory name:

**Good**: `feature/auth-flow`, `fix/dashboard-crash`

**Bad**: `test`, `temp`, `my-branch`

### Cleanup

Worktrees persist on disk even after sessions are closed. Periodically clean up unused worktrees:

```bash
# List all worktrees
git worktree list

# Remove a specific worktree
git worktree remove .worktrees/session-feature-auth-a1b2

# Prune stale worktree references
git worktree prune
```

### Disk Space

Each worktree is a full copy of your working tree (but NOT the git database). For large repos, multiple worktrees can use significant disk space. Remove worktrees you no longer need.

### Shared vs Isolated State

**Shared** across all worktrees:
- Git history (commits, branches, tags)
- Remote configuration
- Git hooks

**Isolated** per worktree:
- Working tree files
- Staged changes (index)
- HEAD (current branch/commit)

## Troubleshooting

### Worktree Already Exists Error

**Problem**: Creating a session fails with "branch is already used by worktree".

**Solution**: Quack automatically detects and reuses existing worktrees. If this error occurs, the detection failed. Try creating the session again, or manually check `git worktree list` for the existing worktree.

### Git Panel Shows Wrong Branch

**Problem**: The git panel shows the main repo's branch instead of the worktree's branch.

**Solution**: Click on the session to ensure it's the active session. The git panel updates based on the `effectiveGitRootPath`, which prioritizes the active session's worktree path.

### Worktree Files Out of Sync

**Problem**: A worktree doesn't have the latest changes from the main branch.

**Solution**: Navigate to the worktree directory and pull/merge:

```bash
cd .worktrees/session-feature-auth-a1b2
git merge main
```

### Cannot Delete Worktree Branch

**Problem**: Git refuses to delete a branch that's checked out in a worktree.

**Solution**: Remove the worktree first, then delete the branch:

```bash
git worktree remove .worktrees/session-feature-auth-a1b2
git branch -d feature/auth
```

## Related Features

- **[Branch per Session](../02-core-concepts/branch-per-session)**: How to create sessions with specific branches
- **[Project Grouping](../02-core-concepts/project-grouping)**: Group projects for cross-project context

---

**Previous**: [Code Graph MCP](./code-graph-mcp)

**Next**: [Project Management Commands](../04-best-practices/project-management-commands)
