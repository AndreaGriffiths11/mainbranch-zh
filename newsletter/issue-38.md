---
title: "⏳ Main Branch 技术周刊：你的 CI 历史记录要变短了 - Issue #38"
number: 38
date: 2026-08-30
excerpt: "GitHub Actions retention、push rule path exceptions 和 rule insights dashboard，还有一部值得看的 Silicon Valley 讽刺剧，以及我写的 MCP server。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-38
topics: ["GitHub Actions", "Rulesets", "CI", "MCP", "Developer Tools", "Television", "Conferences"]
tags: ["github-actions", "retention", "rulesets", "rule-insights", "ci", "mcp", "developer-tools", "devops-days", "newsletter"]
featured: false
---

[Leer en Español](https://mainbranch.beehiiv.com/p/boletin-en-espanol) · [阅读中文版](https://mainbranch.dev/newsletter/zh/)

朋友们好，

从 10 月 1 日开始，checks、workflow runs 和 statuses 会按照你的 [GitHub Actions retention 设置](https://github.blog/changelog/2026-08-27-actions-retention-will-cover-checks-workflow-runs-and-statuses)保留。现在，不管这个设置写的是什么，它们都会留存 400 天以上。10 月 1 日之后，它们会和 artifacts、logs 用同一套时间清理，默认是 90 天。

大多数 repo 不会感觉到变化。真正会受影响的是那些为了降低 Actions storage 成本，把 retention 调低的 repo。这个字段过去一直表示 artifact and log retention，所以设成 30 天只和 storage 有关。现在它也会决定 CI 历史记录能保留多久。GitHub 会把这个字段改名为 `Check, workflow run, status, artifact and log retention`。

这个改动也不会按你希望的方向追溯。以后把数字调高，已经被清掉的数据也不会回来。

如果你通过 API 构建了任何依赖 run history 的东西，现在就去检查。比如 flaky test dashboard，或者用来找出某个 check 从什么时候开始失败的 query。Public repo 最多保留 90 天，其他 repo 则取决于你的 org 和 enterprise 上限。

10 月 1 日之前去看一下这个设置。一分钟就够。

## 🚢 最新发布

### [Push rules 终于支持 path exceptions](https://github.blog/changelog/2026-08-25-push-rules-in-rulesets-now-support-path-exceptions)

Public preview。以前你只有两个糟糕的选择：给所有人放宽规则，或者在 GitHub 之外实现这个 exception。现在，`Restrict file paths` 和 `Restrict file size` 都有 Allowed exceptions 输入框。你可以在整个 repo 禁止 JAR 文件，只允许 `**/gradle/wrapper/*.jar`。也可以先设 file size 上限，不用立刻重写那些已经超出限制的文件。保存时，GitHub 会验证 patterns。

### [Rule insights dashboard 已经 GA](https://github.blog/changelog/2026-08-25-rule-insights-dashboard-generally-available)

Repo 和 org 级别都支持。你可以查看一段时间内的 successes、failures 和 bypasses，找出最常 bypass 的人，也能在两个级别导出 CSV。每张图表都会 deep-link 回 insights 页面，而且 filters 已经填好，所以你会直接落到对应的 rows，不用重建 query。

## 📺 我在看

**The Audacity**，Jonathan Glatzer 创作，现已上线 Netflix

我把 Silicon Valley 重看过很多遍。第一次看的时候我还没进入 tech 行业，之后每重看一次，都觉得更好笑。The Audacity 给我的感觉刚好相反。我已经被故事吸引住了，所以第二季还是会看，但这一季不好笑。它写得非常好，我能想到最贴切的形容是：tech 剧里的 Dr. Pimple Popper。很恶心，可你还是会想看看接下来会挤出什么。

如果你想看一个诚实写出的 Valley，这部值得看。

## 🔧 我在用

[machine-mcp](https://github.com/AndreaGriffiths11/machine-mcp) 是一个运行在 laptop 上的 MCP server，让 agent 可以在已经登录 Copilot CLI 的那台机器上执行 tools。`run` 使用 `shlex.split`，不使用 `shell=True`，把执行范围限制在 workspace root，默认 timeout 为 30 秒，并从所有 output 中隐藏 `github_pat_` tokens 和 AWS key patterns。

```json
{
  "mcpServers": {
    "machine-mcp": {
      "command": "path/to/.venv/bin/machine-mcp"
    }
  }
}
```

## ✨ 本周

我已经从 DevOps Days Lima 回到家。Lima 团队把活动组织得非常好，我也很开心能在线下认识这么多有才华的人。活动期间，我还花了很多时间听大家讲对 GitHub 的不满。我也是 GitHub 用户。没错，这段时间确实很难熬。我能说的是，我愿意给它时间和耐心。我知道里面有真正在乎的人，但我们必须做得更好。到此为止。

我在 Peru 时还录了一期 [Cafe con Mito](https://www.youtube.com/@MitoCode)。那一期会在 9 月中旬上线，我很期待。

*这是 DevOps Days 的一张照片。多棒的一群人。*

![Andrea Griffiths 和 DevOps Days Lima 的观众](https://mainbranch.dev/images/issue-38-devops-days-lima.jpeg)

感谢你的阅读，下周见。

Andrea

## 📌 P.S.

9 月 23 日到 25 日，我会在 San Jose 参加 [WeAreDevelopers World Congress North America](https://www.wearedevelopers.com/world-congress-north-america/tickets)。如果门票是唯一拦着你的东西，回复告诉我。

## 💛 支持

如果 Main Branch 对你有用，[订阅](https://mainbranch.beehiiv.com/)或[在 GitHub 上赞助我](https://github.com/sponsors/AndreaGriffiths11)。

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
