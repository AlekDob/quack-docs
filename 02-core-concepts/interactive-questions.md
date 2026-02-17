Interactive Questions let AI agents pause and ask you for clarification when they encounter ambiguous situations. Instead of guessing or making assumptions, the agent presents you with clear choices, waits for your answer, and continues with full context.

## Why Interactive Questions Matter

Traditional AI assistants often guess when faced with ambiguity:

**The Problem:**
```
You: "Add a database to this project"

Agent: *Assumes PostgreSQL, installs it, configures it*

You: "I wanted MongoDB..."
```

**With Interactive Questions:**
```
You: "Add a database to this project"

Agent: "Which database would you like to use?"
        ○ PostgreSQL (Relational, ACID-compliant)
        ○ MongoDB (Document-based, flexible schema)
        ○ SQLite (Lightweight, embedded)

You: *Selects MongoDB*

Agent: *Installs MongoDB with correct configuration*
```

## How It Works

When an agent needs clarification, it:

1. **Pauses execution** - Work stops until you respond
2. **Shows questionnaire UI** - Clean, focused interface
3. **Presents clear options** - Each with helpful descriptions
4. **Waits for selection** - No timeout, take your time
5. **Continues with context** - Uses your choice to proceed correctly

## The Question Interface

### Question Card Layout

When the agent asks a question, you'll see:

```
┌─────────────────────────────────────────────────────┐
│  Which state management library?                    │
├─────────────────────────────────────────────────────┤
│  ○ Redux Toolkit                                    │
│    Full-featured with DevTools and middleware       │
│                                                      │
│  ○ Zustand                                          │
│    Lightweight and simple API                       │
│                                                      │
│  ○ Jotai                                            │
│    Atomic state management                          │
│                                                      │
│  [Submit Answer]                                    │
└─────────────────────────────────────────────────────┘
```

### Components

Each question includes:

- **Header**: The question being asked
- **Options**: Radio buttons (single choice) or checkboxes (multiple choice)
- **Descriptions**: Context for each option
- **Submit button**: Confirm your selection

### Single vs Multiple Choice

**Single Choice:**
- Radio buttons (○)
- Pick exactly one option
- Used for mutually exclusive choices

**Multiple Choice:**
- Checkboxes (☐)
- Pick one or more options
- Used for features, plugins, or settings

## When Agents Ask Questions

Agents use Interactive Questions for:

### Technology Choices

```
Question: "Which testing framework should I use?"
Options:
  ○ Vitest - Fast, Vite-integrated
  ○ Jest - Battle-tested, wide ecosystem
  ○ Playwright - End-to-end testing
```

### Implementation Approaches

```
Question: "How should I implement authentication?"
Options:
  ○ JWT tokens - Stateless, scalable
  ○ Session cookies - Server-side, secure
  ○ OAuth2 - Third-party integration
```

### Feature Preferences

```
Question: "Which features should I include?"
Options:
  ☑ Dark mode toggle
  ☑ Export to PDF
  ☐ Email notifications
  ☑ Keyboard shortcuts
```

### Destructive Actions

```
Question: "This will delete 15 files. Proceed?"
Options:
  ○ Yes, delete them
  ○ No, show me the files first
  ○ Cancel the operation
```

## Using Interactive Questions

### Responding to Questions

1. **Read the question carefully** - Understand what's being asked
2. **Review all options** - Check descriptions for details
3. **Make your selection** - Click the radio button or checkbox
4. **Submit your answer** - Click the submit button

**The agent won't continue until you respond.**

### Best Practices

**Take your time:**
- No rush - the agent waits patiently
- Read option descriptions
- Consider implications of each choice

**Ask for more info if needed:**
- Type a message before submitting
- Ask the agent to explain options further
- Request pros/cons if unclear

**Change your mind:**
- Select a different option before submitting
- Only the submitted answer is final

## Examples in Action

### Example 1: New Feature Implementation

**Your Prompt:**
```
Add user profiles to the app
```

**Agent Questions:**

**Question 1:**
```
Where should profile data be stored?
  ○ Local Storage (offline-first, no backend)
  ○ Supabase (cloud database, real-time)
  ○ Custom API (full control, more setup)
```

**You select:** Supabase

**Question 2:**
```
Which profile fields should be editable?
  ☑ Display name
  ☑ Avatar image
  ☑ Bio
  ☐ Email (managed separately)
  ☑ Social links
```

