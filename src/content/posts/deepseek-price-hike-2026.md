---
title: DeepSeek 宣布大幅涨价, 便宜的时代要结束了?
published: 2026-08-08
description: 8 月 6 日 DeepSeek 突然宣布 API 价格将大幅上调, 没有数字没有日期. 刚打完价格战就涨价, 这篇文章聊聊我看到的几个原因, 以及真正在变的东西.
tags: [DeepSeek, 大模型, AI, 商业模式]
category: AI
draft: false
---

前几天刚写完 OpenAI 降价 80%、DeepSeek 加量不加价，结果 8 月 6 日 DeepSeek 就在官网贴了条通知：API 价格要上调，"涨幅会比较大"，具体方案之后公布。没有数字，没有生效日期，就一句话。Bloomberg、SCMP、The Next Web 都报了，标题里全是 significant。

放在今年看，这事有点魔幻。7 月 21 日 VentureBeat 还在报道 DeepSeek 降价 75%，半个多月，风向就反了。

先看看现在便宜到什么程度。V4 Flash 的价格：输入 $0.14/百万 token，输出 $0.28，缓存命中价 $0.003，在 Artificial Analysis 收录的 101 个模型里缓存价格排第一，上下文 1M。换算成人民币就是输入 1 块、输出 2 块。这个价位跑 Agent 任务，一次任务调几十次模型，成本基本可以忽略。前几天那篇里写过爱范儿拿它干五件事、烧了三千万 token 只花 2.85 元。"便宜"两个字，就是这次涨价公告的背景板。

更尴尬的是，涨价公告前一周，V4 Flash 0731 刚官宣进入公开测试，能力还涨了一截。Artificial Analysis 的智能指数它排第 3，52 分，中位数才 26；ARC-AGI-2 半私有集上 max effort 拿到 61.4%，每个任务成本只要 4 美分。还有开发者分享，304B 的模型一张 AMD MI300X 就能跑起来，单流 168 token/s，64 路并发还能扛住 830 token/s。能力贴脸、价格贴地，这本身就是不可持续的。所以涨价，我一点不意外。

意外的是时机。为什么偏偏是现在？

我排了四个可能的原因。

一是成本真的压不住了。推理需求涨太快，GPU 还是紧的。之前预告的峰谷定价其实就是信号：高峰时段算力挤不动，说明便宜额度被大量不赚钱的流量吃掉了。

二是价格本身就是筛选器。$0.003 的缓存命中价，长上下文批量任务几乎免费，吸引来的不止开发者，还有爬虫、刷量、套壳的。这些人不产生收入，只产生负载。

三是期望管理。先放风再出方案，给市场留个心理准备期，免得正式调价那天炸锅。而且这个动作本身就是免费营销。你看，连我都在写它。

四是竞争维度变了，这条我觉得最根本。以前开源模型拼"接近闭源"，现在 Qwen3.8 Max 在 agentic index 上登顶，开源模型已经能跟闭源正面掰手腕。当便宜不再是差异化优势，价格战就打不下去了，该转向按价值定价。官方更新日志里还写着 V4-Pro 正式版很快发布，涨价公告卡在 Pro 前头，很难说是巧合。

作为天天调 API 的人，我不反对涨价，前提是别涨太狠。把地板价拉回正常价，行业反而健康。价格长期失真，基于 API 的商业模式全是泡沫，人人都在赌补贴能撑多久。我真正盯着两个信号：官方方案出来前，缓存价格和免费额度哪个先动；第三方平台会不会趁机抢客户。反正后路一直在，304B 的模型一张 MI300X 就能本地跑，虽然那卡不是普通人买得起的，但至少说明"贵"是有上限的。

半年里所有人都在说模型会越来越便宜，结果第一个喊涨价的，恰恰是当初把价格打到地板的人。我倒不觉得这是坏事。AI 开始算自己的账了，总比所有人一起烧钱、等对手先死要好。

## 信息来源

- DeepSeek API 更新日志：https://api-docs.deepseek.com/updates/
- Artificial Analysis 模型页：https://artificialanalysis.ai/models/deepseek-v4-flash
- ARC Prize 结果页：https://arcprize.org/results/deepseek-v4-flash-0731
- Bloomberg《DeepSeek Plans 'Significant' Price Increase for Its AI Services》：https://www.bloomberg.com/news/articles/2026-08-06/deepseek-plans-significant-price-increase-for-its-ai-services
- SCMP《DeepSeek signals 'significant' price hike, testing its low-cost edge》：https://www.scmp.com/tech/tech-trends/article/3363129/deepseek-signals-significant-price-hike-amid-surge-demand-low-cost
- The Next Web《DeepSeek warns of a 'significant' price rise》：https://thenextweb.com/news/deepseek-significant-api-price-increase
- VentureBeat《DeepSeek cut prices 75%. The 100x problem remains》：https://venturebeat.com/orchestration/deepseek-cut-prices-75-the-100x-problem-remains
- 单卡 MI300X 部署配置：https://github.com/ryanzhou/deepseek-v4-flash-mi300x
- Chuanxilu 对涨价动机的分析：https://blog.chuanxilu.net/en/posts/2026/08/deepseek-price-increase-beyond-gpu/
