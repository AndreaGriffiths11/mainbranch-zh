---
title: "💥 Main Branch 技术周刊：这次你的覆盖率检查一直在骗你"
number: 43
date: 2026-10-04
excerpt: "新分支上传覆盖率不再导致 CI 失败，dynamic workflows 登陆 Copilot CLI 和 Copilot 应用。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-43
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-your-coverage-check-was-lying-issue-43
topics: ["GitHub Actions", "Code Coverage", "Copilot CLI", "AI Agents"]
tags: ["code-coverage", "github-actions", "copilot-cli", "dynamic-workflows", "hydrafusion"]
featured: false
---

*作者：Andrea Griffiths • [Leer en Español](https://mainbranch.dev/newsletter/es/) • [阅读中文版](https://mainbranch.dev/newsletter/zh/)*

朋友们好，

已经十月了。我这个周末都在布置万圣节装饰。虽然我住在佛罗里达，这里一年到头热得要命，但我真的很喜欢秋天。

这是我最喜欢的季节，也是我最忙的时候。我正在为 [GitHub Universe](https://github.blog/news-insights/company-news/10-technical-talks-im-excited-about-at-github-universe-2026/) 做准备，今年会很特别。我有一件非常重要的事要和大家分享，希望下周就能说。先来看看发布了什么。

## 🚢 最新发布

**[新分支上传代码覆盖率不再导致 CI 失败](https://github.blog/changelog/2026-10-01-code-coverage-uploads-no-longer-fail-ci-for-new-branches)**

以前如果你在 PR 创建之前就 push 了分支，`upload-code-coverage` 会让 job 失败。API 需要 PR 编号，但当时还没有。现在它会跳过上传，并明确提示。默认分支和 PR 事件照常上传。如果你只在 `push` 上运行，覆盖率要等到 PR 打开后的下一次 push 才会上传。想早点拿到，就加一个 `pull_request` trigger。适用于 Team 和 Enterprise Cloud，包括 data residency。不支持 Enterprise Server。

**[Copilot CLI 和 Copilot 应用支持 dynamic workflows](https://github.blog/changelog/2026-10-01-dynamic-workflows-in-copilot-cli-and-the-copilot-app)**

公开预览，所有 Copilot 套餐都能用，覆盖应用、CLI 和 SDK。你在 Copilot 扩展里用代码写出每个步骤，包括哪些并行运行、什么时候轮到 agent 执行。`/fleet` 仍然负责分发任务，而这个功能运行的是你自己写好的流程。应用无需配置。在 CLI 中，用 `/experimental on`（或 `--experimental`），版本落后的话先运行 `/update`。可以让 Copilot 帮你写一个，或者问它你已经有哪些。

## 📖 我在读什么

**[A warning about ‘model welfare’](https://mustafa-suleyman.ai/a-warning-about-model-welfare)**

Mustafa Suleyman 的文章，引用了 Anthropic 2026 年 1 月发布的 Claude constitution，包括 Claude 的道德地位“live enough to warrant caution”（现实到需要谨慎对待）这句话，以及 Opus 3 的退役访谈。他提出了三点反对意见：循环论证、拟人化，以及意识是生物性的这一观点。这一点我站他这边。我不敢相信我们在给人造的东西赋予生物属性。

如果你想知道前沿实验室里在发生什么，这篇值得一读。有些人好像看完 [Westworld](https://www.imdb.com/title/tt0475784/)（《西部世界》），还以为那是纪录片。

## 🔧 我在用什么

HydraFusion。single、cascade、critique 这些模式不是 GitHub 发明的，你本来就在手动用。HydraFusion 是个捷径：它根据你的 prompt 选择模式，再分派任务。在我和 Julia Kasper 的 [Checkout 节目](https://youtu.be/EeOz2w5wPEI)里，她展示了：84.8 AIU（AI 单位），对比单独用 Opus 5 的 146.5 和单独用 Fable 5.1 的 159。现在应用里也能用了，我正在开心地做实验，把结果和未使用 HydraFusion 的 session 做对比。

## ✨ 本周动态

我在准备月底要落地的各项事情，所以这周很忙。另外，等你读到这里的时候，我应该正准备抽出（好吧，是让 Copilot 抽出）门票赠送的获奖者。最后参与机会：[gh.io/win](https://gh.io/win)。

下周见！

谢谢你，  
Andrea

## 💛 支持 Main Branch

[订阅 Main Branch](https://mainbranch.dev) • [在 GitHub 上赞助我](https://github.com/sponsors/AndreaGriffiths11)

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
