---
title: "🔐 让你的凭据不再存在于 .env 文件中"
number: 22
date: 2026-04-13
excerpt: "报税季提醒我们，“未来的我会处理这个”永远都是谎言。本周 GitHub 发布了两个功能，减少了你需要手动管理的事项。"
author: Andrea Griffiths
language: zh
relatedSlug: "credentials-stop-living-in-env"  
topics: ["GitHub 安全", "npm", "Copilot", "职业发展"]
---

# 🔐 让你的凭据不再存在于 .env 文件中

大家好,

报税季。我一年中最不喜欢的时候。就是你意识到"未来的我会处理这个"是你连续十二个月每个月都对自己说的谎话的那个时候。

本周 GitHub 发布了两个功能,减少了你需要手动管理的事项。我们来看看。

## 🚢 新发布的功能

### Copilot Autofix 新增批量模式

如果你的 PR 被标记了五个代码扫描警报,不得不一个一个修复,每次都触发完整扫描,这个功能就是为你准备的。

PR 上的代码扫描警报现在显示由 Copilot Autofix 生成的修复建议。之前你只能一个一个应用这些建议,但每次应用都会创建单独的提交并触发新的扫描。现在你可以从 Files Changed 标签页将多个建议添加到批次中,一次性提交所有修复。一次提交,一次扫描。

对于 CI 较重的仓库,这是实实在在的时间差异。如果你的流水线每次扫描需要 10 分钟,而你有四个警报,你就从 40 分钟的扫描时间减少到了 10 分钟。

Copilot Autofix 在公开仓库中无需 Copilot 订阅即可使用。对于私有和内部仓库,你需要 GitHub Advanced Security。

### npm 可信发布支持 CircleCI

npm 可信发布让你在不存储任何凭据的情况下发布包。你通过使用 OIDC 的 CI 流水线进行身份验证,npm 在发布时验证令牌。无需轮换密钥,环境变量中也没有令牌。

它已经支持 GitHub Actions 和 GitLab CI。现在也支持 CircleCI 了。

如果你今天在从 CircleCI 发布 npm 包,可以完全删除存储的 NPM_TOKEN。设置可以在你的 npm 账户设置中完成,或通过 CLI 的 `npm trust circleci` 命令。[可信发布文档](https://docs.npmjs.com/trusted-publishers) 有完整的设置说明。

存储的凭据是供应链事件最常见的来源之一。即使你不使用 CircleCI,这也值得了解,可信发布是 npm 正在构建的模式。如果你还没有设置,现在是个好时机。

## 🎧 最近在听的

**《Radical Candor》by Kim Scott**

我丈夫买了有声书,我一直在一起听作为复习。我几年前读过,但现在感受不同了。Kim Scott 在南方长大,那里的文化是永远不说不,把批评性想法留给自己。听起来熟悉吗?

我一直以感恩的心态领导--"我很高兴能在这里"是我真实的感受。但我正在学习,在竞争激烈的行业中,感恩和为自己争取并不互相排斥。这是我仍在摸索的事情。如何倾向于不舒服的对话。如何大声给自己信用,而不只是私下里。

如果你管理他人,或者你花了太长时间对一个你真正应该坐下的桌子上的座位心存感激,这值得你的时间。

## 🔧 最近在用的工具

**[Keeper Tax](https://www.keepertax.com/invite?referrer=Andrea1445425)** - 我今年再次使用它来管理我的独立承包费用。它连接到你的账户,自动导入你的费用,并找出你可能会错过的抵扣项目。使用第二年了。如果你做任何自由职业或合同工作,值得看看。不是赞助,只是我使用的工具,链接给你 25% 的折扣。

## ✨ 本周

[Andy Warfield 关于 S3 Files 的分析](https://www.allthingsdistributed.com/2026/04/s3-files-and-the-changing-face-of-s3.html) 是我最近看到的更好的工程分析之一。去读一下。但 [Hunter Leath 的推文](https://x.com/jhleath/status/1909683757642359184) 值得反思。他在 2023 年写了这个确切的 PRFAQ,在组织不愿行动时离开,三年后看着他的前同事发布了它。他为他们感到高兴,听起来是个不错的人。这让我思考:有多少好想法因为背后的人厌倦了为它们而战而离开了?

就这样,清理你的凭据,批量修复,思考你在留住谁。

带着感激,下周见,
Andrea

附:我一直在使用 [Mintlify](https://mintlify.com) 为我的[代理上下文系统](https://mainbranch.mintlify.app/) 生成文档,老实说--给我留下了深刻印象。免费,一键,全面输出,真正可读。如果文档是你的痛点,值得看看。