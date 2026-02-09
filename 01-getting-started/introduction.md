# Introduction to Quack

Welcome to **Quack** - your multi-agentic IDE powered by Claude Code!


## What is Quack?

Quack is a **multi-agentic IDE** built on top of Claude Code that revolutionizes how you work on software projects. Unlike traditional IDEs or AI assistants, Quack allows you to:

- Work on **multiple projects simultaneously** with different agents
- Run **multiple agents on the same project**, each focused on specific tasks
- Give each agent **multiple sessions** to work on different things in parallel
- Visualize all sessions on a **Kanban board** for full visibility
- Invoke **droids in swarm mode** within any session for specialized tasks

Think of Quack as your **AI development team** - where each agent is a team member with specific expertise, managing multiple workstreams across your codebase.

## The Quack Hierarchy

Everything in Quack follows a clear four-level hierarchy:

```
Project (a directory on disk)
└── Agent (an AI personality assigned to the project)
    └── Session (a conversation/task the agent works on)
        └── Droids (specialized workers invoked within the session)
```

### How it works in practice

Imagine you have a project called `my-app`. You assign **Agent Jack** (Project Manager) to it. Jack can have multiple sessions running at the same time:

- **Session 1**: "Implement user authentication" (in progress)
- **Session 2**: "Write API documentation" (todo)
- **Session 3**: "Fix login bug" (done)

Each session appears as a **card on the Kanban board**. Within any session, Jack can invoke **droids** - specialized subagents like `frontend-developer`, `test-engineer`, or `code-reviewer` - to handle specific parts of the work. Droids can even work in **swarm mode**, where multiple droids are invoked in parallel within the same session.

This means you can:
- Assign **multiple agents** to the same project (Jack for features, Sophie for product)
- Give each agent **multiple sessions** (parallel workstreams)
- Track everything on the **Kanban board** (Cmd+K)
- Let droids handle specialized work **inside each session**

## Getting Started: Onboarding

When you launch Quack for the first time, the **onboarding flow** guides you through setting up your first project and agents:

1. **Select a project** - Choose a directory on your machine
2. **Pick starter agents** - Select from pre-configured agent bundles (e.g., Project Manager, Product Manager, Personal Assistant)
3. **Automatic setup** - Quack installs the bundled skills, rules, and creates your agents ready to work

Starter agents come with **pre-configured personalities, skills, and rules** so you can be productive immediately. You can always customize them later or create new agents from scratch.

> **Note:** The onboarding screen only appears when you have no projects registered. Once you have at least one project, you'll see the regular workspace.

## Rules: Guiding Agent Behavior

**Rules** are behavioral guidelines that shape how your agents work. They are markdown files stored in your project's `.claude/rules/` folder and define:

- **Workflow patterns** (e.g., "Analyze before acting", "Test after implementing")
- **Code standards** (e.g., "Functions under 20 lines", "TypeScript strict mode")
- **Project conventions** (e.g., "Use conventional commits", "Document in the Second Brain")

When you create an agent (or use a starter bundle), you can assign specific rules. These rules are injected into the agent's `CLAUDE.md` header, so Claude follows them automatically during every conversation.

**Examples of rules:**
- `apatr-d` - Analyze, Plan, Act, Test, Review, Document workflow
- `use-quack-brain` - Use the Second Brain knowledge store actively

Rules can be installed from the **Marketplace** or created manually in `.claude/rules/`.

## Core Concepts

### 1. Projects

A **Project** is simply a directory on your machine (e.g., `/Users/you/projects/my-app`). Quack organizes everything by project - the sidebar groups your agents under their assigned project. You can work on multiple projects at the same time.

### 2. Agents (Your AI Team)

An **Agent** is an AI assistant with a unique personality, role, and equipment. Think of agents as **managers** - they coordinate work, make decisions, and delegate specialized tasks to droids.

When you create an agent, you define:
- **Name and Role**: Who is this agent? (e.g., "Agent Jack - Project Manager")
- **Communication style**: Professional, friendly, technical, creative
- **Custom notes**: Specific instructions for this agent's behavior
- **Equipment**: Which skills, droids, rules, and commands the agent can use

Agents are **cross-project** - you can reuse the same agent across different projects. The list of all your agents is stored centrally and shown when you create a new project.

### 3. Sessions (Parallel Workstreams)

A **Session** is a single conversation/task that an agent works on. This is what makes Quack truly powerful: **each agent can have multiple sessions**, allowing parallel work on different tasks.

Sessions have three states:
- **TODO** - Planned but not started yet
- **In Progress** - Currently being worked on
- **Done** - Completed

Every session tracks:
- Conversation history (managed by Claude SDK)
- Message count and token usage
- Cost tracking (input/output tokens)
- Initial prompt and attachments

**Sessions are the Kanban board.** Each session appears as a card on the board. You can:
- Create a new session from the Kanban board (assign it to any agent)
- Drag sessions between TODO, In Progress, and Done columns
- Click a session card to open the chat and continue the conversation
- Filter sessions by agent or project

### 4. Droids (Specialized Workers)

**Droids** are isolated subagents that handle specific tasks within a session. When an agent needs specialized work done (e.g., a complex git operation, a security audit, or a frontend component), it invokes a droid.

