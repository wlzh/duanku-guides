# 2026最新！手机远程控制Claude Code：Happy安装配置全教程

Happy 安装配置教程：用手机远程控制 Claude Code，覆盖安装配对、会话管理、国内网络问题和自建中继。

> 完整图文与持续更新版本：[2026最新！手机远程控制Claude Code：Happy安装配置全教程](https://869hr.uk/2026/tech/claude-code-happy-mobile-remote-control-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/claude-code-happy-mobile-remote-control-tutorial/
- 更新：2026-05-11
- 分类：技术
- 专题：技术、AI
- 关键词：Claude Code、Happy、手机远程控制、AI编程、远程开发
- 视频：https://www.youtube.com/watch?v=JV_WmhYU-RY

## 正文

<!-- 文章摘要 -->
> 
前几天地铁上突然想起有个 bug 要改，习惯性想掏手机让 Claude Code 处理，然后卡住了。claude 是终端工具，电脑在家关着呢。...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=JV_WmhYU-RY)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 0 分钟。

前几天地铁上突然想起有个 bug 要改，习惯性想掏手机让 Claude Code 处理，然后卡住了。claude 是终端工具，电脑在家关着呢。

## 为什么普通远程方案不够顺手

试了几种方案都不顺手：

- **Tailscale + Termux + tmux**：配得累，触屏 SSH 反人类
- **claude.ai/code 网页版**：读不了本地文件
- **@claude Action**：异步反馈慢
- **Codespaces/Gitpod**：是容器环境，不是你的本地

## Happy 是什么

后来翻到 Happy 这个开源项目（GitHub slopus/happy，MIT协议），装完 5 分钟跑通。

简单说，电脑上的 Claude Code 还是本地跑（能读写你的本地文件），手机 App 走一个加密中继当电脑的遥控器。

三个点搞清楚：

- **Claude Code 真跑在你的电脑上**
- **手机不直连电脑**
- **全链路 E2EE 加密**（Signal 协议）

## 安装与配对

电脑端先安装 Happy：

```bash
npm install -g happy
```

然后进入项目目录运行：

```bash
happy
```

终端会出现 ASCII 二维码。手机端在应用市场搜索 **Happy Coder**，扫码配对即可。

## 会话管理

会话管理主要有三种情况：

1. **电脑端启动**：电脑运行 `happy` 后，手机 App 会自动出现对应会话
2. **手机端新建**：需要电脑端 `happy daemon` 常驻
3. **电脑端续接手机会话**：使用 `happy resume`

日常用法也很简单：

- 电脑起，手机接
- 手机起，电脑干活
- 多 session 并行

## 国内网络问题

国内使用常见问题包括：

- 扫码卡在 Pairing
- session 不同步
- 自动断开
- 语音转文字慢

解法从轻到重：

1. 电脑挂代理
2. 手机走系统代理
3. 自建中继

## 自建中继

自建中继的核心步骤：

```bash
git clone 项目
docker compose up -d
```

然后修改 `HAPPY_RELAY_URL` 指向自己的中继地址。

## 常见坑

- `command not found`：检查 `PATH`
- 二维码扫不出：使用 `--pair-url`
- 同步延迟：挂代理
- 手机新建会话首条被侵害：先发 `hi` 探路

## 本期内容概览

出门在外想改代码？Happy 让你用手机远程操控电脑上的 Claude Code，全链路 E2EE 加密，5 分钟装完。本视频手把手教你从安装到配对、会话管理、国内网络问题解决、自建中继全流程，小白也能跟着做。

注意，相关视频中的内容、命令、脚本、代码，都会整理在博客文章中：

- https://869hr.uk

## 短信及语音接码平台

- https://hero-sms.com/?ref=357885
- https://smspva.com/?ref=1307601

## 白嫖流量

- 500M 试用：https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN，85 折优惠
- 200M 试用：https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码 GXJDIAN，9 折优惠

## 关注与资源

1. 微信讨论群：https://qr.869hr.uk/aitech
2. 超过 100T 资料总站网站：https://doc.869hr.uk
3. Telegram 群聊：https://t.me/tgmShareAI
4. 微信公众号：搜“AI前沿的短裤哥”
5. 视频的文字博客（银行卡、手机号、VPS 主机、IP 测试等）：https://869hr.uk
6. 推特：https://x.com/gxjdian
7. YouTube：https://youtube.com/@gxjdian

## VPS 主机推荐

- Claude 用的丽萨主机：https://lisahost.com/aff.php?aff=9424
- 按流量 VPS：https://www.lycheeip.com/home/ip?affId=1AwYIQ7BW8
- 一年 10 美元的多年保底小鸡：https://clients.zgovps.com/?affid=1207
- 各种云主机，主打性价比：https://my.racknerd.com/aff.php?aff=15809
- 美国 VPS，一年 70 美金搞活动：https://app.cloudcone.com/?ref=13794
- 一年 8.5 美金的美国家宽，稳定靠谱：https://www.webshare.io/?referral_code=55vpv6waorud
- VPS DMIT：https://www.dmit.io/aff.php?aff=21728
- VPS VIRCS 家宽落地机：https://www.vircs.com/welcome?vcd=61a4aae4
- 家宽 IP：https://ipfly.net/activity/OE5TWVlUUEI6TFZKOVhYQzM5NQ==
- 住宅 VPS：https://www.voyracloud.com/?ref_code=5ZG4FHL8

## 账号、礼品卡与 AI 产品充值

- Gmail、Telegram 等账号购买、礼品卡、Claude 充值 AI 产品：https://accboy7gxjdian.acceboy.com/
- https://universalbus.cn/?s=bvDplWi2fZ
- https://www.gamsgo.com/partner/jGh24
- Claude、OpenAI Codex 等充值：https://bewild.ai?code=GXJDIAN

## eSIM 与支付卡推荐

1. 三家 eSIM 让国产手机秒变 eSIM 手机，全方面优缺点对比及开户链接：https://s.869hr.uk/mcc
2. eSIM 9eSIM 打 9 折（优惠码：maq）注册及购买链接：https://www.9esim.com/?coupon=maq
3. eSIM ESTK 打 9 折（优惠码：GXJDIAN）注册及购买链接：https://store.estk.me/zh?aid=16007
4. eSIM XeSIM 打 9 折（推荐码：gxjdian）注册及购买链接：https://xesim.cc/?DIST=RE5FHg==
5. Wise 的申请链接及教程链接（有身份证就可，推荐码：lizhiw12）：https://wise.com/invite/ihpc/lizhiw12
6. N26 的申请链接及教程链接（需要护照，推荐码：lizhiw02766c）：https://youtu.be/HY9OD8rX89s?si=78REb8MyKSJB6cwQ
7. Bybit 支付卡申请链接：https://www.bybit.com/invite?ref=LGNQRG，教程链接：https://youtu.be/3sN7P2t_CeA

## YouTube 播放列表

- AI 产品&技术相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海 VPS 相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

---

如果你觉得这期视频对你有帮助，请务必：

- 点赞本视频
- 在评论区留下你的问题或成功注册的截图
- 订阅频道并打开小铃铛，获取最新硬核白嫖教程和科技前沿资讯！

#ClaudeCode #Happy #手机远程控制 #AI编程 #远程开发 #E2EE加密 #小白教程

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=JV_WmhYU-RY)
- [相关推荐](https://869hr.uk)

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/claude-code-happy-mobile-remote-control-tutorial/)
