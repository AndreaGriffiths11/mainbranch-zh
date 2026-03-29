---
title: "🚗 Main Branch: 就是那种，Agent 学会开车了的那期"
number: 15
date: 2026-02-23
excerpt: "GitHub Agentic Workflows、Copilot 登陆 Zed，还有那些默默撑起我半个技术栈的免费工具。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-15
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-agents-learned-to-drive-issue-15
topics: ["Agentic Workflows", "Copilot", "Developer Tools"]
tags: ["agentic-workflows", "copilot", "zed", "free-tier", "open-source"]
featured: true
---

嗨，朋友们，

上周龙虾<a href="https://youtu.be/f6F7yQUd8rs?si=RKwGeqwZf263e6Gt&amp;t=192">跑出来了</a>。这周 agent 学会开车了。

GitHub 发布了 Agentic Workflows，这东西听起来像 AI 营销话术——直到你亲眼看到 😉。维护者们已经在用它做 <a href="https://github.blog/wp-content/uploads/2026/02/Quotes_Option1.jpg">很多事</a>了：分析成千上万个 open issue 然后筛出重要的。

---

## 🚢 新动态

**GitHub Agentic Workflows（Technical Preview）**

用 Markdown 定义仓库自动化。一个 `.github/workflows/workflow.md` 文件就够了。`gh aw` CLI 把它编译成标准的 GitHub Actions，由 Copilot CLI、Claude 或 Codex 执行。Workflow 默认以只读权限运行。写操作（创建 PR、issue）通过可审查和受控的 safe output 进行。

我们需要一种方式让 agent 在生产仓库里做真正的活。Agentic Workflows 就是那座桥，让 AI 能够维护一个仓库。它可以对 issue 做分类、调查 CI 失败、更新文档、提出修复方案，全部在可见的、可审计的、**沙盒化的环境**里进行。Peli de Halleux 做了一个 <a href="https://github.github.com/gh-aw/blog/2026-01-13-meet-the-workflows/">Agent Factory</a>，展示了 150 多个专业的 agentic workflow。值得看看。

**Copilot Coding Agent：Zed、Windows 和模型选择器扩展**

Copilot 在 Zed 里正式 GA 了，可以用你现有的 Copilot 订阅。Copilot coding agent 现在支持在 Windows 环境下运行，通过 `copilot-setup-steps.yml` 里的自定义 `runs-on`（用 self-hosted runner 或 Azure private networking，因为内置防火墙暂时不兼容）。Business/Enterprise 用户现在可以按任务选择 Claude Opus 4.6、GPT-5.3 Codex 或 Auto，不再被锁定在 Auto 上。

<a href="https://www.jvt.me/posts/2026/02/20/renovate-discussions-data/">打破 GitHub Discussions 的限制</a> - by Jamie Tanna

他是 <a href="https://docs.renovatebot.com/">Renovate</a> 的维护者，想知道社区最关心哪些功能请求。这不是什么过分的需求。但 Discussions 的 UI 没法回答这个问题。"哪些帖子好几周没人回复"或者"这个月关了多少 bug"也一样——都是基本的维护者问题。所以他自己搭了一条数据管线。用 Go 打 GraphQL API，SQLite 存 11,000 条 Discussion 和 55,000 条评论，需要图表时用 Evidence 做可视化。整个系统每天早上同步，给他一个 0.01 秒加载的 triage 面板。

---

## 🧰 在用什么

我 <a href="https://x.com/acolombiadev/status/2025247942542606587">发了条推</a> 问大家最被低估的免费工具。200 多条回复之后，以下是反复出现的：

| 工具（链接） | 用途 |
| --- | --- |
| <a href="https://tailscale.com/">Tailscale</a> | 私有组网（mesh VPN） |
| <a href="https://github.com/juanfont/headscale">Headscale</a> | 自托管私有组网 |
| <a href="https://www.cloudflare.com/">Cloudflare</a> | 安全隧道 & Zero-Trust 访问 |
| <a href="https://infisical.com/">Infisical</a> | 密钥管理 |
| <a href="https://bitwarden.com/">Bitwarden</a> | 密码管理 |
| <a href="https://appwrite.io/">Appwrite</a> | Backend as a Service |
| <a href="https://convex.dev/">Convex</a> | 响应式后端 |
| <a href="https://www.netlify.com/">Netlify</a> | 前端部署 |
| <a href="https://cloudinary.com/">Cloudinary</a> | 媒体管理（图片/视频） |
| <a href="https://grafana.com/">Grafana</a> | 可观测性 & 监控 |
| <a href="https://posthog.com/">PostHog</a> | 产品分析 |
| <a href="https://coderabbit.ai/">CodeRabbit</a> | AI Code Review |

<a href="https://x.com/acolombiadev/status/2025247942542606587">完整帖子</a>值得刷一刷，特别是如果你在有限预算下做东西。我真希望所有公司都能明白：**免费套餐是一个 feature，不是妥协。**

---

## ✨ 这周

和 @elbruno 一起直播的时候看到他用了一个很酷的工具做 live demo。本来想问他是什么来着，完全忘了。所以我自己做了一个：<a href="https://github.com/AndreaGriffiths11/annotation-overlay">annotation-overlay</a>。当天就 ship 并开源了。是给自己做的，但如果你做 live coding、demo 或者想在屏幕上画东西，也许你也会喜欢！

自己造东西是一件很快乐的事。AI 让造的过程比以前快多了。但我觉得值得保持诚实的视角：造东西现在很容易了，维护依然很难。Mitchell Hashimoto 最近说 <a href="https://www.youtube.com/live/0npMvuh7qNc?si=jL4bsBYNdZKPRMnp&amp;t=1752">"应该有更多的 fork"</a>，他说得对。有时候一个只给自己用的方案就是对的范围。Ship 了，用着，继续走。

---

**这就是这周。** Agent 在拿到真正的工作了。免费套餐是 feature，不是妥协。基本功优先。永远如此。

感恩，下周见，

Andrea

🇪🇸 **Léelo en** **[español](https://mainbranch.dev/newsletter/es/issue-15/)**

**支持 Main Branch：** [Subscribe](https://mainbranch.beehiiv.com/) | [GitHub Sponsors](https://github.com/sponsors/andreagriffiths11)
