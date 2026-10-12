---
title: "🚢 让发布前那一刻更诚实的那一期"
number: 29
date: 2026-05-31
excerpt: "Coverage 来到 pull request 上，npm staged publishing 正式 GA，一个 Librarian 模式实验把重复 repo search 的成本算成了美元。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-29
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-shipping-got-more-honest-issue-29
topics: ["GitHub Code Quality", "npm", "Multi-Agent Systems", "Microsoft Build"]
tags: ["code-coverage", "npm", "staged-publishing", "multi-agent-systems", "microsoft-build", "newsletter"]
featured: true
---

朋友们好，

我正在去 San Francisco 的路上，所以这期会短一点。两个 GitHub 功能让代码发布前的那一刻少了一点靠感觉：PR 上的 coverage，以及 npm staged publishing。还有一篇 paper 这几天一直在我脑子里打转，我也做了一个小实验来验证它。如果你在 Microsoft Build，往下滑就能找到我。

## 🚢 最新发布

### [Pull request 里的 code coverage 现在进入 public preview](https://github.blog/changelog/2026-05-29-code-coverage-in-pull-requests-is-now-in-public-preview/)

Coverage 终于出现在它该在的地方：PR 本身。GitHub Code Quality 现在会直接在 pull request 上显示整体代码覆盖率百分比，这样 reviewer 不需要跳到第三方工具，就能看到测试完整度。你可以在现有 CI workflow 里用 [actions/upload-code-coverage](https://github.com/actions/upload-code-coverage) action 上传 Cobertura report。GitHub Apps 和 Actions workflows 需要新的 `code-quality:write` fine-grained permission 才能推送报告。今天已经在 [github.com](https://github.com) 面向 Enterprise Cloud 和 Team 可用，preview 期间免费。Enterprise Server 还不包含在内。

### [npm 的 staged publishing 和新的安装时控制](https://github.blog/changelog/2026-05-29-staged-publishing-and-new-install-time-controls-for-npm/)

npm CLI 11.15.0 里有两个值得知道的更新。Staged publishing 正式 generally available：不再是直接 `npm publish` 后立刻上线，tarball 会先进入 stage queue，直到 maintainer 通过 2FA challenge 批准。把它和 trusted publishing (OIDC) 配在一起，并把 CI workflows 锁成只能 stage，这样非交互式 publish 永远不会自动 release。三个新的 install flags（`--allow-file`、`--allow-remote`、`--allow-directory`）加入 `--allow-git`，每个都接受 `all` 或 `none`。Heads-up：`--allow-git` 的 default 会在 npm CLI v12 里变成 `none`。

## 📖 我在读

**Cho、Choi、Heo、Choi、Moon、Park 和 Kim 的 "Long Live the Librarian!"（[arxiv.org/abs/2605.27787](https://arxiv.org/abs/2605.27787)）**

Multi-agent SWE systems 会浪费大量 output tokens，因为它们反复探索同一批文件。这篇 paper 把这件事量化了：output tokens 的能耗比 input tokens 或 cached tokens 高 30 到 1,000 倍。它提出了一个持久化 search sub-agent，负责追踪 repo-search history，并返回短引用，而不是完整文件 excerpts。在 SWE-Bench Verified 上，这能把每个 episode 的 GPU energy 降低最多 25%，同时不损失任务表现。

值得花时间读，如果：你在 ship 任何包含多个 agent 的东西，并且想知道浪费到底藏在哪里。

## 🔧 我在用

我读完 Librarian paper 之后想要美元数字，所以做了 [github.com/AndreaGriffiths11/librarian-demo](https://github.com/AndreaGriffiths11/librarian-demo)：一个 harness，通过 GitHub Copilot proxy 在 Claude Opus 4.6 上跑 5 个 reviewer agents，审一个 16K-token PR。我测了三种模式的 token counts：naive $1.32，prompt cache $0.45 warm，librarian-pattern digest $0.49 cold-every-call。Cache 在 warm series 里赢；当你的 bot 要服务来自很多 dev、很多 repo 的 PR 时，Librarian 赢。

## ✨ 本周

我这周都在 Microsoft Build，在 GitHub Commons pavilion demo GitHub app。如果你在现场，来找我。不在 San Francisco？可以去 [gh.io/microsoft-build](https://gh.io/microsoft-build) 注册线上参会，然后一起跟进。Build 之后，我会加入 GitHub Universe content committee，帮忙选择今年的 speakers。如果你提交了 talk，回复告诉我。

下周见。

怀着感激，  
Andrea

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
