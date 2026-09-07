---
title: "他花了一年,给反爬虫闸门换上 WebAssembly"
published: 2026-09-07
description: "Anubis 作者 xe 复盘了给这个反 AI 爬虫工具加 WebAssembly 工作量证明的一年。里面有 LLVM 编译器 bug、50 个版本的 Chrome,还有用 AI 测试反 AI 闸门的黑色幽默。"
tags: [WebAssembly, Anubis, 反爬虫, 开源]
category: 技术
draft: false
---

昨天刷 Hacker News,看到一篇 332 分的帖子,标题就很实在:"It took a year to ship WebAssembly in Anubis"——给 Anubis 加个 WebAssembly,花了一年。

不太熟悉 Anubis 的话,简单说:它是加拿大公司 Techaro 做的开源反爬虫工具。现在很多独立开发者的小站会被 AI 爬虫薅到服务器冒烟,Anubis 的思路是给访客出一道工作量证明题,让你浏览器算几秒哈希再放行。你见过的那个"Making sure you're not a bot"页面,十有八九就是它。

作者是 xe(Xe Iaso),一个人扛着这个项目。这篇复盘我看得挺过瘾,比大多数技术文章都有意思。

## 为什么非要上 WebAssembly

原来的 SHA-256 挑战是 CPU 密集型,带来的矛盾很实际:难倒爬虫的同时,也把手机用户难倒了。xe 说他的开发机旁边常年放着一台 Moto G8 Power,一台老安卓,专门用来测试"Anubis 会不会把手机烤热"。

换成 WebAssembly 之后,挑战算法可以升级为 argon2id,内存密集型的那种。这有个很妙的副作用:你想让 Claude 给你"vibeslop 一个 CUDA 解题器"这条路,基本被堵死了——GPU 擅长算力,不擅长被内存带宽卡脖子。用他的原话说,这条路线"on its way to being fundamentally dead"。

另一个好处是客户端和服务器跑同一份二进制文件。注意,不是同一份代码,是同一个文件。以前 JavaScript 和 Go 各维护一份解题逻辑,改一处得同步两处,想想就头疼。

## 一年时间都花在哪了

主体功能几天就写完了,剩下 360 天全在填坑。几个坑我印象很深:

**Rust 标准库坑了他一把。** 他为了兼容老浏览器,用 -mvp 参数只保留 WebAssembly 最基础的特性。结果 Chrome 75 到 100 之间全部编译报错。查了半天发现,rustup 下载的标准库是预编译的,里面用了 reference types 这种新特性,你设的编译参数根本管不到它。

**职业生涯第一个编译器 bug。** 他在 CI 里做可复现构建,发现每次构建产物都会漂移大概 29 个字节。正常人到这一步会怀疑自己,他也一样,直到他发现关掉 ASLR 之后结果就稳定了——问题出在 LLVM 按内存指针顺序遍历异常处理块,地址随机化导致每次编译产物不一样。这是 LLVM 的真 bug(编号 204883),他自己挖出来的。他说干这行这么多年,默认假设永远是"编译器没问题,是我的输入有问题",这次算是破例了。

**为了测试,他建了个浏览器农场。** Anubis 要支持到 Chrome 75,因为大量安卓手机、智能电视被锁死在老版本上,没有升级通道。他写了个叫 chromesweep 的测试工具,一次拉起几十个不同版本的 Chrome 去访问测试实例,每个 Chrome 还套在 Kata 容器微虚拟机里,配好网络策略——老版本 Chrome 本身就是安全漏洞集合体,得当危险品处理。

最讽刺的细节在这:他调 wasm-opt 参数的时候,开了一个 Claude Opus 和 GLM 5.2 的循环去做模糊测试。用 AI 来打造拦 AI 爬虫的闸门,这大概就是这个时代软件开发的日常。

还有个彩蛋,文章末尾他特意声明:本文行文未使用 AI,草稿放在 Google Docs 里,每个字都能查到是谁打的。在一个反 AI 爬虫的项目里写这句话,很难说是巧合。

## 我的一点想法

看完最大的感触是,这类工作的成本和它获得的回报完全不成比例。xe 自己都说,做这种事"tireless and thankless",累且没人谢。很多人拿 Anubis 跟 Cloudflare、AWS WAF 相提并论,但那两边是几千人团队,这边基本是一个人加一台会发热的办公室。

另一点是,工作量证明这个东西转了一圈又回来了。Hashcash 当年是为了反垃圾邮件设计的,后来变成比特币的基石,现在又回来保护小博客不被爬虫啃。技术没有新故事,只有老工具的新岗位。

xe 在文里抱怨了一句,说他给这些老 Chrome 做的安全防护,比大厂给 AI Agent 测试环境做的还用心。这话酸,但可能没说错。Agent 时代大家都在狂奔,基础设施的安全水位反而被一个人维护的开源项目衬托出来了。

Anubis v1.28.0 会带着这套 WebAssembly 挑战发布,默认关闭,v1.29.0 再考虑默认开启。如果你也维护着一个被 AI 爬虫骚扰的小站,值得去试试。

---

**信息来源:**

- [It took a year to ship WebAssembly in Anubis](https://anubis.techaro.lol/blog/2026/anubis-wasm/) - xe,2026-09-06
- [Hacker News 讨论帖](https://news.ycombinator.com/item?id=49588080)
- [LLVM issue #204883](https://github.com/llvm/llvm-project/issues/204883)
- [Anubis 项目仓库](https://github.com/TecharoHQ/anubis)
