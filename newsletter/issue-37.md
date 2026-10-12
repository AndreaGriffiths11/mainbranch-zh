---
title: "🔁 Main Branch 技术周刊：重试让问题更糟 - Issue #37"
number: 37
date: 2026-08-23
excerpt: "GitHub 8 月 17 日 outage 复盘、VS Code retry storm、按 token 类型撤销凭证，以及 blocked user 管理。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-37
topics: ["GitHub Outage", "Reliability", "VS Code", "Credential Security", "Moderation", "Kubernetes", "Node.js", "AI Agents"]
tags: ["github-outage", "reliability", "retry-storms", "vs-code", "credential-security", "blocked-users", "kubernetes", "nodejs", "agents-md", "newsletter"]
featured: false
---

[Leer en Español](https://mainbranch.beehiiv.com/p/boletin-en-espanol) · [阅读中文版](https://mainbranch.dev/newsletter/zh/)

朋友们好，

GitHub 8 月 17 日的 outage 持续了 7 小时 47 分钟。根因只解释了其中大约三个小时。

大多数报道都停在 Istio 配置错误上。[根因分析](https://www.githubstatus.com/incidents/zkxwbgr0cnmx)追溯到一个 sidecar pod 达到并发上限后无法 autoscale，因为 scaling policy 监控的是 host service，而不是 sidecar 的限制。四个 HAProxy 节点耗尽了 flow limits，gateway auth path 也跟着宕了。

16:36 UTC，GitHub 暂停了受影响节点上的 HAProxy，服务立刻大范围恢复。本来应该到这里就结束了。但 Copilot Token Service 直到 21:02 才完全恢复，将近晚了五个小时。原因是 VS Code 中一个潜伏的 retry bug，把每次失败的 token request 变成了一堆后续请求。流量从 7 到 9K RPS 飙到 70 到 100K RPS。

infra 团队大约三小时就修完了自己的部分。一个 client-side retry loop 又把 outage 延长了五小时。

当数百万个 VS Code 实例不做 backoff，一起猛打同一个 endpoint 时，你自己就成了 DDoS。GitHub 的用户为了使用 GitHub 的产品，反过来给 GitHub 打出了一场 retry storm。

[Vlad 的文章](https://github.blog/news-insights/company-news/the-august-17-outage-and-the-work-ahead/)补充了规模背景：从 4 月开始，每月 commits 已经从 14 亿增长到 29 亿。后续工作包括在 service-to-service 交互中统一 retry limits、retry budgets 和可变 timeouts。很好。补齐这些 guardrails 很有必要。

---

## 🚢 最新发布

### [按 token 类型撤销凭证和取消授权](https://github.blog/changelog/2026-08-18-credential-revocation-and-deauthorization-by-token-type)

以前的 kill switch 是全有或全无。事件期间一按按钮，用户拥有的所有凭证都会消失，包括你仍然信任的凭证。现在，enterprise owners、org admins，以及任何拥有 Manage enterprise credentials 权限的人，都可以只撤销一种凭证：personal access tokens、SSH keys、OAuth app tokens 或 GitHub App user access tokens。你可以删除被入侵 EMU 账户的所有 PAT，而不碰它的 SSH keys。所有 enterprise 级批量操作现在也能在 org 级使用，UI 和 REST APIs 都支持。每次操作都会写入 audit log，并向受影响的用户发送 email。

### [更好用的 blocked user 管理工具](https://github.blog/changelog/2026-08-21-better-tools-for-managing-blocked-users)

Blocked user 列表一长，过去很难真正读懂。现在可以按 username、全名或 email 搜索，可以排序、分页，还能按 block reason 筛选。你可以添加 private notes 来保留上下文，org blocks 也会显示由谁执行、何时到期。搜索字段和 block 字段现在分开了，不会再把只是想查找的人误操作成 blocked user。个人账户和 org 都能使用，位置在 Settings > Moderation > Blocked users。

---

## 📖 我在读

**Kubernetes 上 Node.js 的预测式 Autoscaling**，Ivan Tymoshenko、Luca Maraschi 和 Matteo Collina 著

Kubernetes autoscaling 有一个 timing 问题。HPA 会等 CPU 越过阈值，但 event loop 已经饱和、请求开始堆积时，CPU 看起来仍然可能正常。KEDA 增加了更好的 triggers，但保留了同一个 reactive loop，所以它仍然要等 overload 开始后才发现。论文预测新 pods 真正 ready 那一刻的 cluster-wide load，然后提前扩容。这里必须看 aggregate，因为增加 pods 会重新分配 per-instance metrics。只盯着一个 pod 的 scaler，最后会追着自己的改动跑。Benchmark 的结果很明确：在稳定爬升的负载下，中位延迟是 26 ms，KEDA 为 154 ms，HPA 为 522 ms。这是研究结果，不是装上就能用的 controller，但它的思路是对的。Reactive autoscaling 在设计上永远会迟到。

如果你在 Kubernetes 上跑 Node.js，而 p99 和 CPU 图表对不上，这篇值得读。

[arxiv.org/abs/2604.19705](https://arxiv.org/abs/2604.19705)

---

## 🔧 我在用

我一直在做受控实验，测量 `AGENTS.md` 是否真的会改变 coding agents 的行为，而不是直接假设它有用。

两个条件，同一个 task，同一个起始 commit。Baseline 没有 repo instructions。Treatment 拿到一份候选 `AGENTS.md`。然后比较两边的 diffs。

目前的发现是：简单 tasks 通常没有明显差异。Guardrail tasks，也就是能干净 compile、却会在 runtime 出错的任务，信号最清楚。

Open source、MIT、零依赖。还包含一个五分钟的 fixture demo。

[github.com/AndreaGriffiths11/agents-md-benchmark-plugin](https://github.com/AndreaGriffiths11/agents-md-benchmark-plugin)

---

## ✨ 本周

我正在准备去 Lima 参加 DevOps Days。如果你也会去，来找我。

感谢你的阅读，下周见。

Andrea

---

**📌 P.S.** 9 月 23 日到 25 日，我会在 San Jose 参加 [WeAreDevelopers World Congress North America](https://www.wearedevelopers.com/world-congress-north-america/tickets)。如果门票是唯一拦着你的东西，回复告诉我。

GitHub Accesscats 团队正在 [gh.io/access-needs](https://gh.io/access-needs) 做一项无障碍需求调查。大约需要五分钟。

---

💛 如果 Main Branch 对你有用，[订阅](https://mainbranch.beehiiv.com/)或[在 GitHub 上赞助我](https://github.com/sponsors/AndreaGriffiths11)。

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
