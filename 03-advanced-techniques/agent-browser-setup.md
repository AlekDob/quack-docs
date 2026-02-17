This guide walks you through installing agent-browser and configuring it for use with Cloudflare-protected sites like Medium.

## Prerequisites

- Node.js 18 or higher
- npm (comes with Node.js)
- Google Chrome (for CDP connection to protected sites)

## Installation

Install agent-browser globally via npm:

```bash
npm install -g agent-browser
```

This makes the `agent-browser` command available system-wide.

### Verify Installation

Check that agent-browser is installed correctly:

```bash
agent-browser --version
```

You should see a version number (e.g., `1.0.0`).

### Find the Binary Location

On macOS ARM (Apple Silicon):
```bash
which agent-browser
# Output: /opt/homebrew/bin/agent-browser
```

On macOS Intel:
```bash
which agent-browser
# Output: /usr/local/bin/agent-browser
```

If `which agent-browser` returns nothing, the npm global bin directory may not be in your PATH. Fix it with:

```bash
export PATH="$(npm config get prefix)/bin:$PATH"
```

Add this line to your `~/.zshrc` or `~/.bashrc` to make it permanent.

## Basic Usage Test

Test agent-browser with a simple navigation:

```bash
agent-browser open https://example.com
agent-browser snapshot -i
agent-browser close
```

This should open a headless browser, take a snapshot, and close.

## CDP Setup for Cloudflare-Protected Sites

Sites like Medium, LinkedIn, and others use Cloudflare bot protection that blocks Playwright's bundled Chromium browser. To automate these sites, you need to connect agent-browser to your real Chrome browser via CDP (Chrome DevTools Protocol).

### Why CDP?

Cloudflare fingerprints browsers and detects automation tools like Playwright. Your real Chrome browser passes these checks because it has:

- Real Chrome extensions
- Authentic user profile data
- Normal browser fingerprints
- No WebDriver flags

CDP lets agent-browser control your real Chrome remotely while maintaining these fingerprints.

### Step 1: Close Chrome Completely

Quit Chrome entirely (not just close windows):

**macOS**: Press `Cmd+Q` or Chrome menu → Quit

**Windows**: File → Exit

Make sure Chrome is not running in the background. Check Activity Monitor (macOS) or Task Manager (Windows) if unsure.

### Step 2: Launch Chrome with Remote Debugging

Reopen Chrome with debugging enabled:

**macOS**:
```bash
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome \
  --remote-debugging-port=9222 \
  --user-data-dir=/tmp/chrome-debug
```

**Windows**:
```powershell
"C:\Program Files\Google\Chrome\Application\chrome.exe" ^
  --remote-debugging-port=9222 ^
  --user-data-dir=C:\Temp\chrome-debug
```

**Linux**:
```bash
google-chrome \
  --remote-debugging-port=9222 \
  --user-data-dir=/tmp/chrome-debug
```

### Step 3: Log Into the Target Site

In the Chrome window that just opened, navigate to the site you want to automate (e.g., Medium.com) and log in manually using your normal credentials.

This authenticates your session. All agent-browser commands will use this logged-in state.

### Step 4: Verify CDP Connection

Test that agent-browser can connect:

```bash
curl -s http://localhost:9222/json/version
```

You should see JSON output with browser version info:

```json
{
  "Browser": "Chrome/120.0.6099.129",
  "Protocol-Version": "1.3",
  "User-Agent": "Mozilla/5.0 ...",
  "WebKit-Version": "537.36"
}
```

If you get a connection error, Chrome didn't start with debugging enabled. Go back to Step 1.

### Step 5: Use CDP Flag in Commands

All agent-browser commands must include `--cdp 9222` **before** the command name:

```bash
agent-browser --cdp 9222 open https://medium.com
agent-browser --cdp 9222 snapshot -i
agent-browser --cdp 9222 click @e1
```

The flag goes before the command, not after arguments.

## Troubleshooting

### "session already exists" Error

Agent-browser maintains browser sessions. If you see this error:

```bash
agent-browser close
```

Then retry your command.

### Chrome Won't Start with --remote-debugging-port

Make sure:
- Chrome is completely closed first (check Activity Monitor/Task Manager)
- You're using `--user-data-dir=/tmp/chrome-debug` (Chrome refuses debugging on default profile)
- Port 9222 is not in use by another process

### agent-browser Command Not Found

The npm global bin directory is not in your PATH. Fix:

```bash
export PATH="$(npm config get prefix)/bin:$PATH"
```

Add to `~/.zshrc` or `~/.bashrc` for persistence.

### CDP Connection Refused

Check that Chrome is running with debugging:

```bash
lsof -i :9222
```

Should show a Chrome process listening on port 9222.

If not, Chrome didn't start correctly. Close and restart with the debugging flags.

### "Something is wrong" Error on Medium

This happens when using `fill` or `type` commands on Medium's contenteditable editor. Always use `eval` with `document.execCommand('insertText')` instead. See [Medium Publishing Guide](./agent-browser-medium) for details.

## Next Steps

- [Medium Publishing Guide](./agent-browser-medium) — Automate Medium draft publishing
- [Agent Browser Skill Reference](/.claude/skills/agent-browser) — Full command reference

---

**Previous**: [Agent Browser Overview](./agent-browser-overview)
**Next**: [Medium Publishing with Agent Browser](./agent-browser-medium)
