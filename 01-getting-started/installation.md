Learn how to install and set up Quack on your machine.

## Before You Start

Quack is built on top of **Claude Code**, Anthropic's AI coding agent. Before installing Quack, you need to set up three things: Node.js, an Anthropic account with an active subscription, and the Claude Code CLI.

### 1. Install Node.js

Quack requires **Node.js 22 or later**. The easiest way to install it is from the official website.

Go to [nodejs.org](https://nodejs.org) and download the **LTS (Long Term Support)** version.

**macOS**:
1. Download the macOS installer (`.pkg` file) from [nodejs.org](https://nodejs.org)
2. Open the downloaded file and follow the installation wizard
3. Verify the installation by opening a terminal and running:
   ```bash
   node --version
   npm --version
   ```

**Windows**:
1. Download the Windows installer (`.msi` file) from [nodejs.org](https://nodejs.org)
2. Run the installer and follow the setup steps (leave all default options checked)
3. Open Command Prompt or PowerShell and verify:
   ```bash
   node --version
   npm --version
   ```

Both commands should print a version number. If they do, Node.js is ready.

### 2. Get an Anthropic Subscription

Quack uses Claude Code under the hood, which requires a **Claude Pro or Team plan** from Anthropic.

:::callout[info]
A free Anthropic account is not sufficient to run Claude Code. You need an active **Pro** or **Team** subscription.
:::

1. Go to [console.anthropic.com](https://console.anthropic.com)
2. Create an account or sign in
3. Subscribe to the **Pro** or **Team** plan
4. Once subscribed, you are ready to authenticate Claude Code in the next step

### 3. Install and Authenticate Claude Code CLI

Claude Code is the CLI that Quack uses to run AI agents. Install it globally with npm:

```bash
npm install -g @anthropic-ai/claude-code
```

After installation, authenticate with your Anthropic account:

```bash
claude login
```

This opens a browser window where you log in with the same account you subscribed with. Once authenticated, Claude Code is ready.

:::callout[info]
For full Claude Code documentation, visit [docs.anthropic.com/en/docs/claude-code](https://docs.anthropic.com/en/docs/claude-code).
:::

---

## System Requirements

Before installing Quack, ensure your system meets these requirements:

### Operating System
- **macOS** 10.15 (Catalina) or later (currently the only supported platform)

### Software Requirements
- **Node.js** 18.17.0 or higher
- **npm** (comes with Node.js)
- **Rust** 1.77.2 or higher (for building from source)

## Download Quack

### Option 1: Pre-built Binaries (Recommended)

Download the latest release for your platform:

**macOS**:
1. Download the DMG file from GitHub Releases
2. Open the downloaded DMG file
3. Drag Quack into your Applications folder
4. Launch Quack from Applications

**Note**: quack-app repository is currently private. Contact the team for access to the DMG file.

## First Launch

After launching Quack for the first time:

1. **Grant permissions** when prompted (terminal access, file system)
2. **Create your first agent** (see below)

### Setting up Your First Agent

Quack is a multi-agentic IDE, so you need to create at least one agent to start working:

**Step 1: Create an Agent**
1. Click the **"+"** button in the Agents panel
2. Configure your agent:
   - **Name**: Give your agent a meaningful name (e.g., "Frontend Dev", "Code Reviewer")
   - **Personality**: Define the agent's role and behavior
   - **API Key**: Enter your Anthropic API key from [console.anthropic.com](https://console.anthropic.com)
   - **Skills**: Select which skills the agent should have access to
   - **Droids**: Choose which droids (subagents) the agent can use
3. Click **"Create Agent"**

**Step 2: Login to Claude**
1. Open a terminal in your project directory
2. Run the Claude login command:
   ```bash
   claude /login
   ```
3. Follow the authentication flow

**Step 3: Test Your Setup**
1. Navigate to the Chat panel
2. Send a message to your agent
3. Try asking: "Can you help me understand this project?"

## Verify Installation

To verify Quack is working correctly:

1. Open a new terminal tab (Cmd/Ctrl + T)
2. Run a simple command: `echo "Hello Quack!"`
3. Ask Claude a question in the chat panel
4. Check that file explorer shows your project files

If everything works, you're ready to start using Quack!

## Troubleshooting

### Terminal Not Working

If terminals aren't launching:
- **macOS**: Grant Terminal access in System Preferences > Security & Privacy > Privacy > Developer Tools
- Check shell configuration in `~/.bashrc` or `~/.zshrc`
- Restart Quack after granting permissions

### Claude Authentication Issues

If `claude /login` fails:
- Verify your API key is correct in the agent configuration
- Check you have credits in your Anthropic account
- Ensure you're connected to the internet
- Try creating a new agent with a fresh API key

### File Explorer Not Showing Files

If file explorer is empty:
- Navigate to a project directory using the path input
- Check file permissions
- Try refreshing (Cmd/Ctrl + R)

---

**Next**: [First Steps →](./first-steps)
**Previous**: [← Introduction](./introduction)