**You select:** Display name, Avatar, Bio, Social links

**Result:** Agent builds exactly what you need, no wasted effort.

### Example 2: Code Refactoring

**Your Prompt:**
```
Refactor the data fetching logic
```

**Agent Question:**
```
I can refactor this in several ways:
  ○ Extract to custom hooks (React best practice)
  ○ Use SWR library (caching + revalidation)
  ○ Switch to TanStack Query (powerful data management)
  ○ Keep current approach but optimize
```

**You select:** Extract to custom hooks

**Result:** Clean refactor that fits your architecture.

### Example 3: Security Review

**Your Prompt:**
```
Review API endpoints for security issues
```

**Agent Question:**
```
I found 3 potential issues. How should I proceed?
  ○ Fix all automatically (may break things)
  ○ Show me each issue first (recommended)
  ○ Create a security report only
  ○ Fix critical issues, report others
```

**You select:** Fix critical issues, report others

**Result:** Safe fixes with full visibility.

## Advanced Features

### Contextual Questions

The agent considers:
- **Project context**: Your existing tech stack
- **Previous answers**: Earlier choices in the conversation
- **Best practices**: Industry standards

This means questions are relevant and options are appropriate.

### Follow-up Questions

After your answer, the agent might ask follow-up questions:

```
You selected: "Supabase"

Follow-up: "Should I create the Supabase schema now?"
  ○ Yes, create tables and policies
  ○ No, I'll do it manually
```

### Conditional Logic

Some options trigger different paths:

```
Question: "This requires a paid API key. Proceed?"
  ○ Yes, I have an API key → Continues setup
  ○ No, use free alternative → Switches to different approach
  ○ Cancel → Stops the task
```

## Integration with Workflows

### In Regular Chat

Questions appear inline in the conversation:
- Agent explains what it needs
- Question card displays
- You answer
- Agent continues seamlessly

### In Kanban Tasks

When a Kanban task agent asks a question:
- Chat drawer shows the question
- Task status remains "In Progress"
- Progress bar pauses
- Resumes after you answer

### In Background Tasks

Background agents can ask questions too:
- Desktop notification alerts you
- Question appears in chat stream
- Task pauses until you respond
- Continues automatically after answer

## Tips for Better Interactions

### Writing Prompts That Trigger Good Questions

**Be intentionally vague when you want options:**

```
"Add authentication" → Agent asks which method
"Improve performance" → Agent asks which areas to focus
"Fix the bug" → Agent asks for reproduction steps
```

**Be specific when you know what you want:**

```
"Add JWT authentication with refresh tokens"
"Optimize the database queries in UserService"
"Fix the dropdown menu z-index issue"
```

### Encouraging Agent Questions

Some agents are more proactive about asking. To encourage questions:

```
You: "Add a payment system. Ask me questions if anything is unclear."
```

Or in agent personality settings:
```
"Always ask for clarification before making technology choices."
```

## Keyboard Shortcuts

| Shortcut | Action |
|----------|--------|
| `1-9` | Select option 1-9 (when question is focused) |
| `Space` | Toggle checkbox for current option |
| `Enter` | Submit answer |
| `Escape` | Collapse question (doesn't cancel) |

## Troubleshooting

### Question Doesn't Appear

**Cause**: Agent made an assumption instead

**Solution**:
- Be more vague in your prompt
- Add "Ask me questions if you need clarification"
- Check agent personality settings

### Can't Submit Answer

**Cause**: No option selected (single choice questions)

**Solution**:
- Click one of the radio buttons
- Submit button becomes active

### Want to Change Answer After Submitting

**Cause**: Answer already sent to agent

**Solution**:
- Send a follow-up message: "Actually, let's use MongoDB instead"
- Agent will adjust its approach
- Or use `/cancel` to restart

### Too Many Questions

**Cause**: Agent is being overly cautious

**Solution**:
- Give more specific prompts
- Add context in your message
- Update agent instructions to "minimize questions for experienced users"

## Related Features

- **Chat Streaming**: Real-time conversation with agents
- **Agent Personalities**: Customize how agents communicate
- **Background Tasks**: Agents can ask questions even in background

---

**Previous**: [Task Progress Tracking](./task-progress-tracking)

**Next**: [AI Image Generation](./ai-image-generation)
