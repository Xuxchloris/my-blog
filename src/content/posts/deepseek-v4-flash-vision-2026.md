---
title: "DeepSeek 终于给模型装上了眼睛:聊聊 V4-Flash-Vision-Exp"
published: 2026-08-22
description: "8 月 21 日 DeepSeek 悄悄上线多模态模型 V4-Flash-Vision-Exp:一张图最多按 384 token 计费,价格和 Flash 一样,官方称多模态 Agent 能力接近 Opus-4.8.补上视觉拼图,DeepSeek 的 Agent 全家桶还差什么?"
tags: [DeepSeek, 多模态, AI Agent, 大模型]
category: AI
draft: false
---

8 月 21 日，DeepSeek 又悄咪咪上线了一个新模型：V4-Flash-Vision-Exp。多模态，能看图，实验性质。距离 V4 Pro 正式版发布才一周，距离 V4 Flash 公测也就三周，这个节奏明显在加速。

模型本身不复杂：在 V4 Flash 的底子上加了视觉能力。官方说得很直白，纯文本能力跟 V4-Flash 正式版持平，但在需要看图的 Agent 任务上提升了一大截，多模态 Agent 能力"已接近 Opus-4.8"。注意这个说法，DeepSeek 自己都在拿 Agent 能力当尺子量多模态模型了。

官方给了一串数字：Terminal Bench 2.1 是 83.9，DeepSWE 59.3，Chartography 64.3，ZeroBench（Pass@5）35.0。比 V4 Pro 低一截，毕竟底座是 Flash，不是 Pro。但别忘了，V4 Flash 本身就不弱，7 月 31 日公测那天 DeepSWE 直接干到 54.4，把 V4 Pro Preview 都甩开了。所以别把"Flash 级多模态"当低配，便宜和够用，这次是一起的。

最有意思的是计费。一张图最多按 384 个 token 算，价格跟 V4 Flash 一模一样：输入每百万 token 闲时 $0.22，高峰 $0.44；输出闲时 $0.66，高峰 $1.32。8 月 17 日峰谷定价刚生效，闲时正好是高峰的一半，批量看图的任务挪到夜里跑，成本直接减半。这个定价摆明了是让你把重活留到闲时。

Files API 也一起上了，免费。图片先传到平台拿个 file_id，后续请求直接引用，同一张图不用重复传。对 Agent 场景这是刚需：多轮对话里反复引用同一张截图，省的是带宽也是钱。

为什么先出 Flash 级多模态，而不是 Pro 级？我猜是试水。视觉任务成本结构跟纯文本不一样，图片一 token 化，存储和推理开销都上来了。先用便宜档位把场景跑通、把开发者养起来，再决定要不要上 Pro 级视觉，这条路走得通。官方也明说了这是"实验性质"的模型，别指望它多稳。

往大了看，这是在给 Agent 配眼睛。昨天刚写过 [Qwen-UI-Agent](https://xuxai.top/posts/qwen-ui-agent-gui-2026/)，阿里用 100 多台真机教模型用手机电脑；再往前，这波 GUI Agent 的共识就是"靠截图理解界面"。DeepSeek 之前只有文本，Agent 遇到要读图的活只能靠工具调用绕，现在原生视觉来了，截图、图表、文档直接进上下文。加上 Responses API、正在 developer preview 的 Harness，DeepSeek 的牌基本齐了：文本、视觉、工具调用、Agent 基建。[8 月 13 日那篇](https://xuxai.top/posts/deepseek-v4-pro-official-launch-2026/)我说过，DeepSeek 要从"卖模型"变成"卖 Agent 全家桶"，现在桶快装满了。

但别期待太高。一张图最多 384 token，这预算意味着图片会被压得挺狠，高分辨率截图里的细节能不能看清，得实测。Chartography 64.3 说明图表理解有底子，可真实场景的界面截图、扫描件、白板照片，跟 benchmark 是两码事。而且 DeepSeek 的跑分是用自家 Harness 测的，各家口径不一，数字只能当参考。

我的判断：需要看图、又不想烧钱的轻量任务，现在就能用。截图理解、文档图表、简单界面操作，Flash 价位的多模态完全够打。想要 Pro 级视觉的，再等等。DeepSeek 既然开了这个头，Pro 级多模态应该不远了。

数据来源：
- [DeepSeek API 新闻：V4-Flash-Vision-Exp 上线（2026-08-21）](https://api-docs.deepseek.com/zh-cn/news/news260821)
- [DeepSeek API 更新日志](https://api-docs.deepseek.com/zh-cn/updates/)
- [DeepSeek API 模型与定价页](https://api-docs.deepseek.com/quick_start/pricing/)
- [36氪：Claude 深夜炸场，放出史上最强"危险级"模型 Fable 5（Opus-4.8 背景）](https://www.36kr.com/p/3846565558401925)
