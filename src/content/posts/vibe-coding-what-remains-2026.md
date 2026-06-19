---
title: "Vibe Coding 退潮之后，我们还剩下什么"
published: 2026-06-19
description: "从 Karpathy 的转向到开发者的回归，Vibe Coding 的故事远比想象中复杂"
tags: [vibe-coding, AI编程, 开发者, 技术思考]
category: 随笔
draft: false
---

前几天刷到一条消息：Forbes 发了篇文章，标题叫"Is Vibe Coding Dead? Even Karpathy Is Moving On"。Karpathy，就是那个最早提出 Vibe Coding 概念的人，现在自己也在往回走了。

这让我想起今年年初 HN 上那个 865 分的帖子——"After two years of vibecoding, I'm back to writing by hand"。两年 vibe coding，最后还是回到了手写代码。

## 什么是 Vibe Coding

先说说这个概念本身。2025 年初，Karpathy 发了条推，大意是：写代码的时候不看代码，只看效果。能跑就行，管它怎么实现的。他管这叫 Vibe Coding——凭感觉写代码。

这说法一出来就火了。确实，谁不想呢？告诉 AI 你要什么，它帮你写好，你点个运行，完事。省时省力，效率拉满。

我自己也试过。有几次赶 deadline，直接让 Copilot 帮我写了一堆 boilerplate，确实快。但后来 debug 的时候，我发现那些代码我完全不认识——不是说语法看不懂，是我不知道它为什么这样写，也不知道改哪里会影响哪里。

## 问题在哪

Simon Willison 今年五月写了篇文章，说了一件让他自己都"quite upsetting"的事：他发现 vibe coding 和 agentic engineering 的界限在他自己的工作中越来越模糊了。

什么是 agentic engineering？简单说就是：你是个正经工程师，用 AI 工具来提高效率，但你理解安全、可维护性、性能这些东西，你对代码质量负责。

Simon 说，以前他觉得这两种方式分得很清楚：vibe coding 是给个人小工具用的，出了问题只有自己受伤；agentic engineering 是给生产环境用的，你要为用户负责。

但现在呢？Claude Code 写个 JSON API，跑个 SQL 查询，输出个 JSON，每次都对。加测试，加文档，都挺好。他开始不逐行审查代码了。

这让他有点慌。

他的原话是："Claude Code does not have a professional reputation! It can't take accountability for what it's done."

说得挺到位的。人可以建立声誉，可以承担责任。AI 不行。它今天写对了，不代表明天也写对。而且你没法怪它——它连"怪"这个概念都没有。

## 规模化才是真正的麻烦

Olivier Wulveryck 今天发了篇文章，角度更尖锐。他说：你写一个应用，vibe coding 没问题。但你要是同时维护五十个应用呢？

他的核心观点是：每个组织都有自己的"技术标准"——不是行业通用的那种，而是你们团队内部约定俗成的那些东西。代码怎么组织，命名怎么来，错误怎么处理，哪些模式可以用哪些不行。这些东西 AI 不知道。

AI 知道的是"行业最佳实践"，是从互联网上所有开源代码里提炼出来的通用标准。这个标准本身没问题，但它不是你的。

结果就是：每让 AI 写一个新项目，它都会"重新发明"一遍你们团队已经有的东西。一个项目看不出来，五十个项目放在一起，就是一团乱麻。

Jerry Weinberg 有句话说得好：长远的好处总是被短期的好处牺牲掉。Vibe coding 就是典型的短期收益——单个项目交付快了，但系统层面的一致性被吃掉了。

## 开发者的真实感受

HN 上那些评论挺能说明问题的。

一个用户说："AI is incredibly dangerous because it can do the simple things very well, which prevents new programmers from learning the simple things." 这话有点绝对，但不无道理。AI 把简单的事做好了，新手就不学了，然后中级和高级的东西也学不会。

另一个用户的思路更务实："I have AI build self-contained, smallish tasks and I check everything it does." 让 AI 做独立的小任务，自己检查每一行。这个我比较认同。

还有人提到一个有意思的现象：以前看一个 GitHub 项目，有一百个 commit、漂亮的 README、完善的测试，你会觉得作者很用心。现在呢？半小时就能用 AI 搞出一个看起来一模一样的项目。你分不清哪个是认真写的，哪个是 vibe 出来的。

Simon 说，他现在更看重的是：这个东西有人用过没有。一个 vibe 出来的东西，如果你真的每天用了两周，那比一个刚生成的、测试完善的项目有价值得多。

## 所以呢

说实在的，我不觉得 Vibe Coding 会"死"。它会退潮，但不会消失。

有些场景它确实好用：个人小工具、原型验证、一次性脚本。这些场景下，代码质量不重要，能跑就行。Vibe coding 的核心价值就是降低门槛，让不会写代码的人也能做出能用的东西。这个价值不会消失。

但对于正经的、要维护的、给别人用的软件，vibe coding 确实不够。不是因为它写不出好代码，而是因为你不知道它写的是不是好代码。你没有判断力。

这个判断力从哪来？手写代码的经验，debug 的痛苦，维护烂代码的教训。没有什么神奇的方法。

Karpathy 的转向挺有象征意义的。他不是说 AI 写代码不好，而是说，光靠 vibe 是不够的。你得理解代码，得有工程判断力。

所以如果你问我，2026 年的开发者应该怎么用 AI？

用它，但别依赖它。让它帮你写那些你已经知道怎么写的代码。对于你不确定的部分，自己先想清楚，再让它帮你实现。保持阅读代码的习惯，不管是 AI 写的还是人写的。

Vibe coding 的退潮，某种程度上是件好事。至少它让一些人意识到：编程不只是让代码跑起来那么简单。
