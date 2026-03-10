This guide shows you how to use alternative AI models with Claude Code and Quack — from free cloud models via Ollama to paid coding plans from Chinese AI labs. Save your Claude quota for production work, and run experiments on cheaper (or free) models.

## Why Use Alternative Models?

Claude is unmatched for complex architecture and production code. But experiments, side projects, and quick iterations burn through your quota fast. Alternative models let you:

- **Extend your Claude Max plan** to last the full month
- **Run experiments for free** via Ollama's cloud tier
- **Get coding plans from $3/month** with surprisingly capable models

## Method 1: Quack GUI (Recommended)

Quack has native multi-provider support. No terminal commands needed.

### Step 1: Open Settings

Click **Settings** in the bottom-left corner, then navigate to **Claude Code**.

### Step 2: Select Provider

Under **LLM Provider**, change the **Provider** dropdown from `Anthropic` to `Ollama (Local)`.

![Quack Settings — LLM Provider set to Ollama with kimi-k2.5:cloud selected](/images/screenshots/quack-ollama-settings.png)

The **Base URL** auto-fills to `http://localhost:11434`. If Ollama is running, you'll see a green **Connected** status.

### Step 3: Pick a Model

Choose from the **Model** dropdown or type a model name manually. Cloud models (hosted by Ollama) have the `:cloud` suffix:

- `kimi-k2.5:cloud` — Best for TypeScript/React work
- `minimax-m2.5:cloud` — Fast code reviews and refactoring
- `glm-5:cloud` — Solid all-rounder

### Step 4: Start a New Chat

The provider switch takes effect on the next chat. You'll see the model name in the status bar at the bottom.

![Quack chat with Ollama provider — kimi-k2.5:cloud shown in status bar](/images/screenshots/quack-provider-switch.png)

> **Important**: You cannot switch providers mid-session. Always start a fresh chat when changing models.

---

## Method 2: Claude Code CLI

If you prefer the terminal, two environment variables are all you need.

### Prerequisites

Install Ollama from [ollama.com](https://ollama.com):

**macOS:**
```bash
brew install ollama
```

**Linux:**
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

**Windows:** Download the installer from ollama.com.

### Sign In (Required for Cloud Models)

Create an account on ollama.com, then:

```bash
ollama signin
```

### Verify Ollama Is Running

```bash
curl http://localhost:11434/api/tags
```

You should see a JSON response with available models.

### Launch Claude Code with an Alternative Model

```bash
ANTHROPIC_BASE_URL=http://localhost:11434 ANTHROPIC_AUTH_TOKEN=ollama claude --model kimi-k2.5:cloud
```

Claude Code connects to Ollama instead of Anthropic. Same interface, same tools — different brain.

### Save Yourself Some Typing

Add an alias to your `~/.zshrc` (or `~/.bashrc`):

```bash
alias claude-ollama='ANTHROPIC_BASE_URL=http://localhost:11434 ANTHROPIC_AUTH_TOKEN=ollama claude'
```

Then:

```bash
claude-ollama --model minimax-m2.5:cloud
```

---

## Recommended Models

### Kimi K2.5 (Moonshot AI, Beijing)

```bash
ollama run kimi-k2.5:cloud
```

**Best for:** TypeScript, React components, code pattern understanding. Moments where you forget you're not using Claude.

### MiniMax M2.5 (Shanghai)

```bash
ollama run minimax-m2.5:cloud
```

**Best for:** Fast responses, code reviews, refactoring. Solid reasoning for quick tasks.

### GLM-5 (Zhipu AI)

```bash
ollama run glm-5:cloud
```

**Best for:** General tasks, documentation, analysis. Consistently good at everything.

---

## Going Serious: Paid Coding Plans

When you need guaranteed availability and higher rate limits, each provider offers dedicated subscriptions.

### GLM (Zhipu AI / Z.ai) — From $3/month

The cheapest option. Visit [z.ai/subscribe](https://z.ai/subscribe):

| Plan | Price | Prompts | Hours |
|------|-------|---------|-------|
| Lite | $3/month | 120 | 5 |
| Pro | $15/month | 600 | 5 |

```bash
ANTHROPIC_BASE_URL=https://api.z.ai/api/anthropic \
ANTHROPIC_AUTH_TOKEN=your-zhipu-api-key \
claude --model glm-4.7
```

### MiniMax — From $10/month

Visit [platform.minimax.io](https://platform.minimax.io):

| Plan | Price | Prompts | Hours |
|------|-------|---------|-------|
| Starter | $10/month | 100 | 5 |
| Plus | $20/month | 300 | 5 |
| Max | $50/month | 1000 | 5 |

```bash
ANTHROPIC_BASE_URL=https://api.minimax.io/anthropic \
ANTHROPIC_AUTH_TOKEN=your-minimax-api-key \
claude --model MiniMax-M2.5
```

### Kimi (Moonshot AI) — Pay Per Token

No subscription — pay as you go:

- **Input:** $0.60 / million tokens
- **Output:** $2.50 / million tokens

For comparison, Claude Opus charges $5/$25 per million tokens. Kimi is ~10x cheaper.

```bash
ANTHROPIC_BASE_URL=https://api.moonshot.ai/anthropic \
ANTHROPIC_AUTH_TOKEN=your-moonshot-api-key \
claude --model kimi-k2.5
```

---

## Cost Comparison

| Provider | Monthly Cost | Best For |
|----------|-------------|----------|
| Claude Code Max | ~$90/month | Production code, architecture |
| MiniMax Starter | $10/month | Experiments, side projects |
| GLM Lite | $3/month | Budget option, surprisingly capable |
| Kimi (pay-per-token) | ~$5-15/month | Top-tier Chinese model |
| Ollama free tier | $0 | Free cloud models, rate-limited |

**Recommended setup:** Claude Max for production + MiniMax Starter ($10) for experiments. Total: ~$100/month for practically unlimited AI coding.

---

## The Sweet Spot

- **Chinese models** → experiments, side projects, quick iterations
- **Claude** → production code, architecture, the stuff that matters

Not a replacement. A seriously good complement.

---

## Gotchas

1. **No mid-session switching.** Start a fresh chat when changing providers. Mixing providers causes invalid thinking block signature errors.
2. **Cloud models need `ollama signin`.** Without it, you only get local models.
3. **Non-Claude models may have reduced context**, no extended thinking, and variable tool-use quality. Quack shows a warning banner about this.
4. **Rate limits on free tier.** Ollama's cloud models are rate-limited. For heavy use, get a paid plan.