---
title: "🐛 Main Branch：这次，智能体的第一个猜测错了 - Issue #45"
number: 45
date: 2026-10-19
excerpt: "GitHub Actions workflow lockfile 进入公开预览，GitHub Apps 新增 repository_creation:write 等权限，还有一项帮助智能体调试的 skill。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-45
topics: ["GitHub Actions", "GitHub Apps", "Debugging", "AI Agents"]
tags: ["github-actions", "github-apps", "debugging", "ai-agents"]
featured: false
---

[Read in English](https://mainbranch.dev/newsletter/issue-45/) • [Leer en Español](https://mainbranch.dev/newsletter/es/issue-45/)

朋友们好，

秋天这几个月，感觉所有大会都挤到了同一个星期。我们这边忙得连休息都顾不上，我知道你们很多人也一样。希望大家照顾好自己，今天留点时间，做件让自己开心的事。

## 🚢 本周上线

### [GitHub Actions workflow lockfile 进入公开预览](https://github.blog/changelog/2026-10-14-github-actions-workflow-lockfiles-in-public-preview/)

Workflow lockfile 会把工作流用到的每个 action 锁定到确切的 commit，包括传递依赖和可复用工作流。这些锁定记录保存在 `.github/workflows/actions.lock` 中，所以即使 tag 或分支指向变了，实际运行的代码也不会变。  
用 `gh extension install github/gh-actions-lock` 安装扩展，在仓库根目录运行 `gh actions-lock`，然后像审查其他 PR 一样审查 diff。Dependabot 会更新已经接入 lockfile 的工作流对应的条目。锁定依赖并不能说明依赖本身是否安全，所以仍然要保留人工审查。

### [GitHub Apps 在最小权限和管理方面的改进](https://github.blog/changelog/2026-10-13-github-app-improvements-for-least-privilege-and-management/)

两个新权限引起了我的注意。GitHub Apps 和 fine-grained PATs 都能使用它们，让自动化只获得更小范围的访问权限。

以前，创建仓库需要 `repository_administration:write`，而这个权限还允许删除、转移仓库等操作。现在，`repository_creation:write` 让 app 无需申请那个范围更广的权限，也能创建仓库。

第二个权限是 `installation_repositories:write`，允许调用方在组织内为 app 的某次安装添加或移除仓库。它适用于调用方拥有该权限的仓库。如果调用方是用户，还必须是组织所有者或该仓库的管理员。

安装申请创建仓库权限的 app，仍然需要组织所有者批准。批准的是安装本身，不是 app 创建的每个仓库。检查一下，哪些 app 申请 Administration 仅仅是为了创建仓库，这些就可以考虑改用范围更小的权限。

## 📖 我在读什么

[当你已经看不懂代码时，如何有效调试](https://copyconstruct.medium.com/how-to-effectively-debug-when-you-no-longer-understand-the-code-bd3dcb2c5f7b) 作者：Cindy Sridharan。

Cindy 讲了她用智能体修复的三个生产环境 bug：延迟回退、内存泄漏和程序卡住。每次智能体的第一个诊断都错了，直到她提供对照条件、约束，或要求给出依据。她的观点是，代码能告诉智能体什么可能发生，却不能说明实际发生了什么。所以要先收集事实，每个假设都必须解释所有事实。

如果你让智能体帮忙调试，想有一套流程来核查它们的答案，这篇值得读。

## 🔧 我在用什么

### [Hypothesis-Driven Debugging](https://mainbranch.dev/skills/hypothesis-driven-debugging.md)

我最近在用 Hypothesis-Driven Debugging，这是我写的一项 skill，帮助智能体根据证据调试。它引导智能体收集带来源的事实，对比失败和正常的案例，每次检验一个假设。在接受修复之前，它会检查改善是否确实由这次改动引起，并让独立审查者寻找能让补丁出问题的案例。

## ✨ 这周的一点感受

这周会很忙，真的很忙。我最近花了不少时间，旁听 [GitHub Universe](https://githubuniverse.com) 所有主舞台演讲的排练，并提供反馈。跟大家说，这些演讲的质量真的很棒。如果你还没买票，又想来，希望能见到你。如果你原本打算参加后来取消的 Grace Hopper 大会，请私信 [LinkedIn 上的 GitHub](https://www.linkedin.com/company/github/)，领取一张免费的 Universe 门票。

谢谢你，我们下周见，

Andrea

## 📌 附言

P.S. 我读了一篇关于 [mosh pit](https://sethna.lassp.cornell.edu/pubPDF/MoshPits.pdf) 的有趣文章。现在我想知道，大家在 circle pit 里是怎么决定朝哪个方向转的。

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
