---
title: "🔭 Main Branch: The One Where Defaults Stop Being Blind Spots - Issue #36"
number: 36
date: 2026-08-16
excerpt: "Three things shipped this stretch that all come down to the same idea: control over defaults."
author: Andrea Griffiths
language: zh
relatedSlug: issue-36
topics: ["Pull Requests", "Code Scanning", "OAuth", "AGENTS.md", "Open Source", "Node.js"]
tags: ["pull-requests", "code-scanning", "oauth", "agents-md", "open-source", "nodejs", "renderatl", "newsletter"]
featured: false
---

嗨，朋友们，

这段时间发布的三件事，都指向同一个理念：掌控默认设置。GitHub 让组织能够限制开放 PR 的数量，让安全团队能够在无需手动编辑每个 repo 的情况下标准化代码扫描，还让 OAuth 应用通过 redirect URI 和 token 刷新拥有更多腾挪空间。没有哪一项很炫。却都能替某个人省下一个周五下午。

## 🚢 已发布内容

**[在组织级别设置 pull request 限制](https://github.blog/changelog/2026-08-06-set-pull-request-limits-at-the-organization-level)**

现在，你可以限制没有写入权限的贡献者同时能打开多少个 pull request；只需在组织级别设置一次，不必逐个 repo 设置。它位于组织的 Settings → Moderation options → Interaction limits 下。如果你大规模维护 open source，又厌倦了垃圾 PR 在数十个 repo 中吞噬审查时间，这会很有用。

**[大规模自定义 code scanning 默认设置](https://github.blog/changelog/2026-08-04-customize-code-scanning-default-setup-at-scale)**

Code scanning 的默认设置现在可通过新的 `github-codeql-config-file` repository property 接受你自己的 CodeQL 配置文件，因此你可以让组织中的每个 repo 都指向一份共享配置，而不是一次次点开各个 repo 的设置。它现在已在 github.com 上线，GitHub Enterprise Server 支持将在 3.23 版本推出。如果默认设置对你们安全团队的需求来说过于通用，这就是解决办法。

**[OAuth apps 支持多个 redirect URI 和 token 刷新](https://github.blog/changelog/2026-08-14-multiple-redirect-uris-and-token-refresh-for-oauth-apps/)**

OAuth apps 现在最多可以注册十个 redirect URI，而不再只有一个；每个 URI 都可单独配置 wildcard matching，并且可通过 `offline_access` scope 选择使用短期 access token 加上有效期六个月的 refresh token。值得检查一下你自己的 app：如果你过去只有一个 redirect URI，wildcard matching 会作为遗留行为默认开启；现在它已变得可见，而且你可以关闭它。

## 📖 我正在读什么

**[watermarks-remover](https://github.com/guillaumemeyer/watermarks-remover)**，作者 Guillaume Meyer（[他在 X 上的看法](https://x.com/guillaumemeyer/status/2088779299667272150)）

我读 Guillaume 的 README 时，本来以为会看到一个工具的推介，结果读到了更接近一篇文章的东西。他构建了一项 agent skill，用来移除自己内容中的 AI 来源标记；而其中最有意思的是他关于移除实际代价的部分：为了绕过统计水印而重写文本，会损害文字质量。他对此直言不讳，甚至问道，为什么要为 premium model 付费，只为了之后再把它的输出交给一个更便宜的模型处理。读起来像是一个在发布前认真思考过取舍的人，而不是在兜售魔法橡皮擦的人。

Anthropic 本月推出的 watermarking，正是我一直想着那一段的原因。Claude 生成的文本现在默认带有不可见水印，而 Anthropic 的文档也承认，这个标记证明的是处理过程，不是作者身份：因为有人可以用 Claude 翻译、编辑或总结自己的作品，结果仍然会带上这个标记。我每周都会用 Claude 把这份 newsletter 的开头翻译成简体中文，然后再通过 Beehiiv MCP server 发布，同样也是通过 Claude。按照这套逻辑，我自己的文字会沾上一面不该有的旗子。这正是我喜欢 open source 的地方：Guillaume 看到了这个缺口，便构建了一个工具，而不是只停留在争论上。

如果你曾想过“AI detection”实际衡量的是什么，或者你维护的内容 pipeline 会接触 AI 生成的草稿，那么这值得你花时间看看。

## 🔧 我正在用什么

维护 Team X-Ray 让我吃了苦头才明白：除非你明确告诉 agents，否则它们不会读你的 docs。我已经改用有作用域、按目录放置的 `AGENTS.md` 文件，而不是只放一个 README；这样，像“这个 component 需要 Storybook test”这样的规则，就放在它所约束的代码旁边，而不是放在三层文件夹之上、agent 在选择工具前根本找不到的地方。

Nicholas Tindle 在维护 AutoGPT 时也得出了同样的结论：180,000 stars、150 个开放 PR，其中很大一部分由 agents 编写。[本月早些时候，我在 GitHub Blog 写过他是如何处理这件事的](https://github.blog/open-source/maintainers/your-contributors-are-ai-first-now-is-your-project/)。简而言之：放置位置和说明本身一样重要。

## ✨ 本周

这周我从 RenderATL 回到家，说实话，我怎么夸这场 conference 都不够。OpenJS Foundation 在那里举办了 Node.js Interactive track，其中包括一场 Code and Learn session；大家在 Node.js core team 成员 Matteo Collina ([@matteocollina](https://x.com/matteocollina))、James Snell ([@jasnell](https://www.jasnell.me/))、Claudio Wunder ([@wunderacle](https://x.com/wunderacle)) 和 Ethan Arrowood ([@arrowood.dev](https://bsky.app/profile/arrowood.dev)) 的指导下，向项目提交了自己人生中的第一个 PR。我做了一场分享，也和 Node community 的老朋友们叙了旧——这正是我在 2019 年第一次演讲时称为科技界最友好社区之一的那个社区。我仍然热爱这个社区，也为自己能够支持这个 foundation 而感到自豪和感激。

感谢你的阅读，
下周见，
Andrea

## 📌 P.S.

哥伦比亚咖啡产区仍在从 7.4 级地震中艰难恢复。已确认 281 人死亡，超过 12,000 栋房屋被毁。我的家人就在那里。

Asociación de Bancos de Alimentos 今天正在向 Pereira、Armenia 和 Manizales 运送食物：[donahoy.abaco.org.co/colombia2026](https://donahoy.abaco.org.co/colombia2026)

如果你的公司有捐款配捐计划，这周就该用上它。

## 💛 支持

[订阅 Main Branch](https://mainbranch.beehiiv.com/) • [在 GitHub 上赞助](https://github.com/sponsors/AndreaGriffiths11)
