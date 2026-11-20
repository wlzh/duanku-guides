# AdsPower 指纹浏览器自动化实战：Local API+MCP+CLI 告别环境配置重复劳动，多账号隔离｜账号星球 AccountBoy 批量账号一站解决

AdsPower Local API 提供了比较完整的环境管理接口，可以通过代码批量完成：创建、修改、删除、查询浏览器环境；启动、关闭和检查环境运行状态；配置浏览器指纹、User-Agent、代理 IP 等参数；创建和管理环境分组，调整环境归属；批量读取环境信息，维护已有配置。

> 完整图文与持续更新版本：[AdsPower 指纹浏览器自动化实战：Local API+MCP+CLI 告别环境配置重复劳动，多账号隔离｜账号星球 AccountBoy 批量账号一站解决](https://869hr.uk/2026/tech/adspower-local-api-mcp-cli-config-accountboy/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/adspower-local-api-mcp-cli-config-accountboy/
- 更新：2026-11-14
- 分类：技术
- 专题：技术、AI
- 关键词：AdsPower、指纹浏览器、浏览器自动化、Selenium、Puppeteer
- 视频：https://www.youtube.com/watch?v=s8huUBAJwQ4

## 正文

<!-- 文章摘要 -->
> 
做浏览器自动化，脚本写好了，浏览器批量启动、账号环境隔离、代理 IP 配置才是真正的重复劳动。这期以 AdsPower 指纹浏览器为主线，完整讲清楚开发者怎么把这些工作交给工具：...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=s8huUBAJwQ4)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 19 分钟。

## AdsPower 指纹浏览器自动化：告别环境配置重复劳动，账号来源一并解决

## 本期重点

做浏览器自动化的开发者，最容易低估的往往不是写脚本，而是脚本之外的环境问题：浏览器批量启动、账号环境隔离、代理 IP 配置，环境一多，光配置和维护就要吃掉大把时间。这期视频以 AdsPower 指纹浏览器为主线，讲清楚它怎么通过 Local API、MCP Server、CLI 和 Skill 把这些重复工作交给工具，中途还会穿插介绍账号星球 AccountBoy，解决多账号运营里另一个老大难：号从哪来。适合写爬虫和自动化脚本的开发者、用 Claude Code 或 Cursor 这类 AI 编码工具的程序员，以及做跨境多账号运营的团队。

## 痛点场景

做过爬虫或浏览器自动化的人，多半遇到过同一种崩溃：脚本在本地调试一切正常，一开多任务就开始报错。代码检查了一遍又一遍，最后发现问题根本不在代码，而是出在浏览器环境上——多个任务共用一套浏览器数据，Cookie、缓存、登录状态互相污染，轻则任务失败，重则账号被风控。这也解释了为什么环境隔离是批量自动化的第一道坎。

## 指纹环境

AdsPower 是一款指纹浏览器，核心思路是给每个自动化任务创建独立的浏览器环境。每个环境都有固定的指纹配置，Cookie、LocalStorage、缓存等数据分开保存，还可以单独绑定代理 IP，从根上避免多个任务共用一套浏览器数据。举个例子，你要同时运行 50 个网页采集任务，可以给每个任务分配固定的 AdsPower 环境，再通过 API 启动指定环境，让 Selenium、Puppeteer 或 Playwright 接进来执行任务。脚本跑完后，环境配置和已有登录数据都保留着，下次直接启动对应环境接着用，不用从头养号。而且环境创建、启动、关闭、指纹修改、代理配置这些操作全部开放给了 Local API，后面会展开讲。

AdsPower 指纹浏览器的独立浏览器环境界面

## AI 编码

现在不少开发者已经习惯用 Claude Code、Cursor、Codex 写代码、改 Bug，甚至直接把开发任务交给 AI。但想让 AI 帮忙创建浏览器环境、配置代理、修改指纹，通常还得自己写一层接口调用逻辑。AdsPower 现在提供了官方 CLI 和 Skill，可以把浏览器环境管理能力直接接入这些主流 AI 编码工具，让 AI 原生调用，省掉自己封装的功夫。

AdsPower 官方 CLI 与 Skill 接入 AI 编码工具的介绍页

## 指令示例

接入之后，你只需要用自然语言下指令，比如：帮我创建 10 个浏览器环境，使用不同的随机指纹；把这批环境移动到新的分组，检查代理配置；查询当前运行中的浏览器环境，关闭指定环境；修改这几个环境的浏览器指纹配置。AI 就能根据指令调用 AdsPower 对应的工具，完成环境管理操作。开发者不用再为了每个基础功能单独写一层接口适配代码，环境管理变成了一句 prompt 的事。

