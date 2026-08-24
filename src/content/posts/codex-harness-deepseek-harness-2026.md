---
title: "Codex Harness 开源,DeepSeek 的 Harness 拿了 18.8 万星:AI 编程开始卷运行时了"
published: 2026-08-24
description: "OpenAI 开源 Codex Harness,DeepSeek Harness 开源 11 天拿下 18.8 万星。AI 编程的竞争,正在从模型卷到 Agent 运行时,而开发者该关心的是别把生产链路焊死在预览版上。"
tags: [AI Agent, Codex, DeepSeek, Harness, 开源]
category: AI
draft: false
---

8 月 21 日的 AI 日报里，OpenAI 把 Codex Harness 的核心能力开源了。这不是又一个代码生成工具，它是驱动 Codex Web、CLI、IDE 插件和 macOS 应用跑起来的 Agent 执行框架——任务循环、线程生命周期、工具执行，全归它管。说白了，就是 Codex 的"操作系统"。

往回数八天，8 月 13 日，DeepSeek 也把自家 Harness 开源了。到今天，deepseek-ai/deepseek-harness 这个仓库已经 18.8 万星、2 万 fork，MIT 协议，官网上挂着"开发者预览版"的牌子。十一天，一个从零开始的仓库长到这个规模，放在两年前没法想象。

两家前后脚开源 Agent 运行时，这事比模型本身值得琢磨。

先说 OpenAI 这边。Codex Harness 的核心模块包括 Agent Loop、线程生命周期与持久化、配置认证、工具执行和扩展机制。开发者通过 Codex App Server 用双向 JSON-RPC 协议，就能把 Harness 接进自己的 IDE 或桌面应用，还能拿到实时事件流。翻译一下：OpenAI 不只是把命令行工具扔给你，而是把整个 Agent 的执行底座摊开，让你在上面搭自己的东西。

更提气的是 OpenAI 顺手晒的内部实践：一个产品，5 个月，Codex 写了约 100 万行代码，完成约 1500 个 Pull Request，团队核心理念从"人工写代码"变成"人类定目标、Agent 执行"。这组数字比任何 benchmark 都实在——毕竟是你自家产品在跑。

DeepSeek 的路线不一样。DeepSeek Harness 的口号是"一切皆插件"：模型、工具、技能、会话、沙箱、存储、循环、调度、UI，全是插件，靠 Cordis 内核组合。装完 `npx @deepseek-ai/dsh web` 就能起一个本地 Web UI。想换模型换工具，改配置就行，不用动源码。

一个卖成熟度，一个卖自由度。OpenAI 是"我把执行框架给你"，DeepSeek 是"我把组装方式给你，零件随便换"。挺符合两家一贯的打法。

我的判断：AI 编程的竞争，正在从模型层下移到运行时层。模型差距在缩小——上周 GLM-5.3 不换底座、纯靠后训练就把编程能力拉了一大截（[8 月 19 日那篇](https://xuxai.top/posts/glm-5-3-post-training-scaling-2026/)）。模型随时能换，但开发者一旦把工作流、插件、CI 集成焊死在某个 Harness 上，迁移成本就是另一回事。谁拿到开发者生态的入口，谁就赢了下半场。

这不是我脑补的趋势。GitHub 上这一周冒出来的新项目全是这个方向：CopilotKit/OpenBot 给每个 Agent 配一台自己的电脑（浏览器、文件、工具），yetone/cumora 做 Agent 团队的聊天平台，ShawnPana/phone-harness 让 Agent 直接操作手机，阿里 AMAP 团队也发了 LongHorizon-Harness。人人都想当 Agent 的"家"。连行业分析都在说，四小龙里 DeepSeek 的护城河就是性价比加 Harness 开源框架。

但得泼点冷水。DeepSeek Harness 自己写着：开发者预览版，正在快速迭代，会有破坏兼容性的变更。18.8 万星很好看，可预览版就是预览版，你在上面搭的生产链路，下个版本可能就碎给你看。OpenAI 同理，框架开源不等于开箱即用，集成调试、跟现有开发环境的兼容性，都得自己踩坑。我写 Superpowers 那篇时说过，别被 stars 骗了——现在这句话依然成立。

所以我的建议很朴素：现在就可以玩，但别急着把生产链路焊死。想试 DeepSeek 的，先翻翻它的插件生态——已经有人整理了 awesome-dsh-plugin 精选列表，比盯星星数靠谱。想用 Codex Harness 的，先拿小项目跑通再说。等两家把"破坏性变更"的警告摘掉，再认真考虑搬家。

[8 月 13 日那篇](https://xuxai.top/posts/deepseek-v4-pro-official-launch-2026/)我说过，DeepSeek 要从"卖模型"变成"卖 Agent 全家桶"。现在桶开源了，对面的 OpenAI 也把桶摆上了货架。模型是灵魂，运行时是肉身，灵魂可以随时换，肉身才是开发者真正住下来的地方。谁家的底座更顺手，最后是插件生态说了算。

数据来源：
- [DeepSeek Harness - GitHub（18.8 万星，2026-08-13 创建）](https://github.com/deepseek-ai/deepseek-harness)
- [DeepSeek Harness 官网：开发者预览版，一切皆插件](https://deepseek.com/harness)
- [OpenAI Codex - GitHub](https://github.com/openai/codex)
- [AITOP100 每日 AI 资讯 2026-08-21：OpenAI 开源 Codex Harness 等](https://www.aitop100.cn/ai-daily-2026-08-21)
- [AITOP100 每日 AI 资讯 2026-08-20：中国 AI 四小龙进入淘汰赛等](https://www.aitop100.cn/ai-daily-2026-08-20)
