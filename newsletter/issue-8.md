---
title: "🚀 Main Branch：就是那种，工具终于快起来了的那期"
number: 8
date: 2026-01-05
excerpt: "TypeScript 7 快了 10 倍。Actions 页面终于能用了。还有我的 2026 预测。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-8
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-tooling-gets-faster-issue-8
bskyPostId: "3mbzdy5gto22a"
topics: ["TypeScript", "GitHub Actions", "Developer Tools", "Performance"]
tags: ["typescript", "actions", "performance", "developer-tools"]
featured: true
---

嗨，朋友们，

2026 快乐。新年第一期，我来个预测：今年是工具终于跟上来的一年。

不是 AGI，不是 agent，是那些无聊的东西。编译器、包管理器、workflow 页面。我们等了好几年的基础设施突然快了 10 倍。让我来给你看看我说的是什么。

## 🚢 新动态

**TypeScript 7 来真的了（而且很快）**

Microsoft 正在用 Go 重写 TypeScript 编译器。他们叫它 Project Corsa。[12 月的更新](https://devblogs.microsoft.com/typescript/progress-on-typescript-7-december-2025/)确认它已经稳定到可以日常使用了。

数据：编译速度快 10 倍。编辑器启动快 8 倍。VS Code 代码库（150 万行）从 9.6 秒加载时间降到了 1.2 秒。

TypeScript 6 将是最后一个基于 JavaScript 的版本。没打错字。处理你 TypeScript 的编译器，将不再用 TypeScript 编写。为什么选 Go？简单说：这是移植，不是重写。Go 的模式跟现有代码库非常匹配，所以他们能快速推进又不破坏兼容性。用 Rust 的话得从头重写好几年。Go 几个月就搞定了。

想现在试试的话，安装 `@typescript/native-preview` 然后运行 `tsgo`。

**Actions Workflow 页面：终于能扛大活了**

如果你曾经看着 Actions workflow 页面在 matrix build 上卡死，好消息来了。GitHub 发布了[对 300+ jobs 的 workflow 的懒加载支持](https://github.blog/changelog/2025-12-22-improved-performance-for-github-actions-workflows-page)。

更棒的是：你现在可以按状态筛选 jobs 了。只看失败的、只看进行中的。再也不用在几百个绿色勾里翻找那一个红叉了。小改进，但对跑复杂 CI 或 monorepo 的人来说，生活质量大幅提升。

## 📖 推荐阅读

Peter Steinberger 的 ["Shipping at Inference-Speed"](https://steipete.me/posts/2025/shipping-at-inference-speed) 讲述了一个开发者如何随着 AI 工具演进他的工作流。但让我印象最深的部分跟 AI 无关：他在每个项目里维护一个 `docs/*.md` 文件夹，记录子系统和功能的文档，然后用脚本强制加载特定主题的上下文。

把好的文档放在可预期的位置。不管是给新团队成员还是 AI agent 做 onboarding 都管用。基本功。

## 🔧 在用什么

这周不是开发工具。是个人健康推荐，我一直在吃 [Pendulum Akkermansia](http://rwrd.io/hrwolw6?c/) 调理肠道健康。效果很明显——精力、专注力、消化都改善了。有时候最好的效率提升工具不是另一个 CLI 工具，而是照顾好自己。

## ✨ 这周

假期回来了。严格来说我没完全停工，但能按自己的节奏和时间做事感觉真好。看了 Stranger Things 大结局。神奇的是我们对虚构角色会有那么深的感情。我看着那些孩子长大，同时自己也在成长。五季过后，说再见比想象中更难受，是的我也喊了"不要啊别是 STEVE"。

就这些。新的一年，新的能量。去造东西吧。

感恩，下周见，

Andrea$

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
