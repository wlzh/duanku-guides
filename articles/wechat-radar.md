# WeChat Radar 微信群聊情报看板｜一键聚合群消息、话题、链接和趋势，本地运行零上传

介绍 WeChat Radar 本地优先的微信群聊情报看板，说明消息、话题、链接和高信号人物的聚合方式、技术栈、安装与数据边界。

> 完整图文与持续更新版本：[WeChat Radar 微信群聊情报看板｜一键聚合群消息、话题、链接和趋势，本地运行零上传](https://869hr.uk/2026/tech/wechat-radar/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/wechat-radar/
- 更新：2026-05-26
- 分类：技术
- 专题：技术
- 关键词：WeChat Radar、微信看板、群聊管理、开源项目、微信情报
- 视频：https://www.youtube.com/watch?v=mqk9ViLo4M8
- 系列：[基础软件与效率工具](../series/software-and-tools.md)

## 正文

<!-- 文章摘要 -->
> 
作者说：微信仪表盘开源了，为了避免风险，一天后转私有库，需要的尽快fork！！！...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=mqk9ViLo4M8)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 6 分钟。

作者说：微信仪表盘开源了，为了避免风险，一天后转私有库，需要的尽快fork！！！

WeChat Radar 是一个本地优先的微信群聊情报看板。它把群消息、话题、链接、@我的消息和高信号人物聚合成一个可按日期查看的工作台。

你得到的不是“聊天记录列表”，而是每天可以直接处理的情报：

* 今日优先看：消息、文章、工具、异动分区展示

* 话题雷达：用 Codex CLI 按天聚合跨群话题

* 链接情报：文章/工具资源去重，生成可读标题

* 群日报：每天活跃群可生成摘要报告，方便复制给 AI 继续处理

* 本地存储：聊天数据落到你自己的 SQLite，不上传到第三方服务

* 明暗主题：默认奶白色浅色主题，也支持深色模式
## 快速开始

git clone https://github.com/joeseesun/wechat-radar.gitcd wechat-radarpnpm installpnpm rebuild better-sqlite3pnpm dev

