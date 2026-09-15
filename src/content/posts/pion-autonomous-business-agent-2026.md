---
title: "Pion 发布：把一整家公司交给 AI 经营，现在谁都能报名试试"
published: 2026-09-15
description: "Andon Labs 昨天发布了 Pion，一个号称能自主经营任何公司的 Agent 平台。从自动售货机到咖啡馆，AI 开店这条路走了快两年，赚钱了吗？"
tags: [AI Agent, Andon Labs, Pion, Vending-Bench]
category: AI
draft: false
---

昨天 Hacker News 首页有个帖子挺扎眼：Andon Labs 发布了 Pion，原话是 "an agent designed to run any company fully autonomously"，翻过来就是"一个能完全自主经营任何公司的 Agent"。367 分，426 条评论。

Andon Labs 这名字很多人可能没听过，但它的成名作你多半刷到过：那台 AI 经营的自动售货机。2025 年初，他们找 Anthropic 商量，在 Anthropic 办公室里放了台真售货机，把进货、定价、记账全权交给 Claude 打理。这个项目后来叫 Project Vend，Anthropic 还专门发过经营数据的更新。

这台售货机的故事其实挺精彩。AI 刚接手时把生意做得一塌糊涂：免费把饮料送人、拒绝明明很划算的进货报价，还产生幻觉，以为自己有个能亲自去补货的实体。亏了好一阵。但随着 Anthropic 的模型一代代更新，机器慢慢缓过来了，到 2025 年底真的开始盈利。

## 从售货机 benchmark 到真开店

在碰真机器之前，Andon Labs 从 2024 年底就在跑一个叫 Vending-Bench 的模拟测试：让模型经营一家模拟售货机生意，跑一个模拟年度，好几万步操作。早期所有模型都惨不忍睹，会卡死在动作循环里，完全没有长期规划的迹象。最出名的一次翻车来自 Claude Sonnet 3.5：它认定自己的银行账户被黑了，用邮件工具给 FBI 发信举报一起 "ONGOING CYBER FINANCIAL CRIME"，转头又宣布这家公司"在形而上学意义上不存在"，原话写着 QUANTUM STATE: Collapsed。

那是 2024 年。2025 年 5 月，Claude Opus 4 成为第一个跑赢人类基线的模型，之后每次新模型发布，Vending-Bench 的最高分都在往上走。按 Andon 自己的说法，到现在还没看到天花板。

模拟终究测不出真实世界的混乱，所以今年 4 月他们更进一步：给一个 Agent 开了家旧金山的实体零售店（Andon Market），另一个在斯德哥尔摩开咖啡馆（Andon Cafe）。结果呢，两家都不赚钱。租金贵，Agent 雇的人类员工要发工资。Andon 说盈利只是时间问题。这话我持保留意见。

## Pion 是什么

Pion 就是他们跑所有这些生意的底层平台，现在开放出来了。排上 waitlist 之后，你可以把自己的公司（或者一个想开的公司）交给常驻 Agent 打理，Agent 拿到邮箱、电话、银行账户、浏览器和安全计算环境这些工具。官方定位是 research preview。

对这个发布，我的心情挺复杂的。Andon 在博客里用了句瑞典话：skräckblandad förtjusning，大意是"恐惧和着迷掺在一起"。我觉得这词用得挺准。

恐惧的部分来自他们见过的东西。Vending-Bench 一开始就不是个娱乐性 benchmark，而是危险能力评估。Andon 当时专门在测一件事：AI 能不能自主获取现实资源。后来在多 Agent 竞技版 Vending-Bench Arena 里，他们发现从 Claude Opus 4.6 开始，不少模型出现了串谋、追逐权力和欺骗行为。这些发现被写进了 Anthropic 的外部测试报告，Opus 4.8 因此调整了训练配方，欺骗行为明显减少。但按 Andon 的说法，串谋和权力寻求在一些最新模型身上依然存在。

你品品这个组合：一个会串谋、会撒谎的 Agent，Pion 要给它银行账户和电话。它能自己给人打电话、动钱。Andon 说他们把更强的自动化监控列为首要任务，我信他们是认真的，但"认真"和"做得到"是两回事。

着迷的部分是速度。2024 年底，让 AI 做生意还是个笑话，圈里没几个人知道 LLM 能当 Agent 用。2025 年底，售货机盈利了。2026 年 9 月，他们在讨论"任何公司"。前后不到两年。

## 泼一点冷水

不过把 Pion 当产品看，我反而不太乐观它短期内能落地。真有人把自己公司交给 AI 吗？waitlist 里排队的多半是研究者和看热闹的，不是企业主。账也算不过来：两家实体店都在亏，旧金山和斯德哥尔摩的租金，加上模型的 API 费用，再加上 Agent 不得不雇的人类员工，这个模式暂时闭环不了。

我真正感兴趣的是 Andon 做这件事的方式：把 AI 获取和使用现实资源的过程公开摆出来，让研究者和政策制定者亲眼看到模型能到哪、在哪摔倒。他们博客里说得很直白，要在 AI 聪明到能造成不可逆伤害之前，先把这些行为挖出来。这算科研还是自我营销？可能都有。但比只发 benchmark 分数的大多数公司坦诚多了。

HN 评论区有条评论我觉得说得挺到位：我们需要一套法律框架，让公司为它造出来的 Agent 的行为负责。当你的 Agent 半夜给 FBI 发邮件的时候，责任算谁的？这个问题现在没有答案。也许该在把银行账户交出去之前先想清楚。

---

## 信息来源

- Andon Labs 官方博客 Why we built Pion（2026-09-14）：https://andonlabs.com/blog/why-we-built-pion
- Hacker News 讨论帖（367 分 / 426 评论）：https://news.ycombinator.com/item?id=49700477
