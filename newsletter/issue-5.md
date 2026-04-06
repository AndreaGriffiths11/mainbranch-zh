---
title: "💡 Main Branch：就是那种，Git 冷知识救你命的那期"
number: 5
date: 2025-12-15
excerpt: "大多数人不知道的命令。真正帮你省时间的 Git 基础。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-5
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-with-git-tips-nobody-tells-you-issue-5
topics: ["Git", "Version Control", "Developer Tools"]
tags: ["git", "version-control", "fundamentals", "productivity"]
---

嗨，朋友们，

我们大多数人活在 `git add`、`git commit` 和 `git push` 里。活干完了，PR 推了，代码上线了。但 Git 有一整层知识就在那里，能帮你省几个小时、保持历史干净、debug 更快、review 更精准。这周我们把那些真正改变你工作方式的 Git 基础拉出来聊聊。

## 💡 大多数人不知道的命令

| 命令 | 干什么的 | 什么时候用 |
| --- | --- | --- |
| `git reflog` | 显示你 checkout 过的每一个 commit。找到你要的那个，`git reset --hard <hash>`，回到安全状态。 | 在一次糟糕的 reset 或 rebase 之后一切都崩了的时候，在你打算全部扔掉之前。 |
| `git bisect` | 二分查找你的历史，找到引入 bug 的那个确切 commit。`git bisect start`，标记 bad/good，它会引导你。 | 调试 regression 而不是翻 200 个 commit。 |
| `git show <hash>` | 一次性输出一个 commit 的元数据和 diff。 | 比去 GitHub 上点快。 |
| `git log --oneline --graph` | 分支历史的 ASCII 可视化图，比原始 log 好读太多。 | 一眼看清分支结构。 |
| `git clean -fd` | 删除未跟踪的文件和目录。不是 rm，不是 .gitignore。 | push 之前彻底清理。 |
| `git fetch --prune` | 清掉本地追踪的已删除远程分支。 | 别再追已经不存在的分支了。 |

## 🚢 新动态

**[Workflow dispatch 现在支持 25 个 input 了](https://github.blog/changelog/2025-12-04-actions-workflow-dispatch-workflows-now-support-25-inputs/)**

GitHub Actions workflow dispatch 从 10 个 input 跳到了 25 个。以前：你得把 `environment`、`database`、`feature_flags`、`version` 和 `region` 塞进一个乱糟糟的 JSON blob 里。现在你可以用干净的、独立的 input。

```yaml
on:
  workflow_dispatch:
    inputs:
      environment:
        description: 'Deployment environment'
        type: choice
        options: [dev, staging, prod]
        required: true
      database: 
        description: 'Database connection string'
        type: string
      feature_flags:
        description: 'Feature flags to enable'
        type: string
        required: false
      version: 
        description: 'Application version to deploy'
        type: string
        required: true
      region: 
        description: 'AWS region'
        type: choice
        options: [us-east-1, us-west-2, eu-west-1]
```

## 🎧 推荐阅读

**[被讨厌的勇气](https://www.simonandschuster.com/books/The-Courage-to-Be-Disliked/Ichiro-Kishimi/9781668065969) - 岸见一郎、古贺史健**

一个哲学家和一个年轻人关于阿德勒心理学的对话。用颠覆你惯常思维的观点把你拉进去。让我重新思考我们为什么用现在的方式构建东西，以及恐惧如何塑造决策——不管是写代码还是做人生选择。提醒一下：这本书把创伤说成是一种选择，有时候听着挺刻薄的。觉得有道理的留下，不认同的放过。

值得一读如果：你喜欢质疑自己的假设，想看看心理学和人际关系的逆向观点。

## 🔧 在用什么

刚用 [FFmpeg](https://ffmpeg.org/about.html) 把一个 4.3GB 的播客[视频](https://gh.io/allstacks)压缩到了流媒体可用的大小。如果你在做视频或音频相关的事，FFmpeg 是"神器"。坦白讲我给 Copilot CLI 丢了文件路径然后它给了我需要的所有命令（我当然 review 了一遍免得[悲剧发生](https://www.reddit.com/r/ClaudeAI/comments/1pgxckk/claude_cli_deleted_my_entire_home_directory_wiped/)）。好机器人 🤖。

## ✨ 这周

我已经准备好休假进入全面 🎄 假期模式了。但在年底之前还有活要干，各家公司现在都在疯狂赶进度。你真的能停下来吗？已经进入假期模式了？回复告诉我，我想通过你来体验一下。

就这些。真正帮你省时间的 Git 基础知识。

觉得有用的话转发给你的团队。如果觉得没用，回复告诉我你真正想看什么。

感恩，下周见，

Andrea

P.S. - MCP server 和 AI agent 越来越聪明了。但如果你在东西炸了的时候不知道 `git reflog`，你就卡住了。工具会变，Git 基础不会。记住你的命令。

P.S.S. - 特别感谢 [Brian Rinaldi](https://mastodon.xyz/@remotesynth) 和 [CFE 团队](https://www.youtube.com/@CFEdev) 多年来提供的免费高质量活动。
$

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
