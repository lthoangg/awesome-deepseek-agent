[English](./openagentd.md) | [简体中文](./openagentd.zh-CN.md) · [← Back](../README.md)

# Integrate with OpenAgentd

OpenAgentd is an open-source, mobile-first cockpit for local AI agents. It features a FastAPI backend, React Web UI, and cross-platform desktop/mobile Tauri shell with multi-agent orchestration, CLI, and native MCP support.

#### 1. Install OpenAgentd

Install OpenAgentd using `uv` or `pip`:

```bash
uv tool install openagentd
```

Or via `pip`:

```bash
pip install openagentd
```

Verify the installation:

```bash
openagentd status
```

> **Note:** Desktop and mobile app installers are also available on the [OpenAgentd Releases](https://github.com/openagentd/openagentd/releases) page.

#### 2. Configure DeepSeek Provider

OpenAgentd supports DeepSeek out of the box using direct API keys or keyless free models via OpenCode Zen (`opencode:deepseek-v4-flash-free`).

To configure direct DeepSeek API access:

1. Obtain an API Key from the [DeepSeek Platform](https://platform.deepseek.com/api_keys).
2. Set the `DEEPSEEK_API_KEY` environment variable:

**Linux / macOS**:
```bash
export DEEPSEEK_API_KEY="sk-..."
```

**Windows (PowerShell)**:
```powershell
$env:DEEPSEEK_API_KEY="sk-..."
```

Alternatively, configure the API key via the Web/Desktop UI in **Settings → Providers → DeepSeek** or add it to `~/.config/openagentd/.env`:

```env
DEEPSEEK_API_KEY=sk-...
```

#### 3. Select Model and Configure Agent

Agent configurations live in `~/.config/openagentd/agents/` as Markdown files with YAML frontmatter.

To set your lead agent model to DeepSeek V4:

Edit `~/.config/openagentd/agents/lead.md`:

```yaml
---
name: lead
description: Lead orchestrator agent
model: deepseek:deepseek-v4-flash
---
```

For complex reasoning tasks, use `deepseek-v4-pro`:

```yaml
---
name: lead
description: Lead orchestrator agent
model: deepseek:deepseek-v4-pro
---
```

OpenAgentd natively handles DeepSeek V4 features:
- Full **1M context window** (1,048,576 tokens).
- Thinking / reasoning mode support (`thinking: {type: "enabled"}`) and proper handling of reasoning content during agent tool calls.

#### 4. Run OpenAgentd

Launch the OpenAgentd backend service and Web Cockpit:

```bash
openagentd serve
```

Or open interactive CLI chat directly in your terminal:

```bash
openagentd chat
```

You can also switch models dynamically during a session from the UI agent settings or model picker.
