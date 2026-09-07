---
title: 一周五个大模型,我反而不想看了
published: 2026-09-07
description: 这周 Anthropic、Meta、Google、OpenAI 扎堆发模型,Nvidia 还花 129 亿美元收购了 Hugging Face。CNBC 管这叫 model fatigue,我深有同感:追新已经追不动了,真正该做的是把系统和某一家模型厂商解耦。
tags: [大模型, model fatigue, AI Agent, Nvidia]
category: AI
draft: false
---

这周 AI 圈的发新节奏有点失控。周二 Anthropic 更新 Claude Fable 5.1 和 Mythos 5.1,周三 Meta 发 Muse Spark 1.3、Google 发 Gemini 3.8 Flash,周四 OpenAI 直接端出 GPT-6 Astra,同一天阿布扎比的 MBZUAI 还开源了 K2 Horizon 系列。周五再看新闻,Nvidia 宣布花 129 亿美元收购 Hugging Face。CNBC 给这波起了个名字:model fatigue,模型疲劳。

说实话,我确实疲劳了。

先说个有点黑色幽默的事。8 月中我在这个博客写过,Astra 因为"无法排除关键级网络能力"被 OpenAI 主动暂停研发,当时觉得这家公司总算学会了踩刹车。结果刹车踩了三周不到,周四 Astra 就这么发布了,CNBC 的报道标题写着,这是 OpenAI 第一个跨过"Critical"网络安全能力线的模型,而且是"警告完就上线"。安全评估从暂停键变成了免责声明,这个转变比我预想的快得多。

为什么大家都挤在同一周发?OpenAI 的 Altman 对 CNBC 的解释是"大家都进入了更快的节奏",顺带归因于暑假结束。Notre Dame 商学院教授 Abbasi 的说法更直接:这是在玩 share-of-wallet 游戏,谁也不能让开发者觉得自己创新慢了。背景数字是 Gartner 预测今年全球 AI 支出 2.59 万亿美元,比去年涨 47%,其中 Anthropic 和 OpenAI 的私募估值都已经逼近 1 万亿,两家都在往公开市场走。发布本身成了融资动作,这就解释了为什么节奏停不下来。

但发布多不等于进步多。AI 金融初创公司 Farsight 的技术负责人 Faro 在采访里区分得很清楚:这周除了 GPT-6 Astra,其余都是 point release,在现有模型上做小升级。他认可的真正"动了针"的模型,是 6 月的 Fable 5 和 7 月 Moonshot AI 的 Kimi K3。也就是说,一个季度里真正值得迁移一次的可能就两三个,剩下的发布更多是提醒你还活着。

对企业来说,追新的成本是实打实的。Clockwork Systems 的 CEO Vasudevan 说,他们要评估一个任务用哪个模型,本来该测 10 个,现在只敢挑 5 个,因为评估本身要烧算力和人力。我觉得这个数字很能说明问题:当发布速度超过评估速度,所谓"永远用最强模型"在工程上就是不成立的,你只能选择性地忽略一部分新模型。

那怎么办?我这两天正好看到一篇很对味道的文章,前联合国大学工程师 Juan Reyero 9 月 6 号写的《Don't build your organization around a model provider》。他的核心论点是:真正危险的不是被某一家模型锁死,而是你的 Agent 体系被某一家的基础设施锁死。

这个担忧有现实依据。今年 7 月 OpenAI 在 Responses API 里推出多 Agent beta,支持托管的 Agent 派生、消息传递;8 月 Anthropic 给独立的 Claude Code 会话之间加了通信能力。Agent 之间能对话,就能分工、互相检查结论、积累任务上下文。问题是,如果这些 Agent 的身份、任务、通信记录全长在厂商的平台上,换供应商就不是换个 API key 的事,而是重建整个协作体系。Reyero 举的例子很具体:一个 reviewer Agent 应该属于组织,不管底下跑的是哪家模型,它积累的知识、其他 Agent 找它的方式、它的审批权限,都应该跟着组织走。他给的解法是开源的 Agent 身份和通信层,加上 A2A 这类跨框架的开放协议。

我的看法是,模型疲劳其实是个信号,说明大模型正在商品化。既然发布方自己都承认大部分更新是 point release,用户就更没必要为每一次发布焦虑。合理的姿势大概是:固定一两个主力模型,每季度认真评估一次要不要换,平时把精力花在解耦上,让 prompt、工具定义、Agent 的任务和记忆尽量不绑定任何一家的私有格式。这样哪天 Kimi 或者 Gemini 真的大跳一步,你迁移的成本是一周而不是一个季度。

Faro 那句话我很认同,真正动针的模型一个季度也就两三个。剩下的,让它发去吧,反正你的评估队列不需要跟着它们的发布会走。

---

**参考来源:**

- CNBC: 'Model fatigue' sets in as AI labs race to roll out new versions at frenetic pace(2026-09-06): https://www.cnbc.com/2026/09/06/meta-google-openai-anthropic-ai-model-fatigue.html
- Juan Reyero: Don't build your organization around a model provider(2026-09-06): https://juanreyero.com/article/ai/model-provider-independence
- 本博客: OpenAI 给 Astra 踩了刹车:Agent 变强之后,第一次有人主动喊停(2026-08-15)
