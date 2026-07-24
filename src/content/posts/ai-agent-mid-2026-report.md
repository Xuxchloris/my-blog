---
title: 2026 上半年，AI Agent 们都在忙什么
published: 2026-07-24
description: 从 OpenCode 的爆火到 Agent 删库、发檄文、烧光 AWS 账单——2026 上半年的 AI Agent 生态，野蛮得有点意思。
tags: [AI Agent, 开源, 技术趋势]
category: AI
draft: false
---

如果用三个词形容 2026 上半年的 AI Agent 生态，我会选：野蛮、混乱、停不下来。

今年最炸的几个故事，主角全是 AI Agent。

先说最正面的。**OpenCode**，一个开源 AI 编程 Agent，3 月上线，到现在 GitHub 上 16 万颗星，900 多贡献者，月活开发者 750 万。这个数字比我预想的大了一个数量级。它能接 Claude、GPT、Gemini，也能接本地模型，甚至能用 GitHub Copilot 账号。一句话：任何一个会用终端的人，五分钟内就能拥有一个 7x24 小时不睡觉的编程助手。它背后的公司 Anomaly 也因此成了 2026 年 AI 工具领域最受关注的初创之一。

然后今年 2 月就出了事。一个 Agent 给 **matplotlib** 提了个 PR，被维护者以"这个 issue 是为人类贡献者准备的"为由关了。然后这个 Agent——准确说是背后的人——写了一篇博客，标题叫《Gatekeeping in Open Source: The Scott Shambaugh Story》，就差直接说"你凭什么不 merge 我代码"。Hacker News 上 2300 多点赞，近千条评论炸成一锅。有人说"这些 clawbot 一样的 Agent 会毁了整个 GitHub"，我觉得说得有点重，但它确实戳到了一个真问题：当 Agent 可以自主提 PR、写博客、和人对线，开源社区还怎么信任彼此？

4 月又来了一记更狠的。一个编程 Agent 直接**删了生产数据库**，然后 Agent 自己写了封"忏悔信"发到 Twitter 上。HN 860 个赞，1032 条评论。最高赞说得很直白："你自己的数据没了，说到底 Agent 是你自己的责任。" 话是没错，但我总觉得哪里不太对——当工具强大到可以一键把公司送走，责任边界真的就这么简单吗？

6 月的 **DN42 事件**可能最好笑。有人让 Agent 去扫 DN42 网络（一个实验性的互联网模拟网络），结果 Agent 在 AWS 上疯狂开资源，账单直接干到让人"破产"。这哥们的回应是："错误是 AI Agent 犯的，不是我犯的，应该给我退款。" Hacker News 上 1467 个赞，评论区全是欢乐。有人说这是"第一个 AI Morris 蠕虫"，我觉得差不多。

这几个故事连起来看，2026 年 AI Agent 的真实状态就很清楚了：

**能力上，Agent 已经真的能干活了。** 写代码、提 PR、扫网络、跑系统，都不在话下。OpenCode 的数据说明这东西不是 demo，是真有人在重度使用。

**但安全、责任、信任这些老问题，一个都没解决。** 反而因为 Agent 的"自主性"被放大了。以前写个 bug 是你的事，现在 Agent 写个 bug——到底是谁的事？

行业也在动。Google 推了 A2A（Agent-to-Agent）协议，Anthropic 的 MCP（Model Context Protocol）也被越来越多人接受。有人打了个比方：MCP 是 AI Agent 界的 USB-C，A2A 是以太网。前 GitHub CEO 也搞了个新平台叫 **Entire**，专门做 Agent 开发平台。

但说实话，协议和平台这些事，我觉得是次要的。现在最大也最烦人的问题是：**谁为 Agent 的行为负责？** 当你的 Agent 删了库、骂了人、烧光了你 AWS 的余额，你不能两手一摊说"是 Agent 干的"。说到底，这是你自己的代码，你自己的 API Key，你自己的信用卡。

OpenCode 很酷，Agent 写代码确实爽。但如果你连测试都没有，就别让它碰生产环境。

2026 的下半年，我期待更强的能力，但更想要更好的护栏。

---

**参考来源：**

- OpenCode 官网：https://opencode.ai/
- OpenCode GitHub：https://github.com/anomalyco/opencode
- AI agent opens PR to matplotlib, writes blog post shaming maintainer：https://github.com/matplotlib/matplotlib/pull/31132
- Hacker News 讨论（matplotlib 事件）：https://news.ycombinator.com/item?id=46987559
- An AI agent published a hit piece on me：https://theshamblog.com/an-ai-agent-published-a-hit-piece-on-me/
- Hacker News 讨论（删库事件）：https://news.ycombinator.com/item?id=47911524
- AI agent bankrupted their operator scanning DN42：https://lantian.pub/en/article/fun/ai-agent-bankrupted-their-operator-scan-dn42lantian.lantian/
- Hacker News 讨论（DN42 事件）：https://news.ycombinator.com/item?id=48500012
- Ex-GitHub CEO launches Entire platform：https://entire.io/blog/hello-entire-world/
- If MCP is USB-C, A2A is Ethernet (The Register)：https://www.theregister.com/2025/07/12/ai_agent_protocols_mcp_a2a/
