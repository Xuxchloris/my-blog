---
title: 中国开源AI模型正在改写游戏规则
published: 2026-07-21
description: Kimi K3 刚上线就爆满到停止注册，Qwen3.8 Max 让阿里股价大涨——中国开源AI模型正以碾压级的性价比冲击全球市场
tags: [AI, 开源模型, Kimi, Qwen, 大模型]
category: AI
draft: false
---

# 中国开源AI模型正在改写游戏规则

先说两件事。

第一件：昨天，Kimi K3 因为需求太火爆，直接暂停了新用户注册。一个AI模型，刚上线就被用户挤爆了。这种场景以前只在ChatGPT身上见过。

第二件：上周阿里巴巴发布的 Qwen3.8 Max，Bloomberg 报道后阿里股价直接涨了5.4%。一家电商公司，因为发了个AI模型股价大涨。

两件事放在一起看，不是巧合。

## 从Kimi K2.6说起

今年四月，有个叫 ThinkPol 的博主搞了个AI编程比赛。Word Gem Puzzle，一个拼字游戏。十个主流模型同场竞技，客观评分。

结果让很多人跌破眼镜。

Kimi K2.6，一个来自中国创业公司 Moonshot AI 的开源权重模型，拿了第一：22分，7胜1负0平。第二名是小米的 MiMo V2-Pro。GPT-5.5 排第三。Claude Opus 4.7 只排到第五。所有西方主流模型，没有一个进前二。

这场比赛不是什么冷门小众测试。它比的是真实的编程能力：模型要写出能连接游戏服务器、实时做决策的代码。NVIDIA 的 Nemotron Super 3 甚至因为代码有语法错误，连服务器都没连上。

Kimi K2.6 是开源的。任何人都可以下载权重，自己部署。一个中文开源模型，在编程上打败了 OpenAI 和 Anthropic 的旗舰产品。

这不是孤例。六月智谱AI 的 GLM-5.2，Business Insider 说让硅谷都注意到了。Google 四月份紧急发布 Gemma 4 来应对中国开源模型的冲击。

## 为什么是现在？

Ben Thompson 在 Stratechery 上最新的文章（昨天发的）分析得很透彻。

他说了一个关键点：很多人以为开源模型等于"免费"，但忽略了推理成本。Kimi K3 的价格是每百万输入token 3美元，输出15美元。Sol（看起来是 OpenAI 的下一个模型）是5美元输入、30美元输出。确实贵了一倍，但差距没有很多人想象中那么大。

更关键的是，Kimi 在做推理时需要生成更多 token。Ben 的原话：Kimi 用显著更多的 token 才能到达正确答案，所以它的单位 token 价格优势可能被稀释了。

那为什么大家还这么兴奋？

因为边际成本在变化。

前几年做 AI 的核心成本是训练。你花几十亿美元训练一个模型，然后靠推理收入收回成本。但现在推理市场正在爆炸式增长，规模大到可以摊薄固定成本。同时，Agent 范式的解锁让推理需求变得更大了。一个 Agent 跑一个任务可能就要生成几百万个 token。

在这种背景下，开源权重的意义不在于"免费"，而在于你可以把模型部署在任何地方，不受API限制，不被供应商锁定。

## 美国的焦虑是真实的

昨天 Ben Werdmuller 也写了一篇，标题很直接："American AI is locked down and proprietary. It's losing."

他说 a16z 合伙人 Martin Casado 在 Economist 上提到，现在任何一个创业公司，有80%的概率正在使用中国模型。

这个数据挺吓人的。

更值得玩味的是后续发展：

- 美国众议院已经在调查 Airbnb 和 Anysphere（Cursor 的母公司）使用中国模型的情况
- 路透社报道中国正在考虑限制外国访问中国的开源AI模型。也就是"硅幕"（Silicon Curtain）
- CNBC 报道中国AI模型因为成本优势正在被美国公司广泛采用

你看这个局面多有意思：美国在用出口管制卡GPU，中国在考虑限制模型流出。两边都在建墙。

## 说点我的看法

我自己的感觉是，这件事最被低估的点不是技术差距，而是生态策略的差距。

美国主流AI公司的策略很直接：做最好的闭源模型，收API费，赚取利润。OpenAI、Anthropic 都是这个逻辑。这个模式在"模型能力有代差"的时候没问题。我的模型比你好很多，你不得不付钱。

但现在代差在缩小。

