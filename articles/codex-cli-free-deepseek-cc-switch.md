# Codex CLI 免费接入 DeepSeek！CC Switch 本地路由三步搞定

1:15721） 3️⃣ 切换供应商，重启 Codex（即可使用 DeepSeek V4 Flash 等模型） 整个过程对 Codex 完全透明，API Key 保存在 CC Switch 里不暴露给 Codex 配置文件，安全又方便

> 完整图文与持续更新版本：[Codex CLI 免费接入 DeepSeek！CC Switch 本地路由三步搞定](https://869hr.uk/2026/tech/codex-cli-free-deepseek-cc-switch/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/codex-cli-free-deepseek-cc-switch/
- 更新：2026-06-01
- 分类：技术
- 专题：技术、AI
- 关键词：Codex、DeepSeek、CC Switch、API路由、协议转换
- 视频：https://www.youtube.com/watch?v=3C7YQRjnZzY

## 正文

<!-- 文章摘要 -->
> 
**开头：你的 Codex 是不是也"水土不服"？**...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=3C7YQRjnZzY)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 7 分钟。**开头：你的 Codex 是不是也"水土不服"？**

很多人拿到 Codex CLI 的第一反应是：能不能接 DeepSeek、Kimi 这些国产模型？

毕竟 OpenAI 的 API 贵，国内模型性价比高得多。

但一上手就懵了——把 DeepSeek 的 API 地址填进 Codex 配置，要么模型列表不对，要么直接 404。**问题出在哪？协议不兼容。**

Codex CLI 用的是 OpenAI Responses API（ `/responses` ），而 DeepSeek、Kimi、MiniMax、SiliconFlow 这些供应商走的是 Chat Completions API（ `/chat/completions` ）。

这两种协议的请求体、流式事件、返回结构完全不一样，直接填进去当然不行。**CC Switch 的解决方案很简单：在本地搭一个"翻译层"，让 Codex 以为自己在跟 OpenAI 对话，实际请求全部转给 DeepSeek。*****
## **CC Switch 是什么？**

一句话：一个本地的 AI 编码工具路由器。

它能让你在 Claude Code、Codex CLI、OpenClaw 等多个 AI 编码工具之间自由切换供应商，核心能力就是**协议转换 **。

对 Codex 来说，CC Switch 的工作流程是这样的：
1. 1\. Codex 始终连本机 `http://127.0.0.1:15721/v1` ，发 Responses API 请求
2. 2\. CC Switch 识别到当前供应商是 Chat 格式（ `apiFormat = "openai_chat"` ）
3. 3\. 把请求改写成 Chat Completions 格式发给 DeepSeek
4. 4\. DeepSeek 返回后，再把响应转回 Responses 格式给 Codex

整个过程对 Codex 完全透明，它根本不知道背后换了个供应商。***
## **三步搞定：Codex 接入 DeepSeek**
###**准备工作**

你需要三样东西：

* • ✅ 已安装 CC Switch（3.16.0+）

