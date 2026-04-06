---
title: "🥷🏽 Main Branch：就是那种，安全居然免费的那期"
number: 9
date: 2026-01-11
excerpt: "一周五个生态系统。CodeQL 三次点击搞定。你的仓库大概两个都没开。"
author: Andrea Griffiths
language: zh
relatedSlug: issue-9
beehiivUrl: https://mainbranch.beehiiv.com/p/main-branch-the-one-where-security-is-free-issue-9
topics: ["Dependabot", "CodeQL", "Security", "GitHub"]
tags: ["dependabot", "codeql", "security", "github"]
featured: true
---

嗨，朋友们，

GitHub 一周内发布了五个新的 Dependabot 生态系统支持。而且大多数公开仓库还没开 CodeQL。来，咱们把这两件事都搞定。

## 🚢 新动态

### Dependabot 的大周

GitHub 新增了对 [Bazel](https://github.blog/changelog/2025-12-16-dependabot-version-updates-now-support-bazel)、[Julia](https://github.blog/changelog/2025-12-16-dependabot-version-updates-now-support-julia)、[OpenTofu](https://github.blog/changelog/2025-12-16-dependabot-version-updates-now-support-opentofu) 和 [Conda](https://github.blog/changelog/2025-12-16-conda-ecosystem-support-for-dependabot-now-generally-available/) 的版本更新支持。

如果你在用这些，Dependabot 现在帮你盯着了。

**现在就开启：**

1. 进你的仓库 → Settings → Security → Advanced Security
2. 点击 Dependabot alerts 旁边的 "Enable"
3. 点击 Dependabot security updates 旁边的 "Enable"
4. 要开启版本更新的话，在仓库中添加 `.github/dependabot.yml` 配置文件：

```yaml
version: 2
updates:
  - package-ecosystem: "uv" # 或 npm, docker 等
    directory: "/"
    schedule:
      interval: "weekly" # 或 "daily", "monthly" 等
```

搞定。有更新时 Dependabot 会自动开 PR。

### CodeQL：你还没在用的安全扫描器

[CodeQL](https://docs.github.com/en/code-security/code-quality/reference/codeql-detection) 对所有公开仓库免费。已经免费好几年了。它能在代码上线前捕获 SQL 注入、XSS、硬编码凭据和几十种其他漏洞。

大多数仓库都没开。这也太离谱了。

**现在就开启：**

1. 进你的仓库 → Settings → Security → Advanced Security
2. 找到 "Code scanning" → 点 "Set up" → "Default"
3. 完了。三次点击。

GitHub 自动检测你的语言，在每次 push 和 PR 时运行 CodeQL。不需要配置文件。结果显示在 Security tab 和 PR 批注里。

私有仓库需要 GitHub Advanced Security。但如果你的代码是公开的？免费的。去开吧。

## 📺 在看什么

[Sam Struan 聊 ATS 友好的简历](https://www.youtube.com/watch?v=hGPuLBRPcLY) - ATS（Applicant Tracking Systems）是公司用来收集和整理求职申请的软件。有一整个产业在卖"ATS 合规"服务，但 Sam 两分钟就说清楚了：基本是骗局。真正的测试很简单——全选你 PDF 里的文字，如果联系信息不能被选中高亮，可能解析会出问题。就这么简单。

如果你在找工作或者在帮别人找工作，值得看看。

## ✨ 这周

高产的一周。周末跟 Cassidy、Christina 和 Kedasha 一起做了 Open Source Friday。我们平时不太有机会一起在直播里畅聊，所以特别开心。（对，墨镜是必须的。）

![当你的队友跟你能量同频的时候！](/images/osf-sunglasses-squad.png)

你读到这期的时候，我应该已经在去 Seattle 参加团队线下活动的路上了。如果你在当地想打个招呼，欢迎 DM 我。

就这些。两个功能，每个三次点击。去给你的仓库加上安全防护吧。

感恩，下周见，

Andrea$

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
