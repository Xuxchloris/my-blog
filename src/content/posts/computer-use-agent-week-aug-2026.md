---
title: "这周,Agent 开始替你点鼠标了"
published: 2026-08-07
description: "Qwen-CUA 在 OSWorld 拿下 86.2 分,蚂蚁把能操控界面的模型压到 1.3B 激活参数,腾讯用 Agent 一句话生成报表.8 月第一周,大厂集体把 Agent 塞进了你的电脑."
tags: [AI Agent, Computer Use, Qwen-CUA, 技术趋势]
category: AI
draft: false
---

8 月第一周没什么炸场的大模型发布，但翻新闻的时候我注意到一件事：大厂不约而同地把 Agent 往"操作真实界面"这个方向推，动作还都挤在这几天。

8 月 5 号，阿里 Qwen 团队和 XLang Lab 发布了 Qwen-CUA，一个原生 Computer Use Agent。它只靠截图理解界面，不看 DOM 树，也不读无障碍元数据，直接输出键盘和鼠标事件去操作浏览器、桌面应用和专业软件。OSWorld-Verified 基准上拿了 86.2 分，更大的 Max 版本 87.6 分，参数超过一万亿。

两天后，蚂蚁百灵放出 Ling-3.0-tiny：总参数 7.9B，每 token 只激活 1.3B，一个为端侧场景设计的混合推理小模型。它原生支持工具调用，能完成浏览器和移动端的 UI 自动化，完全本地推理，已经上线 OpenRouter 和 Vercel，权重即将开源。

夹在中间的是腾讯。8 月 6 号，Omega 上线，一个 AI 原生数据分析平台：上传数据或者连上数据库，一句话描述需求，Agent 自己规划指标、写 SQL、选图表，几分钟出一张可交互的仪表盘，还能定时推送、版本回滚。内测版名字挺可爱，叫"马尔摩斯"。

再往前翻几周，Anthropic 的 Claude Managed Agents、OpenAI 的 Workspace Agents、谷歌云的 agents-cli 也陆续冒头。Anthropic 主打托管和长时任务，说成功率比标准提示循环最多能高十个点；OpenAI 把 Agent 搬进 ChatGPT 和 Slack，敏感操作要人工审批；谷歌云最实在，直接发了个命令行工具，把 Agent 的开发、测试、部署全流程塞进去。

把这些放一起，我的感觉是：Agent 的叙事换了，从"模型会不会用工具"，切到了"谁把 Agent 变成能天天干活的生产设施"。

Computer Use 这条线尤其值得聊。我上个月写过浏览器自动化，当时 browser-use 靠十万 star 证明了"浏览器即 API"。Qwen-CUA 把这条线往前推了一大步——不只是浏览器，桌面应用、专业软件，只要是人能看的界面，它都想接管。以前没有 API 的软件是 Agent 的禁区，现在禁区在缩小。本质上是给 AI 加了一层兼容层：不用为每个软件写接口，让它像人一样看屏幕、点鼠标就行。

这次小模型和大模型一起上，也是个信号。Ling-3.0-tiny 只有 1.3B 激活参数，能本地跑；Qwen-CUA-Max 万亿参数，在云端干重活。端侧小模型处理高频琐碎任务，大模型处理复杂任务，这种分层以后会是常态。不是所有任务都值得烧大模型的 token，尤其是天天要跑的那种。

但先别急着 high。OSWorld 86 分听着漂亮，可真实世界里点错一个按钮的代价，基准分算不出来。我自己在浏览器 Agent 上踩过类似的坑：表单填对了九成，最后一步把提交点成了取消。demo 里不会出现这种事，真实业务里就是事故。

所以我反而最在意这波产品里那些不性感的细节。OpenAI 给 Workspace Agents 配了权限控制和人工审批，Anthropic 强调治理机制和断点续传，腾讯 Omega 做了 diff 对比和版本回滚。这些才是"敢让 Agent 干活"的前提。

我的判断：最先跑通的会是数据分析这类只读为主的场景。Omega 这种产品错了顶多重新生成一张图，损失可控。Computer Use 这种能真正改数据的操作，短期内还是得人盯着，类似自动驾驶的 L2——Agent 开，人看着，出问题随时接管。什么时候企业敢给 Agent 开无人值守的权限，那才是真正的拐点。

---

*参考：*
- *Qwen-CUA（阿里 Qwen × XLang Lab，OSWorld-Verified 86.2 / Max 87.6）: https://ai-bot.cn/qwen-cua/*
- *Ling-3.0-tiny（蚂蚁百灵，7.9B 总参 / 1.3B 激活）: https://ai-bot.cn/ling-3-0-tiny/*
- *Omega（腾讯 AI 原生数据分析平台）: https://ai-bot.cn/omega-marmos/*
- *Claude Managed Agents（Anthropic）: https://ai-bot.cn/claude-managed-agents/*
- *Workspace Agents（OpenAI）: https://ai-bot.cn/workspace-agents/*
- *agents-cli（谷歌云，ADK + A2A）: https://ai-bot.cn/agents-cli/*
- *每日 AI 资讯聚合: https://ai-bot.cn/daily-ai-news/*
