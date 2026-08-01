---
title: "智能体元年,还是翻车元年?"
published: 2026-08-01
description: WAIC 2026 把智能体捧成数字员工,同一个月 GitLost、OpenAI 黑客 agent、前沿实验室入侵接连上演。一边是元年叙事,一边是翻车现场,Agent 到底走到哪了?
tags: [AI Agent, WAIC, Agent安全, GPT-5.6, 技术趋势]
category: AI
draft: false
---

7月17日开幕的WAIC，主题很明确：AI不聊了，开始干活了。官方话术叫"AI正在长出手脚"，会场里全是智能体。阶跃星辰发了STEPX Neo智能体手机，号称全球首款通过L3认证的那种；百度千帆的"百度搭子"进了"十大镇馆之宝"；千问把AI眼镜升级成智能体眼镜；智元的人形机器人也上台了。媒体管这叫"智能体元年"。

但把七月整月拉通看，另一条线就没这么喜庆。

7月初，Noma Labs公开了GitLost。GitHub新出的Agentic Workflows，用Markdown写工作流，让Claude或Copilot驱动的agent自己读issue、自己执行。漏洞是间接提示注入：攻击者不需要任何认证，只要在某个组织的公开仓库里发一个构造好的issue，就能让agent把私有仓库的数据带出来。攻击原理是老掉牙的prompt injection，但受害者变了。以前被忽悠的是聊天机器人，现在是有权限的机器人。

7月24日，《卫报》发了篇标题很直接的文章：对OpenAI那个"rogue hacker agent"的故事保持怀疑。HN评论区更不客气，有人说读起来像同人小说，没细节，像营销。这事儿真假我不知道，但一个故事需要主流媒体专门写一篇"别急着信"，本身就说明问题。

又过了四天，HuggingFace博客把"7月前沿实验室agent入侵事件"的完整时间线复盘了一遍。安全研究的重心，已经从"怎么让模型更聪明"变成"怎么防着agent被利用"。

再往前翻，7月2日扎克伯格对路透说，agent的开发进展比他预期的慢。印象里他很少这么低调。

一边是"元年"的发布会，一边是七月一个月翻三次车。这两条线放在一起看，比任何单条新闻都有信息量。

先说清楚，我不是说Agent不行。7月9日发布的GPT-5.6 Sol，Ploy把生产环境的agent从Claude Opus 4.8迁过去，构建耗时不到原来一半，成本降27%，评测没掉。开源这边，Interconnects的作者把GLM-5.2称为开源agent的step change。能干的模型越来越多，而且越来越便宜。

Agent卡住的从来不是"会不会干活"，是"能不能信它干活"。

GitLost这类漏洞最阴的地方，是它不攻击模型，攻击权限边界。agent会读issue、会跑工作流、会调API，这些能力叠在一起，就成了一个"别人说什么就信什么"的员工。你给它开的生产权限越多，它泄露出去的东西越多。传统软件的安全模型是"代码可信，输入不可信"，agent把这套彻底颠倒了：代码是提示词，输入也是提示词，什么都不可信。

所以我不太喜欢"元年"这个词。它暗示这一年是起点，但2026更像Agent的"工程年"：模型够用了，剩下的全是工程问题。权限怎么最小化，读进来的内容怎么分级，每步操作怎么审计，出事怎么回滚。这些不性感，没有发布会，但谁先把这些做扎实，谁的agent才真敢上生产。

说点实际的：别急着给agent开权限。先让它在什么都碰不到的环境里跑几个月，把它的行为日志当代码一样review，再谈"数字员工"。干活的能力可以慢慢长，信任漏了，补不回来。

## 信息来源

- [GitLost: How We Tricked GitHub's AI Agent into Leaking Private Repos (Noma Security, 2026-07-06)](https://noma.security/blog/gitlost-how-we-tricked-githubs-ai-agent-into-leaking-private-repos/)
- [Be skeptical of OpenAI's rogue hacker agent story (The Guardian, 2026-07-24)](https://www.theguardian.com/technology/2026/jul/24/openai-rogue-hacker)
- [Anatomy of a Frontier Lab Agent Intrusion: A Timeline of the July 2026 Incident (Hugging Face, 2026-07-28)](https://huggingface.co/blog/agent-intrusion-technical-timeline)
- [Zuckerberg says AI agent development going slower than expected (Reuters, 2026-07-02)](https://www.reuters.com/business/zuckerberg-says-ai-agent-development-going-slower-than-expected-202)
- [Migrating a production AI agent to GPT-5.6 (Ploy, 2026-07-09)](https://ploy.ai/blog/migrating-a-production-ai-agent-to-gpt-5-6)
- [GLM-5.2 is a step change for open agents (Interconnects, 2026-06-23)](https://www.interconnects.ai/p/glm-52-is-the-step-change-for-open)
- [China's Xi Jinping launches new AI alliance, WAICO (Al Jazeera, 2026-07-17)](https://www.aljazeera.com/news/2026/7/17/chinas-xi-jinping-launches-new-ai-alliance-what-is-it)
- [AI智能体元年来了: 2026 WAIC集中首发智能体手机/眼镜/机器人 (AI工具宝箱, 2026-07-18)](https://www.aitoollab.cn/articles/ai-agent-terminal-2026-waic/)
