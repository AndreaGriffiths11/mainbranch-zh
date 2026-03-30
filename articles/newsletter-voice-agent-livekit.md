---
title: "我给技术周刊加了语音对话功能"
date: 2026-03-30
excerpt: "在技术周刊网站的聊天组件里加了麦克风按钮，点击后可以和 AI 智能体实时语音对话——它了解我写过的每一期内容。基于 LiveKit + RAG + GitHub Models 构建，部署在单个容器里。"
author: Andrea Griffiths
language: zh
relatedSlug: newsletter-voice-agent-livekit
tags: ["LiveKit", "语音 AI", "RAG", "GitHub Models", "Python", "FastAPI"]
featured: true
---

# 我给技术周刊加了语音对话功能

我运营一个面向全球开发者的技术周刊 [Main Branch](https://mainbranch.dev)，专注于 GitHub 功能和开发基础知识。最近给网站加了一个聊天组件——输入问题，它会在所有历史期刊中搜索，返回带引用来源的回答。

文本聊天做完之后，我在输入框旁边加了一个麦克风按钮。点击它，你就进入了一段实时语音对话：你说话，AI 智能体听，然后用语音回答你。不是录音回放，不是把文字回复转成语音。是真正的双向实时语音交互。

用的核心技术是 LiveKit。这篇文章分享一下实现过程，因为它比我预想的要简单不少。

## LiveKit 做了什么

LiveKit 是一套实时通信基础设施。如果你用过腾讯会议、飞书会议或 Zoom，可以把 LiveKit 理解为"可编程版的视频会议系统"——它把 WebRTC 的复杂性（房间管理、音频路由、编解码器、延迟优化）全部封装好了。

对 AI 语音智能体来说最关键的能力：LiveKit 提供了一个智能体框架。你写一个 Python worker 连接到 LiveKit Cloud，然后等待分配。当用户加入房间时，LiveKit 自动把你的智能体派遣进去——监听麦克风、处理语音、调用大模型、生成语音回复，全部实时完成。

实际体验中延迟非常低，感觉像在和真人对话。

## 整体架构

分三个部分：

**API 服务** — FastAPI 构建，负责文本聊天（RAG 检索周刊内容）和生成 LiveKit 房间令牌（用户点击麦克风时触发）。

**语音智能体** — 基于 LiveKit Agents SDK 的 Python worker。向外连接到 LiveKit Cloud，等待房间分配。被派遣后，内部流程包括：语音活动检测（Silero VAD）→ 语音转文本（Azure Speech）→ 大语言模型推理（GPT-4.1-mini，通过 GitHub Models 调用）→ 文本转语音（Azure Speech）。每次回复前，都会重新检索知识库中最相关的内容，和文本聊天共用同一套 RAG 管道。

**前端** — Astro 组件中的麦克风按钮。点击后按需加载 LiveKit 客户端 SDK，向 API 请求房间令牌，通过 WebRTC 接入房间。智能体自动加入，对话即刻开始。

API 和语音智能体部署在同一个 Railway 容器中，用一个 bash 脚本同时启动两个进程——任何一个挂掉，容器退出，Railway（海外的容器托管平台，类似国内的 Sealos 或阿里云 SAE）自动重启。

## RAG 检索

每次用户说话，智能体执行以下流程：

1. 语音转文本（Azure Speech STT）
2. 通过 GitHub Models API 生成向量（text-embedding-3-small，1536 维）
3. 在 sqlite-vec 向量数据库中检索最相关的内容片段
4. 用检索结果重建系统提示词
5. 调用大模型生成回复（GPT-4.1-mini，通过 GitHub Models）
6. 将回复转为语音输出（Azure Speech TTS）

这个流程在**每句话后都会执行**。智能体的知识始终跟用户当前的提问同步，不会停留在第一个问题的上下文上。

**混合检索策略：** 纯向量检索无法回答"最新一期是什么？"——语义相似度不理解排序逻辑。解决方案：启动时，智能体查询数据库中所有 newsletter issue 的 URL，提取期号，在每次系统提示词中注入内容索引：

```
可用 newsletter 期数：issue-1, issue-2, ..., issue-20
最新一期：issue-20
总期数：20
```

这样大模型既能从向量检索中获取语义上下文，*又*能获取 embedding 无法学到的结构化元数据。问"最新一期是什么？"它能回答。问"跟我讲讲 GitHub Copilot"，向量检索会找到对应片段。这就是混合检索。

## 几个值得注意的点

**LiveKit 智能体是 worker 模式，不是服务器模式。** 它不监听端口、不接收 HTTP 请求。它主动连接到 LiveKit Cloud，由平台调度进入房间。一开始我按 HTTP 服务的思路去理解，走了弯路——它本质上是一个处理实时音频流的后台工作进程。

**语音场景对延迟的要求远高于文本聊天。** 文本聊天等 2-3 秒很正常。但语音对话中，如果说完话后沉默 2 秒，体验会非常差。LiveKit 的流式架构解决了这个问题——TTS 在大模型还没生成完整回复时就开始输出语音了。

**sqlite-vec 值得关注。** 我在 SQLite 里做向量检索。没用 Milvus，没用 Pinecone，没用任何托管向量数据库。对于约 130 个内容片段的知识库（涵盖全部 20 期 newsletter、文章和 GitHub 博客文章），sqlite-vec 完全够用，查询耗时在毫秒级。嵌入向量通过 GitHub Models API 在数据摄入时生成——preview 期间免费，质量高（text-embedding-3-small，1536 维），不需要本地加载模型。

**生产环境的调试完全不同。** 语音智能体在本地运行正常，但在 Railway 上默默失败。智能体能听、能准确转文本，但每次都回复"我没有这方面的信息。"排查发现是嵌入 API 返回 400 错误——一个旧的环境变量（`LIVEBRAIN_EMBEDDING_MODEL`）还设置的是本地模型名称（`all-MiniLM-L6-v2`），API 不认这个。解决方法：删掉这个变量，让它默认使用 `text-embedding-3-small`。实时日志让问题浮出水面——如果没有在代码里加 `print()` 打印检索到的片段数和相似度分数，可能要猜好几个小时。

## 下一步

我正在把这套方案中可复用的部分提取成一个开源框架：指定一个包含内容来源的 YAML 配置文件，运行数据摄入脚本，就能生成一个了解你内容的语音智能体。周刊、技术文档、博客——什么内容都可以接入。

目前还在整理中。mainbranch-agent 版本已经跑通了，但通用框架需要进一步打磨才能让其他开发者顺畅使用。我会在真正打磨好之后再开源发布。

想体验实际效果，访问 [mainbranch.dev](https://mainbranch.dev)，点击右下角的聊天气泡，麦克风按钮就在输入框旁边。

---

> 🌐 **关于中文版本：** 本文由作者创建并维护于 [mainbranch.dev](https://mainbranch.dev) 上的开源仓库中。如果你发现翻译中有任何不准确的地方，欢迎直接提交 PR 帮助改进：[github.com/AndreaGriffiths11/mainbranch](https://github.com/AndreaGriffiths11/mainbranch-zh)
