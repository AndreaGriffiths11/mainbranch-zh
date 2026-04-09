# GitHub Copilot CLI 技术周刊

> **Copilot CLI — Andrea**

```bash
andrea@copilot-cli ~
$ echo "GitHub Copilot 实用技巧"
```

## GitHub Copilot CLI

**// 你的 AI 终端智能助手**

GitHub Copilot CLI 将 AI 的强大能力直接带入你的终端。使用 `copilot` 命令启动交互式会话，或通过 `copilot -p` 执行单次任务。它能编辑代码、运行 shell 命令、与 GitHub 交互，并解决复杂的多步骤问题——完全无需离开命令行。

```bash
$ ls ./features/
```

## 01 交互式与编程模式

```bash
$ copilot -p "修复失败的测试"
```

使用 `copilot` 启动交互式智能会话，或通过 `copilot -p` 直接传递提示进行脚本化和自动化操作。按 `Shift+Tab` 在询问、编辑和智能体模式间切换。智能体模式可以自主进行代码更改、运行 shell 命令和与 GitHub 交互。

## 02 工具与权限管理

```bash
$ copilot --allow-tool='shell(git)'
```

Copilot CLI 在运行命令或编辑文件前会请求批准。使用 `--allow-tool` 为特定工具（如 `shell(git)`）授予细粒度权限，或使用 `--allow-all-tools` 信任所有操作。使用 `/yolo` 模式跳过所有确认。你始终掌控每一个执行动作。

## 03 自定义指令

```bash
$ cat .github/copilot-instructions.md
```

通过多层级自定义指令引导 Copilot 行为：仓库级别（`.github/copilot-instructions.md`）、组织级别或个人级别（`~/.copilot/copilot-instructions.md`）。所有指令文件会组合生效——告诉它你的约定、首选工具、构建命令和测试模式。

## 04 MCP 服务器与扩展

```bash
$ /mcp add
```

通过模型上下文协议（MCP）服务器将 Copilot CLI 连接到外部工具和实时数据。添加数据库访问、API 集成或自定义工具。在 `.copilot/mcp-config.json`（仓库级）或 `~/.copilot/mcp-config.json`（全局）中配置。大大扩展 Copilot 在本地文件系统之外的能力。

## 05 钩子与自定义智能体

```bash
$ cat .github/hooks/hooks.json
```

设置在 Copilot 会话期间自动运行的钩子——强制代码检查、运行测试或阻止不安全命令。在 `.github/hooks/hooks.json`（云端智能体）或当前工作目录（CLI）中配置，采用包含 `version: 1` 的 JSON 格式。支持的触发器：sessionStart、sessionEnd、userPromptSubmitted、preToolUse、postToolUse、errorOccurred。在 `.github/agents/.agent.md` 中构建自定义智能体作为可重用的专家（使用带 YAML 前言的 Markdown），配备专有指令、工具和权限范围——直接从 CLI 按名称调用。

## 06 BYOK：自带密钥

```bash
$ export COPILOT_PROVIDER_BASE_URL && export COPILOT_MODEL
```

使用你自己的模型提供商——Ollama、阿里云 AI、腾讯云或任何 OpenAI 兼容端点。设置 `COPILOT_PROVIDER_BASE_URL` 和 `COPILOT_MODEL` 环境变量。对于本地 Ollama，无需设置 API_KEY。应用场景：领域特定模型、企业隐私合规、离线/隔离环境，或自定义 OpenAI 兼容端点。

```bash
$ cat README.md
```

## 为什么选择 GitHub Copilot CLI？

- **🆓 所有 GitHub Copilot 计划免费** — 包括 Copilot 免费版
- **🤖 支持多种 AI 模型** — Claude Sonnet 4.5、Claude Haiku 4.5、Gemini 2.5 Pro 等，通过默认支持 + BYOK 实现
- **💻 跨平台支持** — Linux、macOS 和 Windows（PowerShell + WSL）
- **♻️ 95% token 自动压缩** — 会话可无限期运行
- **🔗 原生 GitHub 集成** — 创建 PR、管理 issue、触发 Actions
- **⚡ 真正的斜杠命令**：`/compact`、`/review`、`/context`、`/yolo`、`/cd`、`/feedback`
- **🔧 高度可扩展** — MCP 服务器、自定义智能体和钩子
- **🔑 BYOK 支持** — 使用 Ollama、阿里云 AI、腾讯云或任何 OpenAI 兼容模型
- **📂 适用任何仓库** — 无需设置，直接运行 `copilot`

---

**订阅 [mainbranch.dev](https://mainbranch.dev) 获取每周 GitHub 技巧和开发基础知识**

```bash
andrea@github: ~/copilot-cli
```

**GitHub Copilot 技术周刊 | 2026**

---

**翻译说明**：本内容翻译自英文原版，面向全球中文开发者社区。如发现翻译问题或建议改进，欢迎访问 [GitHub 仓库](https://github.com/AndreaGriffiths11/mainbranch-cz) 提交 Pull Request。
