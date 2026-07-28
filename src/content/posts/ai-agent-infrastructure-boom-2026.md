---
title: "2026 年中盘点：AI Agent 还没消灭程序员，先养活了一整圈周边工具"
published: 2026-07-28
description: "Claude Code 快 14 万星了，但真正疯涨的是它周边那些基础设施——Agent 路由器、插件市场、性能调优工具。2026 年最热门的 AI 赛道，不是 Agent 本身，而是 Agent 的基建层。"
tags: [AI Agent, 开发者工具, Claude Code, 开源生态, 技术趋势]
category: AI
draft: false
---

上周聊了三件大事，今天换个方向。不聊 Agent 本身——聊聊围在它周围的那一圈。

2026 上半年最魔幻的事情，我觉得不是哪个 Agent 多能打，而是给 Agent 盖房子的那批人，涨得比 Agent 还凶。

## 一个数字就够了

ECC。不是加密算法那个 ECC，是 GitHub 上一个叫 `affaan-m/ECC` 的项目。

今年 1 月 18 号创建的，到今天——**234,320 颗星**。

六个月。二十三万颗星。

我盯着这个数字愣了两秒。PyTorch 用了 7 年才到这个量级。一个今年才冒出来的项目，半年就跑完了别人一辈子的路。

ECC 干的事是给 AI 编程 Agent（Claude Code、Codex、Cursor 这些）做一套性能调优系统——管技能、管记忆、管上下文、管安全。往白了说：**Agent 自己不操心的那些底层功夫，你想在生产环境用好它，就得有人帮你兜着。**

而 GitHub 星数告诉你：需要这个的人，比我以为的多得多。

## 不只是 ECC

翻翻最近几个月的榜单，画风出奇一致：

- **CC Switch**（12 万星）：跨平台的桌面壳子，把 Claude Code、Codex、OpenCode、Grok Build 甚至 Hermes Agent 全塞进去。Rust 写的，7 月 20 号刚发了一版。
- **Claude Code Router**（3.6 万星）：名字就是它的功能——给 Agent 们配个控制平面，跨模型路由、统一编排、集中监控。一个工具管所有。
- **wshobson/agents**（3.8 万星）：多 Harness 的 Agent 插件市场。Claude Code、Codex、Cursor、Copilot、Gemini CLI 都能往里插。
- **Serena**（2.7 万星）：给自己标签是"Agent 的 IDE"——语义检索、智能编辑、上下文管理，一套全包。
- **LobeHub**（8 万星）：更激进，直接当"Agent 首席运营官"，招聘、排班、写日报，帮你管整个 Agent 团队。

注意到没？前面那一长串，**没一个是 Agent 本体。**

全是 Agent 的邻居、房东、物业管理。

## 这事儿我琢磨了一下

为什么这一整圈突然爆炸了？

一个原因是 Agent 自己的差距在缩小。去年 Claude Code 和 Codex 刚出来那会儿，大家还在拼谁能写更长的代码。今年功能都差不多——都能读写文件、调终端、搞 Git。差异化挤干了，新战场就变成了"你怎么管这些 Agent"。

另一个原因更直接：真拿 Agent 干活的人，发现缺的不是 Agent。

我自己就有这感觉。你一开就是五六个 Agent 跑不同任务，很快就需要一个路由器决定谁干什么。你希望它记住上次的项目配置，就需要一个记忆层。不想每次换环境都重新配一遍，就需要一个技能市场。

Agent 自己不管这些。

还有一个层面是生态位的逻辑。当年数据库火了之后出来监控工具，微服务火了之后出来 Service Mesh——先是应用炸开，然后基础设施补上。2026 年 Agent 用户量到了某个临界点，基础设施的缺口就露出来了。

## 说两个让我意外的细节

Dify 和 FastGPT 这种老牌平台也在涨（15 万星和 2.9 万星），但明显不如专门给 Agent 做工具的那一批快。

CowAgent 的迭代速度有点猛——4.6 万星，最近一个月发了 4 个版本，2.1.0 到 2.1.4，基本一周一个。LibreChat（4.1 万星）也在疯狂加 Agent 和 MCP 支持。

但最让我意外的还是 ECC。234K 星什么概念？已经超过了很多我每天都在用的工具。翻了翻它的 commit 记录，昨天还有人在提交。这不是刷出来的热度，真有人在干活。

## 所以呢

我的感觉是这样的：**下半年 Agent 基础设施会越来越像云原生时代的 DevOps 工具链。**

ChatGPT 是云端的一个产品，你打开浏览器就能用。但编程 Agent 是嵌在你工作流里的——用什么模型、跑什么系统、装什么插件、走什么协议，这些选择都在你手上，也得你自己打理。这个模式天然就会长出一个"Agent DevOps"的市场。

ECC、CC Switch、Claude Code Router 是第一批冲进去的。它们解决的问题，跟当年 Docker 和 Prometheus 面对的很相似——工具好用，环境复杂，需要有人来管这里面的破事。

当然，现在说谁能活下来太早了。234K 星不代表 234K 个付费用户，大多数还在围观。哪些能挺到明年这个时候，哪些会被收购或者消失，谁也说不准。

有一点我觉得挺稳的——如果你还没关注这个方向，半年后再看 ECC 的星数，大概已经不敢上车了。

而我更好奇的是，下一个 ECC 会从哪个角落冒出来。

---

*数据来源：GitHub API 实时查询（2026-07-28）*
- [ECC](https://github.com/affaan-m/ECC) — 234,320 stars
- [CC Switch](https://github.com/farion1231/cc-switch) — 121,839 stars
- [Claude Code Router](https://github.com/musistudio/claude-code-router) — 36,236 stars
- [Agents Marketplace](https://github.com/wshobson/agents) — 38,311 stars
- [Serena](https://github.com/oraios/serena) — 27,059 stars
- [LobeHub](https://github.com/lobehub/lobehub) — 80,911 stars
- [CowAgent](https://github.com/zhayujie/CowAgent) — 46,170 stars
- [Claude Code](https://github.com/anthropics/claude-code) — 139,356 stars
