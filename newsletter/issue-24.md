---
title: "🥇 Main Branch: 传统命令获胜的一周"
number: 24
date: 2026-04-23
excerpt: "现在外面充斥着大量紫色的AI生成噪音。本周我们用Git 2.54的新history命令和你真正应该使用的switch/restore分离来突破这些噪音。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-24
beehiivUrl: https://mainbranch.beehiiv.com/p/3a07d360-73a8-4ed8-8e69-d56bcaacab67
topics: ["Git", "Developer Tools", "Commands", "AI Workflows"]
tags: ["git-2.54", "git-history", "git-switch", "git-restore", "copilot-cli", "google-cloud-next"]
featured: true
---

朋友们好，

现在外面充斥着大量紫色的AI生成噪音。本周我想用两个真正重要的东西来突破这些噪音：一个一直静静坐在你终端里的Git发布版本，和一个大多数开发者完全跳过的调试命令。

## 🚢 新功能发布

### Git 2.54 推出 git history — 这是你不知道自己需要的rebase修复

[Git 2.54](https://github.blog/open-source/git/highlights-from-git-2-54/) 于4月20日发布，带来一个新的实验性命令：**git history**。它做两件事：`reword` 让你修复提交消息而无需启动完整的交互式rebase。`split` 将一个提交分解为两个。

```bash
# 修复最后一个提交消息中的错字
git history reword HEAD~1

# 将一个提交分割为两个
git history split HEAD~2
```

它不会在有合并提交的历史上工作，如果会导致冲突就拒绝继续。这是有意设计的。它在不触碰工作树的情况下运行，所以用于脚本是安全的。

2.54版本中还有：`git rebase --trailer` 一次性向每个rebase的提交追加像 `Reviewed-by:` 这样的trailer。

如果你在快速发布AI生成的代码，你的提交历史可能是一团糟。`git history` 就是清理它的方法。

### git switch 和 git restore 存在。是时候使用它们了。

2019年Git将 `git checkout` 拆分为两个命令。`git switch` 用于分支，`git restore` 用于文件。意图更清晰，出错空间更小。旧命令仍然有效。它只是没有被设计来把一件事做好。

`git switch` 处理分支：

```bash
git switch main # 切换到main
git switch -c my-feature # 一步创建并切换
git switch - # 回到上一个分支
```

`git restore` 处理文件：

```bash
git restore README.md # 丢弃文件的未暂存更改
git restore --staged README.md # 取消暂存文件但不丢失更改
```

区别很重要。使用 `git checkout` 时，`git checkout README.md` 和 `git checkout main` 看起来几乎相同。一个恢复文件。一个切换分支。这种歧义已经造成了真实的数据丢失。

AI生成的脚本仍然到处使用 `git checkout`。现在你知道了现代版本 — 可以发现生成的代码何时落后了。

## 🎧 我在观看的内容

**Copilot CLI更新：chronicle、插件和舰队模式 | GitHub Checkout** by Ryan Hecht，GitHub

Ryan是Copilot CLI背后的产品经理，也是我认识的最清晰的解释者之一。这一集涵盖了 `/chronicle`、插件市场，以及IMO最佳工具的下一步发展。

如果你对代理终端工作流的实际发展方向感到好奇，值得你花时间。[在YouTube上观看](https://www.youtube.com/watch?v=9oAcwmrUE44)

## 🔧 我在使用的工具

我试用了Claude的设计工具和Google Stitch进行UI生成。Stitch获胜，而且差距很大。本周Google还开源了[DESIGN.md](https://DESIGN.md) — 一个简单的markdown规范，为AI代理提供你的实际设计系统：不只是十六进制颜色码，还有每个token背后的原因。

将它放在项目根目录，任何编码代理都能生成符合品牌的UI，无需你在每个提示中重新解释你的品牌。为所有人减少紫色！

## ✨ 本周动态

Google Cloud Next让我在拉斯维加斯，今天下午3:30我将在GitHub展位进行关于多模型AI工作流的闪电演讲。如果你在这里，来打个招呼。这也是为什么这期在周四到达你的收件箱的原因。

怀着感激，  
下周见，  
Andrea

---

📌 **附言：** 我想我找到了我的下一个职业...开玩笑的...还是真的？😀

![DJ MainBranch在拉斯维加斯泳池派对](/images/dj-mainbranch.jpg)

*DJ MainBranch报告上任！*

---

**音频版本**：此技术周刊也提供音频版本，使用[Fish Audio](https://fish.audio/?fpr=andrea63)和我的克隆语音生成。Fish Audio让从文本创建自然语音变得极其简单 — 我只需粘贴周刊内容，几秒钟就能得到高质量音频。