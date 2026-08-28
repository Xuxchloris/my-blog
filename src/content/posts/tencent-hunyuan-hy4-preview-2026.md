---
title: 腾讯开源 Hy4 preview:不晒榜单,晒内部盲测和一道百年几何题
published: 2026-08-28
description: 腾讯混元 8 月 28 日开源 Hy4 preview,770B 参数 1M 上下文,没有公开榜单,只有内部盲测和百年几何难题的进展,聊聊这次发布为什么很腾讯
tags: [腾讯混元, 大模型, 开源, AI for Science]
category: AI
draft: false
---

今天(8 月 28 日)腾讯混元把 Hy4 preview 开源了。总参数 770B,激活 49B,上下文 1M,Apache 2.0,权重和代码一起放,GitHub、Hugging Face、ModelScope 都上了。

这个月国产大模型发得又密又快:DeepSeek 转正 V4 Pro,阿里开源 Max 级旗舰,智谱、MiniMax 各有动作。腾讯一直是那个"闷声"的。4 月发过 Hy3 preview,8 月 14 日财报季预告了新一代,然后就没动静了。今天算是正式下场。

但这次发布最"腾讯"的地方,不是参数,是姿势。

技术上的选择其实挺直白。Hy4 preview 是 MoE,78 层,每层 256 个路由专家,每个 token 激活 8 个。注意力用 Gated DSA 稀疏注意力,官方 README 里明说了,"inspired by DeepSeek and GLM"。当年大家抄 Transformer,现在国产开源模型之间互相"借鉴"已经是明牌,DeepSeek 的稀疏注意力路线成了事实标准之一。模型还内置原生 MTP 层做投机解码,给了 FP8 量化版,vLLM 和 SGLang 都能直接部署。配置给得很全。

更特别的是,腾讯没晒公开榜单,给的是内部盲测:163 名内部专家,203 个工程任务,均分 2.99(满分 4),对 GLM-5.3 的 2.92 略胜(胜率 46.8%),对 Kimi K3 的 2.94 也略胜(胜率 51.2%)。出题、评分都是腾讯自己人。反正我见到"内部盲测"四个字,第一反应是找第三方数据。"进入开源第一梯队"可以信,"稳居第一"先打问号,净胜就 6 个百分点左右,同一档和领先一档是两回事。

真正抓眼球的是科研。官方给了三个案例,配合 Hyra 智能体:机器学习力场分子动力学模拟,32,512 原子的磷脂双分子层,提速 2 倍;低温量子输运器件设计,泄漏率从 48.2% 压到 4.8%;还有一道百年几何难题,三维 Blaschke-Lebesgue 问题,把体积下界从 0.380799 推进到 0.41104,离 Meissner 猜想值 0.41986 只差 2% 左右,还附了完整的证明文档。说实话,看到"百年几何难题"这几个字我愣了一下。

不过话说回来,这些成果都没经过同行评审,证明文档可查,但"可查"不等于"成立"。厂商自报的科研突破,惯例是先打个折再看。但方向值得注意:模型开始从"分析数据"走向"参与证明"了。不管这次水分有多少,光是这个信号就值得盯一阵。

腾讯这次押的也不是 API。定价输入 6 元、输出 18 元每百万 token,不算便宜,真正的重心在产品协同:CodeBuddy、WorkBuddy、元宝、ima 全线接入,训练数据跟内部软工、游戏、金融、安全专家共建。这很符合腾讯的打法:它不缺场景,缺的是把场景喂给模型。开源是姿态,自家产品用上才是目的。

官方自己倒是很坦白:这是早期版本,预训练和后训练都还有提升空间,已知问题包括复杂任务上思考时间过长、过度自我验证。延续的是 Hy3 preview 那套"先发出来挨骂,再迭代正式版"的打法。比起满嘴"遥遥领先",我确实更喜欢这种写法。

这个八月,开源旗舰一家接一家,竞争从"谁参数大"卷到"谁能在真实场景把活干完"。腾讯这份答卷不算惊艳,但姿态挺清楚:承认局限,晒内部数据,押注产品。至于那道几何题的证明到底成不成立,交给数学家们去验,我先观望。

## 信息来源

- [腾讯混元官方:Hy4 preview 发布](https://hunyuan.tencent.com/research/hy4-preview)
- [GitHub: Tencent-Hunyuan/Hy4-preview](https://github.com/Tencent-Hunyuan/Hy4-preview)
- [Hugging Face: tencent/Hy4-preview](https://huggingface.co/tencent/Hy4-preview)
- [第一财经:腾讯混元发布 Hy4 preview(2026-08-28)](https://www.yicai.com/news/103338434.html)
- [新浪科技:腾讯混元 Hy4 preview 发布并开源(2026-08-28)](https://finance.sina.com.cn/roll/2026-08-28/doc-inipwaiv5706885.shtml)
- [ChooseAI:腾讯混元开源 Hy4 preview 拆解(2026-08-28)](https://www.chooseai.net/news/6281/)
- [DataLearner:Hy4 preview 模型页(定价与评测)](https://www.datalearner.com/ai-models/pretrained-models/hy4-preview)
