---
title: "⏸️ Main Branch：这次，不活跃仓库的告警要暂停了 - Issue #49"
number: 49
date: 2026-11-16
excerpt: "从 2026 年 12 月 8 日起，Dependabot 告警将在不活跃的仓库中暂停；新的 pull request Overview 页面也已进入 public preview。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-49
topics: ["Dependabot", "Pull Requests", "Security", "AI Agents"]
tags: ["dependabot", "pull-requests", "secret-scanning", "personal-software"]
featured: false
---

[Read in English](https://mainbranch.dev/newsletter/issue-49/) • [Leer en Español](https://mainbranch.dev/newsletter/es/issue-49/)

朋友们好，

这周我修复了 IssueCrush 里一个严重的 `shell-quote` 漏洞，一个 override 都没加。`concurrently` 把有漏洞的 `shell-quote` 精确锁定在 1.9.0，所以我在 lockfile 里把 `concurrently` 从 9.2.4 升到 9.2.5，`shell-quote` 也随之升到了 1.12.0。

这个 diff 新增 7 行，删除 7 行。两个版本都通过了 8 个测试套件里的全部 83 个测试。安全探测脚本在 `main` 上复现了这个 bug，在修复版本上则通过了。那一刻我觉得自己脑子特别好使，哈哈。有时候，传递依赖的修复就在依赖链上游的下一个 patch 版本里。

## 🚢 本周上线

### [Dependabot 告警将在不活跃的仓库中暂停](https://github.blog/changelog/2026-11-10-dependabot-alerts-will-pause-on-inactive-repositories/)

从 2026 年 12 月 8 日起，GitHub 将关闭大多数过去一年没有活动的仓库的 Dependabot 告警。现有告警会被归档，你随时可以恢复。GitHub 会把这些操作算作活动：向任意 branch 或 tag 推送、创建仓库，或开启 Dependabot 告警。任何一次推送，或在设置中重新开启告警，都会恢复归档的告警，并重新开始一年的计时。如果某个强制执行（enforced）的 security configuration 开启了告警，或者企业策略不允许管理员开关告警，告警会保持开启。这项变更适用于 github.com 上的所有方案，以及启用数据驻留（data residency）的 GitHub Enterprise Cloud，不适用于 GitHub Enterprise Server。

### [新的 pull request Overview 页面进入 public preview](https://github.blog/changelog/2026-11-05-new-pull-request-overview-page-in-public-preview/)

2026 年 11 月 5 日，GitHub 以 public preview 的形式推出了可选加入的 pull request Overview 页面。它把合并状态和下一步可执行的操作放在页面顶部，组成一个紧凑的就绪摘要；重新设计的 merge box 用不到一半的空间展示同样的信息。Checks、评论和审批也都在旁边。

你可以筛选未解决的对话或自己写的评论，把评论按从新到旧排序，也可以使用右上角的摘要。在页面顶部选择 `Try the Overview page` 即可加入，预览期间也可以通过同一个菜单切回经典 overview。我喜欢它让我不用在长 PR 里没完没了地滚动，不过说实话，我还没完全拿定主意。欢迎在 [Overview 预览讨论](https://github.com/orgs/community/discussions/212186)里分享反馈。

## 📖 我在读什么

[Hacking a new home screen for my Samsung TV](https://cassidoo.co/post/hacking-samsung-tv-screen/)，作者 Cassidy Williams

我的老板 Cassidy 用 GitHub Copilot 和 Nathan Clark 的开源项目 CleanFrame，把三星电视满是广告的主屏幕换成了自己的启动器，又把遥控器的 Home 键改成打开它。这就是个人软件（personal software）的实践：想摆脱那些让你烦的东西，不需要谁批准，也不需要产品团队，哪怕是电视开机太慢这种事。它让人看到，如今借助 agent 能做到多少事。

如果你也曾想解决自己设备上某个烦人的小问题，却觉得不值得花这个力气，这篇值得读。

## 🔧 我在用什么

我在测试一个 secret scan gate，之后准备把它接成会阻止合并的 PR 检查。我在本地的 Git Bash 里跑了 contract script 和一些边界情况：`ghp_`、`github_pat_` 和 `sk-` 的示例都被拦了下来，占位符和只有前缀的字符串都顺利通过，现有的 `src/` 也是零匹配。下一步是放到 GitHub Actions 里跑。

## ✨ 这周

我会在 Nerdearla México 演讲，时间是 11 月 19 日（周四）墨西哥城时间上午 10:10 到 10:50，地点在 Escenario verde（绿色舞台）。演讲题目是 [Corta el loop: el harness es el producto](https://nerdearla.com/en/mexico/schedule/corta-el-loop-el-harness-es-el-producto/)。如果你也在现场，超期待和你线下见面。请一定告诉我你是订阅者，我给你准备了一份礼物。

带着感激，下周见，

Andrea

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
