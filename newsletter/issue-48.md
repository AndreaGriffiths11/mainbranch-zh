---
title: "📅 Main Branch：这次，你的 workflow 有了新的截止日期 - Issue #48"
number: 48
date: 2026-11-09
excerpt: "GitHub Actions 将于 12 月 2 日开始默认阻止 pull_request_target，11 月的 brownout 会测试公共仓库 workflow，pull request 限制也新增了按账号年龄或合并记录设置的豁免规则。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-48
topics: ["GitHub Actions", "Pull Requests", "AI Agents"]
tags: ["github-actions", "pull-requests", "copilot-automations", "product-engineering"]
featured: false
---

[Read in English](https://mainbranch.dev/newsletter/issue-48/) • [Leer en Español](https://mainbranch.dev/newsletter/es/issue-48/)

朋友们好，

我的工作之一，是和比我懂得多的人交流，为大家带来技术含量很深的对话。每次录制前我都会花很多时间准备，但我不会假装自己才是专家。我带着好奇心去聊，也总能带着新收获离开。这周，分享一个值得你好奇的话题。

## 🚢 本周上线

### [pull_request_target 将于 12 月 2 日开始默认阻止](https://github.blog/changelog/2026-11-02-pull_request_target-blocked-by-default-december-2/)

从 2026 年 12 月 2 日起，GitHub Actions 将在公共仓库中默认阻止 `pull_request_target`，除非适用的 Actions event policy 明确允许它。这适用于 Free、Team 和 Enterprise Cloud，不包括 GitHub Enterprise Server。私有和内部仓库不受影响。

Brownout 会在 11 月 9 日和 16 日举行，时间都是太平洋时间上午 8 点到 10 点。被阻止的尝试会生成失败的运行记录和错误注释，workflow 不会执行。之后规则会回到 evaluate 模式，允许运行并显示警告。现在就检查 Insights，再决定保留默认规则，还是明确允许这个 trigger。你也可以指定 workflow 文件，只允许特定 workflow。

![检查 pull_request_target 的三种方式：查看最近的 Actions 运行、搜索 workflow 文件，并在 Insights 中查看策略影响。如果没有最近的运行记录，也要检查 workflow 文件和 Insights，再判断是否会受影响。](https://mainbranch.dev/images/issue-48-pull-request-target-checks.svg?v=48)

### [Pull request 限制：按账号年龄或历史记录豁免贡献者](https://github.blog/changelog/2026-10-28-pull-request-limits-exempt-contributors-by-age-or-history/)

Pull request 限制现在允许维护者根据贡献者的账号年龄或已合并 pull request 的记录设置豁免。这些限制针对没有写入权限的贡献者。

在组织或仓库设置里的 `Moderation > Interaction limits` 中，可以启用一项或两项规则。你可以设置账号的最低使用天数，或该仓库中已合并 pull request 的最低数量。满足任意一项已启用的规则，就可以获得豁免。原有的个人豁免名单也仍然有效，仓库级别的限制设置会覆盖组织级别的设置。这样就能让熟悉项目的贡献者继续参与，不必逐个添加到名单里。

## 🎧 我在听什么

### [#503：数学中的 AI 危机，与 Lex Fridman、Ankur Moitra、Steven Brunton 和 Alex Kontorovich 对谈](https://lexfridman.com/math-ai-crisis)

数学家正在经历一场身份危机，和程序员面对 AI 时的处境很像。三位数学家聊到 AI 正在解决数学中一些最难的问题，从 Navier-Stokes 到黎曼假设，也聊了 Lean 和机器验证的证明。模型比人更快地解决复杂问题，这公平吗？也许不公平，但比起维护我们的自尊，让人类整体继续进步是不是更重要？

如果你也在想：当模型能替你完成一部分工作时，你的工作意味着什么，这期值得听。

## 🔧 我在用什么

[Copilot Automations](https://docs.github.com/copilot/concepts/agent-capabilities/agent-powered-workflows-and-operations/about-automations)。Automations 可以在事件发生时运行 prompt，不用人手动把告警贴进聊天。一个 automation 包含 prompt、trigger，以及 Copilot 可以使用的工具。它保存在仓库之外，所以不会有内容提交到 Git。我最近用它处理那些总要手动完成的重复仓库任务。把工作描述一次，它就会自动运行，并根据运行情况逐步调整。我还在摸索，但从这些琐事开始很合适。

## ✨ 这周

我很期待分享上周在西雅图录制的内容。我们聚集了一群非常出色的人，用更实际的方式聊了 10 月 changelog 里的重要更新。不知道你是不是也这样，面对一页又一页的 changelog，真的很难看出它对自己和团队有什么影响。视频今天晚些时候会发布到 YouTube，上线后我会更新这个链接。

带着感激，下周见，

Andrea

P.S. [Kent Dodds 在与 Jay Parikh 的对谈中说了一句话，让我一直记着](https://www.youtube.com/watch?v=j0VWYhvoyM8)。今年，他作为开发者经历了两次存在危机，之后转向成为 product engineer，因为现在关键是知道该构建什么。这和本周的两项更新有关。贡献变多后，判断哪些改动应该进入项目，比写代码本身更考验判断力。工具会继续变化，但最终还得有人做这个决定。

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
