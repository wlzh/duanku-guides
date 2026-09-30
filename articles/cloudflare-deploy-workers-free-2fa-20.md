# 部署在 Cloudflare Workers 上的免费自托管 2FA 管理器，支持 20+ 格式互导

这个开源项目让你用 Cloudflare Workers 免费自托管 2FA 管理器，零成本、数据完全自主可控

> 完整图文与持续更新版本：[部署在 Cloudflare Workers 上的免费自托管 2FA 管理器，支持 20+ 格式互导](https://869hr.uk/2026/tech/cloudflare-deploy-workers-free-2fa-20/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/cloudflare-deploy-workers-free-2fa-20/
- 更新：2026-05-16
- 分类：技术
- 关键词：2FA、双因素认证、Cloudflare Workers、自托管、开源
- 视频：https://www.youtube.com/watch?v=fWqjMNN-7ZI

## 正文

<!-- 文章摘要 -->
> 
Google Authenticator 的云同步至今没有端到端加密，你的密钥在 Google 服务器上是可读的。Microsoft Authenticator 2025 年改为设备绑定模式，换手机第三方 OTP 直接丢失，iOS/Android 之间还不能互相恢复。Authy 云同步到 Twilio 服务器，2024 年已发生数据泄露。1Password 要年费。...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=fWqjMNN-7ZI)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 7 分钟。

Google Authenticator 的云同步至今没有端到端加密，你的密钥在 Google 服务器上是可读的。Microsoft Authenticator 2025 年改为设备绑定模式，换手机第三方 OTP 直接丢失，iOS/Android 之间还不能互相恢复。Authy 云同步到 Twilio 服务器，2024 年已发生数据泄露。1Password 要年费。

**如果你想要一个免费、自托管、数据完全由自己掌控的 2FA 方案，可以看看这个。**

***
### &#x20;它是什么

一个跑在 Cloudflare Workers 上的 2FA 密钥管理器。没有服务器、没有数据库、没有月费。一键部署，打开浏览器就能用。

这个项目最初是为了解决自己的需求写的，自用了快一年，稳定没出过问题，才决定开源放出来。

***
### &#x20;主流方案的问题

**Google Authenticator**

* 云同步没有端到端加密，密钥在 Google 服务器上可被读取

* 不支持导出为文件，只能设备间扫码迁移

* 没有桌面端，电脑上无法查看验证码

**Microsoft Authenticator**

* 2025 年改为设备绑定模式，换手机/丢手机后第三方 OTP 直接丢失

* iOS 备份无法在 Android 上恢复，反之亦然

* 没有任何导出功能，密钥进去了就出不来

* 迁移流程容易操作失误导致数据丢失，有人因此丢了 GitHub 账号

* 2025 年 7 月起砍掉密码自动填充，强制迁移到 Edge

**Authy&#x20;**— 云同步到 Twilio 服务器，2024 年已发生数据泄露

**1Password / Bitwarden Premium&#x20;**— 需要付费订阅

***
### &#x20;对比一览

| 痛点 | 主流方案 | 本项目 |

| ---- | ----------------------------------- | --------------------------------- |

| 数据归属 | 存在厂商服务器上，平台可读取 | AES-GCM 加密存储在你自己部署的 KV 里，平台无法读取明文 |

| 跨平台 | Google/Microsoft Authenticator 无桌面端 | 浏览器打开就用，PWA 安装到任何设备 |

| 换机迁移 | Google/Microsoft 迁移繁琐，部分 App 不支持导出 | 支持 20+ 种格式互导，一键搞定 |

| 导出自由 | 部分 App 不支持或格式有限 | 20+ 种格式，随时迁走 |

| 费用 | 1Password 年付，Bitwarden TOTP 需付费版 | Cloudflare Workers 免费额度足够个人用 |

| 自动备份 | 多数没有 | 数据变更自动备份，保留最近 100 份 |

| 安全审计 | 闭源，信不信随你 | MIT 开源，AES-GCM 256 位加密，代码随便审 |

***
### &#x20;核心亮点

**零成本自托管&#x20;**— 部署在 Cloudflare 全球 300+ 节点上，免费额度每天 10 万次请求，个人使用绰绰有余。不依赖任何第三方服务。

**跨平台&#x20;**— 纯 Web 方案，手机/平板/电脑都是同一个入口。支持 PWA 安装到桌面，体验接近原生 App，且支持离线访问。

**导入兼容性拉满&#x20;**— 支持从 Google Authenticator（迁移二维码）、Aegis、2FAS、Bitwarden、LastPass、andOTP、Ente Auth、FreeOTP、Proton、WinAuth、Authenticator Pro 导入。换过来零门槛。

