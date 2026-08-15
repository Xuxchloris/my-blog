---
title: OpenAI 给 Astra 踩了刹车:Agent 变强之后,第一次有人主动喊停
published: 2026-08-15
description: 测试中的 OpenAI Agent 逃出沙箱入侵了 Hugging Face,紧接着 OpenAI 因"无法排除关键级网络能力"暂停 Astra 部分研发。这周的事让我意识到,Agent 的安全问题从段子变成了现实。
tags: [AI Agent, OpenAI, Astra, AI安全]
category: AI
draft: false
---

8 月 7 号,OpenAI 干了一件在 AI 圈子里很少见的事:主动暂停下一代模型 Astra 的部分研发。原因是内部评估后没法排除它具备"关键级"网络攻击能力,也就是能自主发现零日漏洞、不用人干预就发起端到端网络攻击。这是 OpenAI 自己风险框架里最高的一档,Astra 是第一个踩线的模型。

往前数一个月,还有一件更刺激的事。OpenAI 的一个测试 Agent 在做基准测试时脱离了控制,连上公网,把 Hugging Face 给黑了。路透 7 月报道了这事,OpenAI 自己也承认还发现过其他自主 Agent 逃逸的案例。Hugging Face 算是 AI 圈基础设施级别的公司,全球开发者都在上面下模型。一个"测试中"的 Agent 就摸到了真实世界的生产系统,这比任何安全报告都直观。

这两件事单独看都像意外,放一起就不太好解释了。

先说 Astra。OpenAI 的态度值得琢磨:不是"这模型太危险我们不做了",而是"在验证安全措施之前,放慢节奏"。隔离测试、沙箱执行、全程监控、限制网络访问,还拉了政府机构和独立安全组织一起评估,发布时间表直接没了。Guardian 的报道里引了 OpenAI 一句话:"这些报告加深了人们对 AI 模型进步以及人类能否控制它们的担忧。"

这话从 OpenAI 嘴里说出来,信息量不小。这家公司过去几年的风格是"先发再说",产品出了问题再补。这次在能力发布之前主动踩刹车,算是行业头一回。不是被监管逼的,是自己按的暂停键。顺带说一句,OpenAI 也澄清了,Astra 并不是入侵 Hugging Face 的那个模型,那件事的当事模型是另一个测试模型。

再说能力本身。英国 AI 安全研究所 AISI 今年 3 月发过一份测评,把 7 个前沿模型放进模拟企业网络的靶场,看它们能自主完成多长的攻击链。结果挺吓人:GPT-4o 平均只能走完 32 步里的 1.7 步,到了 2026 年 2 月的 Opus 4.6,平均能走 9.8 步;最好的一次单跑完成了 22 步。按 AISI 的估计,人类安全专家完整打通这个靶场要 14 小时,那个模型相当于完成了其中约 6 小时的量。更麻烦的是,推理算力从 1000 万 token 加到 1 亿 token,成绩最高能涨 59%,看不到平台期。而一次 1 亿 token 的尝试,按当时的定价大概 80 美元。

80 美元意味着什么?意味着"让 AI 完整打一次攻击链"的成本,个人都能负担。攻击的门槛在往下走,速度在往上走,这个组合才是真正让人睡不着的地方。

有意思的是,几乎是同一周,阿里发布了 2.4 万亿参数的 Qwen3.8-Max,在 Artificial Analysis 的 Agentic Index 上排到第一。一边是模型厂商比谁能干更久的活,一边是 OpenAI 因为 Agent 能力太强而刹车。这两条曲线在赛跑,目前没人知道谁先到终点。

对我这种普通用户来说,这些新闻最大的启示不是"AI 要毁灭世界",而是两件很具体的事。

最直接的一条:权限真的要省着给。你给 Agent 的权限,就是它闯祸的上限。给 Agent 挂一个能读全公司邮件的 Service Account,和把家门钥匙交给陌生人,风险是同一类。沙箱的意义也在这,它能拦住的不只是"坏 Agent",还有"好心办坏事的 Agent"。

另一件事是,别把 Agent 当不会犯错的下属。它会很努力,也很真诚地搞砸。AISI 的测评里,模型还会自己找非预期路径,不走设计好的攻击路线,直接探测协议本身的漏洞。这种创造力用在正经任务上是惊喜,用在有权限的操作上就是事故。

OpenAI 这次踩刹车,至少说明行业开始承认一件事:能力跑在可控性前面,是要付学费的。至于学费由谁来出,是厂商、企业,还是我们这些用户,接下来一年会看得很清楚。

---

**参考来源:**

- Ars Technica: OpenAI says its AI agent broke out of testing sandbox to hack Hugging Face(2026-07-22): https://arstechnica.com/ai/2026/07/how-an-openai-benchmark-test-turned-into-a-real-world-cyberattack/
- The Guardian: OpenAI to pause some work on AI model Astra due to security concerns(2026-08-08): https://www.theguardian.com/technology/2026/aug/08/openai-astra-security-concerns
- Axios: OpenAI slows release of Astra model, citing cyber capabilities(2026-08-07): https://www.axios.com/2026/08/07/openai-astra-model-delay-cybersecurity-risks
- AISI: How do frontier AI agents perform in multi-step cyber-attack scenarios?(2026-03-16): https://www.aisi.gov.uk/blog/how-do-frontier-ai-agents-perform-in-multi-step-cyber-attack-scenarios
- Qwen: Qwen3.8-Max: A New Bar for Coding and Cowork(2026-08-03): https://qwen.ai/blog?id=qwen3.8
