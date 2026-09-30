# 0元白嫖两个顶级域名！.bond/.cyou首年免费+Cloudflare托管保姆级教程

还支持自定义NS，可无缝接入Cloudflare托管，免费域名+免费CDN+免费SSL一起打通，个人项目上线基本0成本

> 完整图文与持续更新版本：[0元白嫖两个顶级域名！.bond/.cyou首年免费+Cloudflare托管保姆级教程](https://869hr.uk/2026/tech/cloudflare-0-domain-bond-cyou-free-step-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/cloudflare-0-domain-bond-cyou-free-step-tutorial/
- 更新：2026-09-12
- 分类：技术
- 关键词：域名、0元域名、顶级域名、nicnames、doma protocol
- 视频：https://www.youtube.com/watch?v=qUU4B33XmJs

## 正文

<!-- 文章摘要 -->
> 
今天分享一个0元拿两个顶级域名的方法：Nicnames官方联合Doma Protocol在Discord社区发放首年100%免费福利，0元购.bond、.cyou顶级后缀。一个账号能同时领两张券，一次白嫖两个域名！还支持自定义NS，可无缝接入Cloudflare托管，免费域名+免费CDN+免费SSL一起打通，个人项目上线基本0成本。...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=qUU4B33XmJs)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 7 分钟。

背景

今天为大家分享一个 0 元拿两个顶级域名的白嫖方式：目前 Nicnames 官方联合 Doma Protocol 在 Discord 社区发放首年 100% 免费的优惠福利，可以 0 元购 `.bond` 、 `.cyou` 等顶级后缀， **一个账号能同时领两张券，等于一次白嫖两个**。还支持自定义 NS，可以无缝接入 Cloudflare 托管。下面是完整的白嫖步骤。

### 第一步：注册 Nicnames 账号

打开官网： [https:// nicnames.com/en/login ](https://nicnames.com/en/login)

直接输入邮箱和密码即可快速注册，流程极简。

### 第二步：加入 Discord 并完成身份验证

1. 点击加入官方群组： [https:// discord.gg/doma ](https://discord.gg/doma)

2. 进入后查看 Welcome 提示（ `Welcome to Doma Protocol!` ），点击消息下方的 `doma` 表情符号完成验证，即可解锁服务器的所有频道权限。

点击确认

### 第三步：领取代金券/优惠码（重点）

1. 验证通过后，在左侧频道列表找到 `Partner Promos` 类别下的 `#nicnames-promos` 频道。

2. 在频道聊天框输入 斜杠命令 `/promos` 唤出机器人 (NicNames Bot)。

获得优惠码

1. 机器人会向你的注册邮箱发送一个 6 位数的 OTP 验证码，输入验证。

2. 验证后会弹出一个下拉菜单，选择你需要的福利（建议同时勾选 `.BOND Domain Registration - 100% off for 1st year` 和 `.CYOU` 两个选项）。

3. 获取成功后，机器人会提示 `Promo Activated Successfully!` ，并给你一串 Coupon ID，复制这串优惠码。

### 第四步：免费 注册域名

回到 Nicnames 平台，搜索你心仪的 `.bond` 或 `.cyou` 域名，在结算页面输入刚才复制的 Coupon ID（优惠码），即可首年 0 元免费拿下！

可用后缀： `bond` 、 `cyou`

点击进去要你付款

下面会有一个输入兑换码的选项，你把兑换码复制下去。然后就不需要你付钱了。并且也不需要过走信用卡，直接就交付成功了。

成功获得域名

### 第五步：关闭自动续费

券是「首年免费」，第二年会按原价续费，所以注册完务必关闭自动续费。

点击域名详情页，把 `Auto-Renew` 自动续费关掉。

### 附加：接入 Cloudflare 托管

经过实际测试，Nicnames 注册的域名是可以添加到 Cloudflare 里面托管的。

具体做法：

1. Cloudflare 后台 `Add Site` → 选 Free 计划

2. Cloudflare 会分配两个 NS 地址 （形如 `xxx.ns.cloudflare.com` ）

3. 回到 Nicnames 域名详情页，把 DNS 服务器 改成 Cloudflare 给的那两个

4. 等几分钟全球生效，Cloudflare 后台出现小绿勾就接上了

接上 Cloudflare 之后

免费域名 + 免费 CDN + 免费 SSL 一起打通，个人项目上线基本就是 0 成本。

### .cyou 和 .bond 怎么挑？

聊点我自己的看法。

`.cyou` 是 “see you” 谐音，调性偏年轻、社交。我自己更倾向用它做个人主页或者博客—— `yourname.cyou` 这种短链看着舒服也好记，拿来搭个工具站、demo 站也挺顺手。

`.bond` 含义是”纽带 / 连接”，做 API 网关、上下游对接这类”把两边连起来”的事情特别合适。拿来搭个人工具集合页、API [聚合层 ](https://zhida.zhihu.com/search?content_id=278225234&content_type=Article&match_order=1&q=%E8%81%9A%E5%90%88%E5%B1%82&zd_token=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJ6aGlkYV9zZXJ2ZXIiLCJleHAiOjE3ODkzNTMyNzQsInEiOiLogZrlkIjlsYIiLCJ6aGlkYV9zb3VyY2UiOiJlbnRpdHkiLCJjb250ZW50X2lkIjoyNzgyMjUyMzQsImNvbnRlbnRfdHlwZSI6IkFydGljbGUiLCJtYXRjaF9vcmRlciI6MSwiemRfdG9rZW4iOm51bGx9.Vzop05LgD9mc7B4NbMYoGmxfsGvoUfUyVmPH4eTQEyk&zhida_source=entity)也很顺手， `.bond` 这种短词缀拼起来也好看。

### 引用链接

* Nicnames 官网： [https:// nicnames.com/en/login ](https://nicnames.com/en/login)

* Doma Protocol Discord 群： [https:// discord.gg/doma ](https://discord.gg/doma)

* Nicnames 官方图文教程： [https:// nicnames.com/en/news/Ho w\_to\_Get\_a\_Promo\_Code\_via\_NicNames\_Discord ](https://nicnames.com/en/news/How_to_Get_a_Promo_Code_via_NicNames_Discord)

今天分享一个0元拿两个顶级域名的方法：Nicnames官方联合Doma Protocol在Discord社区发放首年100%免费福利，0元购.bond、.cyou顶级后缀。一个账号能同时领两张券，一次白嫖两个域名！还支持自定义NS，可无缝接入Cloudflare托管，免费域名+免费CDN+免费SSL一起打通，个人项目上线基本0成本。

本视频完整步骤：
1. 注册Nicnames账号
2. 加入Discord完成身份验证
3. 领取代金券/优惠码（重点：一个账号领两张券）
4. 0元注册域名（无需信用卡）
5. 关闭自动续费（避免第二年原价扣费）
6. 接入Cloudflare托管
7. .cyou和.bond怎么选

详细图文教程和所有链接见博客，记得关闭Auto-Renew自动续费！

📎 **本视频涉及资源：**
- https:// nicnames.com/en/login: https://nicnames.com/en/login
- https:// discord.gg/doma: https://discord.gg/doma
- https:// nicnames.com/en/news/Ho w\_to\_Get\_a\_Promo\_Code\_via\_NicNames\_Discord: https://nicnames.com/en/news/How_to_Get_a_Promo_Code_via_NicNames_Discord

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

- [YouTube视频原地址](https://www.youtube.com/watch?v=qUU4B33XmJs)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/cloudflare-0-domain-bond-cyou-free-step-tutorial/)
