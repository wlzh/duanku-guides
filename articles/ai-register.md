# 零基础用AI写浏览器自动化！手把手教你做注册机

面向零代码基础读者演示如何借助 AI 编写浏览器自动化注册脚本，包含需求拆解、元素定位、运行调试和失败处理方法。

> 完整图文与持续更新版本：[零基础用AI写浏览器自动化！手把手教你做注册机](https://869hr.uk/2026/tech/ai-register/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/ai-register/
- 更新：2026-05-26
- 分类：技术
- 关键词：浏览器自动化、AI编程、零基础教程、注册机、Claude Code
- 视频：https://www.youtube.com/watch?v=Rd0nEHsvIXY

## 正文

<!-- 文章摘要 -->
> 
这次带来的教程是零基础教程，没错是零基础，注意有代码基础的就不要喷我了，我是一个0代码基础的男人...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=Rd0nEHsvIXY)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 7 分钟。

这次带来的教程是零基础教程，没错是零基础，注意有代码基础的就不要喷我了，我是一个0代码基础的男人

用到的工具是：Claude code，opencode 模型用的是 DeepSeek，GPT-5.5（5.5只是负责修bug）

编写程度：手工结合ai

难度：0
1.我们要有目标，也就是url

url是什么就是，你打开浏览器，浏览器里面的

如果比如你要制作什么自动化是吧

你先打开你要的url

然后呢如果是大力出奇迹的话可以选择f12-里面有个

或者是谷歌浏览器里面的f12-

把你动作录制下来，然后下次在你要自动化的界面进行播放就好了

但是我们今天讲的是另一个方法，定位器结合驱动规则进行自动化

所以依旧是打开想要自动化的url

然后按f12

红框的内容是元素选择器，点击这个来选择我们要自动化输入的位置，等等相当于定位

比如我现在选择的是

你会发现元素选择选择网页的时候右边的元素代码会跟着动，你把鼠标指针在右边代码来回移动你会发现左边的页面也跟着动，好你在右边的代码里面选择你要定位的输入位置右键复制

把复制的outerhtml 丢给ai

然后跟ai说：

我要创建一个xxx 自动化扩展或者是js脚本或者是py脚本

帮我把下面内容提取高价值属性，autocomp name 匹配使用最优的选择定位器，提取制作为驱动规则和自动化

然后ai就哔哩哔哩的给你写了,我这里推荐的化制作为浏览器扩展，新人友好一点

然后就可以去运行调试了，扩展安装的化一般是点击扩展管理

然后打开扩展的界面，这样子

扩展里面的开发者选项一定要打开，然后加载这个解压扩展就相当于是你让ai写扩展的哪个文件夹

推荐你写的时候让ai帮你加入：浏览器右侧面板界面和动态运行日志：运行日志格式：中文标签 ai友好型结构化json，完整的错误内容

方便你后续让ai修bug

扩展的错误一般都可以在f12的控制台看，也可以在扩展管理里面看，每次修完bug记得重新加载浏览器扩展和刷新url

教程结束，谢谢各位观看

至于为什么不写协议自动化教程，因为能力有限，没有办法过风控拦截，如果花钱打码的话我认为不值得

至于为什么说用ds，因为目前最稳定的破限制方案就是混搭破，众所周知国模是没道德的，所以搭配gpt5.5修bug也是一种吧

遇到了几个问题。
1.gpt不愿意全自动化
2.我手动去抓dom，一步步让gpt写，他愿意，但是遇到cloudflare，他不愿意给过。

答案是，
1. 切opus，切DeepSeek

2，同理，cloudflare是请求参数异常，才会出，可以网上再找一下，缝合一下，最省事

零基础也能用AI写浏览器自动化！本教程手把手教你：1.打开目标URL 2.F12元素选择器定位 3.复制outerHTML给AI 4.AI自动生成浏览器扩展 5.安装调试运行。用Claude Code+DeepSeek，无需编程基础！不涉及协议注册，纯浏览器驱动方案。#浏览器自动化 #AI编程 #零基础教程

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

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=Rd0nEHsvIXY)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/ai-register/)
