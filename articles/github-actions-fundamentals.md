---
title: "GitHub Actions 实战避坑指南"
date: 2026-03-30
excerpt: "我在 GitHub 工作，每天都用 Actions。我也调试过 YAML 到凌晨，推了太多 commit 只为修一个条件表达式。这篇文章是我希望第一天就有人告诉我的东西。"
author: Andrea Griffiths
language: zh
relatedSlug: github-actions-fundamentals
tags: ["GitHub Actions", "CI/CD", "开发者工具", "基础知识"]
featured: true
---

# GitHub Actions 实战避坑指南

我在 GitHub 工作，每天都在用 Actions。同时，我也在凌晨两点调试过 YAML，看着日志查看器把浏览器吃掉，连续推了十五个 commit 只为搞清楚一个条件表达式为什么没有生效。

我不打算告诉你 Actions 是完美的。它不是。日志查看器让资深工程师开始怀疑人生。YAML 表达式语法的学习曲线更像是学习悬崖。"推代码 → 等待 → 失败 → 重复"的调试循环能把一个五分钟的修复变成一整个下午的消耗战。

这些我都经历过。也见过无数开发者经历同样的事。

但我也观察到：大部分痛苦来自于可以避免的使用模式。不是全部——有些确实是平台需要追赶的地方。但很多问题已经有现成的解决方案，只是大家还没发现，因为复制粘贴 YAML 太容易了，就一直在忍受。

这篇文章整理的是我希望第一天就知道的那些实用技巧。

## 别用日志查看器了

我是认真的。Web 界面的日志查看器是 Actions 最大的槽点之一，最快的解决方法就是不用它。

```bash
gh run view --log-failed
```

就这一行。失败的步骤直接输出到终端，立刻可见。不用点三层页面，不用等浏览器决定今天要不要渲染，不用体验返回按钮的随机跳转。

查看完整日志：

```bash
gh run view --log
```

实时观察运行进度：

```bash
gh run watch
```

CLI 更快，可以用 grep 搜索，而且不会在测试输出 50,000 行日志时崩溃。如果 2026 年了你还在通过 Web 界面一层层点进去看构建日志，是时候改变了。

## YAML 膨胀是真实存在的问题，但可以控制

所有 CI 系统最终都会变成"一堆 YAML"。Actions 也不例外。但一个清晰做一件事的 40 行 workflow 和一个充满嵌套条件、矩阵策略和内联 bash 脚本的 400 行怪物之间，差别巨大。

400 行怪物的出现，是因为很多人不了解专门设计来解决这个问题的两个功能。或者知道但不用。

### 可复用 Workflow

如果你在多个仓库中有相同的 CI 步骤，大概率在复制粘贴 workflow 文件。别这么干了。

```yaml
# .github/workflows/ci.yml
jobs:
  build:
    uses: your-org/.github/.github/workflows/build.yml@main  # 内部仓库用 @main 没问题
    with:
      node-version: '20'
    secrets: inherit
```

一个 workflow，维护在一个地方，所有仓库调用。更新一次，所有使用它的仓库自动生效。不会出现版本漂移，不会出现"等等，哪个仓库里的部署脚本是最新的？"

### 组合 Action（Composite Actions）

可复用 workflow 用于完整流水线。组合 action 用于步骤级别——可以理解为构建积木。

```yaml
# .github/actions/setup-project/action.yml
name: 'Setup Project'
runs:
  using: 'composite'
  steps:
    - uses: actions/setup-node@53b83947a5a98c8d113130e565377fae1a50d02f # v6.3.0
      with:
        node-version: ${{ inputs.node-version }}
    - run: npm ci
      shell: bash
    - run: npm run build
      shell: bash
```

这样你的 workflow 文件读起来像句子，不像电视连续剧：

```yaml
steps:
  - uses: actions/checkout@de0fac2e4500dabe0009e67214ff5f5447ce83dd # v6.0.2
  - uses: ./.github/actions/setup-project
    with:
      node-version: '20'
  - run: npm test
```

YAML 还在。但从 120 行缩减到了 12 行。设置变更时只需改一个地方。

## 打破"推代码 → 等待 → 失败"的循环

调试 Actions 最折磨人的地方：改了一个字符，推上去，等四分钟等 runner 启动，结果发现漏了一个引号。十五个 commit 之后，你的 git 历史看起来像一封求救信。

