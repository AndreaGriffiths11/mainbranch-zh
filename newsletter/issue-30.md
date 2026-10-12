---
title: "🚢 Main Branch 技术周刊：Teams 不再到处复制"
number: 30
date: 2026-06-07
excerpt: "GitHub Enterprise Teams 正式 GA，Windows runner image 迁移即将开始，Git worktrees 让 demo 准备少一点脆弱感。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-30
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-teams-stop-multiplying-issue-30
topics: ["GitHub Enterprise", "GitHub Actions", "Git Worktrees", "Microsoft Build", "GitHub Universe"]
tags: ["github-enterprise", "github-actions", "git-worktrees", "microsoft-build", "github-universe", "newsletter"]
featured: true
---

朋友们好，

这周有两个 changelog 更新。一个能让你少做很多重复又无聊的活。另一个如果没注意，可能会把你的 Windows CI 弄坏。

## 🚢 最新发布

### [Enterprise Teams 已经 generally available](https://github.blog/changelog/2026-06-04-enterprise-teams-is-now-generally-available/)

如果你管理的不止几个 org，你肯定懂这个痛点：同一个 SRE team 要在每个 org 里重复创建、重复对齐。Enterprise Teams 让你在 enterprise 层定义一次 group，然后把它分配到下面各个 org 的角色里。你可以把 50 个 org 的 PR review 都路由给同一个 security team，而不是维护 50 份 team。也可以给 platform team 配一次 ruleset bypass，让它在需要的地方都生效。成员关系可以交给你的 identity provider 从头管到尾。少很多需要照看的 team 副本。

### [Actions windows-latest 将迁移到 Visual Studio 2026](https://github.blog/changelog/2026-05-14-github-actions-upcoming-image-migrations/)

如果你用 Windows runners，注意一下。从 6 月 8 日开始，`windows-latest` 和 `windows-2025` labels 会默认迁移到 Visual Studio 2026。rollout 会在 6 月 15 日完成。如果你的 build 依赖 VS 2022 里的某个东西，它可能会安静地坏掉。需要先稳住的话，pin 到 `windows-2022`。想在切换前测试新 image，就用 `runs-on: windows-2025-vs2026`。`macos-latest` 到 macOS 26 的迁移会在 6 月 15 日开始，大概持续 30 天。下周变麻烦之前，先看一眼你的 matrix。

## 📖 我在读

**Robert Scoble 和 Irena Cronin 的 [The AI IPO Race](https://www.unaligned.io/p/the-ai-ipo-race)**

Scoble 和 Cronin 看的是 AI 竞赛背后的资本部分：Anthropic、OpenAI 和 SpaceX 都越来越接近公开市场。AI 不像普通软件那样 scale。每一次 query 都要花 compute。使用量越高，收入会上去，成本也会上去。Fidelity 也把 SpaceX IPO 的最低门槛从 $500K 降到 $2K，所以 retail buyers 也可能会进入这个很奇怪的 debut。

值得花时间读，如果：你每天都在用 AI 工具构建东西，并且想理解它们背后的钱是怎么算的。

## 🔧 我在用

这周我更有意识地在用 Git worktrees。准备 demo 或测试改动时，我不想让干净 branch 和乱糟糟的实验 branch 在同一个文件夹里打架。worktree 可以把一个新 branch checkout 到单独的目录：

```bash
git worktree add -b demo-clean ../demo-clean main
```

这样我可以保留一份 repo 专门用来录制，另一份拿来随便试。这个点对我很重要。准备 demo 本来就够紧张了。我不想因为一个小测试，改掉镜头前需要的那个准确状态。有了 worktrees，我可以试东西、弄坏东西，同时让 demo branch 安安静静待在原地。

```bash
git worktree list
git worktree remove ../demo-clean
```

如果你录 demo、写教程，或者测试风险比较高的改动，把 worktrees 放进你的 Git 肌肉记忆里。

## ✨ 本周

我去了 Microsoft Build，然后留下来参加 GitHub Universe content committee。GitHub 在 Build 上出现感很强，但真正让我兴奋的是 review talks。这个 talk pool 很有范围：技术问题、复杂系统、open source、maintainers、community、craft，还有那些真正重要的日常工作。今年的活动会很好看。

Build 期间我还做了一场 livestream，给 chat 现场搭了一个带 GitHub auth 的 check-in [wall](https://gh.io/hi)。它 polished 吗？完全没有。它是不是用最好的方式保持了 unserious？是的。

![Andrea Griffiths 和 Cassidy Williams 在 Microsoft Build 的 The Terminal Live 上演示 livestream check-in web app。页面写着 "Where are you watching from?"，观众可以用 GitHub 登录，把自己的城市加到 wall 上。](https://mainbranch.dev/images/issue-30-rubber-duck-checkin.png)

*Rubber Duck Tuesday with Andrea Griffiths & Cassidy Williams*

这本来就是重点。如果你在互联网上 live build 一个东西的时候不能玩得开心，那我们到底在干嘛。

我回到家时很累，也很感谢那些让这个 community 变得真实的人。

下周见。

怀着感激，
Andrea

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
