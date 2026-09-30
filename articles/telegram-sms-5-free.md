# Telegram登录要收SMS费？5种方法免费绕过，亲测有效！

这个情况好像是官方今年8月份新出的政策公布就出现了，正常情况下，你输入的手机号如果它的地区是亚洲部分国家（不光只是东大）还有英国的手机号（我也试了）去注册，极大概率都会跳付费请求。

> 完整图文与持续更新版本：[Telegram登录要收SMS费？5种方法免费绕过，亲测有效！](https://869hr.uk/2026/tech/telegram-sms-5-free/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/telegram-sms-5-free/
- 更新：2026-05-16
- 分类：技术
- 专题：技术
- 关键词：Telegram、SMS Fee、Telegram登录、Telegram注册、绕过SMS费
- 视频：https://www.youtube.com/watch?v=ugguWmPE0BI

## 正文

<!-- 文章摘要 -->
> 
关于Telegram显示SMS Fee unavailable无法注册下一步问题...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=ugguWmPE0BI)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 7 分钟。

关于Telegram显示SMS Fee unavailable无法注册下一步问题

**不是收不到短信！的问题！**

这个情况好像是官方今年8月份新出的政策公布就出现了，正常情况下，你输入的手机号如果它的地区是亚洲部分国家（不光只是东大）还有英国的手机号（我也试了）去注册，极大概率都会跳付费请求。

最下方出现了unavailable无法获得。

我根据网上各种说法自己也试出来一个方法。这个方法我成功了，也可能是概率问题，也可能随时被修复，仅作个人的交流分享。

首先 存好app的安装包不要删除，关掉手机地理位置

按常规的注册过程过一遍，关闭通知，输入手机号（保险起见，你的手机号是哪个IP就用对应IP地址），邮箱，验证邮箱码，等跳出这个SMS Fee的页面。

退出应用，不卸载它不删除它。重新打开你下好的安装包进行下载。

下载完直接打开，进入页面和刚刚一样的注册步骤，到输入邮箱验证码的时候，输完。他会跳一个邮箱报错。

接着返回上一级，输入邮箱那里。

**输入一个新的邮箱！输入一个新的邮箱！输入一个新的邮箱！**

然后输入新的邮箱验证码。它就会跳转到手机验证码那个界面了。

后面就是接收验证码，一切回归正常流程，没有这个恶心的短信收费了。

遇到的问题：
1.没进行上面重复安装就遇到这个报错，可能是因为在出现sms fee的画面时你就重新删缓存删软件重新注册了很多次，同一个邮箱多次受到验证码，就可能直接遇到这个报错。解决方法就是再用一个新邮箱。
2.如果你没按上面方法就已经跳出了邮箱报错窗口。记住你哪些邮箱跳出了报错！直接去下载Telegram X（相当于原版的极速版）。然后还是输入手机号，邮箱 输入你前面试过了会报错的邮箱！输验证码，跳报错。返回上一级，输入新的邮箱。然后再次发送邮箱验证码。输入完，成功跳过SMS fee 短信付费界面进入手机号验证！

新设备登录Telegram，如下让付费短信才能登录的画面
#### &#x20;情况1：账号可用，有设备在线

在可用的设备上，绑定邮箱或passkey。在新设备上，用11.6.1 以下版本登录电报，此时只需要用旧设备接收验证码。然后升级到最新版即可
#### &#x20;情况2：账号无设备在线

使用俄罗斯版的电报Telega登录，如顺利，会向邮箱发送验证码。

telegram x 之前可直接发短信验证码，现在存疑，没招了可以试试

换节点对我不适用。

对我来说，除了 谷歌下的电报+特定手机号 这种情况，其他都不用SMS Fee
### &#x20;Q\&A

Q1

A1

以下方法未经测试，但有反馈可行