[`act`](https://github.com/nektos/act)，一个社区维护的工具，可以在本地 Docker 容器中执行你的 workflow。相同环境，无需推送。

```bash
act -j build
```

它不是完美复刻。有些 GitHub 特有的上下文在本地不存在。但对于"YAML 有没有写错"和"bash 脚本到底能不能跑"这类问题，它把反馈循环从分钟级缩短到秒级。

如果只想做语法校验：

```bash
gh workflow view ci.yml
```

如果 YAML 有明显问题，它能快速发现。虽然不是完整的 linter，但足以在不推代码的情况下排除基本错误。

## Marketplace 的信任问题

每写一行 `uses: 某个陌生人/酷炫-action@v2`，就是在让你从未见过的人的代码访问你的仓库和密钥。这是真实的安全风险。"固定到 SHA"是正确答案，但几乎没人执行。

实际可行的做法：

1. 固定到 SHA，让 Dependabot 管理更新：

```yaml
uses: actions/checkout@de0fac2e4500dabe0009e67214ff5f5447ce83dd # v6.0.2
```

在注释中写上版本号方便阅读。Dependabot 会在新版本发布时自动开 PR，你可以审查 diff 后再更新。

2. 尽量使用 GitHub 官方维护的 action。`actions/checkout`、`actions/setup-node`、`actions/cache` —— 由构建平台的同一个团队维护，经过审计和测试。

3. 其他 action，先读源码。都是开源的。如果一个 marketplace action 本质上就是一个 20 行的 shell 脚本套了个 Dockerfile，不如直接把这 20 行复制到 `run:` 步骤里，自己掌控。

4. 用 OpenSSF Scorecard 在采用前评估 action 维护者的安全实践。

## 条件逻辑的生存法则

`${{ }}` 表达式语法属于那种"入门简单，深入之后让人崩溃"的东西。字符串插值、truthy 判断、类型强转的边界情况坑过所有人。

几条实用规则：

```yaml
# if 中的表达式始终加引号
if: ${{ github.event_name == 'push' }}

# 用 fromJSON 处理 input 中的布尔值
if: ${{ fromJSON(inputs.deploy) == true }}

# 多条件？用 >- 将换行折叠为空格
if: >-
  ${{ github.ref == 'refs/heads/main' &&
      github.event_name == 'push' }}
```

如果你的条件逻辑复杂到需要画流程图，说明你需要的是一个[带输入参数的可复用 workflow](https://docs.github.com/en/actions/sharing-automations/reusing-workflows)，而不是更多的 `if:` 语句。

[`case()` 函数](https://docs.github.com/en/actions/reference/workflows-and-actions/expressions#case) 是近期新增的功能，值得了解。可以理解为表达式中的 switch 语句，用来替代没人能读懂的嵌套三元表达式。

## 让 Copilot 来写 YAML

写 YAML 不好玩，我不装了。但在 2026 年，大部分 YAML 不需要你手写。

在 VS Code 中使用 GitHub Copilot，用注释描述你想要的效果：

```yaml
# push 到 main 时自动部署生产环境，先跑测试，
# 缓存 node_modules，失败时通知飞书群
```

Copilot 生成 workflow，你审查和调整。它处理语法细节——`on:` 触发器、`runs-on:`、步骤排列——你只需要关注流水线应该**做什么**，不用纠结 `environment` 到底写在 `jobs:` 里面还是外面。

对于已有的 workflow，Copilot 智能体模式可以把一个 400 行的 YAML 文件重构为可复用 workflow 和组合 action。告诉它你的目标，审查 PR 即可。

这不是修复 Actions 本身，而是让你不用直接跟它肉搏。

## 哪些在变好，哪些还需要努力

既然说了不粉饰，那就具体说说哪些改善了，哪些还差得远。

**已经改善的：**
- Job summaries，结构化输出，不只是日志行
- 更大的 runner，64 核机器可用，ARM runner 已经 GA
- Required workflows，组织级别强制执行，无需复制粘贴
- 不可变 action，发布到 GHCR 并附带 provenance
- `case()` 函数和近期表达式能力增强

**仍需改进的：**
- 日志查看器。有进步，但对大型构建来说还不够好。用 CLI 吧。
- 调试体验。`act` 有帮助，但如果官方提供本地执行能力，会改变一切。
- 表达式的学习曲线。文档团队一直在持续改进，效果有目共睹——但仍有提升空间。

我写这篇文章不是为了给 GitHub 辩护。是因为我见过太多团队在有解决方案的问题上反复受苦，而这些方案传播得不够快。

基础能力是有的。平台能用。但"能用"和"好用"是两码事，中间的差距就是你下午消失的地方。这些实践能缩小这个差距。不能完全消除，但够用了。

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch-zh](https://github.com/AndreaGriffiths11/mainbranch-zh)
