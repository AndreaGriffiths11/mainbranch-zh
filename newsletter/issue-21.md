---
title: "🏠 Main Branch 技术周刊：PR 收件箱终于好用了"
number: 21
date: 2026-04-04
excerpt: "github.com/pulls 面板从零重建，新增收件箱视图、保存视图和高级筛选。另外：Actions 中 service container 支持自定义 entrypoint。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-21
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-your-pr-inbox-got-fixed-issue-21
topics: ["Pull Requests", "GitHub Actions", "Copilot CLI", "AI Tools"]
tags: ["pull-requests", "github-actions", "copilot", "service-containers"]
featured: true
---

大家好，

你有没有打开过 github.com/pulls，然后瞬间懵了？四十个 PR，没有上下文，完全分不清哪些需要你处理，哪些在等别人。

这周开始不一样了。另外，如果你在 Actions 里跑 service container，又一直想自定义 entrypoint，这次有好消息。

## 🚢 本周更新

**全新 Pull Requests Dashboard** — [查看 changelog](https://github.blog/changelog/2026-03-26-new-pull-requests-dashboard-is-in-public-preview/)

github.com/pulls 面板进行了完全重建。新增了收件箱（Inbox）视图，把你的 pull request 分成三组：需要你 review 的、需要你操作的、可以 merge 的。一眼就能看清什么在阻塞、什么可以推进。

此外还有保存视图功能。如果你经常按特定组织或仓库筛选 PR，现在可以保存搜索条件并固定到侧边栏。筛选语法支持 AND、OR 和嵌套查询，和 Issues 搜索一样强大。

**GitHub Actions 中 service container 支持自定义 entrypoint** — [查看 changelog](https://github.blog/changelog/2026-04-02-github-actions-early-april-2026-updates/)

如果你在 workflow 中使用 service container，一定体会过这个痛点：镜像有默认 entrypoint，却没有干净的方式去覆盖它。常见的绕行方案是写一个 wrapper 脚本，或者单独构建一个自定义镜像来改启动命令。

现在可以直接在 workflow YAML 中使用 `entrypoint` 和 `command` 字段。命名遵循 Docker Compose 的约定，上手很自然。

```yaml
services:
  db:
    image: postgres:17
    entrypoint: ["docker-entrypoint.sh"]
    command: ["postgres", "-c", "log_statement=all"]
```

## 🎧 最近在听

**[An AI state of the union](https://www.youtube.com/watch?v=wc8FBhQtdsA&pp=ygUPbGVubnkncyBwb2RjYXN0) — Simon Willison 上 Lenny 的播客**

Simon 是 Django 的联合创始人，"prompt injection" 这个术语就是他提出的，也是公开构建做得最多的人之一。这期播客长 1 小时 40 分钟，讨论了 agent 工程模式、这种工作方式带来的精神消耗，以及为什么中级工程师才是真正面临风险的群体。关于"致命三要素"的部分非常值得一听。推荐给想了解 AI 对软件开发到底改变了什么、但不想听炒作的人。

## 🔧 最近在用

GitHub Copilot CLI。[Anthropic 刚刚禁止了 OpenClaw 用户使用 Claude 订阅服务](https://www.theverge.com/ai-artificial-intelligence/907074/anthropic-openclaw-claude-subscription-ban)（OpenClaw 是一个开源 AI 代理框架）。如果你的工作流依赖单一 AI 供应商，这件事值得关注。Copilot CLI 包含在你的 Copilot 许可证里，不需要额外的 API key。

我用 CLI 构建了 [proof-agent](https://github.com/AndreaGriffiths11/proof-agent)，一个 GitHub Action，它会启动一个独立的 Copilot 驱动的 agent 来验证 AI 生成的 PR，在 merge 之前进行检查。写代码的 agent 和验证代码的 agent 完全独立。因为自我验证不算验证。

## ✨ 随便聊聊

听 Simon Willison 上 Lenny 的播客时，Lenny 提到有公司在收购 2022 年之前的代码。这让我想到了 [GitHub Arctic Vault](https://archiveprogram.github.com/arctic-vault/)。GitHub 无意中创造了世界上最有"匠心"的代码存档。我写过的烂代码也在里面。如果你的也在，你的 GitHub 个人资料上会有一个小徽章。想想看，我这辈子写过的最差的 Java 代码被完好保存着，随时准备在机器人起义时重建文明 😆。

感谢阅读，下周见，
Andrea

📌 附：如果你在用 OpenClaw，想切换到 Copilot 作为模型供应商：

```
openclaw models auth login-github-copilot
openclaw models set github-copilot/claude-opus-4.6
```

两条命令搞定。

---

*本文由 Andrea Griffiths 撰写，中文版为社区翻译与文化适配版本。如发现翻译问题，欢迎到 [mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh) 仓库提交 PR 帮助改进。*
