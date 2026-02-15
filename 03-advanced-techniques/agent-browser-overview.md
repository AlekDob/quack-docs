# Agent Browser Overview

Agent Browser is a fast, AI-optimized browser automation CLI built on Playwright. It enables Quack agents to interact with websites programmatically — navigate pages, fill forms, click buttons, take screenshots, and extract data.

## What It Is

Agent Browser (by Vercel Labs) is a command-line tool designed specifically for AI agents. It provides a streamlined interface for browser automation with 93% less context usage than Playwright MCP.

Key difference from traditional automation tools: agent-browser uses **element references** (`@e1`, `@e2`) instead of CSS selectors, making it easier for AI agents to interact with dynamic web content.

## Why Use It

Agent Browser unlocks new capabilities for your Quack agents:

- **Automated publishing**: Publish drafts to Medium, LinkedIn, or other platforms
- **Data collection**: Scrape structured data from websites
- **Form automation**: Fill out repetitive web forms
- **Testing**: Automate web app testing workflows
- **Screenshot capture**: Document web states for debugging

## Current Integrations

### Medium Writer

The `medium-writer` skill uses agent-browser to publish article drafts directly to Medium. After writing an article, an agent can:

1. Open Medium's new story page
2. Insert the title and body text
3. Save the draft for review
4. Let you add images and publish manually

This workflow saves significant time when publishing technical content.

## Key Capabilities

### Navigation
- Open URLs
- Navigate through multi-page workflows
- Wait for page loads and network idle states

### Interaction
- Click buttons and links using element references
- Fill form fields with text
- Select dropdown options
- Check/uncheck checkboxes
- Press keyboard keys

### Data Extraction
- Capture page screenshots (full or viewport)
- Extract text from specific elements
- Get current URL and page title
- Run custom JavaScript for complex extractions

### Session Management
- Persist cookies and localStorage across runs
- Maintain multiple parallel browser sessions
- Connect to your real Chrome browser for sites with bot protection

## How It Works

Agent Browser follows a simple workflow:

1. **Navigate** to the target page
2. **Snapshot** to get element references (`@e1`, `@e2`, etc.)
3. **Interact** using those references
4. **Re-snapshot** after page changes to get fresh references

```bash
agent-browser open https://example.com/form
agent-browser snapshot -i
# Output: @e1 [input "email"], @e2 [button] "Submit"

agent-browser fill @e1 "user@example.com"
agent-browser click @e2
```

The snapshot command returns a human-readable list of interactive elements, making it easy for AI agents to understand page structure.

## When to Use Agent Browser

Use agent-browser when:

- You need to interact with websites that don't have APIs
- You want to automate repetitive web tasks
- You're publishing content to platforms like Medium
- You need to test web applications
- You're collecting data from websites

Don't use it when:

- A REST API exists and is easier to use
- The task can be done with a simple HTTP request
- The website actively blocks automation (check terms of service)

## Next Steps

- [Setup and Installation](./agent-browser-setup) — Install agent-browser and configure CDP for protected sites
- [Medium Publishing](./agent-browser-medium) — Step-by-step guide to publish Medium drafts
