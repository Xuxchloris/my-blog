---
title: "V4 Pro 正式版上线了, DeepSeek 的涨价公告还挂着"
published: 2026-08-13
description: "8 月 12 日晚 DeepSeek 突然发布 V4 Pro 正式版(V4-Pro-0813), 定价是 Flash 的 3 倍, Agent 跑分贴脸 Fable 5, 还撞上了 Grok 4.6. 涨价没来, Pro 先来了, 聊聊这波操作."
tags: [DeepSeek, 大模型, AI, API 价格]
category: AI
draft: false
---

昨晚深夜，DeepSeek 把 V4 Pro 正式版端出来了。机器之心 00:26 发的稿子，标题就是"刚刚"。模型名叫 DeepSeek-V4-Pro-0813，API 文档先行更新，官方价格一分没动——涨价公告还挂在定价页上："计划近期整体上调 DeepSeek API 服务的定价，预计涨幅较大。"

上篇我写过，涨价公告卡在 Pro 前头，很难说是巧合。现在 Pro 真来了，倒是先得给 DeepSeek 记一功：说好的"大幅涨价"，至少没在发布当天顺手把刀落下。

先看价格。V4 Pro 每百万 token：输入 $0.435，输出 $0.87，缓存命中 $0.003625。对照 V4 Flash 的 $0.14/$0.28/$0.0028，正常价正好是 3.1 倍，但缓存命中只贵了 29%。上下文同样是 1M，最大输出 384K，并发限制从 Flash 的 2500 砍到 500。这定位很清楚：Pro 不是给你高并发刷量的，是干重活、跑长任务的。

再看能力，这是最有意思的部分。按 DeepSeek 官方放出的对比表，V4 Pro 在 Agent 相关评测上已经贴脸闭源天花板：Terminal Bench 2.1 拿到 87.9，Claude Fable 5 是 88.0，Opus-4.8 是 85.0；Cybergym 更猛，83.3 直接把 Fable 5（70.0）和 Opus-4.8（78.3）都甩开。最夸张的是 DeepSWE，从 Preview 版的 12.8 直接干到 62.7。一个版本的差距，翻了快五倍，这轮 post-training 基本全砸在 Agent 能力上了。

但别急着吹。NL2Repo（一句话搭仓库）V4 Pro 是 61.5，Fable 5 有 83.1；HLE 上 42.7/60.0，也比 Fable 5 的 53.3/63.0 低一截。说白了：代码执行和工具调用它能打，但"自己从零把项目搭起来"和纯推理硬功夫，跟顶级闭源还有肉眼可见的差距。Artificial Analysis 给的智能指数是 53，中位数 27，属于第一梯队，但不是第一。输出速度 83 token/s，倒是比平均的 64 快不少。

为什么是现在发？我猜有三层。第一，Flash 顶不住了。机器之心说 V4 Flash 正式版上线后全球用户量大涨，官方 API 已经多次性能下降，推理算力不够。Pro 这时候来，能把重负载分流走。第二，抢在涨价前让用户先上车。现在按旧价体系用 Pro，等真涨价了，锚点已经立住了——"Pro 本来就比 Flash 贵三倍"，到时候 Flash 涨点价，心理上也顺理成章。第三，撞车 Grok 4.6。xAI 这两天也发了 Grok 4.6，1.5T 参数基座，官方口号"同样价格、显著提升"，对比图直接拿 GPT-5.6 Sol Max 和 Fable 5 Max 当靶子。两家前后脚发新品，注意力就这么多，谁先发谁赢。

顺带说个细节：社区里已经有人发现 V4 Pro 的思维链风格跟 Preview 不一样了，机器之心也提了这茬。平时没人关心这种事，但真在跑 Agent 流水线的人会在意，思维链长短直接影响成本和超时设置。我的习惯是，换模型先拿带工具调用的任务回归一遍，别光信榜单。

我的判断：DeepSeek 的"涨价"，大概率不是粗暴地把 Flash 拉高，而是靠产品分层把价格体系理顺。Pro 卖 Pro 的价，Flash 继续当价格屠夫。缓存命中价差只有 29%，说明批量、长上下文场景是他们的价格锚点，这个盘子他们不想动。对开发者来说，这反而是好事——想要 Agent 能力又嫌贵的，先用 Pro 的旧价窗口期跑起来；跑量的话 Flash 依旧便宜。至于 Harness，更新日志里已经预告"即将发布"，DeepSeek 这是要连着 Agent 基建一起卖。从"卖模型"到"卖 Agent 全家桶"，这步棋比涨价本身值得看。

数据来源：
- DeepSeek API 定价页（V4-Pro-0813 价格、涨价公告）：https://api-docs.deepseek.com/quick_start/pricing/
- 机器之心《刚刚，DeepSeek V4 Pro正式版发布！》（公众号，2026-08-13）：https://mp.weixin.qq.com/s/HIPTB397zHkvEAt5MySCrA
- Artificial Analysis - DeepSeek V4 Pro 0813 模型页：https://artificialanalysis.ai/models/deepseek-v4-pro
- DeepSeek API 更新日志（V4-Flash-0731 公测、Harness 预告）：https://api-docs.deepseek.com/updates/
