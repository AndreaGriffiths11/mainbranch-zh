---
title: "🚧 Main Branch 技术周刊：这次给 workflow 划定边界 - Issue #41"
number: 41
date: 2026-09-20
excerpt: "Ubuntu 26.04、GitHub Actions 的 workflow 执行保护，以及 Jev 返回的带类型决策"
author: Andrea Griffiths
language: zh
relatedSlug: issue-41
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-workflows-get-boundaries-issue-41
topics: ["GitHub Actions", "Ubuntu", "Product Engineering", "TypeSafe AI", "Jev"]
tags: ["github-actions", "ubuntu", "workflow-security", "product-engineering", "typesafe-ai", "jev", "newsletter"]
featured: false
---

*作者 Andrea Griffiths • [Leer en Español](https://mainbranch.dev/newsletter/es/) • [阅读中文版](https://mainbranch.dev/newsletter/zh/)*

朋友们好，

这周发布的两项变更指向同一个方向。一项改变 runner 的底层环境，另一项决定谁有资格启动 workflow。两项都不会先征求你的同意。`ubuntu-latest` 按计划迁移，公共仓库则会收到默认策略，无论有没有人打开过设置。这周你要做的，就是查清哪些 workflow 会受影响。

## 🚢 最新发布

**[Ubuntu 26 正式发布及 latest 迁移](https://github.blog/changelog/2026-09-17-ubuntu-26-generally-available-and-latest-migration/)**

Ubuntu 26.04 已结束公开预览，在 x64 和 arm64 托管 runner 上都已全面支持生产 workflow。10 月 19 日至 11 月 19 日期间，`ubuntu-latest` 会自动从 24.04 迁移到 26.04，所以只要用了这个标签，无论你准备好了没有，都会迁移。与之前的镜像相比，新镜像更新了工具及其版本，也移除了其中一些，依赖特定软件版本或预装包的 workflow 可能因此出错。现在就用 `runs-on: ubuntu-26.04` 或 `ubuntu-26.04-arm` 提前试试，看看哪里会出问题。如果需要更多时间，就固定使用 `ubuntu-24.04`。

**[GitHub Actions 的 workflow 执行保护正式发布](https://github.blog/changelog/2026-09-17-workflow-execution-protections-in-github-actions-generally-available)**

Actor rules 用允许列表规定谁可以触发 workflow，event rules 则规定哪些事件可以启动它。Actions 会在每次运行前评估这两类规则，让贡献代码的权限与运行 CI 的权限分开。正式版增加了按 workflow 文件指定规则的能力，你可以把 `deploy.yml` 限定为只有一个团队能运行，同时让 CI 继续对所有人开放。Insights 会显示哪些运行将被阻止，REST API 则让你可以用代码管理规则。没有适用事件策略的公共仓库会收到一项默认策略，禁用 `pull_request_target`。这项策略目前处于 evaluate 模式，将于 11 月 2 日开始强制执行。私有和内部仓库不会自动应用这项默认策略。现在就检查 Insights，然后决定保留阻止规则，还是按 workflow 文件显式允许 `pull_request_target`。

## 📖 我在读

**[我们现在都是产品工程师了](https://seldo.com/posts/we-are-all-product-engineers-now/)，作者 Laurie Voss**

Laurie 是 npm 的联合创始人，所以当他说编写软件的成本骤降，三十年来所有变量第一次都变了，这话的分量就不一样。他把工作拆开，逐项看哪些部分会被 agent 接手。写代码，已经被接手了；审查和维护，正在被接手；接下来是发布和扩展规模。留下来的工作，是弄清一个人到底想要什么，再把需求定义得足够精确，让人能据此做出来。因为这些知识只在某个面包师的脑子里，从来没有写下来，也不在任何训练数据中。他指出，这份工作早就存在，叫系统分析师，二十五年前才拆成产品和工程两个方向。行业需要有背景知识和判断力的人，而 Google 的 APM 项目每年从一万两千名申请者中只招收大约五十人。

如果你想过五年后自己的工作会是什么样，这篇值得读。

## 🔧 我在用

Jev，[TypeSafe AI](https://typesafe.ai/) 的第一个 System One Model。它返回带类型的决策和置信度估计来代替自然语言段落，你的代码可以设定阈值，决定什么时候采取行动、什么时候请求审查。我拿一个经常遇到的问题试了试：这个文件能删吗？我用了一个小工具，收集 git 历史和引用，标出无法确定的地方，再把同一份证据交给 Jev，让它判断这些证据对删除文件的支持程度，以及还有哪些不确定性。

## ✨ 本周

我要去圣何塞参加 WeAreDevelopers World Congress，这是大会第一次来到美国。我之前在柏林参加过两次，技术内容有深度，也能遇到值得认识的人，这趟很值。我的演讲在周五，会聊聊我的 VS Code 扩展 [Team X-Ray](https://github.com/AndreaGriffiths11/teamxray)，以及从一年前开始做它到现在，它发生了哪些变化。在这个行业，一年就是一个地质年代。

心怀感激，

Andrea

## 📌 附言

如果你想来但还没有票，回复这封邮件，我给你安排一张。如果你已经打算来，给 [@acolombiadev](https://x.com/acolombiadev) 发条私信，我们可以见个面。

## 💛 支持

[订阅 Main Branch](https://mainbranch.dev) • [在 GitHub 上赞助我](https://github.com/sponsors/AndreaGriffiths11)

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
