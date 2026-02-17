Quack provides a powerful project management system through four global slash commands that integrate with the Kanban board and AI droids.

---

## Overview

| Command | Purpose | Use Case |
|---------|---------|----------|
| `/task` | Generic task | Any work item |
| `/bug` | Bug resolution | Fix issues with test coverage |
| `/feature` | New functionality | Create something new |
| `/improvement` | Enhance existing code | Refactoring, performance, UX |

All commands use the **quack-pm** skill and create tasks on the Kanban board (Cmd+K).

---

## The Core Workflow: Analyze-Plan-Act-Test-Review-Document

All commands follow a structured workflow with 7 phases:

1. **Analyze** - Understand existing code and context
2. **Plan** - Create detailed implementation plan
3. **Act** - Implement the solution
4. **Test** - Write and run tests
5. **Act** - Refine based on test results
6. **Review** - Code review for quality
7. **Document** - Save knowledge for future reference

---

## /task - Generic Tasks

The simplest command for any work item.

**Usage:**
```bash
/task Implement dark mode toggle
```

**Workflow:**
1. Discovery - Find available agents
2. Create task on Kanban
3. Assign appropriate droid

**Best for:** Quick tasks, miscellaneous work, one-off items.

---

## /bug - Bug Resolution

Specialized for fixing issues with a focus on root cause analysis and prevention.

**Usage:**
```bash
/bug Dropdown menu closes unexpectedly on mobile
```

**Workflow:**
1. **Analyze** with `code-explorer` droid
2. Identify root cause
3. **Implement fix**
4. **Write test** to prevent regression
5. **Document** solution in MCP Memory

**Key Features:**
- Always starts with code analysis
- Requires test to verify fix
- Automatically saves solution to Second Brain

---

## /feature - New Functionality

For creating something new from scratch.

**Usage:**
```bash
/feature Add user preferences panel with theme and language settings
```

**Workflow:**
1. **Analyze** - `code-explorer` examines codebase
2. **Plan** - Detailed implementation plan
3. **Act** - Implementation with droids:
   - Frontend: `frontend-developer`
   - Backend: `data-engineer`
4. **Test** - `test-engineer` writes tests
5. **Review** - `code-reviewer` validates
6. **Document** - Save to `.claude/docs/`

**Parallel Execution:**

For full-stack features, run droids in parallel:

```bash
/background @data-engineer Implement API endpoints for user preferences
/background @frontend-developer Implement UI for user preferences
```

**Droid Selection:**

| Feature Type | Primary Droid |
|--------------|---------------|
| UI/React | frontend-developer |
| API/Rust | data-engineer |
| Full-stack | code-explorer (then subtasks) |

---

## /improvement - Enhance Existing Code

For refactoring, performance optimization, UX improvements, and cleanup.

**Usage:**
```bash
/improvement Optimize the file tree rendering performance
```

**Key Difference from /feature:**

| Aspect | /feature | /improvement |
|--------|----------|--------------|
| Code | New | Existing |
| Risk | Low | Medium-High |
| Test first | No | **YES** |
| Benchmark | Optional | Required (if performance) |

**Workflow:**
1. **Analyze deeply** - Understand current implementation
2. **Test FIRST** - Verify existing tests pass
3. **Plan** - Incremental refactoring strategy
4. **Act** - Small, safe changes
5. **Test** - Verify no regressions
6. **Benchmark** - Measure improvements
7. **Review** - Validate changes

**Improvement Types:**

| Type | Focus | Droid |
|------|-------|-------|
| Refactoring | Code structure | code-explorer |
| Performance | Speed, memory | data-engineer |
| UX | Usability | frontend-developer |
| Cleanup | Tech debt | code-reviewer |
| Security | Vulnerabilities | code-reviewer |

**Golden Rule:** Existing tests must pass BEFORE and AFTER refactoring!

---

## Droids Reference

The commands automatically assign work to specialized droids:

| Droid | Specialty |
|-------|-----------|
| `code-explorer` | Analyze codebase, find patterns |
| `frontend-developer` | React, UI, state management |
| `data-engineer` | Backend, Rust, APIs, data |
| `test-engineer` | Vitest tests, coverage |
| `code-reviewer` | Code quality, security |
| `documentation-writer-expert` | Technical docs |
| `second-brain-manager` | MCP Memory storage |

---

## Parallel Execution with /background

Speed up work by running droids in parallel:

**Full-stack (backend + frontend):**
```bash
/background @data-engineer Implement backend for [feature]
/background @frontend-developer Implement UI for [feature]
```

**Test + Review together:**
```bash
/background @test-engineer Write tests for [feature]
/background @code-reviewer Review code for [feature]
```

**Documentation (non-blocking):**
```bash
/background @second-brain-manager Save pattern to MCP Memory
```

**When to use parallel:**
- Backend/Frontend independent → Parallel
- Tests depend on code → Sequential
- Review + Test → Parallel
- Documentation → Always parallel

---

## Best Practices

### Choosing the Right Command

- **Something new?** → `/feature`
- **Something broken?** → `/bug`
- **Something to improve?** → `/improvement`
- **Something quick/misc?** → `/task`

### Task Naming

- Use action verbs: "Implement", "Fix", "Optimize", "Add"
- Keep titles short (5-10 words)
- Be specific about scope

### Droid Selection

1. Start with `code-explorer` for analysis
2. Match implementation droid to tech stack
3. Always use `test-engineer` for tests
4. End with `code-reviewer` for validation

### Documentation

All completed work should be documented:
- Technical docs: `.claude/docs/[name].md`
- Patterns/solutions: MCP Memory (Second Brain)
- Use `second-brain-manager` droid

---

## Quick Start Example

**Creating a new settings feature:**

```bash
# 1. Create the feature task
/feature Add settings page with theme toggle and notification preferences

# 2. Monitor in Kanban (Cmd+K)

# 3. When analysis is done, run implementation in parallel
/background @data-engineer Implement settings API endpoints
/background @frontend-developer Implement settings UI components

# 4. After implementation, run test and review
/background @test-engineer Write tests for settings feature
/background @code-reviewer Review settings implementation

# 5. Document the feature
/background @second-brain-manager Document settings feature implementation
```

---

## See Also

- [Kanban Board](../02-core-concepts/kanban-board.md) - Visual task management
- [Background Tasks](../02-core-concepts/background-tasks.md) - Non-blocking execution
- [Second Brain](../02-core-concepts/second-brain.md) - Knowledge management