方法1：触发登录频繁 [Telegram开启邮箱登录 - zimk's blog](https://zimk.org/technology/16.html)

方法2：寻求人工客服帮助 [请教tg如何开启邮箱登录？](https://linux.do/t/topic/155392)

Q2

A2

谷歌Play商店搜 `telega`

[telega](https://play.google.com/store/apps/details?id=ru.dahl.messenger&hl=zh)
### &#x20;建议

tg号绑定passkey、邮箱，在多个地方登录
### &#x20;参考：

[账号仍有设备在线时 Telegram 新设备登录绕过 SMS fee 的方法](https://linux.do/t/topic/1369181)

[换了新手机Telegram不让免费用了，你看我像有钱人吗？SMS Fee](https://linux.do/t/topic/1642378)

[关于Telegram显示SMS Fee unavailable无法注册下一步问题](https://www.bilibili.com/opus/1113993613316980738)

[Telegram开启邮箱登录](https://zimk.org/technology/16.html)

[请教tg如何开启邮箱登录？](https://linux.do/t/topic/155392)

账号仍有设备在线时 Telegram 新设备登录绕过 SMS fee 的方法

这两天 TG 登录出了点问题，记录一下处理过程，给遇到类似情况的人做个参考。

经过

账号原本只在 AyuGram 上登录使用，后来把客户端降级了一次，导致账号信息丢失，需要重新登录。重新登录时提示验证码会发到“已登录设备”上，但一直收不到验证码，尝试了很多方法都没有解决。

中间尝试

用官方 Telegram 登录时提示需要 SMS fee。

用 Telegram X（TGX）登录一直报 400 错误。

期间还去办了张招行万事达卡，打算直接付sms fee，但又遇到和谷歌信息对不上，需要再改资料。

解决方式

后来看到酷安有人提到 Telegram 旧版本可以触发“向其他已登录设备发送验证码”，就按这个思路试了一下，最终成功在手机上登录回来了。

后续打算

手上还有平板和电脑等设备，等账号都确认正常后会升级到最新版，先把 passkey 绑定上，尽量避免之后再遇到类似的登录验证问题。

下载与备份建议

11.6.2 可以在 APKPure 找到；其中 “Telegram” 通常是谷歌版，“Telegram Messenger” 通常是开源版，实测两者都能正常收到“发到其他设备”的验证码。

如果手机有 root，登录恢复后建议用 DataBackup 之类的工具把应用数据额外备份一份，后面遇到风控或登录异常时可以直接恢复。

&#x20;

&#x20;

前段时间换了新手机，发现我的Telegram死活登不上去了。登录的时候要跳SMS收费页面。卸载了无数遍，今天终于被我登录进去了。

下面是我成功的详细方法：

我的设备是oppo findx9 pro
1. 关掉手机的定位功能

1) 用的是日本的节点

2) 关掉wifi,用流量（这一步很，我用wifi都会跳SMS的页面）

3) 卸载掉telegram，重新下载安装

4) 然后就可以成功登录进去了

Telegram注册或新设备登录时跳SMS Fee付费页面怎么办？本视频汇总5种亲测有效的免费绕过方法：

方法1：重装+换新邮箱法 — 最推荐，成功率高

方法2：Telegram X极速版法 — 换新邮箱跳过

方法3：旧版本登录法 — 11.6.1以下版本

方法4：俄罗斯版Telega法 — 无设备在线时可用

方法5：关闭定位+关WiFi+用流量法 — OPPO亲测成功

还分享了绑定passkey和邮箱的建议，防止以后再遇到同样问题。

相关链接见评论区置顶。
#Telegram #SMSFee #绕过SMS费 #Telegram登录 #Telegram注册

0:00 开场摘要

0:41 什么是SMS Fee问题

1:21 方法1：重装+换新邮箱法

2:37 方法2：Telegram X极速版法

3:23 新设备登录的两种情况

4:31 方法5：关定位+关WiFi+用流量法

5:15 建议与Q&A

6:09 总结

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
#Telegram #SMSFee #Telegram登录 #Telegram注册 #绕过SMS费 #Telegram无法登录 #电报登录 #免费登录Telegram #Telegram教程 #Telega

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=ugguWmPE0BI)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/telegram-sms-5-free/)
