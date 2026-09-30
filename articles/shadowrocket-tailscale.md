# Shadowrocket更新Tailscale！代理和内网穿透终于能同时用了

介绍 Shadowrocket 集成 Tailscale 后如何配置 Auth Key，让代理与内网穿透同时运行，并验证文件共享、SSH 和远程桌面连接。

> 完整图文与持续更新版本：[Shadowrocket更新Tailscale！代理和内网穿透终于能同时用了](https://869hr.uk/2026/tech/shadowrocket-tailscale/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/shadowrocket-tailscale/
- 更新：2026-07-13
- 分类：技术
- 关键词：Shadowrocket、Tailscale、内网穿透、远程访问、iPhone代理
- 视频：https://www.youtube.com/watch?v=DOGtAVq9S7Q

## 正文

<!-- 文章摘要 -->
> 
本质上，Tailscale 就是在公网之上帮你搭建了一张安全、稳定、无需端口映射的私人局域网。...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=DOGtAVq9S7Q)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 6 分钟。

🔥Tailscale 有什么用？

本质上，Tailscale 就是在公网之上帮你搭建了一张安全、稳定、无需端口映射的私人局域网。

之前教程，🚀 完美内网穿透方案

Tailscale 私人网络搭建保姆级教程 | 白嫖国内 DERP 到自建节点一次讲透

，视频教程链接 https://youtu.be/SmV8zahYhgI

很多人问我，Shadowrocket 这次更新的 Tailscale 功能到底怎么用？

其实不复杂，几分钟就能搞定。

最常见的场景就是远程访问家里或公司的设备。

举个例子：

Mac 开启文件共享

iPhone 打开「文件」App

连接服务器：smb://电脑局域网IP

这样即使不在同一个网络下，也能直接访问电脑里的文件。

注册 Tailscale

先到 Tailscale 官网注册账号：

注册完成后，会自动创建一个属于你的虚拟局域网（Tailnet）。

安装电脑客户端

在 Mac / Windows 上安装 Tailscale 客户端并登录。

登录成功后，这台电脑会获得一个固定的内网 IP（例如 100.x.y.z），以后无论身处何地，都能通过这个地址访问它。

在 Shadowrocket 中配置

以前 iPhone 上直接开启 Tailscale 有个问题：

👉 开启 Tailscale 后，代理会自动关闭，无法与🪜同时使用。

而 Shadowrocket 这次更新，直接解决了这个痛点。

配置步骤：

1\. 登录 Tailscale 后台 并 创建 Auth Key

2\. 将 Auth Key 填入 Shadowrocket

4\. 开启 Tailscale

小火箭上线后的设备列表中查看在线状态

搞定后，看是远程桌面还是SSH连接这个设备IP

之前怎么连局域网远程桌面和SSH的都可以操作了

Shadowrocket 这次更新终于支持 Tailscale 了！以前 iPhone 开 Tailscale 代理就断，现在用 Shadowrocket 集成 Tailscale，代理和内网穿透同时在线！

🔥 本期内容：
- Tailscale 是什么？为什么它能帮你搭建私人虚拟局域网
- 注册 Tailscale 账号，创建你的 Tailnet
- 在电脑上安装 Tailscale 客户端，获取固定内网 IP（100.x.y.z）
- 在 Shadowrocket 中配置 Tailscale Auth Key，一键启用
- 代理 + 内网穿透同时运行，终于不用来回切换

🏠 最常见的场景：远程访问家里或公司的设备，Mac 文件共享、SSH、远程桌面，不在同一网络也能直接连。

📎 **本视频涉及资源**
- 之前教程视频：Tailscale 私人网络搭建保姆级教程 https://youtu.be/SmV8zahYhgI
- Tailscale 官网：https://tailscale.com

注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有 🔗https://869hr.uk

## 短信及语音接码平台

- 或https://smspva.com/?ref=1307601

纯净住宅IP白嫖流量
- 500M试用， 链接 https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN ， 85 折优惠
- 200M试用，链接 https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码GXJDIAN， 9 折优惠
- eSIM各国纯净IP流量：https://www.redex.vip/zh?partnerId=31
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
7. Bybit支付卡申请链接 （推荐码：LGNQRG）https://youtu.be/3sN7P2t_CeA

8. YiKa虚拟卡实操开卡教程，不需KYC，一个邮箱开50张卡，订阅ChatGPT/Claude/推特蓝V出海必备 https://youtu.be/XaLeXKu4PTM

## YouTube 播放列表

- AI产品&技术相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海VPS相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=DOGtAVq9S7Q)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/shadowrocket-tailscale/)
