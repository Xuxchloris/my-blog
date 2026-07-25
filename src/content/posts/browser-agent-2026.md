---
title: "浏览器即 API：2026 年，AI Agent 正在接管你的浏览器"
published: 2026-07-25
description: "从 browser-use 到 UI-TARS，AI Agent 通过浏览器操控万物的时代来了。聊聊这股浪潮背后发生了什么，以及它为什么重要。"
tags: [AI Agent, 浏览器自动化, 开源, 技术趋势]
category: 技术
draft: false
---

前几天翻 GitHub 趋势榜，被一个数字吓了一跳。

browser-use，一个让 AI Agent 操控浏览器的 Python 库，已经 **106k stars** 了。更吓人的是它的增长速度——去年底才几千星，半年多冲到了十万级。

同一时间，字节跳动的 UI-TARS-desktop 拿了 38k stars，OpenCLI 把任意网站变成命令行也有 27k，Nanobrowser 靠一个 Chrome 扩展做到 13k。这些东西指向同一个方向：**2026 年，浏览器正在成为 AI Agent 的操作系统**。

## 这事儿为什么突然火了

先说我自己的感受。过去两年，大家一直在讨论怎么让 AI 跟真实世界交互。API 是一条路，但大部分服务没有 API——或者有，但文档过时、限流、要申请权限。Slack 的 API 挺好用，但银行的网银呢？公司的 OA 呢？政府网站呢？

这些地方，人类用户靠浏览器访问。AI 为什么不能？

Browser-use 的思路就是这个。给 AI 一个浏览器，让它像人一样看屏幕、点按钮、填表单。听着简单，做起来全是坑。

技术上的突破其实来自多模态模型。2025 年以前，让 AI"看"网页基本靠解析 HTML，准确率凑合，但遇到 JavaScript 渲染的页面就抓瞎。2025 到 2026 年，GPT-5、Claude Opus 4、Gemini 3 Pro 这些模型在视觉理解上的进步，让 AI 直接截图加理解成了可行方案。

Browser-use 在 Odysseys 排行榜上拿了 **70.4% 的平均分**——200 个真实浏览器任务，超过了 OpenAI、Anthropic、Google、Microsoft 的同类产品。他们还搞了自己的专用模型 bu-2-0，专门优化浏览器操控场景。

## 不只是自动化测试这么简单

很多人听到"浏览器自动化"，第一反应是测试。Selenium 和 Playwright 不早就干这个了吗？

区别在于，以前的自动化框架是写死的脚本——"点这里，等三秒，输入那个"。AI Agent 的浏览器操控是动态的：它看到页面，理解内容，然后决定下一步。页面结构变了？没事，它重新理解就是了。

这就打开了很多以前做不了的事。

数据采集是第一个用例。以前爬网页靠 XPath 和正则，遇到反爬就头疼。Browser-use 的做法是让 Agent 像人一样浏览，看到什么提取什么。他们的 demo 里有个例子让 Agent 去提取关注者列表导出 CSV——传统爬虫要写一堆适配代码才能搞定。

QA 测试也在变。"帮我对这个本地网站做 QA 测试，报告 bugs、可用性问题、视觉不一致"——这是 Browser-use 官方的一个示例 prompt。Agent 真的会打开页面，一个个功能点去试。不需要写测试用例，自然语言描述就行。

最离谱的是求职。有人写了脚本让 browser-use 自动在招聘网站投简历、填表单。我猜 HR 系统还没准备好迎接一群 AI 同时投递。

## 几个有意思的趋势

各家走的路子不太一样。

Browser-use 走 Python 库路线，给开发者最大的灵活性。你可以在自己的代码里 import browser-use，用任何 LLM 驱动它。他们还做了 Cloud API，让生产环境规模化部署更省心。

UI-TARS-desktop 走桌面应用路线，更像一个"AI 助手"产品。它的核心是字节自研的 UI-TARS 多模态模型，专门为 GUI 理解优化过。你可以让它操作你的电脑，不只是浏览器。

OpenCLI 的思路更清奇——把网站变成命令行。你用自然语言描述要做什么，它转成 CLI 命令执行。这其实解决了 Agent 最头疼的一个问题：什么时候该用浏览器，什么时候该用 API？OpenCLI 的回答是：你不需要关心，工具帮你选。

另一个有意思的事是 MCP 生态正在跟浏览器操控合流。

MCP 协议是 Anthropic 推的，现在基本成了事实标准。Browser-use 提供了 MCP server 集成，让 Agent 通过 MCP 调用浏览器能力。MCP-Chrome 项目有 12k stars，它是个 Chrome 扩展，让 Agent 通过标准 MCP 协议控制浏览器。

这意味着 Agent 框架不用操心"怎么操控浏览器"了。MCP 往左连各种工具，往右连各种 Agent 框架。浏览器只是其中一个工具，跟发消息、查数据库、调 API 平起平坐。

最后，开源的势能真的太猛了。Superpowers 框架 260k 星，browser-use 106k 星，LangChain 142k 星。2026 年 AI 开源生态已经不是"社区驱动"了，是"社区狂奔"。Browser-use 刚发布的 0.13.6 版本引入了 Browser Harness，社区贡献者在 GitHub 上提了 5200 多个 PR。这种迭代速度，任何商业产品都跟不上。

## 当然也有让人发愁的地方

让 AI 操控浏览器，最让人怕的就是它会不会在某个页面不小心点了一个"确认删除"按钮。Browser-use 的解法让用户先肉眼确认 Agent 的操作计划——类似自动驾驶的 L2 级别，AI 开，人盯着。但这样一来，效率最终还是被人卡住了。

网站也越来越聪明。Cloudflare、reCAPTCHA、行为分析——它们不区分是人类还是 AI，只看操作"异常"不"异常"。Browser-use 搞了隐身浏览器、代理轮换来应对，但这是猫鼠游戏，不会停。

还有一件事还没人认真聊——品牌和信任。如果你的网站在被 AI Agent 批量访问，你是欢迎还是拒绝？GitHub 怎么看待 AI 替人提 PR？电商平台接不接受 AI 帮你比价下单？这些规则目前基本是空白。我估计几年内会有不少官司打。

## 所以

浏览器即 API 这个趋势，本质上是 AI 对现实世界的"兼容层"。

我们不可能要求所有网站和服务都提供完美的 API。没有 API 的网站，在 AI 眼里就是"不兼容"的。浏览器 Agent 做的就是在这层不兼容上加一个适配器——让 AI 像人类一样使用网络。

技术上，这个方向已经跑通了。Multi-agent 框架在浏览器里协作，一个 Agent 做数据提取，一个做页面导航，一个负责验证结果——Nanobrowser 和 magentic-ui 已经实现了这种架构。

剩下的不是技术问题，是信任和治理。这往往更花时间。

但方向已经很清楚了。下次你在浏览器里手动填表单的时候，可以想想——也许明年这个时候，这件事就交给 Agent 去做了。

---

*参考：*
- *Browser-use GitHub (106k stars, Apache 2.0)*
- *Browser-use 0.13.6 发布说明 (2026.7)*
- *UI-TARS-desktop GitHub (字节跳动, 38k stars)*
- *OpenCLI GitHub (27k stars)*
- *Nanobrowser GitHub (13k stars)*
- *Odysseys Benchmark 排行榜*
- *Superpowers 框架 (obra, 260k stars)*
- *MCP 协议规范与 MCP-Chrome 项目*