* • ✅ 已安装 Codex CLI（至少运行过一次，让 `~/.codex/ `[`config.toml`](http://config.toml) 存在）

* • ✅ DeepSeek API Key（从 [platform.deepseek.com ](http://platform.deepseek.com)\[1] 获取）

***
###**第一步：添加 DeepSeek 供应商**

打开 CC Switch，切到顶部的**Codex **标签，点击右上角的**+ **添加供应商。

选择内置预设里的**DeepSeek **，只需要做两件事：
1. 1\. 填入你的 DeepSeek API Key
2. 2\. 点击保存

预设已经帮你配好了 DeepSeek 的请求地址、默认模型、模型菜单、thinking/reasoning 参数，并且自动开启了"需要本地路由映射"。

你不需要手动拼任何接口路径，CC Switch 的 DeepSeek 预设全部搞定。***
### **第二步：开启本地路由，接管 Codex**

进入 CC Switch 的**设置 → 路由 **页面，完成两个开关：
1. 1\.**打开路由总开关 **— 启动本地服务，默认地址 `127.0.0.1:15721`
2. 2\.**在"路由启用"中打开 Codex **— 如果只想让 Codex 走路由，Claude 和 Gemini 的开关可以保持关闭

接管后，CC Switch 会自动把 Codex 的 live 配置指向本机路由，并用占位符管理认证。**你的 DeepSeek API Key 永远保存在 CC Switch 里，由本地路由在转发时注入，不会暴露给 Codex 的配置文件。**

这一点比直接把 Key 写进 Codex 配置安全得多。***
### **第三步：切换供应商，重启 Codex**

回到 Codex 供应商列表，点击 DeepSeek 供应商的**启用 **。

如果看到"需要路由"标记，说明这个供应商必须在路由运行时使用——这是正常的。

切换后，**建议重启当前 Codex 终端会话 **。原因有两个：

* • Codex 进程可能已经缓存了旧的 [`config.toml`](http://config.toml)

* • 模型目录（ [`modelcatalog.json`](http://modelcatalog.json) ）需要新进程才能刷新

重启后进入 Codex，输入 `/model` 查看，应该能看到 DeepSeek 的模型，比如 **DeepSeek V4 Flash**。

***
##**其他 Chat 供应商怎么接？**

不只是 DeepSeek，Kimi、MiniMax、SiliconFlow 等常见 Chat 格式供应商在 CC Switch 里都有预设，操作流程完全一样：
1. 1\. 选预设 → 填 Key → 保存
2. 2\. 开路由 → 接管 Codex
3. 3\. 切换 → 重启**只有预设里没有的供应商才需要手动配置 **，这时选"自定义"，按对方文档填 API Key、base URL，把 API 格式选为"OpenAI Chat Completions（需开启路由）"即可。

如果上游直接支持 Responses API（比如 OpenAI 官方），就不需要开路由，CC Switch 可以直连。***
## **常见问题速查****Q：Codex 报 404 或找不到 /responses？ **

检查 `~/.codex/ `[`config.toml`](http://config.toml) 是否指向 `http://127.0.0.1:15721/v1` 。通常是没开启 Codex 接管，或者手动把上游地址写给了 Codex。**Q：DeepSeek 上游报 404？ **

用的是内置预设的话，先确认 Codex 路由已启用。自定义供应商才需要检查 base URL——应该是服务根地址（如 [`https://api.deepseek.com`](https://api.deepseek.com) ），不是完整接口路径。**Q：/model 看不到 DeepSeek 模型？ **

保存供应商后重启 Codex。CC Switch 会生成模型目录，但运行中的 Codex 不会热加载。**Q：开了路由但请求走错供应商？ **

确认三处一致：Codex 标签下当前供应商是 DeepSeek、路由服务正在运行、路由启用里 Codex 开关已打开。**Q：能用官方 OpenAI 账号走本地路由吗？ **

不建议。CC Switch 会在接管模式下阻止切到官方供应商，用代理访问官方 API 可能有账号风险。路由主要用于第三方、聚合或协议转换场景。***
## **写在最后**

Codex CLI 是个好东西，但它的协议限制让很多人卡在了"只能用 OpenAI"这一步。

CC Switch 的本地路由方案，本质上就是做了一层协议翻译——让 Codex 不用改一行代码，就能接入 DeepSeek 等国产模型。

三步配置，全程零代码，API Key 还不暴露给 Codex。

文章满满都是干货，最后大家不要忘记 「**点赞 **」 和 「**关注 **」以免之后找不到了。**CodeX可以支持国产模型后你怎么看？评论区聊聊？**

很多人拿到 Codex CLI 后想接入 DeepSeek 等国产模型，但一上手就发现——协议不兼容！Codex 用的是 OpenAI Responses API，而 DeepSeek 走的是 Chat Completions API，直接填地址根本不行。

本视频教你用 CC Switch 在本地搭一个「翻译层」：

1️⃣ 添加 DeepSeek 供应商（内置预设，只需填 API Key）

2️⃣ 开启本地路由，接管 Codex（地址 127.0.0.1:15721）

3️⃣ 切换供应商，重启 Codex（即可使用 DeepSeek V4 Flash 等模型）

整个过程对 Codex 完全透明，API Key 保存在 CC Switch 里不暴露给 Codex 配置文件，安全又方便。不仅是 DeepSeek，Kimi、MiniMax、SiliconFlow 等 Chat 格式供应商同样适用！

📌 CC Switch 本地路由核心优势：

• 协议自动转换：Responses API ↔ Chat Completions API

• 支持批量供应商一键切换

• API Key 本地存储，安全隔离

• 零代码，三步搞定

常见问题速查：

• Codex 报 404？检查 config.toml 是否指向 127.0.0.1:15721/v1

• 看不到 DeepSeek 模型？保存供应商后重启 Codex

• 请求走错供应商？确认三处一致：供应商选对了、路由在运行、Codex 开关已打开

📎**本视频涉及资源：**
- `config.toml`: http://config.toml
- platform.deepseek.com: http://platform.deepseek.com
- `modelcatalog.json`: http://modelcatalog.json
- `https://api.deepseek.com`: https://api.deepseek.com

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

- [YouTube视频原地址](https://www.youtube.com/watch?v=3C7YQRjnZzY)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/codex-cli-free-deepseek-cc-switch/)
