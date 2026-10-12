---
title: "🚦 Main Branch 技术周刊：让 bot 来跑你的 CI（如果你允许的话）"
number: 31
date: 2026-06-14
excerpt: "GitHub Actions 现在允许 bot 创建的 PR 在审批后跑 CI，GitHub Agentic Workflows 进入 public preview。还有一个给 Copilot 用的 Chromium canvas。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-31
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-the-bots-run-ci-if-you-let-them-issue-31
topics: ["GitHub Actions", "Agentic Workflows", "GitHub Copilot", "CI/CD", "Playwright"]
tags: ["github-actions", "agentic-workflows", "github-copilot", "ci-cd", "playwright", "newsletter"]
featured: true
---

朋友们好，

这周有两个发布，而且主题很押韵。GitHub 这周一直在确定一件事：谁能在 Actions 里跑东西。一边是帮你开 pull request 的 bot，一边是你指向 repo 的 agent。两个都带着一道闸门发布。

## 🚢 最新发布

### [bot 创建的 PR 现在可以跑你的 CI，但要先通过审批](https://github.blog/changelog/2026-06-11-bot-created-pull-requests-can-run-workflows-if-approved)

在此之前，由 `github-actions[bot]` 开的 pull request 没法触发你的 CI/CD workflows，所以 bot 的改动可能一路 merge，而你的 checks 从没跑过。从 6 月 11 日起，只要有 write access 的人批准，这些 PR 就会跑已配置的 workflows。这个审批步骤是故意设计的：它能避免生成的代码自动跑那些可能碰到 secrets 的 workflows。如果你天天和 [Dependabot](https://docs.github.com/en/code-security/dependabot) 或 [Renovate](https://docs.renovatebot.com) 打交道，这补上了一个实实在在的缺口，同时也意味着 CI 启动前会有人点一下。

### [GitHub Agentic Workflows 进入 public preview](https://github.blog/changelog/2026-06-11-github-agentic-workflows-is-now-in-public-preview/)

你现在可以在 Actions 里跑 coding agents，去处理那些需要推理的杂活：issue triage、CI 失败分析、文档更新。你用普通语言写一个 Markdown 文件来描述自动化，它会编译成标准的 Actions YAML，所以它跑在你现有的 runner groups 上，遵守你已经在执行的那套策略。默认情况下 agent 是 read-only，在一个容器里 sandbox 起来，前面挡着 Agent Workflow Firewall，还有一个 threat-detection job 会在改动应用之前扫描它们。Quickstart 在 `gh.io/gh-aw-quickstart`。

## 📖 我在读

**Scott Berkun 的 [Make the System Work for You](https://www.linkedin.com/pulse/make-system-work-you-scott-berkun-jlibc/)**

这是 [Why Design Is Hard](https://scottberkun.com/why-design-is-hard/) 的一段节选。Berkun 引用了 Deming 的说法：一个组织 94% 的结果来自它的系统，而不是个人。他主张更聪明的做法是先搞清楚你的 org 实际是怎么运转的，而不是正面硬刚。我一直在琢磨 Chesterton's Fence 那句话：在你弄明白一个流程为什么存在之前，别急着把它拆掉。

值得花时间读，如果：你就是那个总想用蛮力去修组织、最后把自己耗干的人。

## 🔧 我在用

[Chromium Control Canvas](https://gist.github.com/AndreaGriffiths11/b9ebe41deabdcdd0930954d5542cd918)，一个我自己做的 GitHub Copilot canvas 扩展。宿主 app 自带的 browser canvas 跑在 WebKit 上，所以这个扩展通过 [Playwright](https://playwright.dev) 启动一个真正的 headful Chromium，并把完整的动作集（`snapshot`、`click`、`type`）交给 agent。它复用了 [Claw Relay](https://clawrelay.dev) 的那套模式：一个持久化的 profile、一个站点 blocklist、一份 audit log。当 agent 需要一个真正登录过的 Chrome 会话时我就会用它，比如确认一次 deploy 渲染正常，或者走一遍 signup 流程，访问范围受控且全程留痕。

## ✨ 本周

我得了世界杯热病。整个夏天 Main Branch 会改成每两周一期，好让我能真正歇一下。第一站是去哥伦比亚陪小儿子一周看望家人，同时我大儿子正跟着 [houseband.live](https://houseband.live) 在路上巡演。然后七月我会回到柏林参加 [WeAreDevelopers World Congress](https://www.wearedevelopers.com/world-congress)（7 月 8 日到 10 日），很高兴能和欧洲的朋友们叙叙旧。去年我在那里带了一个 workshop，做的是 [GitVision](https://github.com/GH-Event-Demos/gitvision-workshop)，一个把你的 GitHub commits 变成 AI 精选 Eurovision 歌单的 app，一次一个 Copilot prompt 地搭出来。一年过去了，我不会再一个函数一个函数地手动 prompt 它了。我会在 [Spec Kit](https://www.youtube.com/live/bIioEmT2KEM?si=5XbkQRuv4J1MiQd-) 里把 spec 一次写清楚，然后让 coding agent 去做 plan 和 tasks，我负责把方向、做 review。等夏天过去就恢复每周一期，这样也正好留更多时间看世界杯。

两周后见。

怀着感激，
Andrea

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
