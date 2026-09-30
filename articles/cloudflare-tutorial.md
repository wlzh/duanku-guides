# 零基础 Cloudflare 优选教程｜网站速度翻倍提升

面向零基础读者介绍 Cloudflare 优选 IP 的原理、测速筛选、线路配置和结果验证，重点说明不同运营商的延迟与丢包差异。

> 完整图文与持续更新版本：[零基础 Cloudflare 优选教程｜网站速度翻倍提升](https://869hr.uk/2026/tech/cloudflare-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/cloudflare-tutorial/
- 更新：2026-05-20
- 分类：技术
- 关键词：Cloudflare优选、CDN加速、网站优化、DNS分地区解析、阿里云DNS
- 视频：https://www.youtube.com/watch?v=Gi9X3oFqlWE

## 正文

<!-- 文章摘要 -->
> 
至于为什么联通的延迟那么高, 根本原因是联通能用的亚太ip丢包都特别严重, 严重到非高峰期20%丢包, 根本没法正常用.(至少没发现联通不丢包的亚太ip) 因此联通走的是LAX....

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=Gi9X3oFqlWE)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 10 分钟。

先看优选结果图，

至于为什么联通的延迟那么高, 根本原因是联通能用的亚太ip丢包都特别严重, 严重到非高峰期20%丢包, 根本没法正常用.(至少没发现联通不丢包的亚太ip) 因此联通走的是LAX.
# &#x20;一. 啥是优选, 对我网站的优化明显吗?

由于众所周知的原因, Cloudflare 的大部分节点在高峰期的表现的不堪入目. 所以引申出了节点优选. 通常是把特定区域的流量引导至我们想要的 PoP(例如 HKG/NRT/SIN). 优选的节点通常会有更优的线路和性能. 优选的原理如下:

```yaml

用户 (海外或大陆)

|

v

第三方 DNS 服务商 (例如阿里云, 华为云的解析服务)

|

v

├── 海外用户返回 Cloudflare 分配的IP

└── 大陆用户返回 自定义的 Cloudflare IP

|

v

用户访问对应节点, 实现优化

```

至于效果是否明显, 我觉得还是挺明显的. 大部分前端文件都可以被Cloudflare Edge缓存, 最明显的效果就是静态资源和前端页面加载的更快了, 用户只需要等待Cloudflare Edge返回api请求即可.
# &#x20;二. 如何为我的网站配置优选?

从本段开始就是正式教程了. 只要你按照教程一步一步做, 我就不信还有人能看不明白. (要是还看不明白我就真没招了)
## &#x20;1. 检查条件

必要条件, 没有的可以不用往下看了

* 一个有支付方式的Cloudflare 账号 (据说此步骤可以卡bug跳过检查, 可自行查找解决方法)

* 至少一个可用的主域绑定在Cloudflare 上, 至少一个可添加多个解析的子域名(不同主域). (单域名接入请看我的另一个优选教程)

* 一个支持分地区解析的DNS服务商 (例: 阿里云, 腾讯云, 华为云…)
## &#x20;2. 基础配置

**A. 配置回源**

根据情景带入, 我的主域是 sin.fan, 回源域名为 abab.sin.fan. 所以我先为回源添加一个解析:

&#x20;

**B. 配置自定义主机名**

