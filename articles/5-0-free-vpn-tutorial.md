# 5分钟搭建0成本完全免费VPN节点-手把手喂饭级教程

因为是cloudflare的ip，如果一些对家庭宽带IP、纯净IP等有要求的，比如Claude、ChatGPT等软件，需要落地的，可以看评论区的链接开通，如果不会链式代理、落地IP配置等，可以看往期教程，或者访问博客链接 5分钟搭建0成本完全免费的VPN节点，手把手喂饭级教程

> 完整图文与持续更新版本：[5分钟搭建0成本完全免费VPN节点-手把手喂饭级教程](https://869hr.uk/2026/tech/5-0-free-vpn-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/5-0-free-vpn-tutorial/
- 更新：2026-05-15
- 分类：技术
- 专题：技术、AI
- 关键词：VPN、Cloudflare、零成本、Workers、edgetunnel
- 视频：https://www.youtube.com/watch?v=HLqqF0QZcec
- 系列：[出海网络搭建](../series/overseas-network.md)、[出海 VPS](../series/vps.md)

## 正文

<!-- 文章摘要 -->
> 
2. 地址是 [https://dash.cloudflare.com/ ](https://dash.cloudflare.com/)，这里推荐使用小号，别是正式邮箱， **因为有风控的风险**。...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=HLqqF0QZcec)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 8 分钟。

1. **注册 cf账号**
2. 地址是 [https://dash.cloudflare.com/](https://dash.cloudflare.com/)，这里推荐使用小号，别是正式邮箱，**因为有风控的风险**。

1) 进入页面，右上角可以选择语言，简体中文，点击注册；

2. 输入邮箱+密码，勾选统一，并点击注册，出现如下图：

3. 这时先不用管这个界面，可以直接关闭掉，

4. 直接去你的邮箱，会收到一封cf的确认邮件：

* 会重新进入一个新的页面，一路跳过就行了，

* 直到进入如下界面：

* **这时代表已完成cf的账号注册了。**

* **下载部署的js脚本**

* 下载地址： <https://github.com/cmliu/edgetunnel>

1. 如图，点击对应文件，进入到文件界面

2. 让点击如图的，下载按钮

* 下载完成后去下载目录下找到刚才下载的文件，并使用混淆工具进行混淆，这里我使用的是 [https://cf-obfuscator.pages.dev/](https://cf-obfuscator.pages.dev/)来混淆的，混淆后重命名为 \_worker.js，同时创建一个新文件夹（名字随便起，我就叫新建文件夹），然后把混淆后的文件放入文件夹中

* 到这里，就完成了部署的脚本准备工作。

* **配置pages**

* 创建workers 数据库

1. 创建KV命名空间

2. 如图点击创建应用程序

3. 到这个界面，点击开始使用

4. 如图，在拖放文件右边按钮，点击开始使用

5. 为项目创建名称，随便输入字母加数字，这里我们输入test1，点击创建项目

* 然后重新返回菜单 Workers 和 Pages

* 然后点击项目名称test1

* 点击设置、添加按钮

* 添加变量和机密，**设置变量名称，注意必须是大写的 ADMIN（不要问为什么，我也不知道）**

1. 然后输入密码，并点击保存，密码要记住

* 添加绑定

1. 点击KV命名空间

2. 输入大写KV，并选择前面创建的KV数据库名称后，点击保存

3. 选择部署，点击上传资产

4. 选择文件夹，把前面下载的文件\_worker.js在这里上传上去

5. 点击上传按钮

6. 点击"部署站点"

7. 然后显示部署成功，这个url记住，后面我们需要访问

* 到这里，恭喜佬们，你已经完成了对cf的所有配置。

* **配置节点**

* 使用上面的域名输入到浏览器，并添加后缀admin，就是刚才变量和机密的录入项，并回车确认

1. 然后输入部署成功后生成的url，并斜杠加admin后缀，如图

* 这时会出现如下界面，输入上面设置的admin的密码，点击立即登录

* 登录后进入界面，里面就有订阅地址了，拷贝

1. 复制到v2ray中，

2. 点击更新订阅

3. 就刷新出节点了

* 至此你已经有免费节点可以使用了，但是节点质量会很一般。

* **优选节点**

* 进入网址 [https://bestcf.pages.dev/](https://bestcf.pages.dev/)，进入后点击最下面的《优选》按钮

回到刚才的面板界面，在优选订阅模式选择《自定义订阅》，并删除地址的内容

把导航站中的优选地址赋值粘贴到《自定义优选地址》中，**一行一个**

至此，你完成了节点优选的所有配置。

再次进入自己的V2rayN，更新你的订阅

恭喜你，现在开始你就有用不完的订阅了，而且**免费、免费、免费**，且网速实测还不错。

我上面的优选节点只是我随意测试的几个，佬们可以自行详细测试，总有网速快且干净的节点。

因为是cloudflare的ip，如果一些对家庭宽带IP、纯净IP等有要求的，比如Claude、ChatGPT等软件，需要落地的，可以看评论区的链接开通，如果不会链式代理、落地IP配置等，可以看往期教程，或者访问博客链接https://869hr.uk中更多内容获取。

5分钟搭建0成本完全免费的VPN节点，手把手喂饭级教程！

本教程教你利用 Cloudflare Workers Pages 搭建完全免费的 VPN 节点，无需服务器、无需域名、零成本！

步骤概要：
1. 注册 Cloudflare 账号（建议用小号邮箱）
2. 下载 edgetunnel 脚本并混淆
3. 创建 Workers 数据库和 KV 命名空间
4. 配置 Pages 项目，上传脚本部署
5. 设置 ADMIN 变量和 KV 绑定
6. 访问管理面板获取订阅地址
7. 导入 V2rayN 更新订阅

8. 优选节点提升网速

免费节点实测网速不错，适合日常使用。如需纯净IP落地（Claude/ChatGPT等），可参考评论区链接。

更多教程访问博客：https://869hr.uk

0:00 开场总结

0:32 核心概念

1:11 步骤总览

1:51 注册Cloudflare账号

2:41 下载脚本并混淆

3:38 配置Pages

4:30 设置环境变量和绑定

5:20 上传脚本并部署

6:01 配置节点

6:59 优选节点

7:52 资源汇总

8:34 结尾订阅

注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有 🔗https://869hr.uk

## 短信及语音接码平台

- 或https://smspva.com/?ref=1307601

纯净住宅IP白嫖流量
- 500M试用， 链接 https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN ， 85 折优惠
- 200M试用，链接 https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码GXJDIAN， 9 折优惠
1. 微信讨论群：https://qr.869hr.uk/aitech
2. 超过100T资料总站网站：https://doc.869hr.uk
3. Telegram群聊：https://t.me/tgmShareAI
4. 微信公众号：搜"AI前沿的短裤哥"
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
#VPN #免费VPN #Cloudflare #V2ray #科学上网 #零成本 #Workers #edgetunnel #优选节点 #教程

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=HLqqF0QZcec)
- [相关推荐](https://869hr.uk)

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/5-0-free-vpn-tutorial/)
