---
title: "🔑 Main Branch 技术周刊：这次可以删掉一个 PAT 了 - Issue #40"
number: 40
date: 2026-09-13
excerpt: "GitHub Actions 的 cache-mode、Dependabot 无需 PAT 访问私有 GitHub Packages、Cursor 的多智能体研究，以及我的 WebMCP 测试。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-40
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-you-delete-a-pat-issue-40
topics: ["GitHub Actions", "Dependabot", "GitHub Packages", "AI Agents", "WebMCP"]
tags: ["github-actions", "cache-mode", "dependabot", "github-packages", "ai-agents", "webmcp", "newsletter"]
featured: false
---

[Leer en Español](https://mainbranch.dev/newsletter/es/) • [阅读中文版](https://mainbranch.dev/newsletter/zh/)

朋友们好，

这周工作日虽然少，却感觉特别漫长。我一直埋头准备 Universe，也在折腾一些很好玩的东西，已经等不及想分享了。

上周我们聊了 npm 的 trusted publishing 配置。这周有两项更新延续了这个话题。一项收紧了 workflow 对 Actions 缓存的操作权限。另一项让你可以删掉一个 personal access token，你当初创建它，很可能是为了让 Dependabot 访问托管在 GitHub 上的包仓库。

## 🚢 最新发布

### [用](https://github.blog/changelog/2026-09-10-control-github-actions-cache-access-with-cache-mode/) `cache-mode` 控制 GitHub Actions 缓存访问

风险在于：低信任级别的 job 往缓存里写入恶意内容，之后受信任的构建又恢复了这份缓存。现在可以用 `cache-mode` 设定 workflow 或 job 能对缓存做什么：read、write、write-only 或 none。job 级别的设置会覆盖 workflow 级别的设置。如果你使用 reusable workflows，它们获得的权限不能超过调用方授予的范围。像 `pull_request_target` 这样的低信任级别触发器已经默认使用 read。如果你为其中一个声明 write，Actions 会添加警告注释。当这些模式阻止某项操作时，恢复操作会被视为缓存未命中，job 继续运行，所以可以收紧权限而不让构建中断。

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    cache-mode: write
  test:
    runs-on: ubuntu-latest
    cache-mode: read
```

### [Dependabot 自动访问托管在 GitHub 上的包仓库](https://github.blog/changelog/2026-09-08-automatic-dependabot-access-to-github-hosted-registries/)

如果你在用私有 GitHub Packages 包仓库，这次有个好消息。Dependabot 现在无需 PAT 就能读取它们。它的 `GITHUB_TOKEN` 会请求 `packages: read` 权限，并在从 `*.pkg.github.com` 和 `ghcr.io` 拉取时发送该 token。配置在包的设置里完成：打开设置，在 Manage Actions access 下，给运行 Dependabot 的仓库授予 Read 权限。不用改 `dependabot.yml`，基于 PAT 的 registry 配置项也可以删掉了。这听起来可能有些耳熟，因为它最早在 6 月 23 日就上线了。后来有些 npm job 通过 GitHub Packages 解析了公共包，功能因此被回滚。现在自动提供的凭据只用于回退，你显式配置的 registry 凭据仍然优先使用。

## 📖 我在读

### [迈向自动驾驶的代码库](https://cursor.com/blog/self-driving-codebases)，作者 Wilson Lin，Cursor

这篇来得正好，我最近一直在研究 [HydraFusion](https://x.com/acolombiadev/status/2097094692789981208)。我反复在想，选完模型之后会发生什么，以及这个选择是否真有大家想的那么重要。Cursor 使用 planner、subplanner 和 worker 的协作结构，交接时会带上发现和顾虑，而不是直接宣布任务完成。我很认可这种工作方式。他们每小时一千次 commit 的数字有代价：他们接受了明知有问题的代码，同时保留一条独立的、检查通过的 release branch。作为研究结果，这有参考价值。但如果要据此移除生产环境的检查，我会慎重考虑。Cursor 说，更换模型改善了指令遵循能力。模型之间不能随意替换。

如果你正在构建多智能体 harness，或者总看到只谈 commit 速度、不提附带条件的标题，这篇值得读。

## 🔧 我在用

这周我和 Rusty，我的 OpenClaw agent，一起测试了 [WebMCP](https://developer.chrome.com/docs/ai/webmcp)。WebMCP 让页面可以公开 `create-equipment-request` 这样的操作，附上描述和预期输入，agent 就能发现这些工具并通过浏览器调用。我在一个小型本地应用上做了三组配对测试，WebMCP 和应用表单每次都通过了，但 WebMCP 每次运行用了六次操作，UI 则需要 18 到 19 次。六次运行还不足以让我声称节省了成本。Chrome 还让无效输入绕过声明的 schema，传到了我们的工具里，所以仍然需要验证输入并执行权限检查。

## ✨ 本周

我打算比上周更照顾自己一点，也希望你能这样。周六，我在 Twitter 的一个帖子里[问大家](https://x.com/acolombiadev/status/2098749453762982049?s=20)正在做什么项目。读大家分享的内容实在太开心，最后我还给其中一个发出来的项目[做了贡献](https://x.com/GaurangKaria/status/2098920311877927393?s=20)。这正是我喜欢这份工作的地方，我真的需要有意识地多留些时间来做这些事。希望你这周也能做自己喜欢的事。

感谢你的阅读，  
下周见，  
Andrea

## 📌 附言

再分享一个：这是我最近最喜欢的整理笔记的[新工作流](https://lnkd.in/p/eM52akmn)。

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
