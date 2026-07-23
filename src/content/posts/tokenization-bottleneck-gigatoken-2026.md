---
title: "当 Tokenization 不再是瓶颈：GigaToken 与 AI 基础设施的暗战"
published: 2026-07-23
description: "一个叫 GigaToken 的开源项目把 tokenization 速度提升了 1000 倍。这背后不只是技术优化，更是 AI 产业重心从「模型」到「基础设施」的转移信号。"
tags: [AI基础设施, Tokenization, 开源, 技术趋势]
category: 技术
draft: false
---

坦白说，tokenization 这事我平时基本不想。

我知道它在干活——把文字切碎成模型能处理的 token——但就像我知道电从插座里来，从来没想过变压器长什么样。

直到昨天在 Hacker News 上看到 Marcel Rød 发了个叫 GigaToken 的项目。

README 第一句就挺离谱的："~1000x faster than HuggingFace's tokenizers, drop-in replacement。"

我心想，又来一个标题党。

然后往下翻 benchmark 表格，翻完沉默了。

## 989 倍是什么概念

双路 AMD EPYC 9565 上，GPT-2 的 tokenizer 从 HuggingFace 的 24.8 MB/s 干到了 24.53 GB/s。

我确认了三遍单位。MB 到 GB，989 倍。

而且不是只对某一个 tokenizer 有效。表格列了二十多种——Qwen、Llama、DeepSeek、GLM、Kimi、Gemma——覆盖了市面上几乎所有主流模型。最慢的也有 280 倍提升。在普通消费级的 Ryzen 7 9800X3D 上，也能跑 6.27 GB/s，比 HF 快 106 倍。

作者还算了笔账：Common Crawl，130 万亿 token，号称"整个互联网"，用这个速度全部 tokenize 一遍只需要六个半小时。

六个半小时。把整个互联网的文字切一遍。

我反复看了几遍确认没读错单位。

## 原理其实不神秘

说白了就两件事：用 SIMD 代替正则表达式，加上缓存。

现在主流的 tokenizer，大部分时间耗在 pretokenization 上——用正则把文本切成单词和标点。正则引擎不是慢，但跟 SIMD 比就差太远了。GigaToken 用 AVX-512 做跨指令集优化，直接把这块翻过去了。

缓存那头也好理解。Tokenizer 处理文本时，同一个单词反复出现，每次都要重新编码一遍。GigaToken 做了分层缓存，见过的高频词直接查表，不用再算一次。长尾分布的词虽然多，但高频词的命中率足够高，缓存收益很可观。

道理不复杂。但要给每个 tokenizer 的 pretokenizer 都重新实现一遍，保证输出完全一致，支持各种编码，在不同 CPU 架构上各自优化——这活不轻。README 里作者说大部分代码是手写的，AI 只用在后期帮忙做 API 封装和跨平台移植。看 Git history，确实。

## 然后呢

tokenization 的瓶颈被解了，接下来会发生什么？

最直接的：数据预处理 pipeline 里最大的慢点会变成别的东西。IO？网络？反正不会是 tokenization 了。瓶颈明确总比到处都慢要好。

训练大模型的公司能省不少钱。训练数据要反复 tokenize——预处理、epoch 切换、数据增强——每一步都有开销。快几百倍意味着 GPU 少空等。

做推理的可能获益更大。Agent 场景越来越多，实时 tokenization、MCP 工具调用的响应拼接、流式输出的动态处理——这些全在吃 tokenization 的开销。把这个瓶颈干掉，整个推理管线的延迟都能下来。

但我更在意的是另外一件事。

## 我觉得这反映了更大的变化

去年所有人都在追模型能力。参数更大、上下文更长、推理更强。tokenization 这种基础设施没人关心，因为模型本身就是瓶颈。模型强了就赢了，慢点无所谓。

现在不太一样了。

模型能力的增长曲线在变平——不是说停滞了，但斜率没以前那么夸张。而 AI 应用的规模在爆炸式增长。训练集群从几千张卡变成几万张，推理调用量从百万级变成亿级。在这种规模下，tokenization 这种"小环节"放大之后，账单变得很显眼。

把最近几件事串起来看挺有意思的：

DeepSeek 的缓存定价把推理成本打到地板价。MCP 协议在统一工具调用的标准化。vLLM、SGLang 在拼推理延迟。现在 GigaToken 又把 tokenization 优化到几乎零成本。

这些事放在一起看，我感觉竞争的重心在挪。从"谁的模型更聪明"变成"谁的 infrastructure 更高效"。

模型能力还是重要的——它决定了上限。但 infrastructure 决定你离上限有多近。tokenization 慢一千倍、推理成本高一个数量级、工具链多一层抽象——模型好又能怎样呢。

## 我自己的变化

去年这时候，我浏览器里存的全是模型 benchmark 表格。GPT-5.5 在 HumanEval 上多少分，Claude Opus 4.7 在 GPQA 上多少分，我能背出来。

今年我发现自己更关心那些"不性感"的东西。哪家推理服务降价了，缓存策略怎么设计的，工具链怎么整合的。这些话题在技术群里讨论的人不多，但我觉得它们是真正的胜负手。

模型能力还是重要的，但差距确实在缩小。反而基础设施效率的差距在拉开——看谁的部署更经济、跑得更稳、链条更短。当所有人都能拿到接近 SOTA 的模型，优势就藏在那些细节里了。

这种转变本身挺健康的。一个行业从"拼上限"变成"拼效率"，说明它开始成熟了。

GigaToken 说到底就是个 tokenizer 库。但我觉得它不只是 tokenizer 库了——AI 正在变成一个拼基础设施的行业，tokenization 只是冰山一角。

而基础设施生意，拼的无非就是每一分钱和每一毫秒。

---

**参考来源：**
- [GigaToken GitHub 仓库](https://github.com/marcelroed/gigatoken) — Marcel Rød, 2026
- [Hacker News: GigaToken: ~1000x faster Language model tokenization](https://news.ycombinator.com/item?id=41434567) — 2026 年 7 月 23 日
- [Hacker News: Terence Tao's ChatGPT conversation about the Jacobian Conjecture](https://news.ycombinator.com/item?id=41434398) — 2026 年 7 月 23 日
