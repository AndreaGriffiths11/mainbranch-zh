---
title: "🗂️ Main Branch：就是那种，GitHub 终于想起东西放哪了的那期"
number: 17
date: 2026-03-07
excerpt: "可见性、策略和记忆。Repository Dashboard 给你所有仓库一个家。Rulesets 终于能强制谁来 review 什么了。还有，我给 AI agent 加了真正的记忆。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-17
beehiivUrl: https://mainbranch.beehiiv.com/p/cc437d75-ee04-41ae-9337-615d06a02f07
topics: ["GitHub", "Repository Management", "Rulesets", "Projects", "Developer Experience"]
tags: ["repository-dashboard", "rulesets", "required-reviewer", "github-projects", "claude-code", "supermemory"]
featured: true
---

嗨，朋友们，

这周：可见性、策略和记忆。Repository Dashboard 给你所有仓库一个家。Rulesets 终于能强制谁来 review 什么了。我还给 AI agent 加了真正的记忆——来看看怎么做的。

基础为先，开干。

---

## 🚢 新动态

**Repository Dashboard**

你的新大本营，一目了然。[github.com/repos](https://github.com/repos) 展示你在所有 org 里有权限访问的全部仓库，支持筛选和保存自定义视图。GA 版本新增了两样东西：Admin Access 视图（只显示你有 admin 权限的仓库）和 command palette 集成（Cmd+K 直达）。如果你曾经问过"等等，我到底管理哪些仓库来着？"——现在有答案了，不用再考古了。

状态：[GA](https://github.blog/changelog/2026-02-24-repository-dashboard-is-now-generally-available/) | 所有 GitHub 用户 | [github.com/repos](https://github.com/repos)

**Required reviewer rule**

这是 CODEOWNERS 做不到的 ruleset 功能：在整个 org 或 enterprise 范围内，强制指定团队审核指定文件模式。你定义哪些团队必须 review 哪些文件，合并前必须通过。GA 版本新增了 `!` 排除模式——和 .gitignore 一样的语法——让你写精确规则而不会误伤。例如：要求安全团队对 `auth/` 下的所有改动做两人 review，但排除 `auth/tests/`。

```
*.sql → data-platform-team（1 个 approval）
auth/** → security-team（2 个 approvals）
!auth/tests/ → 排除
```

这能跨仓库扩展，强制的是策略而不只是 ownership。CODEOWNERS 继续负责 ownership，这个负责规则。

状态：[GA](https://github.blog/changelog/2026-02-17-required-reviewer-rule-is-now-generally-available/) | GitHub Team、Enterprise Cloud、Enterprise Server

**GitHub Projects：按查询导入 + 层级视图优化**

一次发布，两个更新。第一个：创建新 project 时可以用搜索查询来填充，不用从单个仓库导入了。支持和 Issues 页面一样的筛选器，包括 AND/OR 和嵌套查询。按你想要的 issue 来启动项目，不是导入全部。

第二个：层级视图做了三个体验优化——在 project 里直接创建 sub-issue、拖拽排序和调整父级、sub-issue 的排序在 issues 和 projects 之间保持同步。

状态：[GA](https://github.blog/changelog/2026-02-19-github-projects-import-items-based-on-a-query-and-hierarchy-view-improvements/) | 所有 Projects 用户

---

## 📺 在看什么

[和 Boris Cherny 聊 Claude Code 的构建](https://www.youtube.com/watch?v=julbw1JuAz0) - The Pragmatic Engineer Podcast（2026年3月4日）。Boris 在 Anthropic 构建并领导 Claude Code。这期聊了它实际怎么工作的：并行 agent、PR 结构、确定性 review 模式、跨大型代码库的上下文检索。最让我印象深刻的时刻：当 Gergely 说 Cat Wu（Claude Code 的 Product Lead）更偏产品方向时，Boris 特意补充说她是前工程经理，技术功底很深。Boris 没有让这个被轻描淡写过去。很好。

---

## 🔧 在用什么

[Supermemory](https://github.com/supermemoryai) - 这周我把它接入了 [Zo](https://zo-computer.cello.so/MB86XxwTf9r)，解决一个一直困扰我的问题：记忆在新 chat 窗口里就没了。Supermemory 提供语义搜索和知识图谱，上下文真的能持久保存。API 很干净，搭建比预想快，而且开源。我在 GitHub Open Source Friday 上[采访](https://www.youtube.com/watch?v=83DRdPdod7k)了创始人 [Dhravya Shah](https://x.com/DhravyaShah)——一个才华横溢的 20 岁独立创始人，在攻克前沿问题。

---

## ✨ 这周

一些很慷慨的朋友这个周末带我们全家去滑雪了。客观地说，我滑雪很烂。但我去了，摔了，爬起来，继续滑——主要是因为我想让孩子们知道这就是你该做的事。姿势不好看，没人在意。我们都爬起来了。如果你滑过雪，你就知道这张照片离 Eddie the Eagle 差了十万八千里。然后发生的事我脸上现在还能感觉到 😩。

![滑雪冒险](/images/skiing-issue-17.jpg)

---

就这些。三个东西分别解决了三个基础问题：可见性（Repository Dashboard）、策略执行（required reviewer rule）和项目启动（Projects 导入）。这些无聊但让你安全发布的东西。对了，我在 GitHub 工作——我的热情请带着适当的上下文来看。但竞争只会让这些工具变得更好。Claude Code 给所有 CLI 工具都点了一把火，这对我们所有人都是好事。

感恩，下周见，

Andrea
$

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
