---
title: "🔐 Main Branch：就是那种，Actions 安全终于硬气了的那期"
number: 2
date: 2025-11-24
excerpt: "OIDC token 更精准了，pull_request_target 被锁住了——两个真正影响你 workflow 的安全更新。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-2
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-actions-got-hardened-issue-2
topics: ["GitHub Actions", "Security", "OIDC", "Workflow Security"]
tags: ["security", "actions", "oidc", "compliance"]
---

嗨，朋友们，又见面了。一个安全变更即将上线，一个已经上了——两个都真正影响你的 workflow。

## 🚢 新动态

**GitHub Actions OIDC token 更精准了**

现在你可以在 [OIDC token claims](https://github.blog/changelog/2025-11-13-github-actions-oidc-token-claims-now-include-check_run_id/) 里包含 check_run_id 了。听起来不大，但对合规来说是件大事。以前你只知道哪个 workflow 跑了，现在你能知道是哪个具体的 job、在哪台机器上执行了请求。如果你的 workflow 调用了 Azure 或 AWS 上的内部服务，你可以把那个 token 追溯到发起调用的那个确切 job。当你能把每个 token 绑定到具体 job 而不只是一个 repo 的时候，最小权限控制才算真正落地了。如果你在做"谁在什么时候访问了什么"的审计，这就很重要。

**pull_request_target 事件要被锁住了（12 月 8 日）**

安全上的好消息：pull_request_target workflow 现在会[始终使用你的默认分支作为源](https://github.blog/changelog/2025-11-07-actions-pull_request_target-and-environment-branch-protections-changes/)，而不是某人作为 PR base 用的随便哪个分支。这能防止旧的、有漏洞的 workflow 在过时的分支上被触发执行。现在如果你在 main 上修了一个 workflow 的漏洞，但 feature branch 上还有旧版本，从那个分支发 PR 可能会触发有问题的版本。12 月 8 号，这个门就关上了。

## 🎧 推荐收听

**Darknet Diaries - EP 42: Mini-Stories Vol 2**

Clay 在自己的服务器上发现了一个后门，然后进入了全面侦探模式。用 [John the Ripper](https://www.openwall.com/john/) 破解了攻击者的密码，追踪了他们执行的每一条命令，然后一步一步把他们锁在外面，而不是直接全部删掉。那个取证过程简直是艺术——你能感受到他的肾上腺素飙升。[在 Darknet Diaries 收听](https://darknetdiaries.com/transcript/42/)

## 🔧 在用什么

TypeScript 现在按贡献者数量已经是 #1 语言了。如果你还在纠结新项目要不要上 TypeScript，这个数据可能帮你做决定了。[查看完整 Octoverse 报告](https://octoverse.github.com/)。

我用 TypeScript 做了我的项目 git-history-cleaner。一个用户友好的工具，能生成自定义脚本来清理 git 仓库历史同时保留你的当前文件。如果你有需要清理 commit 历史的仓库，试试看然后告诉我你觉得怎么样：[https://github.com/AndreaGriffiths11/git-history-cleaner](https://github.com/AndreaGriffiths11/git-history-cleaner)。

## ✨ 这周

这周我被感激之情淹没了……说真的。新老朋友们都在分享这份周刊，反馈既有建设性又很暖心。让这份周刊成长为我们都引以为豪的东西，现在感觉真的能实现了。另外这周还去了两次热瑜伽。我感觉自己像个新人（一个浑身疼的新人，但确实是新的 😀）。

就这些。真正影响你 workflow 的基础知识。

觉得有用的话转发给你的团队。如果觉得没用，回复告诉我你真正想看什么。

感恩，下周见，

Andrea

P.S. – 基础优先，永远是。
$

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
