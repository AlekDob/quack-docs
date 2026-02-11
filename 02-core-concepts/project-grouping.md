# Project Grouping

Project Grouping lets you link related projects together so your AI agents know about sibling projects. When projects are grouped, each project's CLAUDE.md is automatically updated with cross-project context, and the sidebar shows them visually connected.

## Why Use Project Grouping?

When you work on related projects (e.g., a desktop app and its marketing website), each AI agent session runs in isolation. The agent working on `quack-app` has no idea that `quackagency-website` exists.

Project Grouping solves this by:

- **Injecting cross-project context** into each project's CLAUDE.md
- **Visually grouping** projects in the sidebar with colored dashed borders
- **Enabling cross-project teams** where agents from different projects collaborate

## Creating a Group

### Requirements

You need at least **2 open projects** in the sidebar to create a group.

### Steps

1. Look for the **Group** button in the sidebar header (next to "New project")
2. Click it to open the Group Creation modal
3. Fill in the details:
   - **Group Name**: A descriptive name (e.g., "Quack Ecosystem")
   - **Color**: Pick a color for the group's visual border
   - **Projects**: Select which projects to include (minimum 2)
   - **Roles** (optional): Assign a role label to each project (e.g., "Desktop App", "Marketing Site")
4. Click **Create Group**

### What Happens After Creation

When you create a group, two things happen automatically:

**1. Visual grouping in sidebar**

```
  v QUACK ECOSYSTEM   2 projects
  |  v quack-app                  |
  |    Agent Graydon              |
  |    Agent Sophie               |
  |  v quackagency-website        |
  |    Agent Alex                 |
  +-------------------------------+
```

Projects inside the group are wrapped with a **dashed border** in the group's color.

**2. CLAUDE.md injection**

Each project's CLAUDE.md receives a new section:

```markdown
<!-- QUACK_GROUP_CONTEXT_START -->
## Project Group: Quack Ecosystem

This project belongs to a multi-project group.
You have access to sibling projects:

| Project | Path | Role |
|---------|------|------|
| quack-app **(current)** | /path/to/quack-app | Desktop App |
| quackagency-website | /path/to/website | Marketing Site |

When working cross-project, read the sibling
project's CLAUDE.md for context.
<!-- QUACK_GROUP_CONTEXT_END -->
```

Now when an agent starts a session in `quack-app`, Claude automatically knows about `quackagency-website` and can read its CLAUDE.md for context.

## Managing Groups

### Collapsing a Group

Click the **chevron** on the group header to collapse or expand the group. Collapsed groups show only the header with the project count.

### Removing a Project from a Group

Right-click the group header to open the context menu, then select **Remove [project name]**.

- The project returns to a standalone position in the sidebar
- Its CLAUDE.md is cleaned (the group context section is removed)
- If fewer than 2 projects remain, the group is automatically disbanded

### Disbanding a Group

You can disband a group in two ways:

**Hover**: Move your mouse over the group header. A small **X** icon appears. Click it.

**Right-click**: Open the context menu and select **Disband group** (shown in red).

When you disband a group:

1. The group context block is removed from every project's CLAUDE.md
2. The group data folder (`~/.quack/groups/{id}/`) is deleted
3. Projects return to standalone positions in the sidebar

## How Context Injection Works

### Placement Priority

The group context block is inserted in your CLAUDE.md following this priority:

1. After `<!-- QUACK_TEAM_ROSTER_END -->` (if a team roster exists)
2. After `<!-- QUACK_AGENT_HEADER_END -->` (if an agent header exists)
3. At the top of the file (if neither marker exists)

### Automatic Sync

Group contexts are synced automatically at app startup. If you edit CLAUDE.md manually and accidentally remove the group section, it will be re-injected on next launch.

### Lifecycle

| Action | Effect on CLAUDE.md |
|--------|-------------------|
| Create group | Injects context into all member projects |
| Update group | Re-injects updated context (removes old, adds new) |
| Delete group | Removes context block from all member projects |
| App startup | Syncs all group contexts to ensure consistency |

## Persistence

Groups persist across app restarts:

- **Storage**: `~/.quack/groups/{id}/group.json`
- **Loading**: Groups are loaded when the sidebar mounts
- **Sync**: After loading, `sync_group_contexts` ensures all CLAUDE.md files are up to date

## Tips and Best Practices

### Effective Grouping

**Good**: Group projects that share context and benefit from cross-referencing.
```
"Quack Ecosystem"
  - quack-app (Desktop App)
  - quackagency-website (Marketing Site)
```

**Bad**: Group unrelated projects just because they're open.
```
"Random stuff"
  - personal-blog
  - company-erp
```

### Role Labels

Use role labels to give agents more context about each project's purpose. Instead of generic "member", use descriptive labels like "Backend API", "Frontend App", "Documentation Site".

### Cross-Project Teams

Project groups pair well with Agent Teams. When agents from different grouped projects form a team, they can reference each other's CLAUDE.md for deeper context.

## Troubleshooting

### Group Context Not Appearing in CLAUDE.md

**Problem**: You created a group but don't see the context section in your project's CLAUDE.md.

**Solution**: Restart the app. The `sync_group_contexts` command runs at startup and will inject any missing context blocks.

### Group Disappeared After Restart

**Problem**: Your group is not showing in the sidebar after restarting.

**Solution**: Check that `~/.quack/groups/` contains your group's folder with `group.json`. If the file is missing, the group was likely disbanded.

## Related Features

- **[Branch per Session](./branch-per-session)**: Manage branches at the session level within grouped projects
- **[Side Panel](./side-panel)**: Agent context and project navigation
- **[Kanban Board](./kanban-board)**: Task management across grouped projects

---

**Previous**: [AI Image Generation](./ai-image-generation)

**Next**: [Branch per Session](./branch-per-session)