在 AI 编码工具中用自然语言管理 AdsPower 环境的示例

## 接入选择

三条通道怎么选，看你的使用习惯：习惯终端的开发者，CLI 比较顺手；如果已经在 Claude Code 或 Cursor 里搭建了 AI Agent 工作流，可以优先考虑 MCP 和 Skill，跟现有工作流结合得更紧。三种方式并不互斥，可以先从一条上手，再按需扩展。

CLI、MCP、Skill 三种接入方式的对比说明

## 配置入口

接入过程也不复杂。AdsPower 客户端提供了「API & MCP」配置入口，选择对应的 MCP、Skill 或 CLI，复制配置代码，再添加到 AI 工具里就行，不需要手动改一堆配置文件。官方帮助中心也有 MCP 的配置文档，照着走一遍就能跑通。

AdsPower 客户端的「API & MCP」配置入口页面

## 老脚本

很多开发者手里已经有一套跑了很久的自动化脚本：Python 加 Selenium、Node.js 加 Puppeteer，或者用 Playwright 做浏览器测试和数据采集。换一套浏览器环境，最担心的就是脚本要大改。AdsPower 的 Local API 可以直接对接这三类主流框架：启动指定浏览器环境后，接口会返回调试信息——Selenium 拿到浏览器调试地址，配对应版本的 WebDriver 连接；Puppeteer 拿到 WebSocket 调试端点；Playwright 通过 CDP 连接 Chromium 环境。按官方文档，Local API 的默认本地服务地址是 http://local.adspower.net:50325 ，调用启动接口就能拿到这些连接参数。比如原来用 Playwright 自动打开网页、填表单、读数据，现在只需先通过 Local API 启动环境，再让 Playwright 连接返回的 CDP 地址，页面操作和数据处理的代码大部分照旧，主要调整浏览器的启动和连接方式。对同时管理多个网站账号、执行批量网页操作的项目来说，每个任务绑定指定环境，Cookie、缓存和登录状态分开保存，任务之间互不干扰。

AdsPower Local API 对接 Selenium、Puppeteer、Playwright 的说明

## 号从哪来

不过，多账号自动化还有个前置问题：手里得先有一批号。自己注册海外账号，难受的地方做过的人都懂——想下载某个海外 App 或游戏，没有对应地区的苹果 ID，自己注册要海外手机号和支付卡，还经常卡在支付方式一步；想订 ChatGPT Plus、Claude Pro、Gemini Advanced，海外信用卡这一关就挡住了大多数人；做外贸、跨境私域运营，需要批量、稳定地获取 Telegram、Facebook、WhatsApp 账号，自己注册存活率极低，一批号养一周死一半；想看 Netflix、Disney+、充值 Spotify，国内支付渠道完全不通；Giffgaff 这类海外实体卡被封后，连替代手机号都难找。这些需求的共同点是：商品是虚拟的、要求交付快、支付通道横跨中外、售后要有保障。这期穿插介绍的账号星球 AccountBoy，就是把这些痛点打包做成标准电商体验的平台。

## 账号星球

