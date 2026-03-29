---
title: "⚙️ Main Branch: 就是那种，帮你穿透 AI 噪音的那期"
number: 12
date: 2026-02-02
excerpt: "Copilot CLI、ACP 预览、session handoff、repo memory、/review、实时引导，还有那个让你飞速 ship 的 --yolo flag。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-12
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-we-cut-through-the-ai-noise-issue-12
topics: ["Copilot", "Developer Tools", "AI", "Agentic AI"]
tags: ["copilot-cli", "developer-tools", "ai", "agentic-ai"]
featured: true
---

嗨，朋友们，

我懂。AI 的炒作让人疲惫。

我反复想明白的一件事是：AI 放大的是你已有的能力。如果你什么都不会，它放大的就是零。[Chris Gregori](https://www.chrisgregori.dev/opinion/code-is-cheap-now-software-isnt?utm_campaign=launch&utm_medium=referral&utm_source=mainbranch.beehiiv.com) 说得好："LLM 已经把生成代码的成本干掉了，但真正理解问题的成本？一点没变。"

入门门槛消失了。**判断力、品味和责任感，依然是你的工作。**

基本功仍然重要。而且比以前更重要了。

## 💡 **为什么 Copilot CLI 是个好起点**

如果你对 AI 工具持怀疑态度，又离不开终端，[Copilot CLI](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/use-copilot-cli?utm_campaign=launch&utm_medium=referral&utm_source=mainbranch.beehiiv.com) 值得看看。

我试过 Claude Code、Cursor、Gemini CLI 等等。为什么一直回来用 Copilot CLI？Copilot Pro 每月 $10，300 个 premium 请求，预览期间每次 CLI 交互都是 1x 倍率。模型选择很灵活——Claude Sonnet 4.5（默认）、GPT-5、GPT-5 mini、Gemini 3 Pro 等等，用 `/model` 随时切换。而且它深度融入 GitHub 生态。如果你已经在用 GitHub 部署、管理 issue、处理开源依赖，Copilot CLI 天然理解这些上下文。GitHub MCP server 预配置好了。

**值得知道的斜杠命令：**

|命令|作用|
|---|---|
|`/diff`|审查当前 session 的所有改动，带行级评论。|
|`/context`|可视化你的 token 用量。|
|`/compact`|对话太长时压缩上下文。|
|`/share file`|把 session 导出为 markdown，很适合做文档。|
|`/mcp add`|添加自定义 MCP server，连接你自己的工具和数据库。|

**快捷键：**

|快捷键|作用|
|---|---|
|`Alt+V` / `Cmd+V`|往 CLI 里粘贴截图和图片。让 Copilot 看到你在看的东西。|
|`Sft+T`|切换 /plan 模式。|
|`Ctrl+X` 然后 `/`|不丢失当前输入的情况下执行斜杠命令。|
|`esc+esc`|撤销和回退改动|

内置的 sub-agent 也很实用。**Explore** 让你在不污染主上下文的情况下提问代码库问题。**Task** 用来执行命令并查看详细输出（测试、构建、lint 等）。

## 🚢 **新动态**

[GitHub Copilot CLI：先规划再动手，边做边调整](https://github.blog/changelog/2026-01-21-github-copilot-cli-plan-before-you-build-steer-as-you-go/?utm_campaign=launch&utm_medium=referral&utm_source=mainbranch.beehiiv.com)。

**ACP 支持进入 public preview。** Agent Client Protocol 让任何 IDE、自动化系统或自定义工具都能接入 Copilot 的 agentic 能力。

**Session handoff。** 用 `/delegate` 把本地 session 推到 GitHub.com，用 `--resume` 拉回来。或者在 prompt 前面加 `&`，后台 delegate，解放你的终端。

**Repository memory。** Copilot 能跨 session 记住你代码库的事——惯例、模式、偏好。

**`/review` 命令。** 直接在 CLI 里分析 staged 或 unstaged 的改动。commit 之前快速 sanity check。

**边想边引导。** Copilot 在处理时你可以排队发后续消息，中途重新引导方向。

**`--yolo` flag。** 一次性开启所有权限。当你信任它可以自由跑的时候用。

## **📺 在看什么**

[**Kimi K2.5 y Agent Swarm explicado**](https://www.youtube.com/watch?v=GwKoFpUV69M) by Caleb Writes Code

Moonshot AI 的新开源模型不是重点。Agent Swarm 才是。不是一个 agent 按顺序啃任务，而是启动一组专业 sub-agent 并行工作：researcher、fact-checker、coder。这就是 agentic AI 的方向。不是一个 agent 干所有事，而是一支协调的专家团队。

## 🔧 **在用什么**

**Copilot CLI 的 `/delegate`：** 我在 [Beehiiv](https://www.beehiiv.com/?via=Andrea-Griffiths&utm_campaign=launch&utm_medium=referral&utm_source=mainbranch.beehiiv.com) 上托管 Main Branch，但我也想把它放到 [GitHub Pages](https://mainbranch.dev/?utm_campaign=launch&utm_medium=referral&utm_source=mainbranch.beehiiv.com) 上。网站结构已经搭好了，渲染方式也想好了。让 agent 把内容从一个地方搬到另一个地方，这种活就该 delegate。

## ✨ **这周**

我要飞去 ATL，主持一场和 Robin Ginn 的炉边对话，她是 OpenJS Foundation 的执行董事。等不及要分享更多了！

最后，关于这期 AI 味比较重的内容——我不是来跟你说"你必须拥抱 AI 否则就会被淘汰"的。那种说法既累人又没什么用。但说实话：**工具就是朝这个方向走的。** 你所在的公司会采用这些工具。你贡献的代码库里会有 AI 生成的 commit。你越早搞懂这些工具是怎么工作的、擅长什么、哪里不行，你就越能用好它们。

**就这些。** 不炒作。只是帮你 ship 得更快的功能。

感恩，下周见，

Andrea

🇻🇪 **Léelo en** **[español](https://mainbranch.dev/newsletter/es/?utm_campaign=launch&utm_medium=referral&utm_source=mainbranch.beehiiv.com)**

**支持 Main Branch：** [Subscribe](https://mainbranch.beehiiv.com/) | [GitHub Sponsors](https://github.com/sponsors/andreagriffiths11?utm_campaign=launch&utm_medium=referral&utm_source=mainbranch.beehiiv.com)
