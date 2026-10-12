---
title: "🥞 Main Branch 技术周刊：拆开巨型 PR"
number: 35
date: 2026-08-09
excerpt: "Stacked pull requests、Dependabot 分支名称，以及对 AGENTS.md 文件的基准测试。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-35
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-the-giant-pr-gets-broken-up-issue-35
topics: ["Pull Requests", "GitHub CLI", "Dependabot", "Open Source", "AI Agents", "Node.js"]
tags: ["pull-requests", "stacked-prs", "gh-stack", "dependabot", "open-source", "agent-plugins", "agents-md", "benchmarking", "nodejs", "newsletter"]
featured: false
---

朋友们好，

下周我会去亚特兰大。最近我读到的大部分内容都在讨论，支撑 open source 的人还愿不愿意继续做下去。下面会多说一点。

产品这边，stacked pull requests 进入了 public preview。我拿一个足够混乱的 repo 跑了一遍，看看它们实际要付出什么成本。

## 🚢 最新发布

### [Stacked pull requests 进入 public preview](https://github.blog/changelog/2026-07-30-stacked-pull-requests-are-now-in-public-preview/)

一个 stack 是一串 pull requests，每个 PR 的目标都是它下面的 branch，而不是 `main`，这样 reviewer 一次看到的是一层，而不是整个改动。

我把一个 fix 重建成了三层 stack，放进一个带着 10 个过期 draft 的 repo 里。它的 test suite 还因为一个 Playwright test 放在 Jest 目录中而失败。先处理 test runners，再处理 locale 行为，最后做浏览器 coverage 和 CI。GitHub 显示为 3/3。

三层都跑了 CI 和 CodeQL。stack 里的每个 pull request 都会以 stack 的 base 为基准进行评估，所以 check 分钟数会随 stack 深度增长。workflow 表达式中可以用 `github.event.pull_request.stack.position` 和 `.size`，这样你可以在每层运行快速 checks，再把完整 suite 留给最顶层或尚未 merge 的最低层。

```bash
gh extension install github/gh-stack
```

### [Dependabot branch 名称现可配置](https://github.blog/changelog/2026-08-04-customize-dependabot-pull-request-branch-names/)

`.github/dependabot.yml` 中新增的 `pull-request-branch-name` 选项可以设置前缀、最大长度、分段和单词分隔符、字母大小写，或完整模板。

```yaml
pull-request-branch-name:
  separator: "-"
  word-separator: "-"
  branch-name-case: "lowercase"
  max-length: 50
```

它会把 `dependabot/npm_and_yarn/Lodash-4.17.21` 变成 `dependabot-npm-and-yarn-lodash-4.17.21`。如果你的 CI 强制命名规则或长度限制，这会很有用。如果你在 monorepo 中，默认名称容易混在一起，它也能帮上忙。不配置任何内容时，默认值完全不变。现已在 github.com 提供，之后会进入 GitHub Enterprise Server 3.23。

## 📖 我在读

**Open Source Must Be Fun (Or It Will Die)**，Mike McQuaid 著

我很幸运能称 Mike 为朋友，也长期欣赏他的职业生涯。他运营 Homebrew 接近 17 年，始终没有 burnout。他非常坚定地保护自己的 maintainers 和项目，而且做得很有风度。

文章开头是一场电话会议，会上请 maintainers 举手，如果过去六个月比之前六个月更好。他是唯一举手的人。他认为 open source 中稀缺的资源是 maintainer 的动力，而钱只有多到足以让一个人减少有薪工作时间时，才能买来时间。

值得读，如果：你维护任何有用户的东西，或者你资助维护项目的人。

[阅读原文](https://mikemcquaid.com/open-source-must-be-fun-or-it-will-die/)

## 🔧 我在用

[Agent Plugins](https://agent-plugins.org/) 现在到了 1.0.0。这是一种 vendor-neutral 格式，用于打包 skills 和 MCP servers，核心 maintainers 来自 Amazon、Cursor、Microsoft、OpenAI 和 Vercel。更多 agent guidance 很快会被打包并分发。

所以我开始做一个 GitHub Copilot plugin，用来 benchmark `AGENTS.md` 文件。它会在有和没有 repo instructions 的情况下运行同一个 coding task，再比较多次运行的结果。这样你能看出这些 guidance 是否真的改善结果，还是只是听起来有帮助。

很快会分享出来。

## ✨ 本周

8 月 12 日和 13 日，我会在亚特兰大市中心 RenderATL 内举办的 Node.js Interactive 上演讲。OpenJS Foundation 邀请了我，我很感谢他们为 Node ecosystem 所做的一切。我的演讲题目是 Node.js After the AI Shift: Building tools developers can trust，也很期待成为 RenderATL 首届 Node.js Interactive 的一部分。

我参加过第一届 RenderATL，此后也一直在那里演讲。我不断回去，是因为 Justin Samuels 和他的团队打造了那个氛围。他们每年都会公布 impact numbers，现在已经有超过 5500 万美元流入 Atlanta。别错过这场。如果你也在那里，来打个招呼。

带着感激，

下周见，

Andrea

## 📌 P.S.

我有两张 RenderATL 的免费门票。如果你想在 8 月 12 日和 13 日来亚特兰大，直接回复告诉我。先到先得。

## 💛 支持 Main Branch

订阅：https://mainbranch.beehiiv.com/

赞助：https://github.com/sponsors/AndreaGriffiths11

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
