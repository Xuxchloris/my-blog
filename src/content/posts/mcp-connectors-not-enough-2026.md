---
title: MCP 能连上所有工具了，然后呢？
published: 2026-07-30
description: MCP 让 Agent 接入了 Slack、GitHub、Jira，但接入不等于理解——950 个连接器之后，下一个瓶颈在哪？
tags: [AI Agent, MCP, 上下文引擎, 工具调用]
category: AI
draft: false
---

7 月 28 号，Anthropic 把 MCP 协议更新到了 2026-07-28 版本，正式推给了 Claude。公告里说现在有 950 多个 MCP 服务器，每天几百万人在用。协议本身也简化了——以前调一个 MCP 工具要走三次 HTTP 往返，现在一次 curl 完事。Hacker News 上有人说"终于不用写那么多样板代码了"，我看了下 diff，确实少了很多行。

同一天，GitHub Copilot 宣布 MCP 和 Agent Skills 全面 GA。微软发了财报，AI 资本开支一分没砍——是几个云厂商里唯一一个在 AI 军备竞赛中踩住油门的。

两天之内，MCP 的信号密集到让人觉得这东西已经稳了。USB-C 的比喻说了快一年，现在看起来越来越像那么回事。

但我第二天读到一篇 blog，观点不太一样。

Dennis Pilarinos，Unblocked 的创始人，7 月 29 号发了篇文章叫《A Pile of MCP Connectors Is Not a Context Engine》。核心观点一句话：MCP 连接器给 Agent 的是 access，不是 understanding。

他举的例子很具体。你问 Agent "为什么支付服务要这样重试？" 答案散落在四个地方：去年一个 PR review 的讨论、Slack 上的某次深夜争论、一个被标成 won't-fix 的 Jira ticket，还有代码本身。没有一个单独的 MCP 连接器能给你完整答案——Slack 连接器只返回 Slack 消息，Jira 连接器只返回 Jira ticket。

Agent 怎么办？它只能自己来。先搜 Slack，拿到一堆消息。再搜 Jira，拿到一堆 ticket。再搜 GitHub，拿到一堆 PR——中间可能还要根据上一轮结果猜关键词、再搜一轮。每一步都把结果堆进 context window，token 越烧越多。最后运气好能找到答案，运气不好方向跑偏了，烧完预算还给你一个错的。

他们跑了 benchmark，数据挺扎眼。同一个 Kotlin SDK 任务，接上 Unblocked 上下文引擎的 Agent 快了 83%，token 省了 48%，成本降了 60%。在遵循团队编码规范这个维度上，有上下文引擎的拿了 9.5 分（满分 10），没用的只拿了 2 分——基本上等于瞎写。

他们还在 Claude Code 上跑了一遍对比。没上下文引擎的版本花了 81 轮子任务去爬代码库，成本高了大概 10 倍，最后答案还是错的。接上 Unblocked 之后，40 秒出正确答案。

这组数据让我想了挺久。

MCP 解决了一个真问题，这点没什么好争的。以前 Agent 读不到公司内部系统的东西，现在能读了。950 个 MCP 服务器不是摆设，生态在收敛，方向是对的。

但收敛完了之后呢？当 Agent 终于能连上所有系统，"怎么高效地找到答案"就成了新瓶颈。这个问题以前不存在——因为以前压根连不上。有点像你把所有房间的钥匙都配齐了，然后发现找钥匙的时间比开门还长。

有意思的是，Anthropic 自己也在关注这件事。Dennis 的文章里提到，前沿实验室已经在写东西讨论"把思考模型和检索模型拆开"——贵的模型做推理，便宜的模型做检索和整理。MCP 负责连接，另一层东西负责理解。

我觉得这会是下半年的一条线。MCP 让连接标准化了，接下来谁能把"理解"也标准化，谁就拿到了下一张牌。上下文引擎、知识图谱、agentic RAG——这些东西可能会越来越频繁地出现在同一段话里，不是在替代 MCP，是在 MCP 上面再盖一层。

写到这里想起 GitHub Copilot 同一天宣布 MCP GA 的事。微软现在是两手抓：一手 MCP（连接层），一手 Copilot（Agent 体验层）。中间那个"怎么让 Agent 更聪明地用这些连接"的层面，还没人认真站出来说"这是我的地盘"。

我猜这个空白不会留太久。

---

信息来源：
- Anthropic MCP 更新公告：https://claude.com/blog/bringing-mcp-2026-07-28-to-claude
- Unblocked：《A Pile of MCP Connectors Is Not a Context Engine》https://getunblocked.com/blog/mcp-connectors-are-not-a-context-engine/
- HN 上关于 MCP 更新的讨论：https://news.ycombinator.com/item?id=49087737
- GitHub Copilot MCP & Agent Skills GA：https://news.ycombinator.com/item?id=49104686
- 微软 2026 Q2 财报（AI capex 未削减）：https://news.ycombinator.com/item?id=49103603
