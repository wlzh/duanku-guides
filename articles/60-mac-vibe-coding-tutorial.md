# 60元小米遥控器变身Mac语音神器！Vibe Coding 开口即输入，手把手教程

几十块大疆4G模块爆改移远EC25，Mac UTM一键部署VoHive完整教程 6。包含适用条件、操作步骤、结果验证和常见问题。

> 完整图文与持续更新版本：[60元小米遥控器变身Mac语音神器！Vibe Coding 开口即输入，手把手教程](https://869hr.uk/2026/tech/60-mac-vibe-coding-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/60-mac-vibe-coding-tutorial/
- 更新：2026-08-29
- 分类：技术
- 专题：技术
- 关键词：小米蓝牙遥控器、RC003、Mac语音输入、Vibe、Coding
- 视频：https://www.youtube.com/watch?v=1e8gXx3c56w

## 正文

<!-- 文章摘要 -->
> 
闲鱼60多元的小米蓝牙遥控器2 Pro（RC003），配开源工具「无线麦 SayAll」就能变成 Mac 的无线语音麦克风+快捷键手柄：按住语音键说话，文字直接进豆包、Cursor、Codex 任何输入框，松手即发；方向键确认键全映射成 Mac 快捷键。本期手把手完整教程：下载安装、蓝牙配对、权限授权、首次向导、连接设置、按键映射、进阶玩法到常见问题排查，一步不落。开源免费、CPU占用不到0.5%、语音不上传，Vibe Coding 和高频语音输入党必试。...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=1e8gXx3c56w)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 20 分钟。

## 小米蓝牙遥控器 2 Pro（RC003）变身 Mac 无线语音遥控器：Vibe Coding 语音操控神器，手把手指导教程

一句话先讲明白

花六十多块钱买的小米蓝牙遥控器 2 Pro（RC003），别只拿来按电视盒子了。配上一个开源小工具「无线麦 SayAll」，它能变成你 Mac 的无线语音麦克风 + 遥控器，专治 Vibe Coding 和一切“开口就想输入”的场景。

整个流程图

无线麦——为 Vibe Coding 而生的语音遥控器

闲鱼花六十多块钱

买了个小米蓝牙遥控器 2 Pro（RC003），本来是给电视盒子和投影用的，结果在我手里变成了 Mac 的无线语音遥控器。

图像

玩法很简单

按住遥控器上的语音键，说话内容直接进豆包、进任何输入框，松手就发。相当于给 Mac 配了个无线麦克风，还是握在手里的那种。

方向键、确认键、音量键也没闲着，全都映射成了 Mac 的快捷键。切 App、调音量、移动光标，躺着就能操作。

说白了就是给 Vibe Coding 和高频语音输入的人量身定做的。双手不离开键盘太久是理想，但真干起活来，能按住一个实体键说两句，比凑到麦克风前喊舒服多了。

遥控器自带的按键就那几个，但胜在便宜、电池耐用、蓝牙连接稳。折腾一晚上，成就感拉满。

## 为什么遥控器，不用普通麦克风

你可能会问：随便买个蓝牙麦克风不行吗？还真不行。普通蓝牙麦往往没有实体按键，语音输入要么手动开关机，要么凑到键盘前按快捷键触发；专业麦克风更麻烦，要开关机、要切输入源。而遥控器天生就有**实体按键**：一个语音键负责“按住说、松开停”，方向键、确认键、音量键还能顺手变成你的控制手柄。便宜、电池耐用、蓝牙连接稳，正好把短板全补齐了。

## 这套玩法是怎么工作的

「无线麦 SayAll」是一个开源的 macOS 应用，思路并不玄乎：遥控器的麦克风通过蓝牙把声音传进 Mac，再经一个叫 `MiRemoteV 2ch` 的回环音频设备，把声音“喂”给你正在用的语音工具（豆包输入法、Typeless、Cursor 等），识别出的文字直接落进当前输入框。

语音输入链路流程图

它**不是**把遥控器伪装成键盘

语音是真的被采集、真的被识别成文字的，只是把“凑到麦克风前说话”换成了“握在手里的遥控器”。

几个让“好用”成立的细节：

-**按住说、松开停**：按下语音键开始采音，松开立即结束，和快捷键的生命周期一致，全程不用手动开关麦克风。

-**足够轻量**：SwiftUI 原生开发，常驻运行时 CPU 占用低于 0.5%，内存约 50 MB，比一个 Chrome 标签页还轻。

-**隐私友好**：语音不上传、不保存，日志里也不记录语音内容、蓝牙地址或外设标识；不会擅自改动 Mac 的默认输入/输出设备。

