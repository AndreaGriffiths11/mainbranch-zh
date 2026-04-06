---
title: "🔄 Main Branch：就是那种，hooks 自己会更新的那期"
number: 18
date: 2026-03-15
excerpt: "这周发了两个实打实的东西。跟 AI 没半毛钱关系。但都能帮你少踩坑。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-18
beehiivUrl: https://mainbranch.beehiiv.com/p/ce293bb4-3da9-4ad2-b990-7c320eaa357b
topics: ["GitHub", "Dependabot", "OIDC", "GitHub Actions", "Security"]
tags: ["dependabot", "pre-commit", "oidc", "github-actions"]
featured: true
---

嗨，朋友们，

三月飞速前进。这周发了两个实打实的东西。跟 AI 没半毛钱关系。但都能帮你少踩坑。

你已经信任 Dependabot 来保持 npm 包和 Actions 版本更新了。但你的 pre-commit hooks 呢？一直靠自己。直到现在。

## 🚢 新动态

### Dependabot 现在支持 pre-commit hooks 了（GA）

如果你用 pre-commit，你懂这个套路。某个人跑了一次 pre-commit autoupdate，然后再也没人跑过。半年后 linter hook 已经古老了，整个团队已经习惯了这个痛。

Dependabot 现在把 pre-commit hook 更新作为一等公民支持了。它可以监控你的 .pre-commit-config.yaml，检测 rev pin 是否落后，然后自动开 PR。

在 dependabot.yml 里加上这个：

```yaml
version: 2
updates:
  - package-ecosystem: "pre-commit"
    directory: "/"
    schedule:
      interval: "weekly"
```

我喜欢这个实现的几个点：

- 保持你的 YAML 格式不变。
- PR 包含 release notes，所以你能看到到底改了什么。
- 支持分组更新，hook 列表长的时候很有用。
- local 和 meta hooks 会自动跳过。
- 即使 hooks 托管在 GitHub 之外也能用。

最终效果：你的仓库不再依赖某个人的记忆来保持更新。详情看 [changelog](https://github.blog/changelog/2026-03-10-dependabot-now-supports-pre-commit-hooks/)。

### GitHub Actions OIDC token 现在可以包含仓库自定义属性了（Public Preview）

GitHub Actions 的 OIDC 已经是最干净的方式来让 workflow 向云服务商认证，不需要长期 secret。难的部分一直是策略蔓延。

GitHub 正在推出 public preview，让你在 Actions OIDC token 里包含仓库自定义属性作为 claim。平台层面的设计很有意思：

- org admin 定义哪些属性要发出去。
- 仓库设置属性值。
- token 携带这些属性。
- 云端的 trust policy 按属性过滤。

如果你要落地这个，从 [官方 OIDC](https://docs.github.com/actions/reference/security/oidc) 文档和 OIDC 自定义 REST [endpoints](https://docs.github.com/en/rest/actions/oidc) 开始。

## 📖 推荐阅读

[Die with Zero](https://www.diewithzerobook.com/)，Bill Perkins 著。OctoVets 读书会这个月的选书。Perkins 认为大多数有纪律的储蓄者——尤其是工程师——把最健康的年华花在攒钱上，但从来没真正用完。他的核心观点：30 岁花在体验上的一块钱能产生几十年的回忆，75 岁的同样一块钱？基本没什么感觉。他管这叫"记忆红利"。说实话我对这本书有点纠结。我在努力给孩子创造体验也在努力付账单。框架是有用的，但 Perkins 是在已经有几百万的基础上写的"花吧"，这肯定影响了他的建议。

推荐给：那种需要别人允许才敢趁年轻享受自己赚的钱的人。

## 🔧 在用什么

[TRMNL](https://usetrmnl.com)：一个小的 e-ink 屏幕，循环展示黑白信息流。GitHub commit 图、天气、自定义 dashboard。没有通知，没有颜色，没有多巴胺套路。就是桌上安静的数据。放桌上才几天我就理解这个东西为什么火了。

## ✨ 这周

一眨眼就春天了。我已经规划好了今年的出差行程，刻意不让自己 overcommit。你知道那个关于等事情慢下来的 meme 吗？它们永远不会慢下来。所以我在试着更 present、更 mindful，不让这一年就这么溜走。如果你也有同样的感觉——也许这就是你的信号，去看看你的日历，保护一些空白时间。

就这些，你的 hooks 值得和 packages 一样被关注。

感恩，下周见，

Andrea

📌 附：GitHub CTO Vlad Fedorov 写了一篇关于最近可用性为什么不太好以及团队要怎么修的文章。没有公关话术，就是计划本身。[值得一读](https://github.blog/news-insights/company-news/addressing-githubs-recent-availability-issues-2/)。

🇨🇴 [Lee el boletín en español](https://mainbranch.dev/newsletter/es/)。
$

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