依据情景带入和上一步添加的回源解析, 我的回源是 abab.sin.fan; 用户要访问的域名是 [abab.rikka-ai.com ](http://abab.rikka-ai.com/). 根据这些信息, 进行配置:

I. 转到配置页面

查看侧边栏, 点击自定义主机名

&#x20;

II. 配置默认回源

在主页面配置回源, 回源就是你在步骤A中添加的解析. 我设置的是 abab.sin.fan. 你应该替换为你自己配置的回源.

&#x20;

III. 添加自定义主机名

现在回源配置完毕, 开始添加自定义主机名.

根据情景带入, 用户应该用 [abab.rikka-ai.com ](http://abab.rikka-ai.com/)访问我的网站.

首先点击 “添加自定义主机名按钮”:

&#x20;

随后在新的页面中完成添加:

&#x20;

最后点击添加自定义主机名按钮保存设置.

至此, 你已经完成了本步骤: 基础配置.
## &#x20;3. 开始接入主机名并完成优选

还记得你在步骤 2.B.III 中配置的自定义主机名吗? 当你成功配置后, 自定义主机名主页会有个类似的卡片:

&#x20;

待会需要你根据卡片中的内容, 进行设置

**A.接入支持分地区解析的服务商**

根据情景带入, [abab.rikka-ai.com ](http://abab.rikka-ai.com/)是我要接入的域名.

这里用阿里云作为示例, 你应该根据你使用的服务商自行调整:

I. 添加域名

将 [abab.rikka-ai.com ](http://abab.rikka-ai.com/)添加到阿里云中, 你应该会收到如下提示:

&#x20;

点击 `TXT授权验证` 会打开一个新的卡片:

&#x20;

根据卡片的描述, 我们需要给 [alidnscheck.rikka-ai.com ](http://alidnscheck.rikka-ai.com/)添加TXT解析,

这里需要你转到原DNS服务商添加解析, 例如我的 [rikka-ai.com ](http://rikka-ai.com/)托管在 Cloudflare 上, 因此我需要到 Cloudflare 上添加解析:

&#x20;

现在回到阿里云, 点击验证. 等待验证通过.

验证通过后, 进入配置页, 查看阿里云为你分配的名称服务器:

&#x20;

转到原服务商, 为子域添加NS解析:

&#x20;

添加完成后, 回到阿里云. 刷新页面后应该能看见 `域名的DNS信息配置正确。` 提示.

II. 添加解析

根据自定义主机名卡片中的要求, 添加以下解析:

TXT:

`_acme-challenge` :

&#x20;

`_cf-custom-hostname` :

&#x20;

接下来是CNAME解析, 一共两条

第一条为 Cloudflare 要求你设置的回源解析, 根据情景导入, 我的回源是 abab.sin.fan, 因此我先添加一条 **解析请求来源为境外&#x20;**&#x7684; CNAME 解析:

&#x20;

第二条为 **为国内流量提供优化的&#x20;**&#x43;NAME 解析, 因此解析请求来源设置为中国地区, 内容为任意的优选域名, 这里我推荐 **saas.sin.fan&#x20;**:

&#x20;

III. 检查是否生效

现在回到 Cloudflare 的自定义主机名页面, 点击刷新. 如果两个待定均变为有效, 代表你的所有设置均是正确的! 至此本篇教程已经结束.

&#x20;

本教程从零开始教你配置 Cloudflare 节点优选，将大陆用户流量引导至最优 PoP 节点，显著提升网站加载速度。

教程内容包括：
1. 优选原理讲解
2. 回源域名配置
3. 自定义主机名设置
4. 阿里云分地区 DNS 解析接入
5. TXT 验证 + CNAME 解析配置
6. 最终生效验证

适用于已有 Cloudflare 账号和域名的站长，跟着做就能完成配置。

0:00 开场摘要

0:40 优选效果展示 1

1:04 优选效果展示 2

1:24 什么是优选

2:20 前置条件检查

2:59 配置回源解析

3:32 转到自定义主机名页面

3:50 配置默认回源

4:13 添加自定义主机名 按钮

4:33 添加自定义主机名 表单

4:54 自定义主机名验证状态

5:15 添加域名到阿里云

5:34 TXT授权验证 卡片

5:59 TXT授权验证 添加解析

6:16 NS解析 名称服务器

6:39 NS解析 添加记录

6:52 DNS配置验证通过

7:12 添加TXT acme challenge

7:37 添加TXT cf custom hostname

7:48 添加CNAME 境外

8:13 添加CNAME 国内优选

8:32 验证最终生效

8:54 总结回顾

9:30 相关资源

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
#Cloudflare优选 #CDN加速 #网站优化 #DNS分地区解析 #阿里云DNS #自定义主机名 #节点优选 #网站提速 #Cloudflare教程 #建站教程

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=Gi9X3oFqlWE)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/cloudflare-tutorial/)
