---
title: "📎 Main Branch 技术周刊：截图和 bug 一起发出去了 - Issue #39"
number: 39
date: 2026-09-06
excerpt: "gh --attach、npm 的多份 trusted publishing 配置，以及我为什么一直在想 orchestration 比原始智能更重要。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-39
beehiivUrl: https://mainbranch.beehiiv.com/p/issue-39
topics: ["GitHub CLI", "npm", "OIDC", "AI Agents", "MCP", "Cloudflare"]
tags: ["github-cli", "media-attachments", "npm", "trusted-publishing", "oidc", "ai-agents", "orchestration", "mcp", "cloudflare", "newsletter"]
featured: false
---

[Leer en Español](https://mainbranch.dev/newsletter/es/) • [阅读中文版](https://mainbranch.dev/newsletter/zh/)

朋友们好，

AI 这周很忙。不管我们喜不喜欢，这个精灵都回不去瓶子里了。模型的新闻像 Thanos 一样，躲不掉。这周新增了 Claude Fable 5.1、GPT-6 Astra、Gemini 3.8 Flash、Meta 的 Muse Spark 1.3，以及 Qwen 的 open-weight Qwen3.8。帮助开发者使用这些模型的公司也在同一场竞赛里。GitHub 宣布了 Project HydraFusion，这是 Copilot CLI 中的 research preview。我的看法是，模型本身不会那么重要，因为总会有新模型出来。更关键的是 coding harness 或其他东西如何 orchestration 模型，以及 planning、tool calls 和 execution 如何发挥更大的作用。

这几天我一直在用它做实验。以下只是我的体验，不是 GitHub 官方分析。就 orchestration 方法而言，它很厉害，确实有助于为解决 issues 理出更清楚的路径。至于成本，我不太确信它有重大改善，不过我还没深入分析实际的 token 消耗。如果你试了，告诉我。

## 🚢 最新发布

### [GitHub CLI `--attach` 支持 issues、PRs 和 comments](https://github.blog/changelog/2026-09-01-github-cli-media-in-issues-pull-requests-and-comments/)

现在可以直接通过 `gh` 把 images 和 small videos 附到 issues、PRs 和 comments。传入 local path，也可以添加 alt text 来提升 accessibility。所有 plans 都支持，前提是使用 `gh` 2.99.0，并且你需要 write access。它还没有登陆 GitHub Enterprise Server。大小限制和 [github.com](https://github.com) 一样。

写描述时，尤其是用 agents 解释 errors，如果要为此使用 tokens，成本基本会翻倍。你付一次钱写它，再付一次钱让 agent 审阅。Vision tokens 也不是免费的，但准确率会提高，而且能省掉后面几轮澄清。有些东西展示出来比说出来更好。

```shell
gh issue comment 42 --attach './login.png#Login error state'
```

### [npm 支持多份 trusted publishing 配置](https://github.blog/changelog/2026-09-03-multiple-trusted-publishing-configurations-for-npm/)

一个 npm package 现在最多可以有十份 OIDC (OpenID Connect) configurations。每份 configuration 都可以有自己的 repository、workflow 和 environment。Stable 和 prerelease 不再共用一个 binding，也不再依赖 long-lived token。所有新 configuration 起初都是 stage-only，但你可以把每一份设置为直接执行 `npm publish`。当你把 packages 放入 stage，它们会留在 approval button 后面，只有 malware scan 完成后才会发布。versions tab 现在会显示 packages 是 approved、rejected，还是仍处于 staged 状态。

今年 npm worms 的情况很可怕。long-lived tokens 被 phishing，worms 也随之传播，Shai-Hulud 和它的朋友们就是例子。后来我们转向 short-lived OIDC 的 trusted publishing，但这还不够。Mini Shai-Hulud 成功污染 runner、scrape OIDC token，即使有有效 provenance 也照样发布。给 configurations 划定范围，并在 scan 后加入人工 stage approval，解决不了全部问题，但能缩小 blast radius。

## 📖 我在读

[Steve Krouse (Val Town) 的 Connecting every app to every other app](https://blog.val.town/connectors)

Zapier 一直是连接各个平台的万能插头，尤其适合 one-click authentication。Krouse 的文章在推广他自己的产品，但也把一个问题讲得很清楚：为每一个 destination 注册 OAuth client。现在有了 MCP，Dynamic Client Registration 让 clients 可以自己完成 provisioning，Client ID Metadata Documents 更进一步，把 client metadata 放在 URL 上，完全跳过 portal。他在没有手动收集一个 client ID 的情况下，做出了一个拥有 3,000+ connectors 的 remix。挑战依然存在，但这可能让 MCP 不需要多数 dashboards 所需的 REST API 就能解锁更多能力。

值得花时间看，如果你正在把 agents 接到 tools，或者已经厌倦再填一份 OAuth app 表单。

## 🔧 我在用

这周我改了 Main Branch subscribe button 背后的 plumbing。我用一个调用 Beehiiv API 的 Cloudflare Worker 替换了旧的 signup integration。Beehiiv 是我目前使用的 newsletter platform，不过我很快会从那里迁走。

这是一个小活儿，能够保持小，是因为 Cloudflare Wrangler 很好用，而 Cloudflare 实在太强了。我在 Twitter 上发了一个 [post](https://x.com/acolombiadev/status/2095096798905802947?s=20) 给他们致意，结果有点 viral。

我一直在写、也一直在想怎么给 automation 设置 guardrails，这就是一种做法。我总觉得自己可能因为旧表单、网站和 Beehiiv API 之间那次 handshake 而漏掉了 subscribers。现在我确定没有，因为我有一段专门的代码，可以检查和维护。如果你在把 static website 连接到一个需要 secret 的 API，Cloudflare 会让这件事容易很多，因为你不必为一个 endpoint 搭建整个 backend。

## ✨ 本周

我会忙着准备 Universe 演讲的大纲。我已经参加很多年了，但这是我第一次以 speaker 身份参加 🎉。

如果你在 Bay Area，或者能到那里，我正在为 GitHub 做 ticket giveaway：[gh.io/win](https://gh.io/win)。很希望我最喜欢的人之一能抽中。希望你报名，也希望你的九月开局顺利。

感谢你的阅读，

下周见，

Andrea

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
