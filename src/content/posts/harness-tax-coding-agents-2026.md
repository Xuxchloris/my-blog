---
title: "你的 Claude 模型,可能根本不需要 Claude Code"
published: 2026-09-17
description: "伯克利团队测了 21 组模型和 harness 的搭配,发现同一个模型换个壳子跑,成功率几乎不变,成本能差两倍。这笔账他们管它叫 Harness Tax。"
tags: [coding-agent, Claude Code, HarnessTax, AI工具]
category: AI
draft: false
---

昨天伯克利的 Melissa Pan 团队（合作者里有 Ion Stoica 和 Matei Zaharia）发了个研究，叫 HarnessTax，直接冲上了 HN 前排。结论一句话就能说完：你选 coding agent 的时候，模型和外面那层壳（harness）是两个独立的选择，而大多数人从来没意识到自己在为壳子单独付钱。

## 他们测了什么

先解释下 harness。Claude Code、Codex CLI 这类工具，本质是包在模型外面的调度系统，替模型管上下文、管工具调用，再按循环把任务推下去。模型是发动机，harness 是整车。

他们挑了 7 个模型、3 个 harness（Claude Code、Codex CLI，加一个极简的开源项目 Pi），两两组合出 21 对，在 SWE-bench Lite 和 Terminal-Bench 2.0 上各跑 30 个任务，每个任务重复三次。

结果里最扎眼的一组数字：同一个 Claude Fable 5，在 Claude Code 里成功率 97.8%，在 Pi 里 96.7%，差一个百分点。但成本呢？每次尝试 $1.33 对 $0.67，整整两倍。

钱花哪了？他们查了每次任务的第一轮调用：所有 7 个模型下，Claude Code 的初始上下文平均是 Pi 的 10 倍以上。Pi 只给模型四个工具：read、write、edit、bash，完事。Claude Code 塞进去的指令和工具 schema 要大得多。有意思的是，两者完成任务用的轮数几乎一样（15.3 对 15.4），也就是说不是多干了活，是每轮都背着更重的包袱在跑。

## 第三个发现更有意思

按常理，厂商自己优化的搭配应该是最优的，毕竟 OpenAI 官方就说 GPT-5-Codex 是“为 Codex 里的软件工程优化过的”。

但数据不这么认为。在 Anthropic 和 OpenAI 的 6 个模型、两个 benchmark、共 12 组对比里，有 9 组的最高成功率来自“别家的 harness”。比如 Sonnet 4.6，在 Codex CLI 里跑 SWE-bench Lite 是 68.9%，在自家 Claude Code 里反而只有 66.7%。GPT-5.6 Sol 在 Terminal-Bench 2.0 上，Pi 里 83.3%，Codex 里 78.9%，成本还便宜一半（$0.42 对 $0.76）。

模型的能力是可以带走的。厂商联调的红利，比宣传的小。

## HN 上的反驳，我觉得有一半道理

这个研究发出来后，HN 评论里有个叫 jswelker 的用户泼了盆冷水：Claude Code 那些“多余的重量”，很多是花在安全和对齐上的。Pi 为了快和简单，把护栏和沙箱全砍了，拿这个对比成本，等于把安全当成可以随便扔的负外部性。他打了个比方：“为什么要交垃圾处理税？倒进海里是免费的。”

这个反驳站得住脚吗？一半一半。确实有人回复说，Pi 可以用容器包一层沙箱，几乎不增加 token 开销，所以“安全必然贵”不成立。但反过来说，普通用户有几个会自己去搭容器隔离？大厂 harness 的溢价里，有一部分买的是“默认安全”，这对大多数人是真价值，不能简单叫税。

我自己的看法是：这笔“税”的真实成分取决于你是谁。会折腾的人，Pi 加个容器就是性价比之王；不想折腾的人，Claude Code 贵的那一倍里，买的是省心和兜底。问题在于厂商从来没把这层账摊开算给你看，默认搭配就是唯一选项。

## 壳子会越来越薄

HN 上有条评论我觉得说到点子上了：“As the model gets smarter, you need to tell it less.” 模型越强，harness 里那些手把手的指令、防呆设计、复杂工具链就越多余。研究团队自己也在文末承认，日常任务里 coding agent 越来越像“模型智能的接口”，真正需要重 harness 的，是那些贴着模型能力上限的硬问题。

所以对 Anthropic 们来说，这研究其实是个不太舒服的信号：harness 的护城河正在被模型本身的进步抽干。当然，SWE-bench 这类开源 benchmark 模型训练时可能见过，结论能不能推广到真实工作流还得打个问号，作者自己也承认了这点。

不过话说回来，下次有人问你“用什么 coding agent”，这个问题本身就问窄了。模型是一个选择，壳是另一个选择，价钱还是两笔。

---

**信息来源：**

- [HarnessTax: How Much Does the Harness Matter for Coding Agents?](https://harnesstax.github.io/)（Pan et al., UC Berkeley, 2026-09-16）
- [Hacker News 讨论帖](https://news.ycombinator.com/item?id=49733726)
- [Pi coding agent（GitHub）](https://github.com/earendil-works/pi)
