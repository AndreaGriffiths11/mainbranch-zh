---
title: "💰 Main Branch：就是那种，Actions 居然降价了的那期"
number: 6
date: 2025-12-22
excerpt: "最好的基础设施，是你团队真正在用的那种。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-6
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-actions-got-cheaper-issue-6
topics: ["GitHub Actions", "CI/CD", "Cost Optimization", "Infrastructure"]
tags: ["actions", "ci-cd", "cost-optimization", "infrastructure"]
---

嗨，朋友们，

GitHub 上周宣布了一项 Actions 的变更，随后又推迟了。老规矩，故事远不止表面这些。

刚在 Twitter 上看到：[一个 15 人的开发团队](https://x.com/brankopetric00/status/1995153027032903695)从 Jenkins 迁到了 GitHub Actions。他们之前的 Jenkins 配置：自建在 EC2 上，47 个插件，Groovy 流水线，只有一个人懂整套系统。服务器维护每月吃掉 10 小时。然后那个人离职了。Jenkins 变成了一个黑盒。切换到 Actions 六个月后：15 个开发者都在写 workflow，流水线变更从每月 2 次涨到了 40 次，构建时间提升了 40%。

他们遇到的问题不是成本，而是只有一个人掌控整个系统，其他人都不想碰。当基础设施需要一个"英雄"来维护时，你其实已经输了。

先说一下：我在 GitHub 工作（观点仅代表个人）。

## 🚢 新动态

**GitHub 托管 runner 降价了（2026 年 1 月 1 日起）**

根据机器规格不同，最多便宜 39%。免费分钟配额不变。打开[定价计算器](https://github.com/pricing/calculator)算算你实际的数字。但更重要的是：你不用管理它们。整个团队共同拥有 CI/CD，而不是一个人变成瓶颈。

**GitHub Actions：Self-hosted Runner 收费（2026 年 3 月，已推迟）**

新增 $0.002/分钟的 self-hosted runner 费用（计入你计划的分钟配额）。

说实话？这次的反对声是合理的。你已经在承担所有运维负担了，而 self-hosted 相关的改进一直感觉含糊又缓慢。我理解。当你自己管基础设施时，你会希望工具也跟上。

但有件事一直被忽略：GitHub 在 2025 年为开源项目提供了 115 亿免费分钟。而且说句公道话，其他 CI 平台也对 self-hosted 收费——Buildkite 按分钟收编排费，Azure Pipelines 按并行 job 收费。模式不同，但概念不新。

那你到底该怎么做？

Self-hosted 在合规、定制硬件或超大规模场景下仍然有意义。如果你是这种情况，把成本算进去继续用就好。但如果 self-hosted 只是为了"避免给 GitHub 付费"？是时候重新评估了。你既要付费又要维护基础设施。算笔账吧——把维护时间、插件各种坑、以及某人离职带走的知识都算进去。

## 📖 推荐阅读

**《Writing for Developers》——Piotr Sarna 和 Cynthia Dunlop 著。**

我的同事 [Brittany Ellich](https://www.linkedin.com/posts/brittanyellich_writing-for-developers-activity-7396357619151667200-UdOc) 发起了 Overcommitted 读书会，我加入了。整本书讲的是磨练写作技巧和建立真正的连接。

如果你正在学习面向技术受众的写作，或者想加入一个一起做事的社区，值得一读。

## 🔧 在用什么

[Parse](https://www.parse.bot/)，一个从任何网站提取和结构化数据的平台。这周我用它构建了 API，把我的 Main Branch 文章提取成干净的 markdown、结构化 JSON 和分块的章节 🤓。

## ✨ 这周

是 🎅🏼 圣诞周啦，对于庆祝的朋友们，我期待坐在圣诞树旁，手里拿着 coquito，享受所有的美好。朋友们，有太多值得感恩的事了，祝你们有一个美好的假期周。下周 Main Branch 会特别短，宣布我们 100 订阅者抽奖的获奖者，还没订阅的赶紧订起来！

就这些。1 月 1 日之前搞清楚你的数字。如果觉得有用就转发给你的团队。如果没用就回复告诉我你到底想看什么。

感恩，下周见，

Andrea

P.S. — 给正在为分钟数付费的朋友一个小技巧：别把分钟浪费在重复运行上。最适合 CI/测试类 workflow，部署类的就别用了。

```yaml
concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true
```$

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
