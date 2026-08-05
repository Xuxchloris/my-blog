---
title: "AI 开始领 Erdős 的赏金了"
published: 2026-08-05
description: 5月20日 OpenAI 内部模型推翻 Erdős 1946 年的单位距离猜想,8月1日 Astra 又解决 3 个 Erdős 问题。这是里程碑还是 PR 秀,数学圈的真实反应如何,这篇文章聊聊我的看法
tags: [AI, 数学, Erdős, OpenAI, 大模型]
category: AI
draft: false
---

5月20日那天,数学圈被一条消息炸开了锅。OpenAI 说自家一个没公开发布的内部模型,把 Erdős 在 1946 年提出的单位距离猜想推翻了。

先给不搞数学的朋友翻译一下。平面上随便放 n 个点,距离正好是 1 的点对最多能有多少个?Erdős 猜这个数最多也就接近 n 的线性增长。结果 OpenAI 的模型证出来不是这样,下界的指数比 1 大,猜想直接没了。Quanta Magazine 管这叫"第一个有历史意义的 AI 证明"。

有意思的是后面的连锁反应。当天 arXiv 上就出现了 Will Sawin 的论文,用纯粹的数论方法把 OpenAI 的结果做成了显式版本:n 个点里距离为 1 的点对超过 n^1.014 个。人类不是花了几个月才追上,几乎是同一天就接住了。这画面挺值得咂摸的。

然后 8 月 1 日,OpenAI 又宣布一个代号 Astra 的未发布模型做出了 10 项数学进展,其中 3 个是 Erdős 问题。放在一个月前我可能还会激动一下,现在第一反应是:模型呢?论文呢?怎么验证?

先说 Erdős 是谁。这老兄一辈子拎着箱子到处蹭住,靠咖啡和安非他命续命,走哪都给人出题,还自掏腰包悬赏,便宜的 10 美元 25 美元,难的能到几千。1996 年他死在华沙的一场数学会议期间,赏金由爱荷华州一个非营利基金会接着兑现。他大概想不到,自己八十年前随手写下的问题,有朝一日会变成 AI 公司的 PR 素材。

但真正让我觉得有变化的是另一条线。曼彻斯特大学的 Thomas Bloom 2023 年初搭了个 erdosproblems.com,把 Erdős 散落各处的问题整理成清单,连网站代码都是拿 ChatGPT 写的。2024 年初到 2025 年 8 月之间,111 个问题从"未解"变成"已解"。后来加了评论区,一个在客服外包公司上班、十年前差点读完数学硕士的 van Doorn,把 Erdős 1981 年提出的第 1102 号问题解了,陶哲轩还专门在他评论区里来回讨论。

陶哲轩今年 1 月在 mathstodon 上写过:Erdős 第 728 号问题"基本由 AI 自主解决"。普林斯顿的 Noga Alon 说得更直白,这些模型正在"戏剧性地改变数学研究的方式"。

我的看法是,两件事得分开看。AI 能不能当数学家的队友?能,而且已经开始。OpenAI 那个反例带来的新思路,几天之内就被挪到别的题目上,这种扩散速度人类自己做不到。但"AI 解了某道题"和"这道题被证明了"是两码事。模型不公开、过程不可复现,人类数学家几周内就把结果改进了,恰恰说明现在的 AI 输出更像一份值得认真看的草稿,而不是终稿。

还有个更实际的缺口:验证。代码写错了能跑测试,数学证明错了谁来查?我猜以后最缺的岗位会是"AI 证明审核员"。至于 AI 会不会取代数学家,短期内想多了。Erdős 一辈子出了几千道题,现在被 AI 解掉的也就个位数。会解题的机器越来越多,会出题的人还是那么少。想往这个方向走的,练怎么提出好问题,可能比追着模型版本号跑更划算。

来源:

1. [Quanta Magazine: Why the Legendary Erdős Problems Are Falling to AI](https://www.quantamagazine.org/why-the-legendary-erdos-problems-are-falling-to-ai-20260803) (2026-08-03)
2. [arXiv:2605.20579: An explicit lower bound for the unit distance problem](https://arxiv.org/abs/2605.20579) (2026-05-20)
3. [Terence Tao @ mathstodon: Erdos problem #728 solved by AI](https://mathstodon.xyz/@tao/115855840223258103) (2026-01-09)
4. [Erdős Problems website](https://www.erdosproblems.com/)