打开 [http://localhost:3000 ](http://localhost:3000/)。首次进入会跳到 `/setup` ，按页面提示填写你的微信名、确认隐私说明，也可以先启用 demo 数据体验。
## 前置条件

* macOS，且已登录微信 4.x

* Node.js 20+： `node --version`

* pnpm： `corepack enable && pnpm --version`

* wx-cli： `wx --version`

* wx daemon 正在运行： `wx daemon status`

* 如果要让话题聚合更好，安装并登录 Codex CLI： `codex --version`

wx-cli 可参考原项目安装与初始化： [jackwener/wx-cli ](https://github.com/jackwener/wx-cli)。
## 配置

默认数据目录是 `~/.wechat-radar/` ，不会写进项目目录。

你可以用环境变量覆盖：

cp .env.example .env.local

常用配置：

WECHAT\_RADAR\_DATA\_DIR=\~/.wechat-radarWECHAT\_RADAR\_MY\_NAMES=张三,San Zhang,zhangsanWECHAT\_RADAR\_DEMO=0WECHAT\_RADAR\_CODEX\_MODEL=

也可以直接在 `/setup` 页面配置。配置会写入 `~/.wechat-radar/config.json` 。
## 使用方式
1. 进入首页，选择日期或时间范围。
2. 点击“重扫”同步当前范围消息。
3. 点击“全量同步”拉取更长历史。
4. 打开“话题雷达”查看跨群主题。
5. 打开“链接情报”查看文章和工具资源。
6. 在活跃群列表点击“日报”查看单群日报。

你可以这样和 AI 配合：

* “把今天所有 Codex 相关话题整理成一篇博客大纲。”

* “复制这个群日报，帮我提炼值得回复的机会。”

* “把链接情报里的工具做成一张试用优先级表。”
## 数据与隐私

WeChat Radar 默认只在本机读写数据：

* `~/.wechat-radar/radar.db` ：SQLite 主数据库

* `~/.wechat-radar/config.json` ：本地配置

* `~/.wechat-radar/backups/` ：可选备份

安全设计：

* wx-cli 调用使用 `child_process.execFile` 参数数组，不拼 shell

* SQLite 使用 prepared statements

* 页面只以 React 文本节点渲染聊天内容

* 不把微信密钥、会话、数据库、模型缓存提交进仓库

提醒：这个项目会读取你本机微信数据。请确认你的使用方式符合微信客户端规则、当地法律、群成员隐私预期和你所在组织的合规要求。不要把包含真实聊天内容的数据库或截图上传到公开仓库。
## 项目结构

```plaintext
app/ Next.js App Router 页面与 API
components/ 看板、侧边栏、图表、消息渲染组件
lib/ wx-cli 封装、SQLite、话题/链接聚合逻辑
scripts/ 本地维护脚本
docs/assets/ README 图片与公开素材
```
## 常见问题
| 问题 | 解决方法 |
| ---------------------------- | --------------------------------------------------- |
| `wx daemon 未运行` | 先运行 `wx daemon start` ，再刷新页面。 |
| `better-sqlite3` native 模块报错 | 运行 `pnpm rebuild better-sqlite3` 。 |
| 首页没有数据 | 先完成 `/setup` ，确认 `wx sessions --json` 有输出，然后点击“重扫”。 |
| 话题雷达为空 | 打开对应日期会自动构建；也可以点击“构建话题”。需要本机可运行 `codex` 。 |
| 不想读取真实微信 | 在 `/setup` 勾选 demo 模式，或设置 `WECHAT_RADAR_DEMO=1` 。 |
## 致谢

* [jackwener/wx-cli ](https://github.com/jackwener/wx-cli)：本项目依赖它读取本机微信数据。

* [Next.js ](https://nextjs.org/)、 [ECharts ](https://echarts.apache.org/)、 [better-sqlite3 ](https://github.com/WiseLibs/better-sqlite3)。

***

项目链接： https://github.com/joeseesun/wechat-radar

WeChat Radar 是一个本地优先的微信群聊情报看板，把群消息、话题、链接和高信号人物聚合成可按日期查看的工作台。支持话题雷达、链接情报、群日报等功能，数据全部存在本地 SQLite，不上传第三方。开源项目，快 fork！

项目地址：https://github.com/joeseesun/wechat-radar

功能亮点：
- 今日优先看：消息、文章、工具、异动分区展示
- 话题雷达：用 Codex CLI 按天聚合跨群话题
- 链接情报：文章/工具资源去重，生成可读标题
- 群日报：每天活跃群生成摘要报告
- 本地存储：SQLite 存储聊天数据
- 明暗主题支持

注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有 🔗https://869hr.uk

## 短信及语音接码平台

- 或https://smspva.com/?ref=1307601

纯净住宅IP白嫖流量
- 500M试用， 链接 https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN ， 85 折优惠
- 200M试用，链接 https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码GXJDIAN， 9 折优惠
1. 微信讨论群：https://qr.869hr.uk/aitech
2. 超过100T资料总站网站：https://doc.869hr.uk
3. Telegram群聊：https://t.me/tgmShareAI
4. 微信公众号：搜“AI前沿的短裤哥”
5. 视频的文字博客(银行卡、手机号、VPS主机、IP测试等）：https://869hr.uk
6. 推特：https://x.com/gxjdian
7. Youtube：https://youtube.com/@gxjdian

## VPS 主机推荐

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

- https://accboy7gxjdian.acceboy.com/
- https://universalbus.cn/?s=bvDplWi2fZ
- https://www.gamsgo.com/partner/jGh24
- Claude、OpenAI Codex等充值 https://bewild.ai?code=GXJDIAN

## eSIM 与支付卡推荐

1. 三家eSIM 让国产手机秒变eSIM手机，全方面优缺点对比及开户链接🔗 https://s.869hr.uk/mcc
2. eSIM 9eSIM打 9 折（优惠码：maq）注册及购买链接 https://www.9esim.com/?coupon=maq
3. eSIM ESTK打 9 折（优惠码：GXJDIAN）注册及购买链接 https://store.estk.me/zh?aid=16007
4. eSIM XeSIM打 9 折（推荐码：gxjdian）注册及购买链接 https://xesim.cc/?DIST=RE5FHg==
5. wise的申请链接及教程链接（有身份证就可，推荐码：lizhiw12） (教程链接https://x.com/wlzh/status/19967997897...) （申请链接https://wise.com/invite/ihpc/lizhiw12）
6. N26 的申请链接及教程链接 （需要护照， 推荐码：lizhiw02766c ） https://youtu.be/HY9OD8rX89s?si=78REb8MyKSJB6cwQ
7. Bybit支付卡申请链接 https://www.bybit.com/invite?ref=LGNQRG，教程链接https://youtu.be/3sN7P2t_CeA

## YouTube 播放列表

- AI产品&技术相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海VPS相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=mqk9ViLo4M8)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/wechat-radar/)
