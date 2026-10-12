---
title: "💸 账单到达前你就能看到"
number: 27
date: 2026-05-17
excerpt: "4月Copilot使用报告现已发布，Dependabot现在可以跨组织访问内部仓库，5月20日直播讲解UBB时代的Copilot最佳实践。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-27
beehiivUrl: https://mainbranch.beehiiv.com/p/f6b5b586-f067-4141-81da-8f01cc3ffea9
topics: ["GitHub Copilot", "用量计费", "Dependabot", "企业"]
tags: ["copilot", "dependabot", "billing", "enterprise", "newsletter"]
featured: true
---

朋友们好，

在[Issue #25](https://mainbranch.dev/newsletter/issue-25/)中，我分析了UBB如何改变每次Copilot调用的成本计算。之后大家最常问的问题是："好吧，那我的团队实际会用多少？"现在有报告可以回答这个问题了。

## 🚢 最新发布

**4月Copilot使用报告现已发布** [阅读更新日志](https://github.blog/changelog/2026-05-12-april-reports-are-now-available-to-prepare-for-usage-based-billing/)

报告会告诉你团队最常用的模型、消耗最高的功能面，以及使用量最高的用户。这不是重新计算的账单，而是在计量器正式启动前的方向性参考。

如果你想了解官方CSV上传流程的详细演示，我制作了一个[关于Copilot计费预览工具的短视频](https://andreagriffiths11.github.io/copilot-interaction-cost-guide/usage-report-video.html)，涵盖了概览、用户、模型、产品和成本中心视图中需要关注的内容。

想深入了解？本周三5月20日美东时间上午11点，我将与Marco Olivo和Francesco Lana进行一小时的直播，讲解UBB时代的Copilot最佳实践。我们将涵盖如何限定上下文范围、获得以代码为中心的答案，以及选择正确的模式，这样agent开销就不会吞噬你的预算。你将获得一份当天就能使用的检查清单。[设置提醒](https://gh.io/ubb-live)。

**Dependabot跨组织访问内部仓库** [阅读更新日志](https://github.com/changelog)

如果你在同一企业中的多个GitHub组织之间维护内部包，Dependabot现在可以访问它们了。以前它只能访问同一组织内的仓库，这意味着跨组织的内部依赖项会悄悄失去自动更新。

从企业的高级安全策略页面启用它。启用后，Dependabot可以为依赖项打开PR，无论哪个组织托管该包。如果你的依赖关系图中有任何跨组织的内部包，请检查哪些一直在悄悄失去监控。

## 📖 我在阅读

**[《Genius Makers: The Mavericks Who Brought AI to Google, Facebook, and the World》](https://www.goodreads.com/book/show/55051662-genius-makers)作者Cade Metz**

Metz追踪深度学习群体从2012年ImageNet时刻，到构建我们今天每天合作的实验室的人才战争。阅读它感觉像是为现在发生的一切提供背景，只是从那些在房间里的人的视角讲述。

值得一读：如果你想了解我们如何从固执的研究人员走到AI成为你账单上的一行项目。

## 🔧 我在使用

**[CSS corner-shape](https://una.im/border-shape)** 作者Una Kravets

作为CSS Borders Level 4的一部分，corner-shape让你定义圆角的实际几何形状。Squircles、超椭圆，border-radius本身无法提供的Apple风格形状。

本周我在我的网站上推出了它，应用于卡片、CTA、徽章、代码块和表单。关键操作是保留border-radius作为后备，这样Firefox和旧版Safari用户仍然可以看到圆角，而Chrome和Edge获得升级。零回归风险。

```css
.surface-card {
  @apply rounded-3xl border border-slate-200;
  corner-shape: squircle;
}
```

## ✨ 本周

我陪小儿子的学校去肯尼迪航天中心旅行，老师们真的工资不够高，就这样。我带的是一个小组，都是现实生活中的好朋友，我很了解他们的父母。我本来以为会很紧张。结果，我度过了最美好的时光。他们是善良的孩子，会做一些搞笑的男孩恶作剧，比如试图从睡袋里偷偷溜出来，但多年的睡眠剥夺训练了我哈哈。

我们睡在巨大的土星五号下面。

![肯尼迪航天中心的土星五号](https://mainbranch.dev/images/saturn-v-kennedy-space-center.jpg)

紧紧抱住你的孩子。时间是小偷，朋友们。

怀着感激之情，

Andrea