-**按键全可定制**：方向、确定、返回、主页、菜单、TV、电源、音量键，每个都能配单击、双击、长按三种动作。

## 开工前的准备清单**硬件**：一台 Mac（Apple Silicon 或 Intel 都行）、一个小米蓝牙遥控器 2 Pro（RC003）。官方零售价 99 元，闲鱼六七十块就能淘到，自带语音键、方向键、确认键、返回/主页/菜单、TV、电源和音量键。**软件**：无线麦 SayAll（从[官网](https://sayall.app/)或 [GitHub Releases](https://github.com/HD838A/remote-mic-app/releases) 下载）+ `MiRemoteV 2ch` 兼容麦克风驱动（随安装包一起装）。**语音工具**：豆包输入法（Mac 版）、Typeless、Cursor / Codex / Claude Code……任选你常用的。本教程默认用豆包输入法演示。

## 第一步：下载并安装 SayAll

1. 打开[官网 sayall.app](https://sayall.app/)，或进入 [GitHub Releases](https://github.com/HD838A/remote-mic-app/releases) 页面下载 DMG。

2. 分清架构：Apple Silicon 装 `Remote-Mic-<版本>.dmg`,Intel 装 `Remote-Mic-<版本>-Intel.dmg`，**两者不能混用**。

3. 打开 DMG，双击唯一的 `Install Remote Mic.pkg`（Intel 用 `Install Remote Mic Intel.pkg`）。

4. 安装器会把 App 装到 `/Applications/SayAll.app`，并检查 `MiRemoteV 2ch`：健康兼容就原样保留，缺失或不可用才会安装或更新。

> 只需要 App、且已经装了其他回环音频设备（比如 BlackHole）的高级用户，可以从同一个 Release 下载 App-only ZIP。新手建议直接用安装包，最省心。

> v1.3.0 起，正式发布包使用 Apple Developer ID 签名并已完成 Apple 公证。请只从官网 Cloudflare CDN 固定入口或本项目 GitHub Releases 下载；要核验的话，同一 Release 里有 `Remote-Mic-<版本>.dmg.sha256` 校验文件。

## 第二步：把遥控器配对到 Mac

1. 打开「系统设置 → 蓝牙」，确认蓝牙已开启。

2.**同时长按遥控器的「主页」和「菜单」两个键**，直到进入配对状态。

3. 在 Mac 的蓝牙列表里，连接名为 `MI RC`、`Xiaomi Bluetooth Remote 2`、`Xiaomi Bluetooth Remote 2 Pro` 或「小米蓝牙语音遥控器」的设备。

4. 显示“已连接”就成功了。

> 配对时把遥控器贴近 Mac 成功率更高。没搜到设备，就再长按一次主页 + 菜单重新进入配对模式。

## 第三步：启动 SayAll 并授权

1. 启动 `SayAll.app`，按提示**允许「蓝牙」权限**（用来连接遥控器、读取实体按键）。

2. 要自定义按键的话，再**允许「输入监控」和「辅助功能」**。

3.**授权完成后，完全退出并重新打开应用**，让权限生效。

4. App 会常驻菜单栏，Dock 里也有图标，随时能打开设置。

> 应用不会为了语音输入自动修改 Mac 的默认输入或输出设备，一切以你在 App 里和语音工具里的选择为准。

## 第四步：跟着首次启动向导走完一遍

这一步别跳过。SayAll 的首次启动向导（对应[官网配置教程](https://sayall.app/tutorial/)）把整套链路拆成 6 个可勾选的检查项，走完基本就通了：

1.**选择常用的语音工具**：豆包输入法、Typeless 或其他。选豆包会准备 Fn/地球键长按的语音行为，选 Typeless 会改用 Fn 点按。

2.**允许三项系统权限**：蓝牙、输入监控、辅助功能，依次完成。

3.**连接遥控器并按一个普通按键**：保持遥控器靠近 Mac，按语音键以外的任意键，向导会显示“已收到实体按键”。

4.**准备兼容麦克风**：检测到 `MiRemoteV 2ch` 后，选中它作为兼容麦克风。

5.**亲自说一句**：点测试输入框，按住语音键说“无线麦已经连接成功”，松开。文字真的出现，链路就通了。

6.**试三个不同普通按键**：方向、确认、音量等，确认实体控制也正常。

> 完整 6 步配置教程见 [sayall.app/tutorial](https://sayall.app/tutorial/)，每一环都给出了明确的“通过标准”，第一次搞不定时照着逐项排查最有效。

## 第五步：连接与语音设置（正式开工）

向导走完，链路已经通了。正式使用时，记住这一套操作：

1. 打开**「连接与语音」**页面。

2. 点**「刷新音频设备」**，选择 `MiRemoteV 2ch`（或你已安装的其他回环音频设备）。

3. 在需要听写或语音输入的应用里，**把麦克风也选成同一个设备**。

4. 单击目标输入框，**按住遥控器语音键说话，松开后结束**，文字就进去了。

连接与语音设置页

### 语音键可以换触发方式

在「按键映射」页的「语音键」区域，可以选择语音触发方式：

-**Fn / 地球键（默认）**：直接兼容豆包、微信等 Fn 长按语音入口，以及 Typeless 的 Fn 点按入口，“按住采音、松开停止”和快捷键生命周期一致，最省心。

-**左 Command 长按 / 右 Command 长按**：适合目标语音应用用 Command 做语音入口的情况。注意它需要「辅助功能」权限，而且很多应用会把左右 Command 合并成通用 Command，需要你在目标应用里实际测一下。

### 先测音频链路再开说

想确认音频链路通不通，可以点**「发送 1 秒测试音」**，或在 QuickTime Player 的「新建音频录制」里观察输入电平。能看到电平跳动，链路就是好的。

> 语音键只负责“按下即开始、释放即结束”的语音会话，不承担短按、双击、长按的附加动作。想一键聚焦前台输入框，请给普通按键配置「聚焦输入框」动作（用的是 macOS 辅助功能，不读取输入内容）。

## 第六步：按键映射，把每个键都用起来

这是“遥控器”的部分，也是让它在 Vibe Coding 里真正顺手的关键。打开**「按键映射」**页面，启用自定义映射后，方向、确定、返回、主页、菜单、TV、电源、音量键都能改功能。

-**每个普通按键**可设一个单击动作，还能额外设双击和长按动作。

-**动作类型**：键盘操作、系统音量、播放控制、打开当前 Mac 已安装的常用应用、聚焦前台输入框，以及任意自定义键盘快捷键。

-**自定义快捷键**：可直接选复制、粘贴、聚焦搜索等常用组合，也可自己选组合键、主键、F1–F20、导航键、数字键盘或单独的左右修饰键，还保留了真实键盘录入入口。

-**打开自定义 App**：从本机选任意 `.app`，可选“只打开应用”“激活后发送该应用的聚焦快捷键”，或“记录一次目标输入框后自动聚焦”（目标 App 升级后输入框结构变了，重新记录一次即可）。

按键映射设置页

### 一套适合 Vibe Coding 的键位方案参考
| 按键 | 单击 | 双击 / 长按 | 用途 |
| --- | --- | --- | --- |
| 方向键 | 光标移动 | 翻页 / 快速移动 | 手动定位光标、选代码 |
| 确认键 | 回车（发送语音） | Command + 回车 | 给 Codex / Cursor 发 prompt |
| 音量键 | 系统音量增减 | 播放 / 暂停 | 听歌、看视频随手调 |
| 主页键 | 聚焦输入框 | 打开常用 AI 工具 | 一键开说 |
| 菜单键 | Command + K | 打开 Cursor | 唤起命令面板 |
| TV 键 | 切换指定 App | — | 按你习惯自定义 |
（这只是示例，一切按你的习惯来。）

### 按 App 自动匹配键位方案

同一只遥控器可以保存多套完整键位方案，你可以手动切换，也可以开启**按 App 自动匹配**：在不同应用里自动套用对应方案，没有匹配规则时回到默认方案。

## 第七步：进阶玩法

### 豆包输入法找不到虚拟麦克风？

用 DMG 里的 `Install Remote Mic.pkg` 装好驱动，然后在 SayAll 里选 `MiRemoteV 2ch`，豆包输入法 Mac 版里也把它选成麦克风即可。

豆包输入法 Mac 版选择 MiRemoteV 2ch 麦克风

### Typeless 用户：开启“语音键模拟 Fn 点按”

Typeless 是“点按 Fn 开始、再次点按结束”的语音工具，和小米遥控器默认的 Fn 长按不兼容。在「按键映射」的语音键区域开启**「语音键模拟 Fn 点按」**后，App 会在语音流开始和排空结束时各发一次 Fn 点按。Typeless 和 SayAll 仍需选择同一个回环设备，并授予「辅助功能」权限。

> 这个模式下仍然是**按住语音键说话、松开结束**——RC003 固件在松开语音键后不会再发送麦克风音频，所以这不是持续录音/免按键模式。豆包等用 Fn 长按的工具，请保持该开关默认关闭。

### 让 AI 客户端读你的“回眸”历史（MCP）

开启「记录回眸」后，SayAll 会只保存**通过它输入并最终稳定出现**的文字，按 App 和日期整理在当前 Mac。再开启「本地 Agent 访问」，就能为每个 AI 客户端创建独立、可撤销的**只读 MCP 授权**，让 Codex、Claude Code、Cursor、OpenCode 等只读访问你的语音输入历史，而且不需要装 Node.js 或任何开发依赖。

### 用统计页看看自己的“语音量”

「统计」页面可以按日、周或全部范围查看遥控器按键次数、语音时长，以及从当前版本开始记录的最长单次语音排行。所有数据只保存在本机，不会上传。

无线麦使用统计页

## 实战：Vibe Coding 的一天是怎么过的

给你一个直观的画面，看看这套东西在真实干活时的体感。

写代码写到一半，脑子里冒出一个需求。以前要么切到麦克风前说，要么停下来打字。现在：**左手拿起遥控器，按住语音键，把需求口述一遍**——“帮我把这个函数拆成三个，加参数校验，写单元测试”——松手，文字已经躺在 Cursor / Codex 的输入框里，再按一下确认键就发送。整个动作手不离键，眼睛不用离开屏幕。

改需求的第二轮、第三轮也一样。遇到要精确定位的，方向键 + 确认键就是你的鼠标。躺着、瘫着、单手端着咖啡，都能操作。

> 双手不离开键盘太久是理想，但真干起活来，能按住一个实体键说两句，比凑到麦克风前喊舒服多了。六十多块钱，换来的是“开口就能输”的自由。

无线麦使用统计页

## 常见问题排查
| 症状 | 处理办法 |
| --- | --- |
| 向导里遥控器没响应 / 没收到实体按键 | 点「重新查找」，或打开蓝牙设置检查配对；确认遥控器已连接、靠近 Mac |
| 说话没有文字出现 | 确认 SayAll 里选了 `MiRemoteV 2ch`，目标语音应用的麦克风也选了同一个；先发 1 秒测试音或在 QuickTime 看输入电平 |
| 豆包输入法找不到虚拟麦克风 | 用 DMG 里的 pkg 安装驱动，再在豆包里选 `MiRemoteV 2ch` |
| 自定义按键不生效 | 检查「输入监控」「辅助功能」是否已允许，授权后完全退出并重开应用 |
| 语音键选 Command 长按但没反应 | 目标应用可能把左右 Command 合并了，改用默认 Fn / 地球键，或在目标应用里实测 |
| 想确认 App 是否最新 | 应用每天自动检查一次更新，也可在「关于」页手动「检查更新」 |
更完整的排障流程见 [官方排障指南](https://github.com/HD838A/remote-mic-app/blob/main/TROUBLESHOOTING.md)。

## 想卸载？

1. 退出 SayAll.

2. 从同一 GitHub Release 下载并运行 `Uninstall Remote Mic.pkg`，移除 `MiRemoteV 2ch` 兼容麦克风（不会改动你已有的 BlackHole）。

3. 删除「应用程序」里的 SayAll.app。

## 结语

六十多块钱的遥控器，本来只是电视盒子旁边的小配件，折腾一晚上，变成了一把握在手里的“语音魔杖”。它便宜、电池耐用、蓝牙连接稳，加上一个开源小工具，就解锁了 Mac 上“开口即输入”的体验。

如果你也在搞 Vibe Coding，或者只是高频语音输入爱好者，这大概是最低成本的尝试路径了。项目开源、作者还在持续更新，值得支持一下。**相关资源：**

- 官网 / 下载：[sayall.app](https://sayall.app/)

- GitHub 项目：[HD838A/remote-mic-app](https://github.com/HD838A/remote-mic-app)

- 官方 6 步配置教程：[sayall.app/tutorial](https://sayall.app/tutorial/)

- 豆包输入法兼容说明、首次安装说明、排障指南、AI 安装与 MCP 配置指南：均在 GitHub 仓库内

闲鱼60多元的小米蓝牙遥控器2 Pro（RC003），配开源工具「无线麦 SayAll」就能变成 Mac 的无线语音麦克风+快捷键手柄：
- 按住语音键说话，文字直接进豆包、Cursor、Codex 任何输入框，松手即发
- 方向键确认键全映射成 Mac 快捷键。本期手把手完整教程：下载安装、蓝牙配对、权限授权、首次向导、连接设置、按键映射、进阶玩法到常见问题排查，一步不落。开源免费、CPU占用不到0.5%、语音不上传，Vibe Coding 和高频语音输入党必试。

📎**本视频涉及资源：**
- 官网: https://sayall.app/
- 官网配置教程: https://sayall.app/tutorial/

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

- [YouTube视频原地址](https://www.youtube.com/watch?v=1e8gXx3c56w)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/60-mac-vibe-coding-tutorial/)
