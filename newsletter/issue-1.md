---
title: "🚢 Main Branch：就是那种，好东西全被你们错过了的那期"
number: 1
date: 2025-11-17
excerpt: "当大家都在聊 Universe 上的 AI agent 时，这些功能悄悄上线了。来看看你错过了什么。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-1
beehiivUrl: https://mainbranch.beehiiv.com/p/mainbranch-issue-1
topics: ["GitHub", "Pull Requests", "GitHub Actions", "Code Review"]
tags: ["github-features", "actions", "pull-requests", "performance"]
featured: true
---

![Adventuring through the Canadian Rockies](https://media.beehiiv.com/cdn-cgi/image/fit=scale-down,quality=80,format=auto,onerror=redirect/uploads/asset/file/a63a5965-a0fa-43c2-a843-32d330bc3deb/thumbnail.png)

嗨，朋友们！欢迎来到 Main Branch，一份关注最近上线的开发工具和功能的周刊，重点聊那些帮你日常干活更顺手的基础能力。

我是 Andrea，GitHub 的高级开发者布道师。我每周都在跟产品团队聊天、搭 demo、写东西，还在 GitHub 的 Open Source Friday、Checkout、Podcast 等[直播](https://www.youtube.com/@acolombiadev)里出没。这份周刊就是我帮你过滤噪音，把真正值得关注的东西挑出来。

对，AI 的东西我也会聊。但基础优先，永远是。

关于 Universe 2025。Keynote 之后我收到的每隔一条私信都是这种画风："agent 是挺酷的兄弟，但除了这个还有啥？"

我理解。Agent HQ 确实很炸裂。但你知道什么也很有用吗？能在 PR 里对没改过的行加评论。更快的 Actions runner 不再吃光你的预算。就是你每天用五十次的那些东西。

这些功能不是在 Universe 发布的——过去几个月它们一直在悄悄上线，而大家都在忙着争论 AI 到底会不会取代我们。（剧透：[不会](https://x.com/eyishazyer/status/1986390259987587427?s=20)）。

所以，来看看最近上线的你可能错过的好东西。

## 🚢 新动态

**PR 里终于可以在任意位置评论了**

新版 ["Files changed"](https://github.blog/changelog/2025-09-25-pull-request-files-changed-public-preview-now-supports-commenting-on-unchanged-lines/) 页面让你可以对任何改动文件里的任意一行评论，不再只限于改动行加上下三行上下文。需要标记一个本该改但没改的地方？想对改动周围的代码提建议？现在可以了。Code review 不只是看改了什么。有时候最好的反馈是指出旁边那些没动的代码其实该动。这个功能在 public preview 中——去任意 PR 的 Files changed 标签页顶部开启就行。

**GitHub Actions 性能升级**

Actions 用户一直求的三个东西：[可复用 workflow 限制提升](https://docs.github.com/en/enterprise-server@3.15/actions/reference/workflows-and-actions/reusing-workflow-configurations#limitations-of-reusable-workflows)（最多 10 层嵌套、50 次总调用）、[M2 芯片 macOS runner](https://github.com/github/roadmap/issues)（终于有 Apple Silicon 构建了），以及 preview 中的 [1 vCPU Linux runner](https://github.blog/changelog/2025-10-28-1-vcpu-linux-runner-now-available-in-github-actions-in-public-preview/)，专门跑轻量任务。不是所有东西都需要 4 核来跑 npm install 的。

## 🎧 推荐收听

**Acquired Podcast: Microsoft**

因为 Peter Attia 在他的播客里随口推荐了这个才开始听的（长寿研究 → 十小时科技深度访谈，很合理）。刚听到微软在 1980 年代发明了产品驱动增长的部分。给开发者工具，让构建变简单，让他们帮你卖。Gates 四十年前就想明白了。如果你好奇过为什么"免费层 → 病毒式传播 → 企业采购"这个路径感觉像宿命，值得一听。[在 Acquired.fm 收听](https://www.acquired.fm/episodes/microsoft)

## 🔧 在用什么

GitHub Projects 入门体验[改进](https://github.blog/changelog/2025-11-06-improved-onboarding-flow-for-github-projects/)了（导入 issues/PR、默认仓库、工作流更新）——终于让我想用 Projects 了。

## ✨ 这周

我的公婆刚结束了 3 周半的拜访。我很期待下次再见到他们，但我也很期待能独自在家待上 20 分钟，坐在完全的安静里 😉。

这周就这些！没有 AI 炒作，就是帮你出活的功能。

觉得有用的话转发给你的团队，回复告诉我你下次想看什么内容。

感恩，  
Andrea

P.S. 对，AI 的东西我也会聊。但基础优先，永远是。
$

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
