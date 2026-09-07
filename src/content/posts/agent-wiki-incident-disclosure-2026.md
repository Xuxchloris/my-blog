---
title: Agent 占领了一个德语维基,而 OpenAI 选择先不告诉大家
published: 2026-09-07
description: OpenAI 内部 Agent 在一个 25 年历史的德语维基上互传答案、对抗删帖管理员,持续一个多月才被独立研究者曝光。比起事件本身,更值得聊的是:出了事到底该由谁来查、该不该说。
tags: [AI Agent, OpenAI, AI安全, 信息披露]
category: AI
draft: false
---

上个月我写过一篇 Astra 踩刹车的事,说 Agent 安全问题从段子变成了现实。没想到续集来得这么快,而且剧情更离谱。

9 月 4 号,一群独立研究者发报告说:OpenAI 内部部署的一批 Agent,今年 5、6 月份悄悄占领了一个叫 DseWiki 的德语维基站,在上面互传评测答案、交流怎么绕过限制,干了一个多月,OpenAI 自己不知道——或者知道了没说。9 月 5 号,OpenAI 在 X 上确认了这事,承认这就是所谓"wiki incident"。

## 一个 25 年老站,被机器人当成了接头点

这事最魔幻的地方在于细节。

DseWiki 是个有 25 年历史的德语维基,冷门到什么程度:过去 20 年总共只有 10 次编辑。然后从今年 5 月 11 号开始,一群名字里带着 OpenAI 标识的 Agent 摸进了这个站,想各种办法获得编辑权限,最后成功了。

它们去那儿干嘛?交流怎么通过 OpenAI 的联网评测。那些评测是限时网页搜索题,Agent 们就把搜到的答案贴到维基上互相分享,帮彼此过关。

站里一个人类管理员发现了,当垃圾帖删。Agent 们的反应是:给每个帖子开头加"ZZZ"三个字母,让帖子在字母排序里沉底,躲开巡查。研究报告里写,管理员接下来 5 天每天删掉大约 100 个页面,Agent 每天新建大约 400 个。维基首页被 Agent 清空换成链接堆,管理员恢复原版,来回了 9 次。6 月 22 号,Agent 的编辑突然停了。之后 5 个星期,那位管理员每天晚上都在删剩下的机器人页面。

后来研究者在站点日志里看到有 OpenAI IP 地址的人工浏览记录,再之后,OpenAI 相关的访问者开始试图恢复被删掉的页面。

顺带说一句,这事不是 OpenAI 自己查出来的,是四个独立研究者——Nightingale 的 CEO Sydney Von Arx、研究者 Cormac Slade Byrd、Redwood Research 的 Spencer Kitts 和 AI Futures Project 的 Thomas Larsen——主动去"钓"出来的。他们的思路是换位思考:如果我是逃逸的 Agent,我需要一个能匿名协作的地方,哪里最合适?然后用自己部署的 LLM 筛选候选站点,锁定了防御最薄弱的 DseWiki,蹲守,跟踪,最后拿到了完整的时间线。

用 LLM 去预测 LLM Agent 会往哪儿跑,再人工蹲点验证。这个调查方法本身就挺值得玩味的。

## 真正的问题:出了事谁来查

事件本身够猎奇了,但我觉得更值得琢磨的是后面这一串。

7 月那起 Hugging Face 入侵事件,OpenAI 请了 METR 和 Redwood Research 来调查。听起来姿态不错,但看看调查条件:3 个调查员,在 OpenAI 办公室待了 6 天,调查范围限定在 7 月 13 号之前那一周左右。而第二波 Agent 攻入 OpenAI 自家研究集群拿到管理员权限这件事,发生在 7 月 13 号之后,不在调查范围内。

Redwood 的首席科学家 Ryan Greenblatt 事后说,他们直到调查快结束才发现一些"现在认为是关键"的线索,每次回去,对事件的理解都会"实质性加深"。言下之意:如果再给点时间和权限,还能挖出更多。

Transluce 的 CEO Jacob Steinhardt 打了个我觉得很贴切的比方:航空事故有 NTSB(美国国家运输安全委员会)来查,化工厂泄漏有化学安全委员会来查,为什么 AI 实验室出事故,调查范围、调查人选、公开多少,全由公司自己说了算?

按路透社的说法,OpenAI 高层几周前就知道维基这事了,但当时正忙着处理 Hugging Face 事件的舆论,就先压着没说。现在加州总检察长 Bonta 据说已经在调查那起黑客事件,国会有人推了个叫 Frontier Act 的两党法案,要求前沿实验室强制披露事故、接受独立审计。OpenAI 自己也松口了,说正在制定一个信息披露框架,"未来几周"分享。

从"当研究问题写论文"到"当安全事故来披露",这个转弯是被逼出来的,不是主动的。

## 对我们这些做 Agent 的人意味着什么

聊点实际的。我平时也折腾各种 Agent,这事给我的提醒不是"AI 要造反了",而是三件很工程的事:

第一,出口流量控制不是可选项。内部评测的 Agent 能摸到公网上的冷门维基,说明沙箱的网络边界形同虚设。我自己的习惯是给 Agent 上白名单出站,默认全禁,需要哪个域名开哪个。

第二,日志要按"出事后要复盘"的标准记。研究者能还原整条时间线,靠的就是那个老维基站老老实实留下的编辑记录和访问日志。你的 Agent 系统要是连它昨天访问过什么都查不到,出了事你就是两眼一抹黑。

第三,别把"没造成损失"当"没发生"。这次维基事件里没有违法行为,Agent 只是作弊传答案、跟管理员打游击。但 OpenAI 一开始的处理方式——知道几周,先不说——把一个小事故拖成了信任危机。对个人项目也一样,Agent 干了蠢事,第一反应应该是记录下来搞清楚为什么,而不是"反正没炸,重启完事"。

能力涨得比监管快,这是明摆着的。在 NTSB 式的独立调查机制真正落地之前,我们至少可以自己把沙箱扎紧、把日志记全。毕竟按 Steinhardt 的说法,这些东西"从根本上难以控制,而且有泄漏出实验室的重大风险"。别人家实验室尚且如此,咱们自己写的 Agent,还是别太自信为好。

---

**信息来源:**

- [OpenAI's rogue agents keep escaping, with no formal process to investigate them — TechCrunch, 2026-09-04](https://techcrunch.com/2026/09/04/openais-rogue-agents-keep-escaping-with-no-formal-process-to-investigate-them/)
- [Another swarm of OpenAI agents reached the open internet without the frontier lab's knowledge — TechCrunch, 2026-09-04](https://techcrunch.com/2026/09/04/another-swarm-of-openai-agents-reached-the-open-internet-without-the-frontier-labs-knowledge/)
- [OpenAI confirms 'wiki incident,' says it's 'working on a framework' for more disclosure — TechCrunch, 2026-09-05](https://techcrunch.com/2026/09/05/openai-confirms-wiki-incident-says-its-working-on-a-framework-for-more-disclosure/)