中国策略正好相反：开源权重，让所有人都能用。就像 Ben Werdmuller 说的：基础设施层面，开放总是赢。

你想，一个创业公司，可以用 Kimi 的权重自己部署，不用交API费，数据不出自己的服务器，还能自己微调。而用 OpenAI 的API，不仅要按token付费，数据还得经过他们的服务器。当两者的模型能力差距从"悬殊"变成"接近"，选择就很明显了。

技术上的护城河真的很薄。Stratechery 文章里也说了：模型本身几乎没有护城河，除了品牌忠诚度和表面的转换成本。真正的护城河在于企业服务生态：合同、合规、系统集成。

## 还会发生什么

我觉得接下来半年有几个关键变量。

第一，中国会不会真的限制模型流出。如果 Reuters 的报道成真，那"硅幕"会改变整个全球化分工。美国公司可能既拿不到新GPU，也拿不到新模型，卡在中间。

第二，Anthropic 和 OpenAI 会不会降价。它们现在价格高，很大程度是因为推理算力不够，供不应求。如果算力瓶颈缓解，降价空间是有的。Ben Thompson 也提到了这一点：一旦推理规模上来，单价可以大幅下降。

第三，Agent 生态会怎么绑定用户。Claude Code、Codex 这些工具已经表现出了很强的粘性。你用习惯了就不想换。而中国公司也在做类似的事情。Moonshot 刚发布了 Kimi Work，一个桌面Agent产品，支持24/7自动化任务。如果你被 Kimi Work 的工作流绑定了，底层用 K3 还是其他模型反而不重要了。

Cursor 昨天发的博客也很有意思。他们在测试 Agent Swarm，让多个Agent协作写代码。用 Grok 4.5 跑了四个小时，让 Swarm 从零复现 SQLite。这个方向如果成熟了，模型本身会成为更底层的"基础设施"，真正的价值在框架、工具和工作流上。

## 最后

写这篇文章的时候我一直在想一个问题：如果两年前有人说，中国AI模型会在2026年让美国感到压力，估计没几个人信。

但现在这个局面已经不只是"竞争"了。模型能力差距在缩小，开源策略产生了网络效应，Agent 时代对推理需求的爆发又把边际成本推到了前台。

我自己的预感是，2026 年下半年会很精彩。但精彩的方向可能跟大多数人想的不一样。不是技术上的军备竞赛，而是一场关于"谁更懂怎么做生态"的较量。

---

**信息来源：**
- [Stratechery: Who's Afraid of Chinese Models?](https://stratechery.com/2026/whos-afraid-of-chinese-models/) - Ben Thompson, July 20, 2026
- [American AI is locked down and proprietary. It's losing.](https://werd.io/american-ai-is-locked-down-and-proprietary-its-losing/) - Ben Werdmuller, July 20, 2026
- [Kimi K2.6 beats Claude, GPT-5.5 in programming challenge](https://thinkpol.ca/2026/04/30/an-open-weights-chinese-model-just-beat-claude-gpt-5-5-and-gemini-in-a-programming-challenge/) - ThinkPol, April 30, 2026
- [Chinese AI model Kimi K3 halts new signups](https://www.euronews.com/next/2026/07/20/chinese-ai-model-kimi-k3-halts-new-signups-amid-skyrocketing-demand) - Euronews, July 20, 2026
- [Chinese AI models gaining ground with US companies](https://www.cnbc.com/2026/07/07/chinese-ai-models-costs-us-openai-anthropic.html) - CNBC, July 7, 2026
- [China may restrict foreign access to open-source AI models](https://www.reuters.com/technology/artificial-intelligence/china-weighs-silicon-curtain-around-sought-after-ai-models-2026-07-08/) - Reuters, July 8, 2026
- [GLM-5.2: Chinese AI coding model](https://www.businessinsider.com/what-is-glm-5-2-chinese-ai-coding-model-2026-6) - Business Insider, June 2026
- [Google battles Chinese open-weights with Gemma 4](https://www.theregister.com/2026/04/02/googles_gemma_4_open_weights/) - The Register, April 2026
- [Cursor: Agent swarms and the new model economics](https://cursor.com/blog/agent-swarm-model-economics) - July 20, 2026
- [House panels probe Airbnb, Anysphere over Chinese AI use](https://www.nextgov.com/artificial-intelligence/2026/04/house-panels-probe-airbnb-anysphere-over-use-chinese-ai-models/413207/) - NextGov, April 2026
