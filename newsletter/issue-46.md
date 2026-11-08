---
title: "🔐 Main Branch：这次，你的 gh token 会按设计过期 - Issue #46"
number: 46
date: 2026-10-26
excerpt: "GitHub CLI 会过期并自动刷新的 OAuth token 进入公开预览，分支保护规则可批量迁移到 rulesets，还有 Jakub Krehel 谈如何判断什么不该做。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-46
topics: ["GitHub CLI", "Security", "Rulesets", "AI Agents"]
tags: ["github-cli", "security", "rulesets", "ai-agents"]
featured: false
---

[Read in English](https://mainbranch.dev/newsletter/issue-46/) • [Leer en Español](https://mainbranch.dev/newsletter/es/issue-46/)

朋友们好，

这封信写于旧金山。我来参加 GitHub Universe，很期待能和你们中的一些人聊聊。前期准备很忙，但来到这里，看到一切都落地成形，真的很值。

## 🚢 本周上线

### [GitHub CLI：可选启用会过期并自动刷新的 OAuth token](https://github.blog/changelog/2026-10-21-github-cli-opt-in-to-expiring-auto-refreshing-oauth-tokens)

从 v2.103.0 开始，`gh auth login --expiring` 会保存一个短期 access token 和一个轮换的 refresh token，`gh` 会在后台刷新 access token。想让每次登录都启用它，运行 `gh config set expiring_credentials enabled`。

如果脚本只运行一次 `gh auth token` 并保存结果，最后拿到的会是一个过期 token，所以每次都要重新读取。对于通过 HTTPS 使用 git，GitHub 建议运行 `gh auth setup-git`，并使用 git 2.46 或更新版本。GitHub App 的安装 token 本来就会在一小时后过期（[#44](https://mainbranch.dev/newsletter/zh/issue-44/)）。现在，你自己的 `gh` 登录也可以这样。

```shell
gh auth login --expiring
gh auth setup-git
gh auth status
```

### [在仓库中把分支保护批量迁移到 rulesets](https://github.blog/changelog/2026-10-20-bulk-migrate-branch-protections-to-rulesets-for-a-repository)

现在可以一步把仓库里的所有分支保护规则转换为 rulesets。进入 Settings > Rulesets，点击 Import branch protection rules。确认之前，审查对话框会预览这些 rulesets，显示哪些规则已经被现有 ruleset 覆盖，并标出需要多个 ruleset 才能保持原有行为的规则。

选择 Active、Evaluate 或 Disabled 作为执行状态，再选择要创建哪些 rulesets。点击 Create rulesets 之后，你可以决定保留还是删除旧的分支保护规则。

## 📖 我在读什么

### [Less is more, more or less](https://jakub.kr/writing/less-is-more)

作者：Jakub Krehel。

Jakub 的观点是，有了 AI，加东西几乎没有成本，所以判断什么不该做反而是更难的能力。他引用了 Antoine de Saint-Exupéry 的话，这位作者也写了我最喜欢的书《小王子》：“完美不是无可增加，而是无可删减。”他在 Interfere 的团队把自己的标准做成了一个 `/codebase-standards` skill 和一个审查命令，让智能体和团队成员用同一套标准。

如果你在用智能体加快交付，又想确保产出真的更好，这篇值得读。

## 🔧 我在用什么

### [GitHub Copilot 现在可以通过 computer use 操作桌面应用](https://github.blog/changelog/2026-10-01-github-copilot-can-now-interact-with-desktop-apps/)

GitHub Copilot app 里的 computer use 让 Copilot 可以在没有 API 或 MCP server 的桌面应用里点击、输入和滚动。它已在 macOS 和 Windows 上进入公开预览，默认关闭；可以在 Settings > Computer Use 中开启，或在会话中运行 `/computer on`。Copilot 在控制某个应用前会先请求批准，按 Stop 或 Esc 可以中断它。我用它做一件每周都要做的杂事：把 newsletter 草稿搬进 Beehiiv 的编辑器。Beehiiv 的 MCP server 只有付费方案才支持写入操作，有了 computer use，我就不用再为付费方案花钱了。

## ✨ 这周的一点感受

我会和 Procore 的 Shishir Tewari 一起在 GitHub Universe 分享 [Build once, run on any agent: a practical guide to agent skills](https://reg.githubuniverse.com/flow/github/universe26/attendee-portal/page/sessioncatalog/session/1785179690271001xi4A)。我会带来我为重复性工作做的 skills；Shishir 会分享他为生产环境数据工程团队构建 skills 的经验。我们会聊聊什么时候一个工作流适合做成可复用的 skill。如果你已经厌倦了一遍遍向编码智能体重复同样的话，想弄清楚什么样的 skill 在工作和个人项目里真正有用，欢迎来参加。

谢谢你，我们下周见，

Andrea

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