账号星球 AccountBoy（[本片入口 accboy7gxjdian.acceboy.com](https://accytbgxjdian.acceboy.com/)）是一个跨境数字商品的一站式交易平台，主打「即时交货、发货时间少于 5 分钟」的自动化发卡模式。首页顶部导航把流量最大的品类直接做成一级入口：Gemini AI 账号、ChatGPT 账号、苹果 ID、苹果礼品卡、TikTok、Telegram、Facebook、推特、Gmail、AI 智能专题。导航下方是四条平台承诺：即时交货，发货少于 5 分钟，卡密账密自动发放；官方口径全球超一百万用户信任；支付安全快捷，支付宝、微信、币安三条通道；24 小时在线客服。要提醒的是，这个站需要海外网络才能访问，国内直连部分线路打不开属于正常现象，挂上代理再进即可。

账号星球首页导航与四条平台承诺

## 类目货架

站内类目栏一共 11 个入口：推荐、苹果 ID、社交账号、邮箱账号、影音会员、办公学习、AI 工具、系统工具、游戏账号、礼品卡密、海外手机卡。跨境数字商品的基本盘基本全覆盖，从下载海外 App 要用的区号 ID，到运营矩阵要用的社交账号、邮箱，再到流媒体和 AI 订阅，逛一圈类目就能对它卖什么有数。

账号星球类目导航栏

## 热门商品

热门商品区是全站销量的晴雨表。实拍时 Top 8 分别是：苹果美国 ID 22.8 元起、推特新号 20 元起、Telegram 美/加手机接码直登号 9.9 元起、TikTok 新号 15 元起、谷歌全区服 ID 17.8 元起、Instagram 新号 10 元起、Facebook 新号 15 元起、Netflix TV 30 天会员 28 元起。低价刚需品（ID、社交号）和订阅类（流媒体）撑起了主要流量，价格区间也能看出这是个走量的平台。

账号星球热门商品区与实拍价格

## AI 订阅

对看这期视频的开发者来说，AI 工具区可能是最实用的板块：ChatGPT Plus 独享 30 天 19 元起、Gemini AI Pro 30 天 30 元起、Grok Premium 4X 代充 19.9 元起、Claude Pro 代充 36 元起、Suno Pro 共享 39.9 元起、DeepL Pro+ 29.9 元起。以 ChatGPT 为例，实拍时 Plus 月会员代充原价 199 元、到手 149 元，Pro 5X 到手 766 元，Pro 20X 到手 1469 元，和官方 20 美元的汇率价基本持平，但它把「海外信用卡」这一关直接替你解决了——对没有外币卡的用户，这就是从买不了到能买的差别。交付形态分两种：平台账号是给你成品号，代充是你提供自己的账号、平台帮你充值订阅。

账号星球 AI 工具货架与价格

## 批量采购

批量需求它也有现成方案。以 Telegram 为例，SKU 细分到注册时长和组合形态：美国/加拿大手机接码直登号 37 元，直登号加汉化包 41 元，注册满半年老号 49 元、满一年 59 元，新手组合包 47 元，推特新号加电报直登的组合包 44 元。所谓手机接码直登，是购买后拿到手机号和接码网址，验证码通过接码网址收取。商品详情里的风控提示写得也很实在：接码网址有效期 1 个月、验证码一次性使用、每获取一次验证码风控增加一次、首登必须手机端、建议登录后尽快绑定邮箱——这些是 Telegram 官方风控的真实约束，照说明操作能省很多售后麻烦。邮箱类目还有面向 B 端的批量采购入口，5 元起，谷歌邮箱 30.8 元起、微软全球邮箱 24.8 元起，用户评价里不少邮件营销买家在长期复购。

Telegram 商品页的 SKU 细分与风控提示

## 支付结算

支付是国内用户最关心的一环，结算页提供三个通道：支付宝，带随机立减、最高 18.8 元；微信支付，加收 20% 手续费；币安 USDT，无额外手续费标注。结论很清晰：能用支付宝就用支付宝，既没有微信的附加费，还能吃随机立减；手里有 USDT 的话币安通道也很干净。费用结构完全透明，订单金额、优惠合计、商品折扣、手续费、应付五项摆在台面上，不会出现最后一步加价的套路。而且支持游客下单，不登录也能买，填一个收货手机号或邮箱接收卡密就行。售后方面：退款原路退回、零手续费；每个商品页都挂着「错误包换」标签，发出来的账密有问题就换到能用为止；账号类、邮箱类商品自购买日起 3 天售后期，质量问题免费更换。

账号星球结算页的三种支付方式与费用提示

## 生态联动

有意思的是，账号星球的合作伙伴页面上，能直接看到它和 AdsPower 的官方联动——一边供给账号资源，一边管理浏览器环境，账号加环境本来就是跨境多账号运营的一体两面。也就是说，从账号星球批量拿号，再放进 AdsPower 的独立指纹环境里分号运营，正好拼成一条完整的工作流。最后把风险也讲在前面：平台免责声明写明购买商品必须遵守各国法律和各平台规则，各平台用户协议普遍禁止账号交易，被官方风控、封禁、回收，平台不兜底；虚拟商品发货后不支持退款（商品本身问题除外），下单前把 SKU 说明读完；海外账号的使用期限以官方风控为准，长期自用的正确姿势是拿到账号第一时间改密、换绑邮箱、保持活跃；另外账号星球有多个相似域名在流通，走本片入口进站、付款前核对清楚落地页，防止仿冒站。

账号星球合作伙伴页与 AdsPower 的生态联动

## 批量管理

回到 AdsPower 这条主线。号有了、环境隔离的思路有了，剩下的就是规模化管理。写自动化脚本不算麻烦，给 100 个浏览器环境挨个配置代理、修改指纹、整理分组，才是真正考验耐心的工作。AdsPower Local API 提供了比较完整的环境管理接口，可以通过代码批量完成：创建、修改、删除、查询浏览器环境；启动、关闭和检查环境运行状态；配置浏览器指纹、User-Agent、代理 IP 等参数；创建和管理环境分组，调整环境归属；批量读取环境信息，维护已有配置。有固定业务流程的团队，还可以把常用环境配置保存成 JSON 模板，用脚本统一生成环境，以后遇到类似项目直接复用配置、改改参数就行。

## 无头模式

有些自动化任务需要长期运行，比如定时采集网页数据、检查网站状态、按固定时间执行一批网页操作。如果每次都要人工打开客户端、启动环境、再跑脚本，维护起来很麻烦。AdsPower 支持 Headless 无界面模式，不显示浏览器窗口也能执行自动化任务。开发者使用 API Key 和对应启动参数，在 Headless 模式下启动服务，再通过 Local API 控制浏览器环境。对部署在服务器上的项目特别友好：把浏览器任务交给 Python 脚本，通过定时任务或现有业务流水线触发，就能按计划执行网页操作。

AdsPower Headless 无界面模式的说明

## RPA

还有一类需求：任务本身不复杂，但重复性极高，人工点来点去很占时间，而业务人员又不会写代码。AdsPower 内置的 RPA 自动化可以通过可视化方式搭建流程，或者直接用模板商店里的现成流程，像网页访问、表单填写、重复点击这类固定操作，不会写代码也能搞定。这让运营团队可以自己消化一部分简单自动化需求，开发资源留给真正需要技术投入的项目。

AdsPower RPA 可视化流程与模板商店

## AI 代理

再进一步是 AI Agent：直接用自然语言描述任务，让 AI 协助执行浏览器操作。比如创建指定数量的环境、检查代理连接情况、按规则执行网页操作，描述清楚需求就行。AI Agent 同时支持接入 MCP 和 Skills，开发者可以按实际需求扩展它能调用的工具。

AdsPower AI Agent 用自然语言执行任务

## 定时任务

对于每天都要重复执行的任务，还可以设置定时运行，支持仅一次、每天、每周、每月等频率，运行结束后能查看执行记录。定时加 Agent，相当于把一批固定网页操作完全托管出去，出错也能从执行记录里回溯。

AdsPower 定时任务的频率设置与执行记录

## 开源文档

开发者选工具，除了看功能，还会关心文档全不全、出了问题能不能自己排查。这块 AdsPower 做得比较开放：GitHub 上公开了 Local API 示例代码、MCP Server 和 CLI 相关项目，其中 MCP Server 提供 TypeScript 和 Python 两种实现，可以按现有技术栈选，也能直接看代码了解接口调用方式；Local API 有独立文档，包含请求参数、返回字段和脚本样例，官方仓库还提供 Python、JavaScript 示例方便对照接入。遇到浏览器启动失败、接口参数错误、框架连不上的问题，可以结合 API 返回信息、文档和源码排查。注意不同客户端版本支持的 API 可能有区别，正式接入前先确认客户端版本、API 权限和运行依赖。

AdsPower 在 GitHub 公开的 Local API、MCP 与 CLI 项目

## 上手路线

如果以前没接触过 AdsPower，建议从自己熟悉的工具入手：已经在用 Selenium 或 Playwright 的，先创建一个测试环境，开启 Local API，用返回的调试地址连接浏览器，确认现有脚本能正常执行；经常用 Claude Code、Cursor、Codex 的，试试官方 MCP Server 或 Skill，先让 AI 做查询环境、创建环境、配置代理这类简单任务，再逐步接入工作流；需要管理大量环境的，用 Local API 写批量创建、修改、查询脚本，把重复配置统一处理；想把自动化交给运营团队的，从 RPA 模板或 AI Agent 起步，先跑通几个常用流程。另外它有永久免费版，环境数量有限，具体以官网价格页为准；注册下载可以直接用本片链接，正式接入前记得确认账号的 API 使用权限和当前套餐限制。

## 要点回顾

总结一下这期的内容。对开发者来说，最费时间的往往不是高难度技术，而是那些重复处理的小事：给浏览器配代理、维护账号环境、改脚本连接方式、反复搭同一套运行配置。AdsPower 用 Local API、MCP Server、CLI、Skill、RPA 和 AI Agent 把这条工具链补全了：老脚本不用大改就能接入，AI 工作流有现成通道，不会写代码的同事也有 RPA 兜底。而多账号运营的前置问题——号从哪来——账号星球用十大类目、5 分钟自动发货、支付宝直付加错误包换给出了一个答案，两者组合正好是「账号资源加环境管理」的完整闭环。最后的合规提醒：账号交易本身受各平台规则约束，工具再顺手，也要用在正当用途上。

## 资源链接

- AdsPower 注册下载（本片链接）：https://www.adspower.net/share/211mj3
- AdsPower Local API 官方文档与代码示例：https://localapi-doc-en.adspower.com/docs/K4IsTq
- AdsPower MCP 配置帮助：https://help.adspower.com/docs/MCP
- GitHub：[AdsPower/localAPI](https://github.com/AdsPower/localAPI)（Local API 示例代码）
- GitHub：[AdsPower/local-api-mcp-python](https://github.com/AdsPower/local-api-mcp-python)（MCP Server Python 实现）
- GitHub：[AdsPower/adspower-browser](https://github.com/AdsPower/adspower-browser)（AdsPower Skill & MCP & CLI，TypeScript 实现）
- 账号星球 AccountBoy（本片链接）：https://accytbgxjdian.acceboy.com/

## 关注频道

以上就是这期的全部内容。如果觉得有帮助，欢迎关注短裤AI分享，评论区聊聊你在浏览器自动化上踩过的坑，我们下期见。

做浏览器自动化，脚本写好了，浏览器批量启动、账号环境隔离、代理 IP 配置才是真正的重复劳动。这期以 AdsPower 指纹浏览器为主线，完整讲清楚开发者怎么把这些工作交给工具：

· 指纹环境：每个任务独立浏览器环境，Cookie/缓存分开保存，单独绑定代理 IP，50 个采集任务并行互不干扰

· AI 编码接入：官方 CLI + Skill 接入 Claude Code、Cursor、Codex，一句话创建环境、改指纹、查代理

· 老脚本迁移：Local API 对接 Selenium（调试地址+WebDriver）、Puppeteer（WebSocket）、Playwright（CDP），原有代码大部分照用

· 批量管理：环境创建/启动/关闭/指纹/代理/分组全部 API 化，JSON 模板复用

· Headless 无头模式：服务器定时任务长期运行

· RPA + AI Agent：不会写代码也能做自动化，支持定时执行

· GitHub 开源：Local API 示例 + TypeScript/Python 双版 MCP Server

中间穿插介绍账号星球 AccountBoy：跨境数字商品一站式交易平台，苹果 ID、ChatGPT Plus/Claude Pro/Gemini 代充、Telegram/推特/Facebook 社交账号、海外邮箱、流媒体、礼品卡、海外手机卡十大类目，5 分钟自动发货，支付宝/微信/币安三种支付，错误包换——自己注册海外账号的痛（海外手机号、外币卡、存活率）它都有现成方案，配合 AdsPower 独立指纹环境就是「账号资源+环境管理」的完整闭环。

AdsPower 注册：https://www.adspower.net/share/211mj3

账号星球入口：https://accytbgxjdian.acceboy.com/

合规提醒：账号交易受各平台规则约束，请用于正当用途。

📎 本视频涉及资源：
- AdsPower/localAPI: https://github.com/AdsPower/localAPI
- AdsPower/local-api-mcp-python: https://github.com/AdsPower/local-api-mcp-python
- AdsPower/adspower-browser: https://github.com/AdsPower/adspower-browser
- 的默认本地服务地址是: http://local.adspower.net:50325
- 相关链接: https://localapi-doc-en.adspower.com/docs/K4IsTq
- 相关链接: https://help.adspower.com/docs/MCP

注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有 🔗https://869hr.uk

## 关注与资源

1. 微信讨论群：https://qr.869hr.uk/aitech
2. 超过100T资料总站网站：https://doc.869hr.uk
3. Telegram群聊：https://t.me/tgmShareAI
4. 微信公众号：搜“AI前沿的短裤哥”
5. 视频的文字博客(银行卡、手机号、VPS主机、IP测试等）：https://869hr.uk
6. 推特：https://x.com/gxjdian
7. Youtube：https://youtube.com/@gxjdian

## 短信及语音接码平台

- https://hero-sms.com/?ref=357885
- https://smspva.com/?ref=1307601

## 白嫖流量

- 500M试用， 链接 https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN ， 85 折优惠
- 200M试用，链接 https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码GXJDIAN， 9 折优惠
- eSIM各国纯净IP流量：https://www.redex.vip/zh?partnerId=31

## VPS 主机推荐

- 大坝的VPS优惠大超市｜VPS 优惠 · 低价年付 · 每日更新 https://vps.869hr.uk/
- Claude用的丽萨主机： https://lisahost.com/aff.php?aff=9424
- 按流量VPS https://www.lycheeip.com/home/ip?affId=1AwYIQ7BW8
- 一年 10 美元的多年保底小鸡， https://clients.zgovps.com/?affid=1207
- 各种云主机，主打性价比 https://my.racknerd.com/aff.php?aff=15809
- 美国的vps，一年 70 美金搞活动，https://app.cloudcone.com/?ref=13794
- 一年 8.5 美金的美国家宽，稳定靠谱：https://www.webshare.io/?referral_code=55vpv6waorud

VPS DMIT
- https://www.dmit.io/aff.php?aff=21728

VPS VIRCS
- 家宽 落地机https://www.vircs.com/welcome?vcd=61a4aae4
- 家宽IP链接：https://ipfly.net/activity/OE5TWVlUUEI6TFZKOVhYQzM5NQ==
- 住宅VPS链接：https://www.voyracloud.com/?ref_code=5ZG4FHL8

## 账号、礼品卡与 AI 产品充值

- https://accytbgxjdian.acceboy.com/
- https://universalbus.cn/?s=bvDplWi2fZ
- https://www.gamsgo.com/partner/jGh24
- Claude、OpenAI Codex等充值 https://bewild.ai?code=GXJDIAN

## eSIM 与支付卡推荐

1. Wise免出国极速开户全教程（身份证+国内手机号即可，完美平替香港卡！）https://youtu.be/AL8cOn49xG8 （申请链接https://wise.com/invite/ihpc/lizhiw12 推荐码：lizhiw12）
2. N26 的申请链接及教程链接 （需要护照， 推荐码：lizhiw02766c ） https://youtu.be/HY9OD8rX89s?si=78REb8MyKSJB6cwQ
3. Bybit支付卡申请链接 （推荐码：LGNQRG）https://youtu.be/3sN7P2t_CeA
4. YiKa虚拟卡实操开卡教程，不需KYC，一个邮箱开50张卡，订阅ChatGPT/Claude/推特蓝V出海必备 https://youtu.be/XaLeXKu4PTM
1. 三家eSIM 让国产手机秒变eSIM手机，全方面优缺点对比及开户链接🔗 https://s.869hr.uk/mcc
2. eSIM 9eSIM打 9 折（优惠码：maq）注册及购买链接 https://www.9esim.com/?coupon=maq
3. eSIM ESTK打 9 折（优惠码：GXJDIAN）注册及购买链接 https://store.estk.me/zh?aid=16007
4. eSIM XeSIM打 9 折（推荐码：gxjdian）注册及购买链接 https://xesim.cc/?DIST=RE5FHg==
5. eSIM卡免手机保号收发短信！几十块大疆4G模块爆改移远EC25，Mac UTM一键部署VoHive完整教程 https://youtu.be/PZRkoggXFco
6. 国行iPhone秒变eSIM！Xesim卡手把手喂饭教程，出国留学旅行必备 https://youtu.be/Mhd2KR8Ydo4

## YouTube 播放列表

- AI产品&技术相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海VPS相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=s8huUBAJwQ4)

---

## 相关推荐

- [手机端 Codex 新手入门教程](https://869hr.uk/2026/tech/api-mobile-codex-beginner-tutorial/)：AI 编码工具的移动端玩法，和本期的 Claude Code/Cursor 接入思路一脉相承
- [Claude/ChatGPT 订阅与虚拟卡支付教程](https://869hr.uk/2026/tech/chatgpt-0-starryblu-claude-v-card-tutorial/)：订阅海外 AI 工具被支付卡住的话，看这篇
- [Gmail 免费开通 ChatGPT/GPT 教程](https://869hr.uk/2026/tech/chatgpt-gmail-free-gpt-k12-plus-tutorial/)：海外邮箱注册 AI 服务的完整流程

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/adspower-local-api-mcp-cli-config-accountboy/)
