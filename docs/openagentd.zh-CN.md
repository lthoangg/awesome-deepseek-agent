[English](./openagentd.md) | [简体中文](./openagentd.zh-CN.md) · [← Back](../README.md)

# 接入 OpenAgentd

OpenAgentd 是一个开源的移动优先本地 AI Agent 控制台（Cockpit）。它包含 FastAPI 后端、React Web UI 以及基于 Tauri 的跨平台桌面端和移动端，原生支持多 Agent 协同、命令行交互与 MCP 协议。

#### 1. 安装 OpenAgentd

可以通过 `uv` 或 `pip` 安装 OpenAgentd：

```bash
uv tool install openagentd
```

或者使用 `pip`：

```bash
pip install openagentd
```

验证安装是否成功：

```bash
openagentd status
```

> **说明：** 桌面端与移动端应用安装包可在 [OpenAgentd Releases](https://github.com/openagentd/openagentd/releases) 页面下载。

#### 2. 配置 DeepSeek 提供商

OpenAgentd 原生支持 DeepSeek，既可以使用自备 API Key 直连，也支持开箱即用的免 Key 免费模型（`opencode:deepseek-v4-flash-free`）。

配置 DeepSeek 官方 API Key 直连步骤如下：

1. 前往 [DeepSeek 开放平台](https://platform.deepseek.com/api_keys) 获取 API Key。
2. 设置 `DEEPSEEK_API_KEY` 环境变量：

**Linux / macOS**：
```bash
export DEEPSEEK_API_KEY="sk-..."
```

**Windows (PowerShell)**：
```powershell
$env:DEEPSEEK_API_KEY="sk-..."
```

也可以通过 Web / 桌面客户端 UI 在 **设置 → 提供商 → DeepSeek** 中配置，或者在 `~/.config/openagentd/.env` 文件中写入：

```env
DEEPSEEK_API_KEY=sk-...
```

#### 3. 选择模型与配置 Agent

OpenAgentd 的 Agent 配置文件保存在 `~/.config/openagentd/agents/` 目录中（包含 YAML frontmatter 的 Markdown 文件）。

将主控 Agent（Lead Agent）模型设置为 DeepSeek V4：

编辑 `~/.config/openagentd/agents/lead.md`：

```yaml
---
name: lead
description: 主控协调 Agent
model: deepseek:deepseek-v4-flash
---
```

如需进行高难度推理编码任务，可选择 `deepseek-v4-pro`：

```yaml
---
name: lead
description: 主控协调 Agent
model: deepseek:deepseek-v4-pro
---
```

OpenAgentd 原生适配 DeepSeek V4 特性：
- 完整支持 **100 万 Token**（1,048,576）上下文窗口。
- 支持 DeepSeek 深度思考/推理模式（`thinking: {type: "enabled"}`），并能正确处理 Agent 工具调用过程中的 reasoning content。

#### 4. 开始使用

启动 OpenAgentd 后端服务与 Web 控制台：

```bash
openagentd serve
```

或直接在终端启动交互式对话：

```bash
openagentd chat
```

你也可以在界面或客户端的设置中随时动态切换模型。
