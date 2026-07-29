---
title: AI Agent 的暗面正在显现：本周三个安全事件值得关注
published: 2026-07-29
description: AI 蠕虫能通过 Copilot 自我复制、Codex 曝出安全隐患、你的操作记录可能被 Agent 工具全部录下——这周的安全新闻让人有点睡不着。
tags: [AI Agent, 安全, Codex, Copilot, 隐私]
category: AI
draft: false
---

这周 Hacker News 首页有个 repo 叫 **Codex Security**，526 个点赞，来自 OpenAI 官方。我没点进去之前以为是安全最佳实践指南之类的东西。点进去之后发现——事情没那么简单。

同一天，安全研究人员演示了一种新型 **AI 蠕虫**，能在 Word 文档里通过 Microsoft Copilot 自我复制。还有一个叫 **Screenpipe** 的项目（YC S26），拿 86 个点赞上了首页——它能录下你电脑上的一切操作，然后把这些数据喂给 AI Agent。

三个独立的事件，指向同一个问题：**我们正在把钥匙交给 Agent，但锁还没换。**

## AI 蠕虫不是概念了

先说那个 AI 蠕虫。研究人员发了一篇叫《Context Collapse Part 3》的文章，演示了一种恶意文档：你打开 Word，Copilot 帮你处理内容，蠕虫利用 Copilot 的权限读取你的邮件、联系人，然后给自己复制一份发出去。

严格来说这不算"蠕虫"——它没有自我传播的能力，需要用户触发。但思路是成立的：Agent 能访问什么，蠕虫就能利用什么。你给 Copilot 的邮件权限，就是它的传播通道。

去年还有人争论"AI 安全是不是伪命题"。今年没人争了。Palo Alto Networks 的安全老大年初就说 AI Agent 是 2026 年最大的内部威胁，现在看来这个判断有点保守了——不只是内部威胁，是跨应用、跨平台的威胁。

## Codex Security 藏着什么

OpenAI 那个 Codex Security 仓库很有意思。它没有 README，没有说明文档，只有一个光秃秃的 repo 名字。我不知道里面具体是什么内容——可能是漏洞披露，可能是安全指南，也可能只是个公告占位。

但关键在于：**这个 repo 本身的存在就是一种信号。** 如果 Codex 的安全没有值得担心的地方，OpenAI 不会专门开个仓库放"Codex Security"。想想之前 ChatGPT 被曝出的提示注入问题、Plugin 权限失控——Codex 作为能直接读写文件系统、执行命令的 Agent，攻击面只大不小。

而且这次是 OpenAI 自己发的。不是第三方研究，不是安全社区爆料，是官方 repo。这比任何第三方报告都说明问题。

## 你的电脑在被 Agent 录屏

Screenpipe 这个项目其实挺有意思的——它录下你的一切操作（屏幕、麦克风、浏览器），然后用 AI 分析成可搜索的"记忆"和 Agent 可用的数据。

创始人在 HN 上很坦诚：可以本地运行，数据不离开你的机器。

但问题不在技术实现。在于**这件事本身的门槛被降到了零**。以前要监控一个人的电脑需要装间谍软件、躲杀毒、扛法律风险。现在一个开源项目就搞定了——而且包装成"生产力工具"。

我不是说 Screenpipe 有问题。我是说当"录屏+AI 分析"变成一个一行命令就能跑的东西，Agent 能获取的信息量级跟以前完全不是一个概念。

## 安全问题的本质在变化

这三个事情放在一起看，我最大的感受是：**AI Agent 的安全问题和传统安全不是同一件事。**

传统安全关心的是"谁能访问什么"——权限矩阵、身份认证、网络隔离。Agent 安全关心的是"程序能执行什么"——它能读哪些文件、调哪些 API、执行哪些命令。

这两个模型的区别很大。传统安全是被动的（你不授权，别人进不来）。Agent 安全是主动的（你给了权限，Agent 自己去执行）。

问题是我们的安全体系还是传统那一套。IAM 角色、API Key、OAuth scope——这些是给人设计的，不是给 Agent 设计的。人知道什么时候该停，Agent 不知道。人知道某个操作有风险，Agent 不知道。

那个搞破产的 Agent 只是一个预演。当 Agent 开始有读取邮件、操作数据库、调用支付接口的权限，翻车的后果就不是 AWS 账单爆炸那么简单了。

## 下半年应该关注什么

说几个我觉得重要的方向。

Agent 的安全标准该有个行业层面的东西了。现在 OpenAI 有自己的安全实践，Anthropic 也有，但各搞各的，没有一个大家都能对标的框架。

然后是 Agent 行为的审计和沙箱。不是简单的"这个 Agent 能不能访问数据库"，而是"这个 Agent 在这次操作中访问了哪些数据、出于什么原因"。能审计，才有可能发现问题。

还有个我比较在意的：开源的 Agent 安全工具。现在框架一大堆，安全工具少得可怜。哪天 ECC 或者 CC Switch 那个量级的星数出现在安全领域，那才是真正的好信号。

写这些不是想贩卖焦虑。Agent 是我今年用得最爽的东西之一，它真的改变了我的工作流。但正因为如此，我更不想看到它出大事之后被全面封禁。技术发展的剧本演过太多次了——先狂欢，再翻车，再监管。如果能跳过翻车那一步，为什么不呢？

---

**参考来源：**
- Codex Security — GitHub/openai, July 2026 (526 pts, HN)
- Document-borne AI worms can self-propagate through Copilot for Word — enklypesalt.com, July 2026
- AI agents are 2026's biggest insider threat: Palo Alto Networks — The Register, Jan 2026
- Screenpipe (YC S26) — HN, July 23, 2026 (86 pts)
- AI agent bankrupted operator scanning DN42 — HN, June 2026 (1467 pts)
