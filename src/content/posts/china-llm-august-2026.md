---
title: 国产大模型的八月:霸榜,涨价,还有一次急刹车
published: 2026-08-27
description: 2026年8月国产大模型密集发布并霸榜OpenRouter,却同时集体涨价,OpenAI还踩了一脚安全刹车.聊聊这一个月发生了什么,以及我的几点看法.
tags: [AI, LLM, open-source]
category: AI
draft: false
---

这个八月，大模型圈子的新闻密度高得离谱。单点的事大家应该都刷到过，我干脆把几条线串起来聊聊，顺便说点我的看法。

## 发布像下饺子

先捋一下时间线。7月16日，WAIC 开幕前夕，月之暗面甩出 Kimi K3，2.8 万亿参数，全球最大的开源模型，完整权重 7 月 27 日开放。8 月 3 日，阿里发布 Qwen3.8-Max，2.4 万亿参数的 MoE，激活参数约 950 亿，还宣布这是 Max 级旗舰第一次开源权重；同一天 MiniMax 开源了 H3，33B 的全模态模型，能生成带原生立体声的 2K 视频。中间还夹着 DeepSeek V4-Flash 正式版上线、智谱 GLM-5.2 这些。21 世纪经济报道把这五款统称"八周五模型"，天聊博客数了数，光 8 月这 20 天就密集发布了 11 款新模型。

一周一个旗舰，参数一个比一个大，这种节奏放在两年前不敢想。

## 比发布更猛的，是调用量

发布归发布，真正让我意外的是使用量。OpenRouter 7 月 27 日更新的数据里，调用量前五全是中国的模型：小米 MiMo-V2.5 以单周 10.5 万亿 token 登顶，月调用量 31.2 万亿，后面跟着 DeepSeek V4-Flash、腾讯混元 3、智谱 GLM-5.2 和 DeepSeek V4-Pro。有媒体统计说，"包揽前五"这个状态已经连续 14 周了。

这不是什么榜单刷出来的。OpenRouter 上全是开发者在真金白银调 API，调用量就是拿脚投票。前几年大家还在争论国产模型"能不能打"，现在的问题是"为什么这么能打"——答案无非是便宜、开源、能力跟得上。

## 然后，集体涨价了

就在霸榜的同时，8 月国产模型集体调价。智谱先动手，接着 DeepSeek 也涨了，有说法是旗舰输出价涨了 350%，8 月 18 日新价格机制生效。网上骂声一片，"价格屠夫"人设塌了。

我倒觉得这事没那么阴谋。推理成本是实打实的，尤其是 Agent 场景，一次任务烧掉的 token 是普通对话的几十倍。用量涨到某个量级，白菜价必然撑不住。涨价这件事本身，说明真的有人在高强度使用——没人用的东西是不需要涨价的。

## 竞争维度变了

这轮发布里，最值得关注的不是参数，是"能不能把活干完"。Kimi K3 的官方演示是 48 小时自主跑完一颗 4 平方毫米芯片的完整设计流程；Qwen3.8-Max 的宣传语是"可自主编程十数天交付完整项目"。不管宣传有多少水分，方向是明确的：厂商开始比长周期任务的可靠性，而不是单次对话的聪明程度。对开发者来说，选型的核心指标已经变了，从"哪个模型聊天厉害"变成"哪个模型能稳定把任务闭环"。

## 一边踩油门，一边踩刹车

这一个月还有两条对照着看的新闻。8 月初，OpenAI 罕见地暂停了 Astra 的部分开发，据说是内部评估发现它可能具备发现并利用零日漏洞的能力，连强化学习训练都停了两周。另一边，字节跳动被曝在训练一个最高 10 万亿参数的大模型，规模大概是 Kimi K3 的三倍多，张一鸣和梁汝波都出来表了态。

一边因为安全风险急刹车，一边在参数上继续狂飙。这个画面挺魔幻，也挺真实——AI 的能力增长和它的风险是同一件事的两面。

## 说点我的看法

几件事，纯个人观点。

别被"参数海报"带节奏。2.4 万亿还是 2.8 万亿，跟你的月底账单没关系，有关系的是激活参数、上下文长度和单位任务成本。选型先算账。

"免费午餐"阶段结束了。开源和低价帮国产模型抢到了开发者，但涨价是迟早的事。现在做技术选型，成本模型得按涨价后的价格算。

多模态开源值得单独说。MiniMax H3 这种 33B 就能本地跑的全模态模型，才是真正"属于你"的模型。云端旗舰再强，数据不出域的需求摆在那，本地能跑的模型会越来越重要。

最后，Astra 不是孤例。能力越强，安全红线越近。以后"某个前沿模型因为太危险被叫停"的新闻只会更多，这不是坏事，但别假装看不见。

这一个月的大模型新闻，大概能写十篇，这篇先到这。下个月如果还有新瓜，我继续。

## 参考来源

- [CNMO科技：月之暗面发布全球最大开源模型 Kimi K3，参数规模 2.8 万亿（2026-07-17）](https://www.sohu.com/a/1051289522_115831)
- [千问 AI 平台：Qwen3.8-Max 模型页（2.4 万亿 MoE、1M 上下文、定价）](https://www.qianwenai.com/models/qwen3.8-max)
- [阿里云开发者社区：2026 年 8 月大模型的三重跃迁（2026-08-04）](https://developer.aliyun.com/article/1753092)
- [CSDN：中国大模型"八周五连发"：开源与低成本重写全球选型（2026-08-10，引 21 世纪经济报道、第一财经）](https://blog.csdn.net/m0_74023007/article/details/163505655)
- [天聊博客：2026 年 8 月 AI 大模型井喷：11 款新模型 20 天密集发布深度复盘（2026-08-23）](https://www.tianliaos.com/post/ai-model-explosion-august-2026-review)
- [新浪新闻：国产大模型包揽 OpenRouter 调用量前五，小米 MiMo-V2.5 登顶（2026-08-03）](https://www.so.com/link?m=z0wnTQSrVgANB7qlV9xmDD78WrRZXNtBvG3WQL9Fqm2lXmQ06XT5vMP0%2F880pk1mPqFuQ90SDpCRhoGA6L4uFdvzXLH%2BtGi8WMfElQuo2wMasy4GI5abyVLo)
- [雪球：国产大模型集体涨价，DeepSeek 旗舰输出价涨 350%（2026-08-18）](https://www.so.com/link?m=wp2itBRN0SRmZ5Q3BIBjqQr4wV7fQYRBI3fGopIKPaiZebw%2BoOqXbg93wegcQTsFHs2Cic0tYpfdqq1DKI0Iy%2Fhj9nnBHZcSP5pKsdI7%2Fud46k1VasriyM)
- [网易订阅：OpenAI 暂停部分 Astra 模型开发，或具备发现并利用零日漏洞能力（2026-08-08）](https://www.so.com/link?m=wrqCj0aA9MLYD6MNn2kKBWP71RrPJzYslcSC7BUWXFTyCtZJC7jbvz8oGJ5dyygGSSa39J9ftNmUe3EQho%2FyNp4G%2BtXn9A2TE%2BTaMsIlS21oGEXkxI%2FO)
- [腾讯新闻：字节跳动被曝训练 10 万亿参数大模型（2026-08-07）](https://www.so.com/link?m=wAa07J95E3GNL2KS%2F14NBt6E%2F9HhONMCdGLA2IzcAkpiQAEPpT9AT2Ff1RhPKlf8VcJrxRo%2BEW%2Bj6JmWpFj%2BAwEfA9mCf8EHi%2Fg3RvLqcwJWAZOK)
