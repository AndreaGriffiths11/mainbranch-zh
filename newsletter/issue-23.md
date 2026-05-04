---
title: "🏪 GitHub 成为应用商店的那一期"
number: 23
date: 2026-04-21
excerpt: "GitHub 修复了没人谈论的 SBOM 超时问题，gh skill 发布时带着我认为你应该了解的警告，我在智利的演讲让我想起了为什么要做这些。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-23
beehiivUrl: https://mainbranch.beehiiv.com/p/60e7b40b-cb40-43e9-a87f-fd5e0ea58a83
topics: ["GitHub", "Agent Skills", "SBOM", "Nerdearla"]
tags: ["gh-skill", "sbom", "agent-skills", "public-preview"]
featured: true
---

各位开发者朋友们好，

刚从智利的 Nerdearla 回来。很高兴能在现场见到这么多朋友。下面会详细说说这次经历。

本周：一个被忽视的 GitHub 修复，以及一个我觉得比表面看起来更重要的新 CLI 命令。

## 🚢 新功能发布

**异步 SBOM 导出** • [Changelog](https://github.blog/changelog/2026-04-16-dependency-graph-async-sbom-exports/)

如果你试过从大型代码库导出 SBOM，就知道容易超时。现在导出改为异步方式。你启动任务，然后在准备好时获取结果。有两个新的 API 端点：

- `GET /repos/{owner}/{repo}/dependency-graph/sbom/generate-report`
- `GET /repos/{owner}/{repo}/dependency-graph/sbom/fetch-report/{sbom-uuid}`

第一个启动任务并返回 UUID。第二个让你检查直到报告准备好，然后返回导出结果（或重定向到结果，取决于客户端）。

界面操作：洞察 > 依赖关系图 > 导出 SBOM。

**智能体技能（公开预览）** • [Changelog](https://github.blog/changelog/2026-04-16-github-cli-skill-command-public-preview/)

智能体技能是可移植的指令集，教 AI 编码智能体如何执行特定任务。类似插件，但专为智能体设计。遵循开放的 Agent Skills 规范，适用于腾讯会议代码助手、阿里云编码助手、Cursor、Codex 和字节豆包编程助手等多个平台。

新的 `gh skill` 命令让你可以安装、更新和发布这些技能：

```bash
gh skill install github/awesome-copilot documentation-writer
gh skill install github/awesome-copilot documentation-writer --agent tencent-coding
gh skill update --all
```

你可以固定到标签或提交 SHA 以确保可重现性。来源元数据会写入技能的前置数据，随文件一起传输。

坦率地说：变更日志警告这些技能未经 GitHub 验证，可能包含提示注入或恶意脚本。安装前请用 `gh skill preview` 检查。供应链安全在这里同样适用。

## 🎧 最近在读

[**AI 帝国** - Erika Hao](https://www.amazon.com/Empire-AI-Erika-Hao/dp/1250862116)

这本书我花了很长时间才读完。不是因为难读，而是内容需要慢慢消化。Hao 写了顶级 AI 实验室如何运作（主要聚焦 OpenAI）以及训练这些模型的实际工作是如何完成的。读完让我既兴奋又冷静——为这项技术的可能性而兴奋，对其代价更加清醒。

推荐理由：如果你想了解 AI 浪潮背后真实的人和故事，而不是炒作版本。

## 🔧 目前在用

**gh skill**：本周我用它安装了第一个智能体技能，在运行任何东西之前立即检查了内部内容。`gh skill preview` 是信任来自公开代码库的任何内容之前的正确选择。把它当作第三方 GitHub Action 对待：先读再用。

## ✨ 本周动态

本周我在圣地亚哥的 Nerdearla 演讲，这是拉丁美洲最大的免费技术活动。我的演讲介绍了 [Team X-Ray](https://github.com/AndreaGriffiths11/teamxray)，这是我构建的 VS Code 扩展，既是个人实验，也是对 Atom 编辑器的小小致敬（我在 GitHub 的第一个角色是 Atom 社区经理）。它通过代码分析进行贡献发现：指向一个代码库，就能显示谁了解什么。演讲追溯了它从原始的 git log 和 git blame 提示，通过 MCP，到当前基于 Copilot SDK 版本的演进过程。

这个社区就是一切。好奇、慷慨，当你为他们出现时真正感激。我会回来的。如果你的公司想在拉丁美洲发展，[Nerdearla](https://nerdearla.com/) 就是你应该在的地方。

另外：下周我将在拉斯维加斯的 Google Cloud Next。来 GitHub 展台找我吧。我会做一个关于 Copilot CLI 的演讲。很想见到你。

致以谢意，下周见，  
Andrea