---
title: "🥊 Main Branch：就是那种，Actions 终于不跟你作对了的那期 🛠️"
number: 19
date: 2026-03-23
excerpt: "Environment 不用假装部署了，cron job 终于能用你自己的时区了。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-19
beehiivUrl: https://mainbranch.beehiiv.com/p/c4b59a5f-580a-4a3d-bc51-91737a047316
topics: ["GitHub Actions", "Environments", "Scheduled Workflows", "Open Source"]
tags: ["github-actions", "environments", "cron", "timezone", "open-source"]
featured: true
---

嗨，朋友们，

你有没有过那种每天都在用的工具，就是……有些棱角？你知道怎么绕过去，workaround 都背下来了，但每次还是要多花五分钟。

这周，GitHub Actions 磨平了我的两个。

## 🚢 新动态

### Actions：使用 environment 不再创建 deployment

[GitHub Actions](https://github.blog/changelog/2026-03-19-github-actions-late-march-2026-updates/) 里的 environment 用来按阶段（staging、production 等）管理 secrets 和 variables 很好用。问题是？每次 workflow 跑在一个 environment 上，就会创建一个 deployment。这意味着那些只是借用 secret 管理、根本不是在部署的 workflow，也会搞出一堆嘈杂的 deployment 历史。

现在可以关掉了。在 workflow YAML 的 environment 块里加 `deployment: false`。这是 per job 的，写在 `jobs.<job_id>.environment` 下面：

```yaml
jobs:
  build:
    environment:
      name: staging
      deployment: false
    steps:
      - run: echo "Using staging secrets, no deployment created"
```

一个注意点：自定义 deployment protection rules（GitHub App 类型的）需要真正的 deployment 对象。如果你设了 `deployment: false`，job 会立即失败。

### Actions：定时 workflow 支持时区了

Actions 里的定时 workflow 一直只能用 UTC。句号。如果你的团队在芝加哥，想让 workflow 在当地早上 9 点跑，你每次改 cron 表达式都得在脑子里做时区换算。

结束了。现在可以在 cron schedule 旁边传一个 `timezone` 字段，用任何 IANA 时区名称。

```yaml
on:
  schedule:
    - cron: '0 9 * * 1-5'
      timezone: "America/Chicago"
```

你的 pipeline，你的时区。终于。注意：夏令时规则适用。如果定时时间落在春季前调跳过的那个小时里，Actions 会在下一个有效时间运行。

## 📖 推荐阅读

**我在 CONTRIBUTING.md 里做了 prompt injection——50% 的 PR 是机器人提交的**，作者 [punkpeye (Frank Fiegel)](https://github.com/punkpeye)

awesome-mcp-servers 的一个维护者开始被 PR 淹没。数量上去了，质量没了。于是他在 CONTRIBUTING.md 里藏了一个 prompt injection 来检测哪些提交来自 AI agent。结果不意外。但影响值得深思。

推荐给：维护任何开源项目的人，或者你最近注意到收到的贡献氛围在变化的人。

## 🔧 在用什么

[`/chronicle improve`](https://x.com/acolombiadev/status/2034375932983599427?s=46&t=yN-IR4Vsn92Y1fOFo93hSQ)——GitHub Copilot CLI 里的实验功能，我停不下来。它会 review 你的编程会话，找到你遇到阻力的地方，然后你可以让它更新你的 Copilot instructions，这样你就不会踩同样的坑两次。它在我的里面发现了一些我自己都没意识到一直在做的事。

## ✨ 这周

Mike McQuaid [说了](https://x.com/MikeMcQuaid/status/2034685886659805377?s=20)一句我反复想起的话：job security 已死，career security 才是真正重要的。你通过学习、改变、跨出自己的舒适区来建立它。

然后我读了那篇机器人 PR 的文章。一个热门开源仓库里一半的贡献是自动化的。维护者用自己的空闲时间在筛选。

作为一个真正的人出现在这份工作中——好奇、负责、present——可能是我们现在最被低估的技能。好好发挥这一点！

就这些，发修复，做个人。

感恩，下周见，

Andrea

## 💛 支持

如果 Main Branch 帮你节省了时间或教了你新东西，考虑支持一下：

- ☕ [GitHub Sponsors](https://github.com/sponsors/AndreaGriffiths11)
- 📬 [订阅](https://mainbranch.beehiiv.com/subscribe)
- 🇨🇴 Lee el boletín en [español](https://mainbranch.dev/newsletter/es/)。
$

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
