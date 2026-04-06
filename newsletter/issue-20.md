---
title: "🔍 Main Branch: 就是那种，终于慢下来读小字的那期"
number: 20
date: 2026-03-28
excerpt: "从4月24日起，GitHub 将使用你的 Copilot 数据来训练 AI。教你如何退出，还有28个新的 secret scanning 检测器，以及一只非常好的老狗。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-20
beehiivUrl: https://mainbranch.beehiiv.com/p/the-one-where-we-slow-down-and-read-the-fine-print-issue-20
topics: ["GitHub Privacy", "Secret Scanning", "Copilot", "Open Source"]
tags: ["privacy", "secret-scanning", "copilot", "terms-of-service", "open-source"]
featured: true
---

嗨，朋友们，

看了标题你们就知道了。

只追求速度不求理解，最后就是一个没人能维护的代码库，和一个没人想过要检查的隐私设置。

说到这个。

## 🚢 新动态

**GitHub 更新了隐私声明和服务条款。** [查看更新日志](https://github.blog/changelog/2026-03-25-updates-to-our-privacy-statement-and-terms-of-service-how-we-use-your-data/)。3月25日发布，你有到4月24日的时间来采取行动。

届时起，GitHub 将使用 Copilot Free、Pro 和 Pro+ 的交互数据来训练 AI 模型。你的 prompt、建议、代码上下文，都包括在内。Copilot Business 和 Enterprise 不受影响。

在 [github.com/settings/copilot](https://github.com/settings/copilot) 的隐私设置中退出。如果你之前已经关闭了产品改进数据收集，那就不用管了。如果你用的是 Free、Pro 或 Pro+，现在就去看看。别想当然。

你私有仓库的源代码仍然不会被使用。这里说的是你在使用 Copilot 时输入的内容，不是存在仓库里的代码。

**Secret scanning 在3月新增了28个检测器。** [查看更新日志](https://github.blog/changelog/2026-03-10-secret-scanning-pattern-updates-march-2026/)。来自15个供应商的28种新 secret 类型，包括 Vercel、Snowflake、Supabase 和 Lark。Vercel API key、Supabase secret key 和 Snowflake 连接字符串现在默认开启 push protection。GitHub 会在 secret 落地之前拦截 commit。

还有新增功能：npm、Airtable、DeepSeek、Pinecone 和 Sentry token 的有效性检查。现在你可以看到被检测到的 secret 是否仍然有效，而不只是知道它出现过。

如果 secret scanning 一直在你的待办清单上，这周就把它划掉吧。

## 🎧 最近在读

[Thoughts on slowing the fuck down](https://mariozechner.at/posts/2026-03-25-thoughts-on-slowing-the-fuck-down/) — Mario Zechner。Mario 的论点不是说 agent 不好，而是说当你退出循环时，你就失去了在事情彻底崩溃之前发现问题的能力。关于"错误的复利效应"那段话在我脑子里转了一整周。

值得你花时间看，如果：你发布过带 agent 的东西，但已经好一阵子没仔细看过了。

## 🔧 最近在用

OpenClaw 经常被人说是"不就是 cron jobs 嘛"。不是的。但它有时确实需要用到你的真实浏览器，这让我不太舒服。所以我做了 Claw Relay 来解决这个问题。Token 认证、权限范围控制、站点白名单、完整日志。我的 agent 用我的真实会话浏览网页，但只能访问我允许的内容。开源：[github.com/AndreaGriffiths11/claw-relay](https://github.com/AndreaGriffiths11/claw-relay)

## ✨ 这周

我家最老的狗撕裂了十字韧带。真的很难受。Charlie 是我们纯属偶然才有的，但他经历了我们的一切。我们的大儿子很长一段时间都不会说话——他学会说 Charlie 的名字比什么都早。我转行的时候，Charlie 跟我们搬到了旧金山。我得癌症的时候，他变成了治疗犬，寸步不离。他按人类年龄算快100岁了，我抱不动他。这个我控制不了。所以我就写代码。他就在旁边，做他一直做的事——做这个世界上最好的男孩。

去摸摸你的狗。

感恩，

下周见，Andrea

📌 附：这是2017年的 Charlie，那年他上了 GitHub 宠物日历。

![2017年的 Charlie 和他的 Octocat 玩偶](/images/charlie-2017.jpg)
$

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
