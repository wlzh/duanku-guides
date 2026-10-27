# InstaBox 云服务器内测记录：单台4核8GB、配额与使用限制

InstaBox 内测使用记录：区分单台4核8GB与最多5台的总配额，介绍邀请、自动暂停和端口限制；历史免费额度不代表当前账号权益。

> 完整图文与持续更新版本：[InstaBox 云服务器内测记录：单台4核8GB、配额与使用限制](https://869hr.uk/2026/tech/free-server-instabox-20-40gb-1-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/free-server-instabox-20-40gb-1-tutorial/
- 更新：2026-10-27
- 分类：技术
- 专题：技术、AI
- 关键词：InstaBox、免费云服务器、云主机、AI Agent、免费资源
- 视频：https://www.youtube.com/watch?v=spuxWoqv2A8
- 系列：[出海 VPS](../series/vps.md)

## 正文

<!-- 文章摘要 -->
> 
InstaBox 为 AI Agent 提供云端 Linux 环境。下文记录的是发布时的内测体验：单台 4 vCPU、8GB 内存；20 vCPU、40GB 是 5 台相加，不是单台规格。免费配额和邀请条件以当前账号控制台为准。

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=spuxWoqv2A8)</div>

## 视频介绍

**2026-10-27 补充：** 下文与视频中的额度、邀请速度、启动耗时和休眠行为是历史体验，不保证新账号相同。当前能力先查 [InstaBox 官方文档](https://instabox.sh/)，涉及收费与配额应在自己的控制台核对。本站未再次登录你的账号验证额度，也不建议将内测免费实例作为唯一生产环境。更多比较见[VPS 专题](https://869hr.uk/series/vps/)与[AI 产品专题](https://869hr.uk/series/ai-products-and-technology/)。

本视频由 短裤AI分享 制作，时长约 3 分钟。

免费领云服务器

最高 20 核 CPU + 40GB 内存！

InstaBox 的云服务
发现一个叫 InstaBox 的云服务，目前正在邀请制内测，主打给 AI Agent 提供云端运行环境。

免费资源相当大方：
• 单台 4 vCPU + 8GB 内存
• 20GB 存储空间
• 最多 5 台，总计 20 vCPU + 40GB 内存
• 启动时间不到 1 秒
• 支持持久化文件、环境配置和快照
• 支持公共 URL 暴露本地端口
• 默认闲置 30 分钟自动暂停

一些使用场景
拿来折腾 AI Agent、跑脚本、部署一些轻量服务都挺合适，不用自己的电脑一直开着。

领取方式：
打开 <https://instabox.sh>

2\. 使用 Google 账号登录

3\. 注册后等待邀请码

我的是一天后收到了，有的gmail邮箱，年份高的，是直接就登录成功了，不需要邀请码，你可以试试你自己的

4\. 收到邀请后即可体验

目前有人反馈上午申请、下午就收到了邀请。

关于端口

根据公开文档，InstaBox 是完整 Linux VM，没有写 UDP 被禁用。

出网（outbound）正常可用，TCP/UDP 都通。

入网（inbound）主要靠：

* 公开端口：只转成 HTTPS URL（TCP）

* SSH / mosh：gateway 会中继 mosh 的 UDP

任意端口直接暴露 UDP 目前不支持，只有他们提供的机制。

另外

官方 CLI 还支持通过 auto-suspend 参数设置不自动休眠。
不过要提醒一下，目前还是内测阶段，免费政策能持续多久尚不明确，别急着部署重要业务。
这种配置如果真能长期免费，确实挺香的。

发现一个叫 InstaBox 的云服务，邀请制内测中，主打给 AI Agent 提供云端运行环境。免费资源相当大方：单台 4 vCPU + 8GB 内存 + 20GB 存储，最多开 5 台，总计 20 vCPU + 40GB 内存，启动时间不到 1 秒。

本期内容：
- InstaBox 免费配置一览：4核8GB/台，最多 5 台
- 支持持久化文件、环境配置和快照
- 公共 URL 暴露本地端口，闲置 30 分钟自动暂停
- 领取方式：Google 登录 + 等邀请码（有人当天就收到）
- 端口能力：完整 Linux VM，出网 TCP/UDP 都通，SSH/mosh 中继
- CLI auto-suspend 参数可关自动休眠
- 内测阶段提醒：免费政策能持续多久未知，别部署重要业务

拿来折腾 AI Agent、跑脚本、部署轻量服务都合适，不用自己的电脑一直开着。更多羊毛与 AI 实操教程，见频道与博客。

📎 本视频涉及资源：
- 相关链接: https://instabox.sh

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

## 相关推荐

- [2025年全球免费VPS白嫖指南（16个免费服务器资源大盘点）](https://869hr.uk/2025/tutorial/free-vps/)
- [Google免费高配云主机震撼来袭！16核64G内存300G硬盘](https://869hr.uk/2025/tutorial/google-idx-vps-register/)
- [GCP谷歌云永久免费新玩法（三）！开通及部署一键脚本](https://869hr.uk/2026/tech/gcp-free-vps-cdn-bypass-part3/)

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=spuxWoqv2A8)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/free-server-instabox-20-40gb-1-tutorial/)
