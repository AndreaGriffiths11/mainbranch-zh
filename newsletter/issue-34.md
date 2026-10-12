---
title: "🚧 Main Branch 技术周刊：给 pull requests 划边界"
number: 34
date: 2026-07-27
excerpt: "归档 pull requests、actions/checkout 对 pull_request_target 的强制限制，以及 VS Code 的 Team X-Ray。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-34
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-pull-requests-get-boundaries-issue-34
topics: ["Pull Requests", "GitHub Actions", "Supply Chain Security", "VS Code"]
tags: ["pull-requests", "github-actions", "actions-checkout", "pull-request-target", "supply-chain-security", "team-xray", "newsletter"]
featured: false
---

朋友们好，

这次有两个更新，决定了一个 pull request 能做什么，以及谁能看到它。一个是 maintainers 想要多年的 moderation 工具。另一个是安全 default，不管你有没有看 changelog，它已经自动应用到了你的 workflows。

## 🚢 最新发布

**[Repository admins 现在可以 archive pull requests](https://github.blog/changelog/2026-07-16-repository-admins-can-archive-pull-requests/)**（7 月 16 日）

Archive 一个 PR 会把它关闭、锁定，并且对 repository admins 以外的所有人隐藏。非 admin 打开这个 URL 会看到 404。你可以批量 archive，也可以一个个来。Unarchive 之后，它仍然是关闭和锁定的状态。

到现在为止，处理 spam 或恶意 PR 意味着删除它，也连同记录一起丢掉。Archive 保留了给 admins 查看的历史，同时把它移出公开视野，也适用于 policy 或 legal 要求你不能删除任何东西的情况。热门 public repos 的 maintainers 想要这个已经很久了。Triage 时用 `is:archived` 把它们找回来。

**[actions/checkout 在 pull_request_target 中拒绝 checkout forks](https://github.blog/changelog/2026-06-18-safer-pull_request_target-defaults-for-github-actions-checkout/)**（7 月 20 日开始强制执行）

`pull_request_target` 使用 base repository 的 `GITHUB_TOKEN`、它的 secrets，以及 default branch cache access。在这个上下文里 checkout 一个未经 review 的 fork PR，就是多个 supply chain incidents 背后的 "pwn request" 模式。

v7 在 6 月发布时默认拒绝这种操作。7 月 20 日，这项强制措施 backport 到每个受支持的 major version，所以像 `actions/checkout@v4` 这样的 floating tag 自动收到了它。Pinned SHAs 没有，仍然需要升级。

现在会失败的是这种写法：

```yaml
# pull_request_target workflow，来自 fork 的 PR
- uses: actions/checkout@v4
  with:
    ref: refs/pull/${{ github.event.pull_request.number }}/merge
```

`ref:` 设为 fork 的 head SHA，或者 `repository:` 最终指向 fork，也一样。

## 📖 我在读

**[The Land and Its People](https://www.davidsedarisbooks.com/titles/david-sedaris/the-land-and-its-people/9780316607339/)**，David Sedaris 著

我喜欢 Sedaris 很多年了。我喜欢他的写法。这本是一本 essays 集，写到当外国人、当兄弟、当一辈子的朋友，也有一段写他在伴侣手术后试着当 caretaker，结果卡在做得好和做得不太好之间。

值得花时间读，如果：你喜欢机智的文字，也需要一小时把脑袋从工作里拿出来。

## 🔧 我在用

Team X-Ray，我自己的 VS Code extension。它读取你本地的 git history、commits、contributors 和 file ownership，然后做出一张谁真正懂 repo 里哪些东西的地图。

[VS Code Marketplace 上的 Team X-Ray](https://marketplace.visualstudio.com/items?itemName=AndreaGriffiths.teamxray)

## ✨ 本周

我正在收尾这一段旅行。上周我在 [Nebraska Code](https://nebraskacode.amegala.com/) 演讲，这是我第一次去 Nebraska，也是我第一次参加 Midwest conference。这是一场很棒的 conference，有很多细小但周到的安排。人们真的很友善。

IRL events 依然是你遇见人、捡到你原本没有在找的东西的地方。Nebraska Code 的 organizers 很在意让 talks 保持高水准。他们请 speakers 不要让 AI 替他们思考。如果你站在台上，你应该足够了解自己的内容，可以跟房间里的人讲，而不是把一篇 script 读回给大家。我讲的是 Team X-Ray。

这周也是我的生日，在 31 号星期五。又绕太阳一圈，我很感激能和家人、朋友在一起。年纪越大，我越能坦然面对那些为了好好活着而做的选择和牺牲，也越愿意对作为妈妈、妻子和朋友的自己多一点宽容。别像我一样，等那么久才明白，真实的友谊、爱，还有肺里的呼吸有多么美好。

带着感激，

Andrea

## 📌 附言

有些人读 Main Branch 很久了，可能记得 [Issue #20](https://mainbranch.dev/newsletter/issue-20/)，我最年长的狗 Charlie 当时撕裂了他的 CCL。7 月 17 日，我们不得不用尽可能有爱、有同理心的方式让他离开。他在家里留下了一个大洞，我觉得另一只狗 Wilson 是最难过的那个。Charlie 是他的伙伴。感谢每一个写信来、理解他对我们意味着什么的人。没有养过狗的人，很难解释那一部分。他真的是家人。

我写过他，也写过我们怎么遇见他的。如果你想好好哭一场，去读 [Let Me Tell You About Charlie](https://andreagriffiths.dev/blog/let-me-tell-you-about-charlie)。

### 世界最大的开发者活动来到 Silicon Valley

[![WeAreDevelopers World Congress](https://mainbranch.dev/images/issue-34-wearedevelopers-banner.png)](https://www.wearedevelopers.com/world-congress-north-america?utm_source=beehiiv&utm_medium=cpc&utm_content=WWC26_US&utm_campaign=ZBSVLTZKDC)

一次旅行，让你的团队不再猜测 AI adoption、platform、security 和 tooling。

[WeAreDevelopers World Congress](https://www.wearedevelopers.com/world-congress-north-america?utm_source=beehiiv&utm_medium=cpc&utm_content=WWC26_US&utm_campaign=ZBSVLTZKDC)，2026 年 9 月 23-25 日，San José, CA，Silicon Valley 的中心。500 多位 speakers 和 10,000 多位 developers 一起解决真正会进入 production 的问题：coding agents、evals、MCP、observability、agent security。

Kelsey Hightower。Thomas Dohmke（GitHub 前 CEO）。Christine Yen（Honeycomb CEO）。Mathias Biilmann（Netlify CEO）。Olivier Pomel（Datadog CEO）。每天在构建你所用工具的人，全都在一个舞台上。

带着一份短短的决策清单来，带着答案和活动后还能联系到的人离开。越接近活动，价格越高。

使用代码 **GITPUSH26** 获得 10% 折扣。

_[领取你的门票](https://www.wearedevelopers.com/world-congress-north-america?utm_source=beehiiv&utm_medium=cpc&utm_content=WWC26_US&utm_campaign=ZBSVLTZKDC)_

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
