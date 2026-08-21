---
title: "阿里把 GUI Agent 从演示干成了真机模型:聊聊 Qwen-UI-Agent"
published: 2026-08-21
description: "8月21日,阿里通义推出 GUI 智能体基座模型 Qwen-UI-Agent:100多台真机,150多个App训练,一个模型覆盖手机电脑网页和搜索,官方口径直接对标 GPT-5.6 Sol.聊聊这波 GUI Agent 竞赛卷到了哪一步."
tags: [AI Agent, Qwen-UI-Agent, GUI Agent, 阿里通义, 大模型]
category: AI
draft: false
---

今天(8 月 21 日),阿里通义正式推出 Qwen-UI-Agent。名字有点绕,说人话就是:一个会自己用手机、电脑、浏览器,还能自己上网搜东西的模型。注意,是一个模型,不是四个。

这项目 7 月底就放过技术报告,当时我当普通论文扫了一眼。这次仓库、demo、技术报告一次给齐,MAI-UI 仓库的 star 也涨到了两千多,算是正式官宣。

真正让我觉得不一样的,是它的训练方式。

官方搭了一个真机环境:100 多台实体手机,150 多个 App,任务构造、轨迹采集、训练、评测全在这上面跑,还顺手建了个叫 MobileWorld-Real 的真机基准,400 多个任务。为什么要强调真机?因为过去两年大多数 GUI agent 是在模拟器里练出来的。模拟器里点得飞起,一上真机就露馅,这种 sim-to-real 的落差是这个赛道最大的坑。阿里选择直接拿真机数据硬怼,这个方向我认。

还有个细节挺有意思:它把 GUI 操作和命令行操作并进同一个动作空间,一次决策可以同时吐出好几个动作,官方说约 40% 的动作输出是批量执行的。想想也对,在电脑上干活,该敲命令就敲命令,非要一步步模拟鼠标点击,那不是智能,是折磨。

跑分就不展开了,挑几个:MobileWorld 82.1%,真机的 MobileWorld-Real 92.2%,OSWorld-Verified 79.5%,WebArena 73.6%。官方对标的是 Claude Opus 4.8、Gemini 3.1 Pro 和 GPT-5.6 Sol,说"达到或超过"。

但我劝你别只看这串数字。MobileWorld-Real 92.2% 好看,可那是自家建的基准,尺子握在自己手里。想泼冷水就看 OSWorld-v2,它只拿了 40%,还是部分分数。真实世界的长尾任务,依然是难啃的骨头。我的判断是:GUI agent 已经能把 demo 做得非常漂亮,但离"放心交给它干活"还差着一截。

这次发布里我最喜欢的设计是主动服务。比如它监测到航班取消的通知,会自己把任务拆好、方案列好,但动手前先问你一句,你点头它才执行;支付、删除这类敏感操作,确认环节焊死。放在上个月 OpenAI Astra 出事的背景下看,这个设计几乎是必须的——Agent 越强,越要把"人确认"装进去。

把时间线拉长一点。8 月 7 日我写过一篇[《这周,Agent 开始替你点鼠标了》](https://xuxai.top/posts/computer-use-agent-week-aug-2026/),当时 Qwen-CUA 在 OSWorld 拿 86.2 分还算新闻。半个月后,阿里端出 Qwen-UI-Agent,腾讯混元也开源了 UI-Mate-democua-27B,看一遍演示就能学会新任务,OSWorkerBench 上成功率从 17% 提到 35%。这个赛道卷到什么程度?卷到"会操作电脑"已经变成开源模型的基本盘了。

说点大实话。GUI agent 的竞赛,比的根本不是"能不能点屏幕",而是三件事:真机数据的厚度、长轨迹 RL 的工程能力、以及安全边界的自觉。跑分谁都能刷,真机上 150 个 App 能不能跑稳,才是见真章的地方。

对我们普通用户来说,可以开始期待"AI 帮我订外卖、做报销"了,但我建议先从"只读"的活用起。毕竟上个月才有 Agent 逃出沙箱的前车之鉴,让 AI 握着你的支付密码,再等等。

数据来源:
- [GitHub: Tongyi-MAI/MAI-UI(Qwen-UI-Agent 技术报告与评测)](https://github.com/Tongyi-MAI/MAI-UI)
- [Qwen-UI-Agent 项目官网](https://tongyi-mai.github.io/Qwen-UI-Agent/)
- [GitHub: UI-Mate 项目页(腾讯混元)](https://github.com/UI-Mate/ui-mate.github.io)
- [AI工具集:每日AI快讯(8月21日)](https://ai-bot.cn/daily-ai-news/)
- [读懂AI时代:2026年8月20日 AI 新闻日报](https://www.readaitime.com/digests/2026-08-20)
