---
title: "⚡ Main Branch 技术周刊：让 steps 不再排队"
number: 32
date: 2026-06-29
excerpt: "GitHub Actions 现在可以并行跑 steps，你的 issues 列表也终于有了值得共享的 saved views。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-32
beehiivUrl: https://mainbranch.beehiiv.com/p/the-one-where-steps-stop-standing-in-line-issue-32
topics: ["GitHub Actions", "GitHub Issues", "CI/CD", "Developer Tools"]
tags: ["github-actions", "parallel-steps", "saved-views", "github-issues", "ci-cd", "newsletter"]
featured: true
---

朋友们好，

如果你曾经看着一个 workflow 一个 step 一个 step 地慢慢爬，或者这周第十次重建同一个 issue 过滤器，那这周的两个更新都是为你准备的。GitHub 恰好修掉了这两种等待。

## 🚢 最新发布

**[Actions 的 steps 现在可以并行跑了](https://github.blog/changelog/2026-06-25-actions-steps-can-now-be-run-in-parallel/)。** 在此之前，一个 job 里的每个 step 都按顺序跑，每一个都要等上一个跑完。你可以用 shell 的 `&` 把一个 step 丢到 background，但日志会交错成一团乱。从 6 月 25 日起，四个新关键字解决了这个问题：`background: true` 启动一个 step 然后继续往下走，`wait`/`wait-all` 会暂停，直到你点名的那些 background steps 跑完，`cancel` 干净地停掉一个你不再需要的 step，`parallel` 把一组 steps 包起来并在结尾加一个 `wait`。日志保持分开。一边在 background 起一个服务，一边跑依赖它的工作，或者在一个 job 里同时编译多个 target。

**[仓库 issues 的 saved views](https://github.blog/changelog/2026-06-25-saved-views-for-repository-issues-and-adjustable-row-heights-in-projects/) 进入了 public preview。** 任何有 triage access 或更高权限的人，现在都能建立共享的过滤视图，比如 "Unassigned bugs" 或 "Needs triage"，设置一次，整个 repo 看到的就是同一份。它们住在一个新的 Issues 侧边栏里，旁边是 `Assigned to me`、`Created by me`、`Mentioned` 这些快捷入口。这个侧边栏也给 Projects 安了个家，并把 milestones 和 labels 露出来。如果你维护着任何持续有 issues 涌进来的东西，这就是「所有人各自重建同一个过滤器」和「所有人从同一个过滤器开工」之间的差别。

## 🎧 我在听

**[Acquired: Ferrari](https://www.acquired.fm/episodes/ferrari)，由 Ben Gilbert 和 David Rosenthal 主持**

这不是一期讲技术的节目。我终于抽出时间听了，它是我最近一段时间听过最好的东西之一。贯穿始终的主线是：Ferrari 把整个生意建立在「决定不做什么」的判断上，把产量始终保持在比需求低一辆车的水平，拒绝那种会稀释这件东西本身的规模。

值得花时间听，如果：你喜欢商业史，或者你曾经靠着「我选择不做什么」来为一个决定辩护过。

## 🔧 我在用

_Andrea's Field Notes_，一个真正在用的 Copilot [app canvas](https://awesome-copilot.github.com/learning-hub/working-with-canvas-extensions/)，它把我正在做或在追踪的一切都收在一起：DevRel 信号、Copilot/App/CLI 的点子、AAIF Ambassador 的工作、志愿项目、demos、内容线索、给 LT-report 的凭证。它是我在决定什么值得花时间之前会去看的唯一一个地方。用这个 [prompt](https://gist.github.com/AndreaGriffiths11/896d37a0ba6e814cd25c0f585f42139f) 搭一个你自己的。

## ✨ 本周

我在哥伦比亚休息一阵，这基本上意味着把自己吃成一个 pandebono，外加被世界杯吓出的几次轻微心脏病发作。此刻我的心为委内瑞拉而沉重，如果你有余力帮忙，Yummy 正在协调援助，好几家公司也承诺会按比例配捐：[Dona con Yummy](https://dona.yummyrides.com/)。

<img src="https://mainbranch.dev/images/issue-32-seleccion-colombia.jpg" alt="准备好为哥伦比亚国家队（la selección Colombia）加油" style="max-width: 400px; display: block; margin-left: auto; margin-right: auto;" />

两周后见。

怀着感激，
Andrea

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
