# 微信群二维码7天过期？用这个开源免费工具生成永久二维码，无需服务器，3分钟搞定！

众所周知，微信群二维码只有 7天有效期，对于一些玩私域的朋友，稳住一个二维码使用完全没招，要么只能忍受，要么市面上有付费使用的，要么免费的总有弹窗广告来维持不变的二维码。

> 完整图文与持续更新版本：[微信群二维码7天过期？用这个开源免费工具生成永久二维码，无需服务器，3分钟搞定！](https://869hr.uk/2026/tech/7-free-tools-server-3/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/7-free-tools-server-3/
- 更新：2026-07-18
- 分类：技术
- 专题：技术
- 关键词：永久二维码、微信群活码、Cloudflare Workers、serverless、qrcode
- 视频：https://www.youtube.com/watch?v=YhxnffqiegU

## 正文

<!-- 文章摘要 -->
> 
微信群聊二维码只有7天有效期，私域运营苦不堪言。今天教你用 serverless-qrcode-hub 这个开源免费工具，基于 Cloudflare Workers + D1，生成永久不过期的二维码，后台随时更新新二维码即可。...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=YhxnffqiegU)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 9 分钟。

微信群聊二维码频繁变动

这个能生成永久二维码的开源免费工具，仅需后台统一更新新二维码。

不需要服务器。也可作为 URL 缩短链接服务使用。

微信群二维码 7 天过期痛点背景

众所周知，微信群二维码只有 7天有效期，对于一些玩私域的朋友，稳住一个二维码使用完全没招，要么只能忍受，要么市面上有付费使用的，要么免费的总有弹窗广告来维持不变的二维码。

苦于微信群聊二维码频繁变动

这个能生成永久二维码的工具， **不需要服务器**。

基于 Cloudflare Workers 和 D1 实现。

这个项目我用了好几年了，虽然后面作者一直在更新我也没再更新过，为了这期教程，我做了更新，发现现在更强大了，支持了二维码过期的提醒各种文字及格式定制

项目链接：https://github.com/xxnuo/serverless-qrcode-hub

## 项目特性

* 🔗 生成永久短链接，指向微信群二维码

* 😋 可当短链接生成器

* ☁️ 无需服务器

* 🎨 自定义二维码样式和 Logo

* 💻 管理后台可随时更新

* 🔐 密码保护

## 预览图

* 登录

* 管理后台1：添加普通短链

* 管理后台2：添加微信二维码

* 管理后台3：短链列表

* 生成二维码

* 微信识别

## 使用步骤

1. 登录 Cloudflare 并创建 D1 SQL 数据库

* 填写随便一个D1 数据库名字

* 复制 D1 SQL 数据库 ID

* 回到 GitHub 并 Fork 仓库

* 在 GitHub 打开你 Fork 的仓库的 `wrangler.toml` 文件，点击图中的按钮编辑

* 将 `d1_databases` 下的 `database_id` 内容替换为你自己拷贝的 D1 SQL 数据库 ID

* 回到 Cloudflare 并创建 Worker

* 选择你 Fork 的 Github 仓库

然后直接点击右下角的 `保存并部署`

* 等待部署成功

自动跳转到了这个页面，此时默认分配的 `*.workers.dev` 域名在国内访问较慢，建议绑定自己的域名

* 绑定自定义域名

如果没有域名，之前分享过如何获取免费域名及挂靠cloudflare的教程，可以见视频下方文字区获取以往视频教程的链接，查看申请免费域名相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw

* 设置一个你在 Cloudflare 托管的域名的子域名

11. 按图中步骤设置访问密码

注意密码格式为英文字母和数字，尽量长尽量复杂，推荐使用两段随机生成的uuid字符串作为密码

12. 部署成功，此时已经可以面板上通过默认分配的 `*.workers.dev` 或者你自定义的域名访问了！

* 访问并登录后，创建短链接例子

* 下载不过期二维码，或者复制二维码链接地址

* 创建微信群聊活码例子

* 新版扩展功能

可以自定义公告和提示，同时支持字体等格式设置

 17\. 打开生成的二维码链接

查看定制公告及提示效果

微信群聊二维码只有7天有效期，私域运营苦不堪言。今天教你用 serverless-qrcode-hub 这个开源免费工具，基于 Cloudflare Workers + D1，生成永久不过期的二维码，后台随时更新新二维码即可。

✅ 完全免费，无需服务器

✅ 开源自部署，数据自己掌控

✅ 支持微信群活码 + 普通短链接

✅ 自定义二维码样式、Logo、公告提示

✅ 密码保护管理后台

📎 **本视频涉及资源**

项目地址：https://github.com/xxnuo/serverless-qrcode-hub

## YouTube 播放列表

- 免费域名申请教程专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw

⏱️**时间轴**

- 注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有 🔗https://869hr.uk

## 短信及语音接码平台

- 或https://smspva.com/?ref=1307601

## 白嫖流量

- 纯净住宅IP白嫖流量
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

- [YouTube视频原地址](https://www.youtube.com/watch?v=YhxnffqiegU)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/7-free-tools-server-3/)
