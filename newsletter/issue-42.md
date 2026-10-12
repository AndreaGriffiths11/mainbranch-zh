---
title: "🔐 Main Branch 技术周刊：这次你的 git push 可能会失败"
number: 42
date: 2026-09-27
excerpt: "GitHub 加强 SSH 安全要求，GitHub Actions 告别 Node 20，JavaScript actions 改用 Node 24。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-42
topics: ["SSH", "GitHub Actions", "Node.js", "AI Agents"]
tags: ["ssh", "github-actions", "nodejs", "openclaw"]
featured: false
---

*作者：Andrea Griffiths • [Leer en Español](https://mainbranch.dev/newsletter/es/) • [阅读中文版](https://mainbranch.dev/newsletter/zh/)*

朋友们好，

GitHub 要提高 SSH 认证的安全门槛了。如果你的 remote 地址还以 `git@` 开头，而且很久没检查过密钥用了多久，记得在 10 月 14 日的 RSA 密钥长度新规和 11 月的 brownout（短时停用测试）前检查一下。HTTPS remote 不受影响。

## 🚢 最新发布

**[SSH 安全改进](https://github.blog/changelog/2026-09-22-security-improvements-for-ssh/)**

GitHub 将停用使用 SHA-1 的 RSA 签名（也就是 `ssh-rsa` 签名类型），以及 `diffie-hellman-group-exchange-sha256` 密钥交换算法。10 月 14 日之后上传的新 RSA 密钥必须至少为 3072 位。github.com 和启用 Data Residency 的 GHEC（美国区域除外）也在加入后量子密钥交换 `mlkem768x25519-sha256`。两次 brownout 分别在 11 月 4 日和 12 月 9 日，最终停用日期为 2027 年 1 月 13 日（changelog 里仍写着 2026 年）。只要客户端支持 `rsa-sha2-256` 或 `rsa-sha2-512`，现有 RSA 密钥就能继续使用，大多数现代 OpenSSH 版本都已支持。新建密钥优先用 Ed25519。以 `https://` 开头的 remote 不受影响。

**[GitHub Actions 不再提供 Node 20](https://github.blog/changelog/2026-09-23-node-20-is-no-longer-available-in-github-actions)**

这次是最终切换。GitHub 托管的 runners 现在使用 Node 24 执行 JavaScript actions，临时退出机制 `ACTIONS_ALLOW_USE_UNSECURE_NODE_VERSION` 也被移除了。如果你维护 JS action，把 `runs.using` 改成 `node24`，然后发布新版本。使用第三方 actions 的话，升级到已经支持 Node 24 的版本。GitHub 官方 actions 已经完成升级。Node 24 不支持 macOS 13.4 及更早版本，也没有官方 ARM32 支持，所以这些平台上的自托管 runners 不再受支持。这项变更已经在 github.com 和 GitHub with Data Residency 生效。

## 📖 我在读什么

**[Breakneck: China's Quest to Engineer the Future](https://www.amazon.com/dp/1324106034/)，作者 Dan Wang**

Wang 把中国描绘成一个工程师主导的社会，把美国描绘成一个律师主导的社会。把一大批工程师召集起来，让他们动手干活，哪怕条件还不理想。你怎么看？与 Wang 笔下律师主导的美国相比，如果 AI 遇上一个擅长动手建设的国家，美国会不会呈现出中国的样子？

如果你在意制度究竟是在给做事的人清障，还是把他们困住，这本书值得一读。

## 🔧 我在用什么

[grokbot2claw](https://github.com/AndreaGriffiths11/grokbot2claw)。我最近一直在用 Grok Bot 尝试做个人事务管理、跑这个 newsletter 的流程，还有交付代码。如果没必要，我不想再多付一份订阅费，所以想在不依赖 Cursor 套餐的情况下搭起这套工具。Copilot CLI 选模型很方便；OpenClaw 则让我继续用已经在跑的那套最省钱的本地 agent 配置，保留同样的 CLI 能力。这个桥接只需要一次经过批准的 Mac Shell 交接：`python3 message.py --send` 在 `127.0.0.1` 上启动 HTTP listener，生成新的 bearer token 和临时 SQLite 邮箱，然后由 `adapters/openclaw.sh` 调用固定的 OpenClaw agent（`openclaw agent --session-key grokbot2claw`，不带 `--deliver`）。回复输出到 stdout，或者写入 `result.json`，目录通过 `--output-dir` 指定。Gateway、路由和工具都留在我的机器上。指定的 agent 仍保留平常的权限；这不是 sandbox。

如果你试了 grokbot2claw，直接回复这封邮件，告诉我哪些地方好用、哪些地方卡住了你。

## ✨ 本周动态

我在 [Café con Mito](https://youtu.be/yRZu1180dSc) 的采访上线了（第 4 季第 2 集，西班牙语）。我们聊了如何把陆军里的团队协作带到软件开发中，也聊了 agents：现在人人都能写代码，但不见得都能运维自己写的代码。判断力和品味仍然属于人。我特别感谢这个团队。他们运作这个播客的方式就像 F1 进站维修团队。整个体验的专业度和质量让我印象很深。如果你不懂西班牙语，可以打开字幕，在 Settings 里进入 Subtitles/CC，选择 Auto-translate，再选 English。手机上也类似，从 Captions 进入。

谢谢你，  
下周见，  
Andrea

## 📌 P.S.

这是参加 GitHub Universe 门票抽奖的最后一周：[gh.io/win](https://gh.io/win)。

## 💛 支持 Main Branch

[订阅 Main Branch](https://mainbranch.dev) • [在 GitHub 上赞助我](https://github.com/sponsors/AndreaGriffiths11)

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
