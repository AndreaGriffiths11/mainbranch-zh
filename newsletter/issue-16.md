---
title: "🚰 Main Branch：就是那种，水管终于修好了的那期"
number: 16
date: 2026-02-28
excerpt: "两个你早就不抱怨了的摩擦点被悄悄修好了——因为你以为它们永远不会变。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-16
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-plumbing-got-fixed-issue-16
topics: ["GitHub Actions", "Developer Experience", "Fundamentals"]
tags: ["github-actions", "workflow-dispatch", "artifacts", "plumbing", "developer-experience"]
featured: true
---

嗨，朋友们，

先说个事：这期是周日发的，不是周一。算是个实验。讨厌的话回复告诉我，喜欢也回复告诉我。顺便帮我加个联系人，别让邮件掉进垃圾箱。

好了，进入正题。

我每天都在用 AI，后面还会告诉你用的哪个模型。但我不打算让 AI 成为这份 newsletter 的全部。打开率也支持我——基础知识类的内容每次都赢。所以这周：那些没人写的、无聊但美好的水管修复，因为大家都忙着吵 agent 的事呢。

---

## 🔍 那些默默浪费你时间的水管问题

你知道那些你已经不再注意的摩擦点吗？就是那种几年前你写了个 workaround 然后再也没回头看的？GitHub 这个月悄悄修了其中两个。

---

## 🚢 新动态

**Workflow Dispatch API 现在会返回 run ID 了**

如果你曾经通过 API 触发 workflow，然后疯狂轮询 runs endpoint 试图用时间戳匹配到底哪个 run 是你的——这个更新就是为你准备的。`workflow_dispatch` API 现在支持 `return_run_details: true`，直接返回 run ID。

CLI 也跟上了。从 v2.87.0 开始，`gh workflow run` 会自动返回 run URL，不需要额外参数。社区里这个需求从 2022 年 1 月就开始提了。

状态：<a href="https://github.blog/changelog/2026-02-19-workflow-dispatch-api-now-returns-run-ids/">GA</a> | 需要：API 参数 `return_run_details: true` 或 CLI v2.87.0+

**Actions artifacts 不再强制打 zip 了**

以前通过 Actions 上传的每个 artifact 都会被 zip。下载一个单独的二进制文件？zip。上传一个 `.tar.gz`？恭喜，你现在有了一个 `.zip` 里套着 `.tar.gz`。

在 `upload-artifact` v7 里设置 `archive: false`，文件就按原样上传。HTML 文件可以直接在浏览器里渲染，图片直接显示。再也不用为了一个文件解压了。

状态：<a href="https://github.blog/changelog/2026-02-26-github-actions-now-supports-uploading-and-downloading-non-zipped-artifacts/">GA</a> | 需要：`upload-artifact` v7 配合 `archive: false`，`download-artifact` v8 | 目前仅支持单文件

---

## 📺 在看什么

<a href="https://www.youtube.com/watch?v=AaLx9NEVJ98">AI 正在取代那些"安全"的工作，该怎么办</a> – Kara Swisher 和 Bill Gurley 的对话

Gurley 是前 Benchmark 合伙人、Uber 早期投资人，写了一本关于打造热爱的职业的书。最打动我的不只是关于热情的部分。Kara 提到在收发室里对她最差的人恰恰是最没才华的人——这点我深有体会。我接触过的最厉害的工程师和领导者，从来不会忘记自己从哪里来，会回你的私信，就是很好的人。

推荐给：正在重新思考职业里什么叫"安全"的你。

---

## 🔧 在用什么

Claude Opus 4.6。做正经开发工作我会选的模型。现在可以直接从 GitHub 把 issue 分配给 Claude，我最近一直在实验这个。引擎非常强大。个人项目我会用更经济的模型比如 MiniMax 2.5，但碰到复杂的工作，Opus 就是首选。

---

## ✨ 这周

我最近感受到了一种难以置信的存在焦虑。大规模裁员。一家试图坚持正确方向的公司。其他公司让我失望到难以言表。

如果你也有同样的感觉，你不是一个人。

我和同事 Gwen 以及 GitHub Star Rishab 做了一期<a href="https://www.youtube.com/live/gmBLoqQQA7k?si=xyZeNTvnpJyj5x2I">对话</a>，他们是 <a href="https://learntocloud.guide/">Learn to Cloud</a> 的创建者（一个免费、开源、动手实践的云计算和 DevOps 学习路线图）。他们把很多成功归因于丰盛思维——慷慨地帮助别人、经营友谊、善良。

为了走出这种低谷，我在做我能做的事：做一个善良的人。希望你也是。

---

**这就是这周。** 四年的 workaround，在两条 changelog 里修好了。无聊的东西很重要。基础为先，永远如此。

感恩，下周见，

Andrea

🇪🇸 **Léelo en** **[español](https://mainbranch.dev/newsletter/es/issue-16/)**

**支持 Main Branch：** [订阅](https://mainbranch.beehiiv.com/) | [GitHub Sponsors](https://github.com/sponsors/andreagriffiths11)
$

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
