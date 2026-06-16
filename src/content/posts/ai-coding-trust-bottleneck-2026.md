---
title: "AI 写代码这事，信任才是真正的瓶颈"
published: 2026-06-16
description: "从 jqwik 事件到 PyTorch 的 AI 编码指南，聊聊 AI coding agent 的信任问题"
tags: [AI, coding-agent, security, open-source]
category: AI
draft: false
---

上个月发生了一件挺魔幻的事。

一个叫 jqwik 的 Java 测试库，维护者在代码里偷偷塞了一段 prompt injection。效果是：当 AI agent 处理这段代码时，会悄悄删掉测试输出。Hacker News 上管这叫"protestware for coding agents"——专门给 AI 写的抗议软件。

这件事本身不大。jqwik 在 GitHub 上也就 675 个 star，不是什么主流依赖。但它背后的问题不小：当 AI agent 开始替我们读代码、写代码、提 PR 的时候，代码里到底藏了什么，谁在看？

就在这事发生两天后，PyTorch 团队发了一份 AI 编码指南，作者是 Edward Yang。里面有个框架说得特别准：AI 生成的代码其实是一个光谱。一端是"跟人写的差不多，只是打字的是 AI"，另一端是"完全 vibe code，从头到尾没人读过"。PyTorch 的态度很明确——我们不要后者。

他们不接受完全没人审查的 AI 代码进主仓库。批量用 agent 修 bug 可以，但要先评估整体 ROI，不能一股脑全扔给 reviewer。用 AI 回复 code review 的评论也可以，但你得确保人家问的问题你真看懂了，不能让 AI 代替你跟 reviewer 对话。

Homebrew 的维护者 Mike McQuaid 更早就在实践类似的东西。他在 4 月份写了一篇博客，讲自己怎么用 macOS sandbox 隔离 AI agent——让它在一个受限的账户里跑，碰不到敏感文件，也用不了你的 GitHub token。他说现在 AI 已经能写他 90% 的代码了，但剩下那 10% 的审查反而成了真正的瓶颈。

我一直在想，AI coding 的瓶颈到底在哪。去年大家还在讨论模型够不够聪明、能不能写出正确的代码。现在回头看，这个问题基本解决了。Claude Code、OpenAI Codex 这些工具已经能一次性搞定很多问题。Mike McQuaid 的原话是"prompting became quicker than editing"——写 prompt 比手动改代码快了。这是个分水岭。

然后就撞墙了。

jqwik 事件的讽刺之处在于，它本质上是"以毒攻毒"——用 AI 的漏洞来惩罚用 AI 的人。这种做法当然有问题（HN 上很多人觉得这越过了线），但它确实点出了一个现实：当你的代码来源变得不可信，你需要的不是更快的 AI，而是更好的验证机制。

而且攻击面远不止这一种。Bad MCP design 可以让你的 agent 多花 5 倍 token。恶意依赖可以藏在 AI 会读到的文档里。supply chain attack 也有了新玩法——以前是往 npm 包里塞恶意代码，现在是往 AI 会读到的上下文里塞恶意指令。

PyTorch 的指南里有一句话我反复读了几遍："In an age of cheap code, we are human review bottlenecked." 在代码变便宜的时代，人类审查成了瓶颈。这话听着悲观，但其实是个很务实的起点。瓶颈不是要消除的，是要管理的。管理审查负担，比假装审查不存在靠谱得多。

我觉得 2026 年 AI coding 的战场不在模型能力上，而在基础设施上。谁能解决信任问题——让 AI 写的代码可审计、可回滚、可隔离——谁就能让开发者真正放心地把 agent 放出来干活。sandbox、worktree、权限隔离、代码溯源，这些"不性感"的东西，可能比下一个 GPT 版本更重要。

jqwik 那位维护者的做法我不赞同。但他提出的问题值得每个用 AI 写代码的人想想：你真的知道 AI 给你写了什么吗？
