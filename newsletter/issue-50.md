---
title: "⏳ Main Branch：这次，gh 会等着你的 PR - Issue #50"
number: 50
date: 2026-11-23
excerpt: "GitHub CLI 现在可以等待 pull request 事件，Red Hat Enterprise Linux runner 镜像也已面向 GitHub Actions 正式提供。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-50
topics: ["GitHub CLI", "GitHub Actions", "Pull Requests"]
tags: ["github-cli", "github-actions", "pull-requests", "rhel"]
featured: false
---

[Read in English](https://mainbranch.dev/newsletter/issue-50/) • [Leer en Español](https://mainbranch.dev/newsletter/es/issue-50/)

朋友们好，

我现在人在 CDMX 的登机口，刚结束在 [Nerdearla](https://nerdearla.com/en/mexico/) 度过的精彩一周。能见到老朋友、认识新朋友，还遇到了编程界的传奇人物 [Mary Ann Horton](https://en.wikipedia.org/wiki/Mary_Ann_Horton)，当然也吃了想吃的所有 chilaquiles，虽然那根本不是早餐时间。这周太棒了。我的演讲《Corta el loop》讲的是那些真正影响模型响应的因素，也就是模型周围的 harness。我正在写一篇博客文章，之后会分享出来。与此同时，这是[西班牙语版的演讲幻灯片](https://mainbranch.dev/talks/corta-el-loop/)。下面进入本周上线：

## 🚢 本周上线

### [使用 GitHub CLI 等待 pull request 事件](https://github.blog/changelog/2026-11-18-wait-for-pull-request-events-with-github-cli/)

如果你曾经把 `gh pr view` 放进 `while` 循环里等 review，或者看着 agent 不停消耗 token 问“CI 好了吗？”，GitHub CLI 2.105.0 带来了一个解决方案。`gh event listen` 接收 pull request URL 和你关心的事件，找到第一条匹配后以 JSON 打印出来，然后退出。它支持 review、状态和 head 变更、merge 冲突，以及已完成的 check suite。

这个功能还在 preview 中，而且需要同样处于 preview 的 Event Streams，所以先加入[候补名单](https://gh.io/event-streams-signup)吧。

### [Red Hat Enterprise Linux runner 镜像现已正式提供](https://github.blog/changelog/2026-11-19-red-hat-enterprise-linux-runner-images-now-generally-available/)

GitHub 托管的 larger runner 现在正式提供 RHEL 9 和 RHEL 10 镜像，并支持生产 workflow。

如果生产环境跑 RHEL，而 CI 跑 Ubuntu，你可能遇到过这种情况：某个 package 在 CI 里通过，部署时却坏掉。现在你可以在实际部署的操作系统上测试，也可以基于它构建 custom image。创建 Linux x64 larger runner，然后在 partner images 里选择 RHEL。Preview runner 仍然可以继续使用。该功能适用于 GitHub Team 和 GitHub Enterprise Cloud。

## 📖 我在读什么

[Maximizing Success in Engineering Interviews](https://www.no.lol/2019-03-25-maximizing-success-in-engineering-interviews/)，作者 Lauren Tan

Lauren 在 2019 年写下这篇文章，起因是她和一位刚入行、不断面试却没有得到反馈的人进行了一次 1:1。她先把面试结果和你作为工程师的价值分开，因为公司宁愿错过一个好工程师，也不愿意招到一个糟糕的工程师。从简单的地方开始，留意提示，讲清楚你的 tradeoff，不知道的时候就说“我不知道”。我最想划线的一点是：即使面试官懂技术，也要解释你在做什么、为什么这样做，并问对方是否需要更多细节。

如果你正在面试，或者你坐在面试桌的另一边，这篇值得花时间读。

## 🔧 我在用什么

我会用不止一个 AI 工具，而 [Faros Desktop](https://fandf.co/3XuTCXP) 把它们放进同一个视图，还会显示按公开 API 价格计算出来的使用价值。它免费、不需要登录，prompt 会留在你的 Mac 上。[这里有一个演示视频](https://x.com/acolombiadev/status/2122736876364632430)。

## ✨ 这周

现在是美国 Thanksgiving，你的女孩已经像炸火鸡一样 crispy 了，所以这周我要和家人休息一下，处理家里的事情，再写点东西。ICYMI，[mainbranch.dev](https://mainbranch.dev) 最近换了新 look，多亏了我那台 [Ultra](https://www.microsoft.com/en-us/surface/devices/surface-laptop-ultra) 上的本地推理，还有太多次飞行。去看看，然后告诉我你的想法。

谢谢你们，
Andrea

## 📌 P.S.

在找工作？[treg](https://treg.to/jobs-api) 可以让你的 agent 在 Greenhouse、Lever 和 Ashby 上搜索开放职位，还能获取真实发布的薪资数据，按调用付费。它是开源的，你也可以自己部署。

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
