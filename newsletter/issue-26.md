---
title: "⚖️ 规则终于说得通了"
number: 26
date: 2026-05-09
excerpt: "更好的 ruleset bypass 控制、MCP 工作流中的 secret 扫描，以及一个让大型代码库提速 3-4 倍的 LSP 实验。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-26
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-the-rules-finally-make-sense-issue-26
topics: ["GitHub Rulesets", "Secret Scanning", "GitHub Copilot", "LSP"]
tags: ["rulesets", "secret-scanning", "copilot", "lsp", "newsletter"]
featured: true
---

各位开发者好，

这周科技圈不轻松。如果你正在经历裁员，请随时联系我。如果我们合作过，我很乐意为你写 LinkedIn 推荐信。需要引荐？给我发私信。

本周有两个实用更新落地：更好的 ruleset bypass 控制，以及 MCP 工作流中的 secret 扫描。

## 🚢 本周发布

现在可以直接通过 UI、REST API 或 GraphQL，将单个用户添加为仓库级 ruleset 的 bypass actor，不再需要专门创建一个团队来给某个人或 service account 授予 bypass 权限。

仓库管理员也可以在不征得组织管理员同意的情况下重命名被 org ruleset 覆盖的分支——前提是新分支名仍在原有所有 ruleset 的范围内。如果超出范围，重命名会被阻止。这个更新是为那些曾经为了把 `master` 改成 `main` 而提交申请的人准备的。

如果你在用 VS Code 或 GitHub Copilot CLI，可以在提交前让 agent 检查是否有暴露的 secret。它会读取你已在仓库或组织层面设置的 push protection 规则，无需重复配置。

```bash
# GitHub Copilot CLI 配置（需要 advanced-security 插件）
/plugin install advanced-security@copilot-plugins

# 提交前让 agent 扫描：
# "Scan my current changes for exposed secrets"
```

需要在仓库中启用 GitHub Secret Protection。安装 GitHub MCP Server，按需添加插件，即可使用。

## 📖 本周在读

Zack 在启用和未启用 language server 两种情况下，用 GitHub Copilot CLI 执行了相同的编码任务。在一个大型 Ruby 单体仓库（约 11.8 万个文件）中，LSP 让 agent 的速度提升了 3-4 倍。在一个只有 61 个文件的小型 Python 仓库中，则没有差别。

没有 LSP 时，agent 会退回到类似 grep 的搜索方式，浪费大量 tool call 追逐误报。有了 LSP，它可以直接问函数在哪里定义，然后径直找过去。

如果你在大型代码库中工作且还没配置 LSP，这篇值得看。

## 🔧 本周在用

[ClawPilot](https://www.geekwire.com/2026/microsofts-openclaw-team-takes-on-the-personal-assistant-challenge/)，微软内部基于 OpenClaw 的桌面 agent。公司电脑限制很多。这周我在帮忙评审一个黑客松，完全想不起来时间和任何细节。ClawPilot 不到一分钟就从我的收件箱里找到了。

## ✨ 本周动态

正在担任 [Geekulcha Top 15 Young Geeks](https://www.geekulcha.dev/young-geeks) 的评委，这是一个表彰非洲科技创新者的项目——他们是真的在做东西的那种人。我曾有机会在南非组织过黑客松，社区在一个下午能做出来的东西会让你大开眼界。非常期待这次活动。

Andrea

## 📌 附言

我们在 [mainbranch.dev](https://acolombiadev.zo.space/contest) 举办了一场写作比赛。如果你一直有个教程或文章的想法没有付诸行动，这就是你的机会。最佳投稿将在这里发布，并赢得价值 $100 的 GitHub 商店积分。投稿截止日期为 6 月 13 日。