Key characteristics:
- Droids work in a **sandboxed environment** - they don't pollute the main conversation
- They execute their task and **return only what the agent needs**
- Multiple droids can be invoked **in parallel (swarm mode)** within a single session
- Examples: `git-commit-manager`, `frontend-developer`, `test-engineer`, `code-reviewer`, `swift-bug-hunter`

```
Agent Jack (Session: "Build login page")
   |
   +-- @frontend-developer  (builds the React component)
   +-- @test-engineer        (writes tests in parallel)
   +-- @code-reviewer        (reviews the final result)
```

Droids are installed from the **Marketplace** as `.md` files in `~/.claude/agents/` and are referenced in the agent's equipment (toolkit).

### 5. Skills (Modular Abilities)

**Skills** are modular capabilities that extend what agents and droids can do. They are **model-invoked** - Claude autonomously decides when to use them based on your request and the skill's description.

- Skills are packaged as **organized folders** containing instructions, scripts, and resources
- They define **how** to approach specific tasks with specialized knowledge
- Claude **discovers and uses them automatically** when relevant

**Examples:** `/commit` (smart git operations), `/code-review` (AI-powered review), `/background` (non-blocking execution)

## Storage Architecture

Quack stores data at three levels:

| Storage | Location | Purpose |
|---------|----------|---------|
| **Agent catalog + Sessions** | `quack-agents.json` in Tauri app data | Central, cross-project list of all agents, their sessions, and token usage |
| **Agent personality** | `<your-project>/.quack/agent-personalities/{id}.json` | Detailed personality config for CLAUDE.md injection, per-project |
| **Active header** | `<your-project>/CLAUDE.md` | The injected header that Claude reads at runtime |

**How it works:**
- The **agent catalog** (`quack-agents.json`) stores all your agents and sessions globally. This is the list you see when creating a new project and choosing "Use" on an existing agent.
- When you assign an agent to a project, Quack saves a **personality file** inside that project's `.quack/agent-personalities/` folder.
- Quack then **injects a personalized header** into the project's `CLAUDE.md` with the agent's name, role, communication style, custom notes, and selected rules.
- Each time you switch agents, the `CLAUDE.md` updates automatically.
- **Sessions** (Kanban tasks) are stored alongside agents in the same file - they are the source of truth that the Kanban board displays.

## The Kanban Board

Toggle the Kanban board with **Cmd+K** to see all your sessions organized visually.

```
 TODO              In Progress         Done
+---------------+ +---------------+  +---------------+
| Build login   | | Fix auth bug  |  | Setup CI/CD   |
| Agent Jack    | | Agent Jack    |  | Agent Sophie  |
| 0 messages    | | 24 messages   |  | 18 messages   |
+---------------+ +---------------+  +---------------+
| Write docs    |                     | Add dark mode |
| Agent Sophie  |                     | Agent Jack    |
| 0 messages    |                     | 42 messages   |
+---------------+                     +---------------+
```

- **Create tasks** from the board and assign them to any agent
- **Drag and drop** between columns to update status
- **Click a card** to open the chat drawer and continue the conversation
- **Filter by agent** to focus on one agent's workload
- **Track costs** with token usage displayed per session

## Real-Time Agent Monitoring

### Live Activity View

- See **what each agent is working on** at a glance
- Monitor **progress and status** across all active sessions
- Switch between agents instantly without losing context

### Smart Notifications

Never miss when an agent completes a task! Quack notifies you through multiple channels:

- **Quack Sound** - A distinctive audio alert when an agent finishes
- **macOS Notification** - Native system notification with task summary
- **Telegram Integration** - Get notified on your phone, wherever you are

This means you can **start multiple agents on different tasks**, go grab a coffee, and get pinged the moment any of them needs your attention.

## Why Quack?

### True Multi-Agent, Multi-Session Workflow

```
Project A                         Project B
|                                 |
+-- Agent Jack                    +-- Agent Max
|   +-- Session: Build auth       |   +-- Session: Refactor API
|   +-- Session: Fix bug #42      |   +-- Session: Add caching
|   +-- Session: Write tests      |
|                                 +-- Agent Doc
+-- Agent Sophie                      +-- Session: Update README
    +-- Session: Product review       +-- Session: API docs
    +-- Session: User research
```

Each agent maintains its own:
- Personality and focus area
- Multiple parallel sessions
- Skill set and droid access
- Token usage and cost tracking

### Parallel Development at Every Level

- **Multiple projects** open simultaneously
- **Multiple agents** per project with different specializations
- **Multiple sessions** per agent for parallel workstreams
- **Multiple droids** per session working in swarm mode

### Context Isolation

Droids ensure clean separation:
- Main agent stays focused on high-level decisions
- Complex tasks are delegated without cluttering context
- Results are synthesized and returned cleanly
- Token usage is optimized

## Who is Quack For?

**Solo Developers** who want to:
- Multiply their productivity with specialized agents
- Work on multiple aspects of a project in parallel
- Build a personal AI development team

**Teams** looking for:
- Consistent agent configurations across developers
- Specialized agents for different roles (QA, Security, Docs)
- Scalable AI-assisted workflows

**Claude Code Power Users** who need:
- Better orchestration of AI capabilities
- Visual management of multiple agent sessions
- Advanced customization of agent behaviors

## Getting Started

Ready to build your AI development team? Continue to the [Installation Guide](./installation) to set up Quack on your machine.

Or jump to [First Steps](./first-steps) to create your first agent and learn the basics.

**Next**: [Installation ->](./installation)
