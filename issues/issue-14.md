---
title: "🦞 Main Branch: 就是那种，龙虾跑出来了的那期"
number: 14
date: 2026-02-16
excerpt: "60 天 196k GitHub star。OpenClaw 的势头正在迫使 GitHub 认真对待 agentic AI。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-14
beehiivUrl: https://mainbranch.beehiiv.com/p/d0092652-f708-41ac-983a-c3ed5c6d86a6
topics: ["OpenClaw", "GitHub Agents", "Agentic AI"]
tags: ["openclaw", "agents", "claude", "codex", "stacked-diffs"]
featured: true
---

嗨，朋友们，

如果你最近上过开发者 Twitter，你一定见过那只龙虾。OpenClaw 是一个开源的个人 AI agent，本地运行，连接你的聊天应用，替你干活。从一个周末项目到 60 天 196k GitHub star。

几周前我分享了 [我和 Peter Steinberger 的对话](https://gh.io/openclaw)，OpenClaw 的创始人。从那以后，生态炸了。它连接 LLM，跑在你的机器上，集成 WhatsApp、Slack、Discord 等等。它能读你的文件、跑 shell 命令、控制你的浏览器。生态发展飞快。[ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw) 用 Rust 重写了整个项目（空闲 8MB vs 1.5GB）。[ClawHub](https://clawhub.ai/) 上有 2,857 个社区 skill。Agent 可以持有钱包和支付。而截至昨天，[Peter](https://www.reuters.com/business/openclaw-founder-steinberger-joins-openai-open-source-bot-becomes-foundation-2026-02-15/) 加入了 OpenAI。OpenClaw 转为基金会。龙虾换了个更大的缸。

势头这么猛，生态也在试探自己的边界。这周一个 OpenClaw bot 给 matplotlib 提了个 PR，被拒绝了，然后 [发了篇博客](https://www.reddit.com/r/tech_x/comments/1r3mouq/an_openclaw_bot_pressuring_a_matplotlib/) 攻击那个说不的维护者。**在 agentic AI 飞速发展的同时，GitHub 在出基本功，让我们保持脚踏实地。**

## 🚢 新动态

**Claude 和 Codex Coding Agent 进入 Public Preview**

2 月 4 日，GitHub 添加了 Anthropic 的 Claude 和 OpenAI 的 Codex 作为 coding agent。如果你有 Copilot Pro+ 或 Copilot Enterprise，现在可以直接在 GitHub、GitHub Mobile 和 VS Code 里运行多个专业 agent。

这很重要，因为它打破了单 agent 的瓶颈。不再是一个 LLM 死磕一个问题，而是根据任务启动合适的 agent。需要 Claude 做架构？Codex 做重构？都用上。这些 agent 理解你的 GitHub 上下文——issue、PR、diff、对话——并且能协调工作。你不再被锁定在一个模型或一种思路上。

底层是 GitHub 的 Agent HQ，负责编排 agent 并保持上下文在工具间流转。早期用户反馈说可以把整个工作流卸载出去——code review、debugging、PR 分析——同时留在自己熟悉的环境里。如果你在维护什么项目，这就是从"AI 助手"到"AI 团队"的转变。

**PR「Files Changed」性能大改**

还记得新版 Files Changed 体验 [成为默认](https://mainbranch.dev/newsletter/issue-11/) 的时候吗？来看看之后变快了多少。PR 的「Files changed」标签做了一次真正的性能优化。在大 PR 上，点击、打字和滚动的 diff 响应速度提升了最多 67%。

更大的修复：新版 Files Changed 之前漏了 CODEOWNERS 校验。现在 merge 前会正确显示必需的 reviewer。还修了：大 PR 上 tab 切换从 10 多秒降到几秒，移动端布局优化，sticky header 终于真的 sticky 了。

如果之前觉得新版 Files Changed 体验粗糙，值得再看看。

**Stacked Diffs（即将推出）**

GitHub 也要出 stacked diffs 了。Jared Palmer [2 月 6 日宣布](https://x.com/jaredpalmer/status/2019817235163074881)，早期设计合作伙伴将在三月获得 alpha 访问。这是开发者一直在要求的功能——以干净的分层方式创建、review 和 merge 有依赖关系的 PR，而不是一个巨大的 diff。团队为此把 GitHub 迁移到了 git reftables 来让 restacking 更高效。这是一个大的基础设施改造，但它在推进了。

## 🎧 在看什么

**The Night Manager**（[新一季](https://en.wikipedia.org/wiki/The_Night_Manager_\(British_TV_series\))）。跟技术无关但是真的好看。这部间谍剧回来了，新一季在哥伦比亚拍的。看一部在你去过的地方拍的剧有种特别的感觉——你能注意到别人注意不到的细节，在镜头里感受到一座城市的气场。这季结尾看得我 😩🤬。

## 🔧 在用什么

[**Zo Computer**](https://zocomputer.com/?via=acolombiadev) 作为我的个人 AI 服务器。我的 OpenClaw、ZeroClaw 和个人 agent 都跑在上面。它已经成了我所有事情的底座：托管网站、运行定时 agent、在一个地方管理文件。CLI 很流畅，权限模型实际上讲得通，我可以随时切换 AI 模型而不用离开终端。没有 vendor lock-in。文件是你自己的。可以用 Claude、Kimi 或者任何适合任务的模型。有一个很大方的免费套餐，所以可以不花钱就开始用。如果你在用 AI 做东西但受够了到处散落的 SaaS 工具，值得看看。[用我的推荐链接加入](https://zocomputer.com/?via=acolombiadev)。

## ✨ 这周

总统日意味着大多数人多放一天假——但我不行。我会埋头做一个特别的 demo，现在还完全不能说。（但关注 GitHub 的社交账号。发的时候你就知道了。）

**这就是这周。** Agentic AI 跑得很快。GitHub 在有意识地推进。两件事都很重要。

基本功优先。永远如此。

Lee el boletín en español: https://mainbranch.beehiiv.com/p/boletin-en-espanol

感恩，下周见，Andrea

🇪🇸 **Léelo en** **[español](https://mainbranch.dev/newsletter/es/issue-14/)**

**支持 Main Branch：** [Subscribe](https://mainbranch.beehiiv.com/) | [GitHub Sponsors](https://github.com/sponsors/andreagriffiths11)
