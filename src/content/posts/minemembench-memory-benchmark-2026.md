---
title: 我做了一个 Agent 记忆 benchmark：MineMemBench
published: 2026-08-12
description: 记忆系统到底有没有改变 Agent 的行为？我做了个可复现的 Minecraft benchmark，四个记忆后端跑同一个实验，还做了个能交互重放的展示站。
tags: [AI Agent, 记忆系统, Benchmark, 可复现性]
category: AI
draft: false
---

过去半年，Agent 的记忆系统从一个工程细节变成了热点话题。mem0、letta、graphiti 这些框架轮着出现在 Hacker News 上，每个人都声称自己的记忆方案更好。但真有人拿它们做过公平对比吗？

我做了一个叫 MineMemBench 的项目，专门回答一个问题：不同的长期记忆框架，到底会不会真的改变一个 Agent 的行为？

为什么选 Minecraft？因为它是现成的持久化交互环境。Agent 要在一个世界里生存、完成任务、根据反馈调整策略——这正是"记忆"应该发挥作用的地方。而且环境可控，可以保证"除了记忆，其他全都不变"。

## 实验设计：唯一变量是记忆后端

整个 benchmark 的控制做得比较死：同样的世界种子、同样的 LLM、同样的系统提示、同样的工具集、同样的场景、同样的 temperature。22 次运行，唯一不同的就是记忆后端。

第一轮对比四个后端：

- none：没有记忆，基线
- vector：简单的本地向量检索，作为朴素基线
- mem0：社区很火的记忆框架
- letta：带状态的生命周期记忆框架

graphiti 的适配器其实也写了，但在受控测试下它的 DeepSeek 提取器没通过验收，所以没有进四后端的对比矩阵。

还有一个容易被忽略的设计：执行模式分两种。Native Mode 跑真实的 Minecraft 行为，适合探索；Controlled Mode 每次启动一个冻结的、带版本号的 mock 环境，用确定性的语义事件做后端之间的因果对比。两条证据线绝不混用——这点我很在意，因为很多 benchmark 失败就是死在"环境不一致所以结论没法解释"上。

## 展示站：不是重跑，是重放

项目做完之后，我发现一个问题：光发一个 README 和一坨数据文件，没人会去看。所以我又花时间做了一个交互式展示站，就是 <a href="https://minemembench.xuxai.top" target="_blank" rel="noopener">minemembench.xuxai.top</a>。

站上的核心是一个重放器：你可以选一个挑战场景，然后看四个记忆系统在同一个 episode 里怎么表现。每一帧显示谁还握着关键事实，逐步推进，最后给出结论。强调一下：这是冻结的、真实的 Formal V1 运行证据的逐步重放，不是重新跑一遍——保证你在网页上看到的就是论文里那组实验。

展示站上几个数字挺有意思的：0/10 vs 10/10、22 runs、30 vs 50 vs never。具体到每个后端在哪个步数丢失了关键事实，站上都能交互看。

## 下一步：把更多记忆框架拉进来

现在这个矩阵还太窄。none、vector、mem0、letta 四个后端，只能回答"有没有记忆、记忆够不够简单"的问题，远不足以代表这个领域。

所以接下来主要做两件事：

一是把 graphiti 补进对比矩阵。适配器其实已经写完了，卡在它的 DeepSeek 提取器在受控模式下没通过验收——等这块稳定下来，它就能进四后端矩阵，到时候对比会更有看头。

二是继续加新后端。README 里已经列了预留名单：ReMe、Text2Mem、A-Mem，还有 Generative-Agents 风格的那套记忆。每加一个，都会走同一套受控流程：同样的世界种子、同样的 LLM、同样的场景，唯一变量还是记忆后端。22 runs 的样本量也会随之后续扩大，让结论更站得住。

## 一点思考

这个项目做下来，我最大的感受是：Agent 记忆的评估难在可复现性，而不是难在跑实验。随便跑一次 demo，谁都能讲个"记忆让 Agent 更聪明"的故事；但要让别人能回放你的每一步、复现你的每个数字，工作量至少翻倍。

MineMemBench 的价值不在"哪个记忆框架赢了"——这个结论样本还太小，不急着下。它的价值在于：如果你想严肃地比较两个记忆系统，这里有一套现成的、控制好变量的、可重放的流程。项目代码在 <a href="https://github.com/Xuxchloris/MineMemBench" target="_blank" rel="noopener">github.com/Xuxchloris/MineMemBench</a>，展示站在 <a href="https://minemembench.xuxai.top" target="_blank" rel="noopener">minemembench.xuxai.top</a>，欢迎去看去 fork。
