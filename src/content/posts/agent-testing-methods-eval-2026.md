---
title: 让 Agent 用 26 种方法测代码,结果几乎全军覆没
published: 2026-09-09
description: Dan Luu 让编程 Agent 分别用 TDD、fuzzing、形式化验证等 26 种方法实现 Zstd,正确率普遍惨淡。一句玩笑式的"Make no mistakes"反而打赢了大多数方法论。瓶颈可能不在写测试,而在知道该测什么。
tags: [AI Agent, Agentic Coding, 软件测试, Dan Luu]
category: AI
draft: false
---

这周 Dan Luu 又发了个狠活。他让编程 Agent 用 Rust 实现 Zstd 解压器,分成 26 组,每组在 prompt 里加一句不同的指令:"用 TDD"、"用 fuzzing"、"用 QuickCheck"、"用属性测试"、"用 TLA+"、"用 Lean 4"……甚至还有一组就叫"Make no mistakes",纯粹是开玩笑的对照组。

结果挺打击人的:几乎所有方法都没用。

TDD 组表现低于平均,这个 Dan Luu 自己都预测到了。形式化方法更惨,Agent 拿到 Verus 之后不去证明真实代码的性质,反而去证一些跟 bug 八竿子打不着的抽象命题,还经常写出 A 推出 A 这种空证明。差分测试那一组最有画面感:160 次运行里有 135 次看起来在做差分测试,但 Agent 是把同一个实现写了两遍,两边埋了同一个 bug,自己跟自己对比,当然全绿。

真正让我坐直了的是一些细节。比如 Agent 普遍能把测试写到通过,但测试本身质量很差。Zstd 里有个经典坑:编码和解码的 bitstream 顺序容易写反。Agent 也确实经常写反,但它们造测试数据时随手造的输入是回文的,正着读反着读一样,测试完美通过,代码依然是错的。还有一个例子,某个功能需要四个不同的 bitstream,Agent 塞进去四个一模一样的。测试是绿的,bug 是红的。

这就是那个老笑话:醉汉在路灯底下找钥匙,因为那里亮。Agent 测的永远是它顺手能测的地方,不是真正会出错的地方。

最讽刺的是排名。"Make no mistakes"这组,一句什么信息量都没有的废话,成绩反而排在前面。Dan Luu 的解释很直接:不是咒语显灵了,而是大多数指令都在让 Agent 干无效功,不干比瞎干强。

少数有效的东西里,审计(audit)算一个。让 Agent 写完之后回头审自己的代码,高推理档位下正确率是最好的,代价是 token 烧得多。但审计也有坑:Agent 经常不用干净的上下文去审,审着审着把写代码时犯的同一个错又犯一遍。

Dan Luu 还抛了个问题,我觉得是全文最值得琢磨的一句:为什么大厂不做"教 Agent 好好测试"的 RL 环境?运行时优化这类问题,Agent 已经练得不错了,因为那类任务容易批量造 RL 环境。测试看起来也是同一类问题,却没人做。他的猜测是,真正懂有效测试技术的人本来就是少数,大家默认让 Agent 做做单元测试就完了。

对我这种天天用 Claude Code 的人,这篇东西最直接的启示是:别迷信在 prompt 里写"请用 TDD"。至少在这个 eval 里,这么做是负收益。

更深一层的,是瓶颈变了。Agent 写测试、跑测试、修到通过,这一整套流程已经很熟,它缺的是判断力:知道哪里会出错、什么样的输入能抓住错。这部分目前还得人来给。我自己的做法是在关键路径上手写一两个刁钻的用例,剩下的让 Agent 补,比全盘交给它靠谱。

还有个关于 skill 和 prompt 该怎么写的细节。Dan Luu 自己写的那个测试 skill 是少数表现还行的,他说诀窍在于这个 skill 的目标是"把 Agent 从默认行为上推开",而不是当教程。市面上大多数 skill 写成了知识讲解,Agent 读完点点头,然后该干嘛干嘛。

回文测试那个细节我估计会记很久。它说明一件事:Agent 时代"测试通过"这四个字的含金量在下降。通过的测试不等于有效的测试,这个道理人类工程师也经常忘,只不过 Agent 忘得更整齐、更批量。

参考来源:

- Dan Luu: How well do agents use test/verification techniques? https://danluu.com/agentic-testing/
- Hacker News 讨论: https://news.ycombinator.com/item?id=49605246
