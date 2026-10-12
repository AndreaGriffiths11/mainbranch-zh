---
title: "🗝️ Main Branch 技术周刊：权限开始挑人了"
number: 33
date: 2026-07-13
excerpt: "新的 ruleset 控制限制了谁能 dismiss pull request review，Copilot CLI 在 GitHub Actions 中使用 GITHUB_TOKEN 运行，不再需要 PAT。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-33
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-permissions-get-picky-issue-33
topics: ["GitHub Rulesets", "Pull Requests", "GitHub Actions", "Copilot CLI"]
tags: ["github-rulesets", "pull-request-reviews", "copilot-cli", "github-actions", "github-token", "newsletter"]
featured: false
---

朋友们好，

我从柏林带着一个新 repo 回来了，稍后说这个。产品这边，GitHub 补上了两个权限漏洞：谁可以 dismiss 一个 pull request review，还有你的 CI 不用 personal access token 能跑什么。

## 🚢 最新发布

**[Rulesets 现在能控制谁可以 dismiss reviews](https://github.blog/changelog/2026-07-07-restrict-who-can-dismiss-reviews-in-rulesets/)**

一个 required review 的防线强不强，取决于它的 dismiss 按钮。到现在为止，任何有 write access 的人都能 dismiss 一个挡住合并的 review，把路清出来让你 merge。新控制项就在 `Require a pull request before merging` 规则里：选定能 dismiss 的用户、团队或 app，其他人的按钮就消失。你可以在 UI、REST API 或 GraphQL 里配置，github.com 上的 repository rulesets 已 GA。要是 required reviews 守着你的默认分支，去把谁能 dismiss 写清楚。

**[Copilot CLI 在 Actions 里不再需要 PAT](https://github.blog/changelog/2026-07-02-copilot-cli-no-longer-needs-a-personal-access-token-in-github-actions/)**

以前在 workflow 里跑 Copilot CLI，得创建 personal access token，把它存成 secret，还得记得轮换。现在 CLI 用 workflow 内置的 `GITHUB_TOKEN` 做认证。你的 job 只需要一个 permission，零个新 secrets：

```yaml
permissions:
 copilot-requests: write
```

在组织拥有的 repos 里，AI credits 直接记到组织账上。有一个设置要留意：必须启用 `Allow use of Copilot CLI billed to the organization` policy。如果你已经允许 Copilot CLI，它默认就是开的。

## 📺 我在看

[美丽人生 (La Vita è Bella)](https://www.miramax.com/movie/life-is-beautiful-la-vita-e-bella/) ，罗伯托·贝尼尼作品

我喜欢历史战争题材的书和电影。这部在我的二战 top 3 里：我很小的时候看过，当了妈妈以后重看，它又用全新的方式把我的心揉碎了。

**值得花时间看，如果：** 你想看一部有史以来最好的电影之一。

## 🔧 我在用

[Ponytail](https://github.com/DietrichGebert/ponytail)。一个给你的 coding agent 用的 skill，原型是那个能把五十行替成一行的 senior dev。前阵子我做了个真实测试：同一个任务，一次开着它，一次没开。没开时，我写了两个 class、五个 function、数字格式化和 89 行代码。开着时，我停在 stdlib。没有 class，没有 formatter，20 行。代码少了 77%，class 是零，两个版本跑出来都一样。

## ✨ 本周

柏林是我在世界上最喜欢的城市之一。每个街区都能感到的历史、那里的人、桑拿文化、那些让你再也看不上其他烘焙食品的烘焙食品。这趟又多了一个来自 booth 的理由：我在 WeAreDevelopers 演示 GitHub Copilot app 时，一段关于 GIF 的对话变成了 [APNG Studio](https://github.com/AndreaGriffiths11/apng-studio)，一个我们在现场搭出来的 canvas。房间里都是准备动手做而不是只来参会的人，事情就会这样发生。把 frames 放进去，为你的 READMEs、slides 或 side projects 拿到干净的 animated PNG。

下周我会去 [Nebraska Code](https://nebraskacode.amegala.com/#about)。你在那里就来打个招呼。如果你是 Main Branch 订阅者，我有份礼物给你。

今天就到这里！

带着感激，

Andrea

附言：WeAreDevelopers 今年九月会把 conference 带到 [San Jose](https://www.wearedevelopers.com/world-congress-north-america)，AAIF VP [Angie Jones](https://x.com/techgirl1908)、Netlify CEO [Mathias Biilmann](https://x.com/biilmann) 还有我的朋友 [Francesco Ciulla](https://x.com/francescociull4) 都在 lineup 上；如果你想去，拜托回复这封邮件告诉我。

![来自柏林的 don](https://mainbranch.dev/images/issue-33-berlin.jpeg)

*别把名字说出来……但它们真的他妈好吃 😁*

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
