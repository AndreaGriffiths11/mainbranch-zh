---
title: "🫣 Main Branch：正则表达式，你就这一个任务"
number: 44
date: 2026-10-12
excerpt: "Token 变长了。密码就藏在眼皮底下。靠外形识别凭据的代码，这周有点难。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-44
topics: ["GitHub Apps", "Secret Protection", "Git Infrastructure", "MCP"]
tags: ["github-apps", "oauth", "secret-scanning", "mcp"]
featured: false
---

[Read in English](https://mainbranch.dev/newsletter/issue-44/) • [Leer en Español](https://mainbranch.dev/newsletter/es/issue-44/)

朋友们好，

你读到这封邮件时，我正在飞往西雅图的飞机上，要去参与一个让我很期待的录制项目。我一直想把有主见的声音、技术领导者和 GitHub 出色的同事们聚到一起。这周终于有机会了。更多消息很快就来，我觉得你们会喜欢接下来的内容。

## 🚢 本周上线

### [GitHub App 无状态 installation token 已完成上线](https://github.blog/changelog/2026-10-02-stateless-github-app-installation-tokens-rolled-out)

4 月 27 日开始的逐步上线已经完成。新的 installation token 仍然以 `ghs_` 开头，但长度从 40 个字符变成了大约 520 个。权限、仓库范围、一小时有效期和 REST endpoint 都没变。切换前签发的 token 会继续有效，直到过期。

可能出问题的是 token 周围的*所有环节*。检查一下：是否有校验逻辑要求长度必须为 40 个字符，数据库字段或凭据存储的长度上限是否太小，代理是否会截断过长的 `Authorization` header，以及脱敏规则是否只匹配旧格式。如果你为了测试新格式加过临时的 `X-GitHub-Stateless-S2S-Token` header，现在可以移除了。

### [专为检测泄露凭据打造的模型](https://github.blog/changelog/2026-10-07-purpose-built-model-for-leaked-secret-detection)

GitHub 有了一个针对凭据检测微调的模型。它会读取字符串周围的代码，判断这是否可能是凭据，包括那些没有固定 token 格式的密码。现有的 AI 密码检测告警已经切换到这个模型，Secret Protection 和 Advanced Security 客户无需额外付费。push protection 中的 AI 检测正在私有预览，Copilot `/security-review` 命令中的检查也即将推出。

在 push protection 中，它能在密码进入提交历史之前发现问题。新的检查会消耗计入组织账单的 AI Credits，*即使*一次检查没有拦截任何内容也会消耗。所以，启用之前先设好预算。

## 📖 我在读什么

### [为智能体规模的开发构建 Git 基础设施](https://github.blog/engineering/architecture-optimization/building-git-infrastructure-for-agent-scale-development/)
作者：Brian Celenza。

GitHub 的 push 量在一年内增长到原来的 4.9 倍，从每月 6.9 亿次增至 33.5 亿次。9 月份，Actions 运行了 32.6 亿次。Brian 解释了现有存储为什么难以应对这个规模。Spokes 默认保存每个仓库的五份完整副本，每次写入都需要所有副本参与。所以，增加读取容量反而会让 push 变慢。重构把权威数据放到 Azure Blob Storage，由缓存 worker 响应读取请求，并把压缩整理和垃圾回收从处理在线请求的主机上移走。

这比 GitHub 在 3 月故障之后公布的隔离和容量修复更大。

如果你在同一个仓库上跑大量 CI 或多个智能体，想弄清楚瓶颈从哪里来，这篇值得读。

## 🔧 我在用什么

### [CIMD MCP 参考服务器](https://mainbranch.dev/cimd/)

我最近在做一个参考服务器，帮助 MCP 维护者采用 Client ID Metadata Documents（CIMD）。思路是：客户端的 `client_id` 是一个 HTTPS URL，指向一个 JSON 文件。授权服务器获取这个文件，就能知道客户端名称和允许的重定向 URI。不用维护注册 endpoint 或开发者门户。

我想提供一个能运行、能学习、也能改用到自己项目里的例子。所以它运行在 Cloudflare Workers 上，完整走过发现、用户同意、PKCE 和经过认证的 MCP 调用流程。你可以先用 MCP Inspector 试用托管版本，不用自己部署。

如果你维护远程 MCP 服务器，可以试试这个项目，用它给自己的服务器加上 CIMD 支持。演示版的同意页面特意保持开放，让任何人都能体验整个流程。在把自己的部署用于生产之前，请加入真正的用户身份认证。

## ✨ 这周的一点感受

失望是种奇妙的感觉。会难受，但也能让人想明白一些事。本来想在这周跟大家分享另一条好消息，可惜没能如愿。

这次落空让我开始想，我为什么做现在这些事。是的，[工资到账很开心](https://www.bing.com/videos/riverview/relatedvideo?q=thatn+what+the.+money+is+for+peggy&&mid=361155510851D7628311361155510851D7628311&churl=https%3a%2f%2fwww.youtube.com%2fchannel%2fUCFE01HiRepY3yqlgW78sj8Q&mmscn=stvo&mcid=A02DBA1694F7407F98F50A5355A3CD02&FORM=VRDGAR)。但我也为自己的工作、为能帮到别人感到很自豪。这部分的价值，没法用钱衡量。

别让别人替你定义你的工作和你自己的价值。它重要，因为你在乎。

谢谢你，我们下周见，

Andrea

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
