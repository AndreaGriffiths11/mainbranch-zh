---
title: "🔌 Main Branch：就是那种，它不是 API 的那期"
number: 4
date: 2025-12-08
excerpt: "MCP 讲明白。不炒作，就是你需要知道的。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-4
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-it-s-not-an-api-issue-4
topics: ["AI", "Developer Tools", "MCP", "Integration"]
tags: ["ai", "mcp", "developer-tools", "integration"]
---

嗨，朋友们，

我从 Vegas 回来了，嗓子没了，走的路比以往都多，那个会议太猛了，65000 个极客挤在一起。混乱，但是魔法般的混乱。这周我们深入聊聊真正在发生变化的东西：MCP。

你听烦了对吧。我理解。但你还是得搞懂它。

MCP 刚满一岁。11 月 25 号，Anthropic 发布了一个重大 spec [更新](https://den.dev/blog/mcp-november-authorization-spec/)。而在 9 月份，GitHub 宣布[逐步下线](https://github.blog/changelog/2025-09-24-deprecate-github-copilot-extensions-github-apps/) Copilot Extensions（旧的基于 GitHub App 的那种）。信号已经很明确了：所有人都被引导向 MCP 作为面向未来的标准。

## 💡 MCP 不是 API

API 是自动售货机：投币进去，JSON 出来，没有记忆。MCP 是跟你结对编程的同事，了解你的仓库、你奇怪的命名习惯，知道什么时候该用哪个工具，不用你说第二遍。

还记得 project_final_v2_ACTUAL_FINAL.FINAL.zip 吗？然后 Git 成了基础设施。MCP 正在经历 AI 集成领域的同样时刻。

MCP 生态系统今年达到了 [85000 次 GitHub commits](https://glama.ai/blog/2025-12-07-the-state-of-mcp-in-2025)。npm 上各类 server 和开发工具每周 3100 万次下载。这不是炒作，是实打实的采用。

## 🧠 从这里开始：GitHub MCP Server

[GitHub MCP Server](https://github.com/github/github-mcp-server) 把你的 AI 直接连接到你的仓库、issues 和 PR。不用再复制粘贴上下文了。

大多数人搞错的地方：这个 server 有将近 100 个工具。太多了。模型会懵。GitHub 自己的[研究](https://github.blog/ai-and-ml/github-copilot/how-were-making-github-copilot-smarter-with-fewer-tools/)表明把 Copilot 默认工具从 40 个裁到 13 个，成功率提升了 2-5%。

**方案一 → toolsets**

`GITHUB_TOOLSETS="repos,issues,pull_requests"`

**方案二（隐藏宝石） → dynamic toolsets**

`GITHUB_DYNAMIC_TOOLSETS=1`

不让 100 个工具抢上下文，dynamic toolsets 一开始只给你 4 个。AI 会根据对话需要再启用更多。这个应该放在 README 最显眼的地方，结果埋在一个 issue thread 里。

老手们正在想明白的一件事：MCP 是给人用的基础设施，不是给 agent 的。如果一个东西可以用 bash 命令或直接写代码解决，就那么干。MCP 的价值在于你需要跨不同 AI 客户端的标准化工具时。它不能替代你对 CLI 的了解。

## 🎧 推荐收听

**[Insecure Agents](https://open.spotify.com/episode/6ocq7hHX5qTrIatq3Fwnnu) – Samuel Colvin（Pydantic）**

Pydantic 的创始人聊为什么 AI agent 的安全还是一团糟。不是末日论——就是在我们还没搞明白护栏之前，对我们正在构建的东西的诚实审视。

值得一听如果：你正打算给 AI agent 生产环境的访问权限。

## 🔧 在用什么

**GitHub MCP Server 新的 --tools 参数** - [刚上线](https://github.blog/changelog/2025-12-10-the-github-mcp-server-adds-support-for-tool-specific-configuration-and-more/)。不用再整组启用 toolset，现在你可以精确挑选想要的工具：

`--tools get_pull_request,list_commits,get_file_contents`

配合 --read-only 用，写入类工具会被自动过滤掉。Toolsets 已经不错了，这个是手术刀级别的。

## ✨ 这周

我的 [freeCodeCamp 播客访谈](https://www.youtube.com/watch?v=voPcxCFMbbM)跟 Quincy 一起录的上线了。反馈非常暖心——这期对我意义重大。freeCodeCamp 是我当初学编程的途径之一。如果你错过了，他们还有一个免费的 Git 入门[课程](https://www.youtube.com/watch?v=mAFoROnOfHs)。

就这些。真正影响你 workflow 的工具基础知识。

觉得有用的话转发给你的团队。如果觉得没用，回复告诉我你真正想看什么。

感恩，下周见，

Andrea

P.S. - Git、HTTP、容器、MCP。有些东西会变成基础设施。
$

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
