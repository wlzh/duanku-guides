# 三方API登录下用手机远控Codex，手把手小白教程

介绍电脑端 Codex 使用第三方或中转 API 时的手机远程控制方案，涵盖连接架构、配置步骤、安全边界和常见故障排查。

> 完整图文与持续更新版本：[三方API登录下用手机远控Codex，手把手小白教程](https://869hr.uk/2026/tech/api-mobile-codex-beginner-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/api-mobile-codex-beginner-tutorial/
- 更新：2026-06-13
- 分类：技术
- 专题：技术、AI
- 关键词：Codex、codex++、三方API、手机远控、ChatGPT
- 视频：https://www.youtube.com/watch?v=_CDCt2OMcOM

## 正文

<!-- 文章摘要 -->
> 
电脑端 Codex 使用三方 API 或中转 API 时，手机端 ChatGPT 里的 Codex 远程连接无法使用。...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=_CDCt2OMcOM)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 10 分钟。

电脑端 Codex 使用三方 API 或中转 API 时，手机端 ChatGPT 里的 Codex 远程连接无法使用。

处理方法是在 codex++ 里使用混合模式，实现两者功能叠加。

电脑端可以继续使用三方 API，手机端也可以通过 ChatGPT 连接 Codex。
## 准备条件
1. 电脑已经安装最新 Codex。
2. 电脑已经安装最新 codex++。
3. 已经有可用的三方 API。
4. 已经有三方 API 的 `baseurl` 和 `key` 。
5. 电脑端 Codex 能正常登录 ChatGPT 账号。
6. 手机端已经安装最新版 ChatGPT。

如果手机端没有 Codex 入口，先更新 ChatGPT。

如果 chtgpt 登录后的电脑端 Codex 左下角没有手机图标，先更新 Codex。
## 第一步：开启代理 TUN 模式

先打开代理软件，开启 `TUN` 模式。

这一步是为了让手机能正常连接电脑端 codex ，实测不开启连接不到。
##  
## 第二步：打开 CCS（CC Switch），把供应商切回官方

打开 CCS，在供应商配置里，先把 Codex 使用的供应商切回官方。

这里是个大坑，虽然 codex++ 也可以切到官方登录，但是用 codex++ 打开后无法正常登录 chatgpt 账号，一定不要用 codex++ 打开。这里使用了 ccs 进行配置切换。下面是 codex++ 官方解释。

 
## 第三步：直接打开 Codex

注意：这里不要通过 codex++ 打开 Codex。

直接打开 Codex 客户端，打开后使用 ChatGPT 登录。

 
## 第四步：打开 codex++ 管理工具

关闭 Codex 后，打开 codex++ 管理工具。

 
## 第五步：添加新的供应商

进入供应商配置页面。

点击添加供应商。

这里新建一个配置，不建议直接覆盖原来的配置。
## 第六步：选择官方登录和混入 API Key

在新增供应商配置里，接入模式选择官方登录。

API Key 处选择混入 API Key。

这一步比较关键。

官方登录用于保留 Codex 的账号状态。

混入 API Key 用于让 Codex 请求走你的三方 API。
## 第七步：填写 Base URL 和 Key

继续填写三方 API 信息，如下图。

确认模型列表能拉出来后，再点击保存。
## 第八步：启用新配置并重启 codex++

保存后，回到供应商列表，启用刚才新建的配置，然后点击重启 codex++。

 
## 第九步：确认 Codex 登录状态

Codex 打开后，确认还是登录状态。

然后看左下角是否有手机图标。

如果有手机图标，说明电脑端基本准备好了。

如果没有手机图标，按下面顺序检查：
1. Codex 是否是最新版。
2. Codex 是否已经登录 ChatGPT 账号。
3. 前面是否先切回官方供应商登录过。
4. codex++ 是否已经重启。
5. 当前配置是否是官方登录 + 混入 API Key。
##  
## 第十步：手机端打开 ChatGPT

手机端下载并打开最新版 ChatGPT。

建议手机端使用全局模式（这里可能要重新登录一次），并挂美国节点（美国节点可用，其他地区可以自己测试）。

如果手机端没有 Codex 入口，检查 ChatGPT 是否是最新版。
## 第十一步：在手机端进入 Codex

打开 ChatGPT 后，左侧栏点击更多。

点击 Codex

然后按提示进行登录和授权。

这里按页面提示操作即可。

如果登录页加载不出来，换节点后重试。
## 第十二步：完成远程连接

登录完成后，手机端就可以远程连接电脑上的 Codex。

这时电脑端仍然可以使用三方 API 配置。

手机端只是通过官方登录状态连接到电脑端 Codex。

连接成功后，手机端代理可以切回规则模式。
#
# 最新版的CCS也可以使用混合模式
# 可以在不使用codex++的实现混合模式
## 第一步：更新CCS到最新版，打开CCS的设置
## 第二步：打开codex应用增强的切换第三方时保留官方登录 ，即可。

电脑端 Codex 使用三方 API 时，手机端 ChatGPT 无法远程连接？本教程手把手教你用 codex++ 混合模式，实现三方 API + 手机远控同时使用。12步搞定，小白也能跟着操作。

📝 本视频涉及资源：
- codex++ 下载：https://github.com/nicepkg/codex-plus-plus
- CCS (CC Switch) 下载：https://github.com/nicepkg/cc-switch

⏱️ 章节时间轴：

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
7. Bybit支付卡申请链接 https://www.bybit.com/invite?ref=LGNQRG，教程链接https://youtu.be/3sN7P2t_CeA

8. YiKa虚拟卡实操开卡教程，不需KYC，一个邮箱开50张卡，订阅ChatGPT/Claude/推特蓝V出海必备https://youtu.be/9CSa9CEz9Hw

## YouTube 播放列表

- AI产品&技术相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海VPS相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=_CDCt2OMcOM)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/api-mobile-codex-beginner-tutorial/)
