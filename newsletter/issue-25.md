---
title: "🤑 Token 开始收费了"
number: 25
date: 2026-05-02
excerpt: "GitHub Copilot 转向按用量计费。哪些变了，哪些不变，怎么控制开销。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-25
beehiivUrl: https://mainbranch.beehiiv.com/p/506cf95d-8d2e-4be1-8546-bbb802993669
topics: ["GitHub Copilot", "Pricing", "AI Agents", "Developer Workflow"]
tags: ["copilot", "pricing", "newsletter"]
featured: true
---

各位开发者好，

Copilot 的 token 现在直接跟钱挂钩了。另外本周启动了一个写作竞赛，详情在最后。

## 🚢 本周发布

**GitHub Copilot 6月1日起转向按用量计费 [详情](https://github.blog/changelog/2026-04-27-github-copilot-code-review-will-start-consuming-github-actions-minutes-on-june-1-2026/)**

Premium Request Units 退场，GitHub AI Credits 登场。6月1日起，你发送的每个 token（输入、输出、缓存）都按各模型公布的 API 费率计费。订阅价格不变，但你能用到的额度变了。

代码补全依然免费。其他所有功能（聊天、代码审查、智能体）现在消耗 credits。关键信息：输出 token 的成本是输入的 5 倍。所以最快的省钱方式是收紧你的输出。在 Copilot 指令中加上 "Code only, no explanation"。格式选 bullets 而非段落。精简你的 copilot-instructions.md 和 AGENTS.md：每多一个字都会在每次调用中运行。简单任务用 Ask Mode，Agent Mode 消耗极快。

我正在写一篇详细文章，敬请期待。

**🧰 TanStack AI：原生音频生成**

TanStack 团队的新功能：他们的开源 AI 库现在支持音频生成。通过新的 generateAudio API，你可以作曲、文字转语音、处理音效，全部通过一套 type-safe hooks 完成。Provider 选择 Fal、Gemini Lyria 等主流方案，即插即用。

文档和代码：[https://tanstack.com/blog/tanstack-ai-audio-generation](https://tanstack.com/blog/tanstack-ai-audio-generation)

## 📺 值得一看

[MCP vs. CLI](https://www.youtube.com/watch?v=CfITzVcUkZA)：智能体工具集成模式的正面对比评测（Laurie Voss, Arize AI）

500 次评测，一个 GitHub 仓库，25 个任务，三种策略：官方 GitHub MCP 服务器、一份冗长的百科全书式 gh skill、一份简短有观点的 skill。正确率都在 ~82% 左右。但在最难的任务上，MCP 成本高出 6 倍，耗时长 5 倍。有一次运行达到 71 次工具调用、8 分钟、$2。

结论不是 MCP 对抗 CLI，而是 MCP 配合 CLI。根据任务选择合适的工具。简短有观点的 skill 永远优于冗长的。

适合观看人群：正在构建智能体，或者在纳闷为什么成本一直涨的开发者。

## 🔧 本周在用

年度绩效反思（FY evaluation）本周截止。我的办公室从没这么干净过。坐下来写关于自己的东西之前，我什么都愿意干。这种抗拒是真实的。我给同事写评估的时候能写诗，自己的？算了吧。

💡 正好这时候一个同事做了个 GitHub CLI 工具：它能拉取你某个评估周期的 GitHub 活动，读取组织架构，然后用你自己的语气起草绩效反思（你完全可以自己用这个 CLI 来做）。感谢 [@ashleywolf](https://x.com/ashleywolf)。另外：我总是忘记自己发布了多少东西，直到全加起来。那一刻总是惊喜。

## ✨ 本周感想

对 GitHub 来说这是艰难的一周。当你是一个高行动力的人，你会感受到一切，包括那些本不该由你承担的事情。当这成为唯一的话题时，会很沉重。说实话，我很讨厌这种感觉。

所以我专注于我能控制的事情。写这份技术周刊就是其中之一。如果你正在阅读这些文字，谢谢你。我想把这个做成对更多人有意义的东西，不只是对我自己。这就是为什么我要启动 Main Branch 写作竞赛。我想听到你的声音：你的工作流、你的基本功、真正改变了你交付方式的东西。

详情：[Main Branch Writing Contest](https://acolombiadev.zo.space/contest)。

期待你的投稿。

Andrea

P.S.：看看这个 [Nerdearla](https://nerdearla.com/en/) 大会的证件有多酷。我还留着我的第一份安全许可申请、大学论文、和一个标了名字的照片文件夹（里面大概三张照片），全塞在我那个旧的线材杂物盒里。

![Nerdearla 大会证件](/images/nerdearla-badge.jpg)

---

*本文由 Andrea Griffiths 原创英文版翻译改编而来。如有翻译不当或建议，欢迎通过 [GitHub 仓库](https://github.com/AndreaGriffiths11/mainbranch) 提交 PR。*