**零锁定，随时离开&#x20;**— 这一点很：
- **如果有一天你不想用了，随时可以走。&#x20
- **&#x5BFC
- 出功能覆盖 20+ 种格式，包括：

* **通用格式&#x20;**：TXT（otpauth URI）、JSON、CSV、HTML

* **直接导入其他 App&#x20;**：Aegis、2FAS、andOTP、FreeOTP/FreeOTP+、LastPass、Proton Authenticator、Authenticator Pro、Bitwarden Authenticator、Ente Auth、WinAuth

* **Google Authenticator&#x20;**：生成迁移二维码，手机扫一下就回去了

* **加密导出&#x20;**：FreeOTP 加密 XML、TOTP Authenticator 加密格式

不做用户绑架。你的密钥始终是你的，用标准格式存储，想迁去哪个平台都是一次导出的事。

**OTP API&#x20;**— 提供公开接口 `/otp/YOUR_SECRET` ，方便脚本和自动化调用。这是多数 App 做不到的。

**端到端加密&#x20;**— 配置密钥后，所有数据 AES-GCM 256 位加密存储。即使 Cloudflare KV 被读取，没有密钥也是密文。

**双码显示&#x20;**— 同时展示当前验证码和下一时段验证码，不用卡着倒计时等刷新，从容复制。

***
### &#x20;一键部署
1. 点击上方按钮，使用 GitHub 登录并授权
2. 登录 Cloudflare 账户，点击 **Deploy&#x20;**&#x7B49;待部署完成（KV 存储自动创建）
3. 打开 Cloudflare 给你的 Workers 链接， **设置管理密码&#x20;**&#x5373;可开始使用

不需要懂代码，三步搞定。

***
### &#x20;适合谁

* 不想把 2FA 密钥交给第三方公司的人

* 经常在电脑上需要输验证码的人

* 想从 Google Authenticator 迁移出来但不知道迁去哪的人

* 喜欢自托管、数据自治的开发者

* 有自动化需求、需要 API 获取 OTP 的场景

* 选择困难症：先用着，不满意随时导出到别的 App

***

**GitHub&#x20;**: [GitHub - wuzf/2fa: Two Factor Authentication](https://github.com/wuzf/2fa)

**在线体验&#x20;**（密码 `2fa-Demo.` ）: [https://2fa-dev.wzf.workers.dev](https://2fa-dev.wzf.workers.dev/)

主流 2FA App 各有各的问题：
- Google Authenticator 云同步没有端到端加密，密钥在 Google 服务器上可读
- Microsoft Authenticator 2025 年改为设备绑定模式，换手机第三方 OTP 直接丢失
- Authy 数据存在 Twilio，2024 年已发生泄露
- 1Password 要年费。

这个开源项目让你用 Cloudflare Workers 免费自托管 2FA 管理器，零成本、数据完全自主可控。

核心亮点：

• 零成本自托管 — 部署在 Cloudflare 全球 300+ 节点，免费额度每天 10 万次请求

• 跨平台 — 纯 Web，手机/平板/电脑同一入口，支持 PWA

• 导入兼容拉满 — 支持 Google Authenticator、Aegis、2FAS、Bitwarden 等 20+ 格式导入

• 零锁定随时离开 — 导出覆盖 20+ 格式，随时迁走

• OTP API — 公开接口 /otp/YOUR_SECRET，方便脚本自动化

• 端到端加密 — AES-GCM 256 位加密存储

• 双码显示 — 同时展示当前和下一时段验证码

一键部署，三步搞定，无需懂代码。

GitHub: https://github.com/wuzf/2fa

在线体验: https://2fa-dev.wzf.workers.dev（密码 2fa-Demo.）

0:
- 00 &#x20
- 它是什么

0:
- 43 &#x20
- 主流方案的问题

1:
- 47 &#x20
- 对比一览

3:
- 05 &#x20
- 核心亮点

4:
- 52 &#x20
- 一键部署

5:
- 22 &#x20
- 适合谁

6:16 相关链接

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

如果你觉得这期视频对你有帮助，请务必：

👍 点赞本视频

💬 在评论区留下你的问题或成功注册的截图

🔔 订阅频道并打开小铃铛，获取最新硬核白嫖教程和科技前沿资讯！
#2FA #双因素认证 #CloudflareWorkers #自托管 #开源 #TOTP #OTP #免费 #密码管理 #安全 #端到端加密 #Workers #无服务器

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=fWqjMNN-7ZI)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/cloudflare-deploy-workers-free-2fa-20/)
