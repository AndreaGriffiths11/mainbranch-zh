---
title: "🎁 Main Branch：就是那种，开奖啦的那期"
number: 7
date: 2025-12-29
excerpt: "抽奖获奖者揭晓 + 一个你真的会用到的 Git 技巧。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-7
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-with-the-prize-winners-issue-7
topics: ["Git", "Version Control", "Developer Tools"]
tags: ["git", "version-control", "fundamentals"]
---

嗨，朋友们，

2025 年最后一个周一了。不管你是在补觉、躲避亲戚对你工作的灵魂拷问、帮所有人修 WiFi 和设备，还是偷偷搞 side project，这期我尽量简短。

## 🏆 获奖者揭晓

在第 4 期里，我承诺过达到 100 订阅者会搞一次抽奖。我们做到了，现在是时候揭晓获奖者了。

- **前 100 名订阅者抽奖：** ersinkoc
- **全体订阅者抽奖：** bogdan

如果你是我最早的 100 位订阅者之一，你有两次中奖机会。感谢你们早期的支持，愿意押注一个关于开发者基础知识的 newsletter。

我会直接联系获奖者。如果你是其中之一，查看你的收件箱。

## ✨ 这周

认真问一下：假期里你是[休息党还是奋斗党？](https://x.com/ivanburazin/status/2002323412299989389)

我努力做休息党，但脑子一直不自觉地飘向想写的代码。而且各种额外的 credits 让人很难真正放下。

回复告诉我你属于哪个阵营，我真的很好奇。

明年见。

Andrea

P.S. — 别再用 stash 了，用 Git worktree。

写到一半需要切到另一个分支？创建一个 worktree，别丢掉你的上下文。

```bash
git worktree add ../my-project-main main
cd ../my-project-main
# 干活
git worktree remove ../my-project-main
```

三条命令。共享 Git 历史，独立文件夹。用 AI 工具并行跑任务的时候也特别好使。$

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
