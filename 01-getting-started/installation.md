# Installation

Learn how to install and set up Quack on your machine.

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
