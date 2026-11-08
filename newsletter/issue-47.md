---
title: "☁️ Main Branch：这次，你的 runner 开始跨云运行 - Issue #47"
number: 47
date: 2026-11-02
excerpt: "Dependabot 可达性分析、运行在 AWS 上的 GitHub Actions，以及需要更新的 IP allowlist。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-47
topics: ["GitHub Actions", "Dependabot", "Security", "AI Agents"]
tags: ["github-actions", "dependabot", "security", "multi-cloud"]
featured: false
---

[Read in English](https://mainbranch.dev/newsletter/issue-47/) • [Leer en Español](https://mainbranch.dev/newsletter/es/issue-47/)

朋友们好，

我还沉浸在 Universe 结束后的状态里。现在可以看 [GitHub Universe · Recap](https://github.com/events/universe/recap)。我们录了几段和 builders 深入交流的内容，我已经迫不及待想分享。它们会发布在 [GitHub 的 YouTube channel](https://www.youtube.com/@GitHub)，记得订阅。等着的时候，可以看看 [changelog](https://www.youtube.com/watch?v=ZQ0Qq6LlAmI)。

## 🚢 本周上线

### [用 reachability analysis 优先处理 Dependabot alerts](https://github.blog/changelog/2026-10-28-prioritize-dependabot-alerts-with-reachability-analysis)

Dependabot 现在可以检查你的代码是否会调用依赖中的易受攻击函数。在托管的 GitHub Actions workflow 中，CodeQL 会为你的代码库和依赖构建 call graph，然后给每个未关闭的 alert 一个 verdict：Reachable、Potentially reachable、Unreachable 或 Reachability unavailable。Potentially reachable 表示分析无法确定你的代码是否会调用易受攻击的函数。这些 verdict 不会关闭或 dismiss alert；你可以按 verdict 筛选，也可以从 REST API 读取。

目前处于 public preview，仅适用于 GitHub Enterprise Cloud 中使用 JavaScript 或 TypeScript、并包含 npm、Yarn 或 pnpm lockfile 的仓库。默认关闭，可以通过 custom security configuration 启用，也可以在 `Settings > Advanced Security` 的 Dependabot 部分开启。预览期间**免费**，不需要 GHAS license。

### [GitHub Actions 增加 multi-cloud compute，提升可靠性](https://github.blog/changelog/2026-10-28-github-actions-adds-multi-cloud-compute-to-improve-reliability)

符合条件的 GitHub-hosted Linux job 现在可以在 AWS 上运行，也可以继续使用 Azure。这包括标准的 2-core 和 4-core Linux runners，以及兼容的 2-core 和 4-core larger runners，且不能使用专用配置。不支持 Windows 和 private networking。Free、Pro 和 Team 会自动启用；Enterprise Cloud 用户可以在 `Enterprise settings > Actions > Hosted compute cloud providers` 中选择 AWS。现有的 runner labels 和 workflow syntax 不变。

新的 runners 会使用额外的出站 IP，因此只信任 Azure IP ranges 的 allowlist 或 Entra Conditional Access policy 可能会阻止它们。这项变更会逐步推出。现在就用 `GET https://api.github.com/meta` 返回的 `actions` ranges 更新这些 policy。

## 📖 我在读什么

[The Read Tool](https://commandcode.ai/docs/harness-engineering/read-tool)，作者 Ahmad Awais

Command Code 为 open models 构建 coding agent。这篇文章讲了他们如何重做 `read_file` 这个工具，减少 token 浪费。他们把它和另外九个 harness 对比，发现一些常见的 harness 会把整份 3,000 行文件交给模型，或者把没有长度限制的压缩单行文本交给模型。我的看法是，open-weight models 还在进步，但 labs 构建的 harness 确实会针对自家的模型优化。这正是 Copilot 在 Fusion 上做 harness 工作要解决的问题。我们在 Universe 录了一期关于 open-weight models 的 GitHub Podcast，之后会分享更多。

如果你在构建 agent 或挑选 harness，想知道 token 都花在哪了，这篇值得一读。

## 🔧 我在用什么

我在 mainbranch.dev 的每期 newsletter 页面都加了 Copy for AI 按钮，灵感来自 Marko Denic 的文章 [Your articles need a "Copy for AI" button](https://markodenic.tech/your-articles-need-a-copy-for-ai-button/)。点一下，就能复制干净的 Markdown，标题和 URL 会放在最前面，这样你粘贴到 AI 工具里时，它也能指回来源。任何 issue URL 后面都可以加 `.md`，例如 [issue-46.md](https://mainbranch.dev/newsletter/issue-46.md)。

```ts
export function buildCopyText(root: Element, title: string, url: string): string {
  return `# ${title}\n\n${url}\n\n${elementToMarkdown(root, title)}\n`;
}
```

## ✨ 这周的一点感受

每年 Halloween 过后，我都会觉得这一年一下子就快结束了。我的大孩子下周过生日，我们会带他去音乐节庆祝。之后我会去 [Nerdearla México](https://nerdearla.com/en/speakers/andrea-griffiths/) 做一场我很期待的新演讲。如果你也在，来打个招呼。

带着感激，下周见，

Andrea

## 📌 P.S.

感谢 Shishir Tewari 和我一起在 Universe 分享 "Build once, run on any agent"。我以前管理建筑项目，而他在 Procore 为这些项目开发软件，所以这次合作有种兜了一圈又回到起点的感觉。slides、两段 demo 和 skill 文件都在 [gh.io/skills-talk](https://gh.io/skills-talk)。

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
