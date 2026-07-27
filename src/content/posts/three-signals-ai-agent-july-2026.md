---
title: 过去这一周，AI Agent 界发生了三件大事
published: 2026-07-27
description: Kimi K3 开源 2.8T 模型、Jack Dorsey 发布 Buzz 要把 Agent 当员工、Fortune 报道 AI Agent 流量一年暴涨 7851%——2026 年 7 月最后一周，三个信号指向同一个方向。
tags: [AI Agent, Kimi K3, Buzz, 技术趋势, 月之暗面]
category: AI
draft: false
---

这周刷 Hacker News 首页，随便往下翻翻，跟 AI Agent 相关的帖子就有七八条。不是那种"又一个 Agent 框架"的软文——新产品上线、研究机构发成果、行业数据报告，内容挺硬的。

我挑三个来说说。它们凑在一起，指向同一个方向。

## 信号一：Kimi K3 开源了 2.8T 参数模型

7 月 16 号，月之暗面（Moonshot AI）发布了 Kimi K3。2.8 万亿参数，100 万 token 上下文，原生视觉能力，Mixture of Experts 架构（896 个专家里激活 16 个）。最关键的是：它是开源的。Kimi 官方的说法是"世界上第一个开源的 3T 级模型"。

Hacker News 上 2107 个 upvote，评论区各种拿它跟 Claude Fable 5 和 GPT 5.6 Sol 比。K3 在大部分基准测试上确实还追不上这两个闭源天花板，但能自己部署、自己微调、拿来搭 Agent，这区别就大了。

让我觉得有意思的是他们放出来的几个案例：

- **GPU kernel 优化**：K3 在 24 小时内独立完成了四个 GPU kernel 的 profile、重写和 benchmark，覆盖了 AttnRes、KDA 和多头 MLA kernel。
- **MiniTriton 编译器**：从头构建了一个精简版 Triton 编译器，有 tile-level IR、优化 pass 和 PTX 代码生成，所有 roofline benchmark 都过了。
- **芯片设计**：这个离谱——K3 在 48 小时内自主走完了芯片设计、优化、验证的全流程，用开源 EDA 工具在 4mm² 憋出了 100MHz 时序收敛。

最后一个最吓人：一个 AI 模型自己设计了跑自己架构的芯片。挺 meta 的，但也证明了它的长程推理和自主执行能力确实到了一个新的级别。

对国内开发者来说，Kimi K3 的意义不只是参数大小。过去半年国内大模型赛道挺安静的，各家都在做应用层，基座模型的突破不多。K3 这个"开源 3T 级"的标签，至少让中国团队在全球 AI 社区重新被看见了。

## 信号二：Jack Dorsey 的 Buzz——把 Agent 当成员工

7 月 21 号，Jack Dorsey 宣布 Block 上线了一个叫 Buzz 的开源 workspace。乍一看像又一个 Slack 竞品——团队聊天、代码托管、项目管理。但 Buzz 有一个关键区别：它把 AI Agent 和人类员工放在同一个身份系统里。

翻译一下就是：你的 Agent 不再是一个绑在 API 后面的工具了。它在 Buzz 里有自己的身份、自己的频道，能参与讨论、处理工单、提交代码。底层基于 Nostr 协议，用签名事件来管理所有交互——不管是人还是 Agent 发的。

Hacker News 上 376 个 upvote，337 条评论。有意思的是讨论的重点不是 Buzz 能不能干掉 Slack，而是一个更根本的问题：**当 Agent 在团队里有正式身份，工作流程会变成什么样？**

我觉得 Buzz 有意思的地方在于，它问了一个挺实际的问题：现在的 AI Agent 都是"附加物"——挂在 Slack 频道里、绑在 CI/CD 流水线上、等人手动调用。它不是团队的一部分，它是一个工具。Buzz 想打破这个界限。如果这条路走得通，Agent 就不再是"你喊它才动"的东西，而是自己看任务、自己协调、自己提 PR 的"同事"。

当然，我知道很多人听到这个会有点发毛。

## 信号三：Agent 流量一年涨了 7851%

7 月 23 号，Fortune 发了一篇报道，标题挺直白的："Dead Internet Theory was partly right: AI agents are eating the Web, growing by nearly 8,000%"。记者 Mia Osmonbekov 引用了一家网络安全公司的数据：能实际执行操作（点击链接、填表单）的 Agent 流量，同比增长了 7851%。

我反复看了两遍这个数字。不是七倍，不是七十倍——七十八倍。

再看看其他数据点：

- 某公司 70% 的 API 调用来自 Agent，不是人。
- API 经纪公司 Alpaca 的月 API 调用量里，Agent 驱动的占比从 2025 年 Q4 的个位数飙到 2026 年 Q1 的 30%。
- 已经有公司开始"以 Agent 为优先"来设计 API——默认消费者是机器。
- 超半数公司将未经授权的 Agent 访问列为安全风险。

同一周，Fly.io 发了篇博客，宣布了他们的 Sprites 产品——他们管这叫"给 Agent 用的计算机"。核心观点很直白：Agent 不想要沙箱，Agent 想要计算机。一台随时创建、随时销毁、带着认证的一次性计算单元。

两件事放在一起，趋势挺明显的：整个互联网正在被 Agent 重构。API 要以 Agent 优先来设计，云计算要提供 Agent 专用计算单元，安全模型要考虑 Agent 身份而不是只防机器人。

## 我的看法

拆开看三件事各是一个方向，放一块儿就看出主线了。

Agent 正在从"工具"变成"主体"。Kimi K3 能自己干长活、Buzz 愿意给 Agent 一个工位、7851% 的流量增长——都在说同一件事：Agent 不再是那种你发一个指令它动一下的东西了。它自己读代码、写代码、调 API、在团队里沟通。自主性到了一个新的临界点。

基础设施也在倒过来适应 Agent，而不是 Agent 去适配基础设施。Fly.io 说得最直白——"Agent 不需要沙箱，Agent 需要计算机"。API 公司开始默认消费者是 Agent 而不是人。这不是"AI 工具怎么接入现有系统"，而是"现有系统怎么服务 AI 主体"。角色完全反过来了。

安全问题还悬着。7851% 的增长里有多少是好的 Agent、多少是不好的？班贝格大学那个研究说检测系统的误报率 7%-15%——也就是说检测工具自己都分不清对面是人还是程序。Agent 的增长速度远远跑在了安全能力前面。

最后一点，中国团队还在牌桌上。Kimi K3 不是最强的开源模型，但它是目前唯一一个到 3T 级别的。这个位置本身就有意义。

2026 年才过了一半。下半年肯定还会有更多东西冒出来。我挺好奇年底回头看的时候，这星期发生的事情会被怎么定义——是转折点，还是只是又一个加速的瞬间。

---

**参考来源：**

- Kimi K3 官方发布：https://www.kimi.com/blog/kimi-k3
- Jack Dorsey 发布 Buzz：https://runtimewire.com/article/jack-dorsey-block-buzz-team-chat-ai-agents-git
- Fortune：AI agents are eating the Web, growing by nearly 8,000%：https://fortune.com/2026/07/23/dead-internet-theory-bots-agents-majority-web-traffic/
- Fly.io：Turn And Face The Strange: Fly.io is betting on computers for AI agents：https://fly.io/blog/kurt-scott-money-sprites/
