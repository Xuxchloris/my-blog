---
title: "有人想让 AI 写的代码必须自证清白：聊聊 Bend 2"
published: 2026-09-18
description: "一个叫 Bend 的新语言冲上 HN 头版，它的卖点很狠：AI 写的代码必须通过数学证明才能合并。我看了它的官网和评论区，觉得这想法有意思，但坑也挺深。"
tags: [编程语言, AI编程, 形式化验证, 开源项目]
category: 技术
draft: false
---

昨天 Hacker News 头版上蹲着一个项目，叫 Bend 2，标题起得很直接：一个通过证明来阻止 AI 犯错的语言，CPU 和 GPU 上都能跑。几个小时冲到 460 多分，200 多条评论。

我去翻了一下，越看越觉得这事儿值得写，因为它戳中的是我最近一直在想的问题：当代码是 AI 写的、你根本没读过，你凭什么信它。

## 它到底想解决什么

Bend 的作者 Victor Taelin 是那种老派硬核语言玩家，之前搞过 HVM，做交互组合子那套东西。这次 Bend 2 的定位挺敢说，官网上大意是：以后人类会慢慢不读不写代码了，但还是得有个没歧义的办法，告诉 AI 我们到底想要什么。

他的答案是两层，**laws**（法则）和 **proofs**（证明）。

你在一个叫 `LAWS.bend` 的文件里声明几条不能破坏的规则，比如"棋局中不可能获胜"。之后每次改动，Bend 都会做类型检查——而它的类型检查器本身就是个证明检查器，跟 Lean、Rocq 是同一类东西。AI 要是改出违反法则的代码，合并这一步在数学上直接不可能。官网原话是"merging a bug is mathematically impossible: it is a theorem"。

我第一反应是：这不就是把 AGENTS.md 里那句"别犯错，乖"升级成了可编译的硬约束嘛。点子确实漂亮。现在大家都往 AGENTS.md 里塞人话规则，什么"不要删测试""保持向后兼容"，全靠模型自觉。Bend 换了个思路，把规则从提示词挪进了类型系统。

顺带说下性能。Bend 编译成原生代码，单核接近 C，同一个二进制扔到 16 核或者 GPU 上能快上百倍。有个细节我挺喜欢：它跑并行不需要你写线程、锁、kernel，一个 `!` 符号就把活儿撒到所有核上再收回来。编译出来的是一个 `.c` 文件，靠宏在 Metal 和 CUDA 之间切，作者说这是为了不用把 runtime 写三遍。

## 但评论区比官网好看

翻 HN 那 200 多条评论挺上头的，骂的和捧的都有料。

先说个最要命的：**法则本身可能是错的。**

用户 garrisonj 说得很损——"问题是我得先把法则 vibe code 出来，而法则本身可能是错的。"作者自己回了句"true"。然后 pdpi 讲了个具体的翻车现场：他试了官网那个"拆掉墙"的例子，结果 AI 把游戏改成斜向移动，还自作主张规定上下走正对角线、左右走负对角线。因为法则只写了"玩家不能赢"，AI 只要守住这一条就行，剩下的随便折腾。

作者也承认，"玩家不能赢"这个法则严重欠定义。他补了一句我挺认同的：

> laws 只保护你还记得写的那部分。它们不是银弹。但它们仍然极其有用，因为一条很小的法则就能挡住一整类 bug。

这正好是形式化验证的老毛病。drdrey 说得更不客气：写规格说明才是真正难的地方。你想拦住 AI 用最省事的办法绕过法则——比如干脆不让玩家动——就得再加一条"玩家必须能移动"。然后还得加"移动必须连续"，加"不能瞬移"。真实程序里这么搞下去基本没完。

还有个事，我是从评论里才知道的。

为了发 Bend 2，作者把仓库历史压成了一个 commit，之前的贡献者记录、benchmark 的 SHA 全没了。AlexErrant 直接开火：在这个 AI 时代信任才是硬通货，清空历史是拉警报的好办法。ModernMech 补刀更专业——你论文里报告了 benchmark 的 pinned SHA，转头又把历史删了，那别人怎么复现？

这个争议我挺能理解的。GitHub 上有 44 个贡献者、41 个人合过 PR，这些人一夜之间就"被消失"了。作者的解释是历史里混进了私人信息和专有代码。后来他在评论区说"Commit history is back!"——我去 API 查了下，现在是 2814 个 commit，确实恢复了。结局算是好的，但第一印象已经花了。

## 我怎么看

不看好它的理由很实际。写证明的前提是先有规格说明，而写规格说明的难度不亚于写代码本身。IshKebab 那句反问很难反驳——"你怎么形式化验证 Facebook？"AI 生成代码图的就是快，你让它在每次改动后跑一轮证明检查，哪怕 Bend 的检查只要一秒，后面那堆逻辑复杂度也是指数级往上走的。

但它戳中的那个点我认。整个行业现在正往"AI 自己写、自己合、自己发布"这条路上狂奔，可我们拿来把关的还是测试加上人眼扫一眼。Apple 前阵子发过一篇博客，讲他们用形式化验证去证明 corecrypto 内核里的加密实现——这种事以前是大厂才有资源干的奢侈品。Bend 的想法是把它压到"AI 每次改完顺手跑一下"的成本。

那 Bend 现在什么状态？我翻了翻它的 open issues，挺诚实的：C 和 JS 两条路径处理非法 UTF-8 的方式不一致、数组边界检查在不同后端行为不一样，还有个 issue 标题干脆写着"Guide 像 AI slop，我看不懂"。官网末尾自己也写着"Bend 还很年轻，出问题就开 issue"。这态度我挺喜欢，比上来就吹"生产可用"的强多了。

有一点得说清楚：Bend 不是"让 AI 不犯错"，是"让你声明的那部分错不了"。这两句差别很大。前者是营销，后者是能落地的工程约束。真正稀缺的从来不是证明能力，而是写得出好法则的人——你得先想明白系统里什么是绝对不能破的。这个本事 AI 现在给不了你。

所以 Bend 与其说是给 AI 用的工具，不如说是逼着开发者把脑子里那些模糊的"这样应该不行吧"，变成一条条明确的、机器能检查的条款。哪怕你永远不会用 Bend，光是把 law 写出来那半小时，可能就够你少吵后面好几顿架了。

---

参考来源：

- Bend 官网：<a href="https://bend-lang.com/" target="_blank" rel="noopener">bend-lang.com</a>
- GitHub 仓库（bendlang/bend）：<a href="https://github.com/bendlang/bend" target="_blank" rel="noopener">github.com/bendlang/bend</a>
- HN 讨论帖（468 分，200+ 评论）：<a href="https://news.ycombinator.com/item?id=49746163" target="_blank" rel="noopener">news.ycombinator.com/item?id=49746163</a>
- Apple 形式化验证博客：<a href="https://security.apple.com/blog/formal-verification-corecrypto/" target="_blank" rel="noopener">security.apple.com/blog/formal-verification-corecrypto</a>
- Bend 论文：GUIDE.md / paper/BendTT.pdf / paper/BendRT.pdf（仓库内）
- 仓库 issue 列表（文中提到的缺陷）：<a href="https://github.com/bendlang/bend/issues" target="_blank" rel="noopener">github.com/bendlang/bend/issues</a>
