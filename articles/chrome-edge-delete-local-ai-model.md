# 🚨你的硬盘被偷吃了？Chrome/Edge暗中下载4GB大模型！教你彻底关闭并删除本地AI【保姆级教程】

最近C盘空间莫名其妙少了几个G？罪魁祸首可能是Chrome或Edge浏览器！Google和微软正悄悄在后台下载接近4GB的本地AI模型，教你彻底删除和禁用。

> 完整图文与持续更新版本：[🚨你的硬盘被偷吃了？Chrome/Edge暗中下载4GB大模型！教你彻底关闭并删除本地AI【保姆级教程】](https://869hr.uk/2026/tech/chrome-edge-delete-local-ai-model/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/chrome-edge-delete-local-ai-model/
- 更新：2026-05-09
- 分类：技术
- 专题：技术、AI
- 关键词：教程、AI、Google、数据安全
- 视频：https://www.youtube.com/watch?v=KQck0xwjHAw
- 系列：[AI 产品与技术](../series/ai-products-and-technology.md)

## 正文

<!-- 文章摘要 -->
> 
注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有 🔗https://869hr.uk

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=KQck0xwjHAw)</div>

## 你的硬盘被偷吃了？Chrome/Edge暗中下载4GB大模型

最近，不少网友突然发现自己的电脑硬盘空间莫名其妙少了好几个 GB。仔细一查才发现，罪魁祸首竟然是天天在用的 Chrome 浏览器！更离谱的是，Chrome 居然在后台偷偷下载了一个接近 4GB 的本地 AI 模型。

很多人压根不知道浏览器里还藏着 AI 功能，更别说用过了。但模型已经悄无声息地躺在硬盘里了。更夸张的是，不只是 Chrome，微软的 Edge 浏览器也在干同样的事儿。

![22a9ad5507b0c9217a4a61e57c1113b8a26c0ce43cbd08d9ba2dabdee9b6208d.png](https://cdn.gooo.ai/web-images/22a9ad5507b0c9217a4a61e57c1113b8a26c0ce43cbd08d9ba2dabdee9b6208d)

## Chrome 到底偷偷下载了啥？

Google 这次下载的，其实是 **Gemini Nano 本地 AI 模型**。这是 Google 正在推进的"设备端 AI（On-device AI）"计划的一部分。

简单来说，以前浏览器里的 AI 功能都是云端运行的。

![20260509045658 690021](https://cdn.gooo.ai/web-images/08579b254a40a850c9615f253d6a713958f7e31699a87e5f73827146b2755f4c)

比如：

- 智能翻译
- 网页内容总结
- AI 辅助写作
- 自动填充建议

这些功能以前都需要把数据上传到 Google 服务器处理。而现在，Google 想直接把 AI 塞进浏览器里，于是 Chrome 就开始在后台自动下载本地 AI 模型了。

## Google 为啥要这么干？

Google 官方的说法听起来挺美好：

### 1、更快

本地推理不用联网等待，AI 响应速度会更快。

### 2、更保护隐私

因为数据不需要上传云端，理论上你的内容可以直接在本地处理，更安全。

### 3、减少服务器成本

**这个其实才是重点。**

如果大量 AI 请求都放到本地执行，Google 的服务器压力会小很多。某种程度上，你的电脑正在慢慢变成 Google 的 AI 终端。

## 最离谱的问题来了

很多用户压根没开启这些 AI 功能，甚至完全不知道浏览器已经内置了 AI。但模型照样下载。

而且很多用户发现，浏览器占用空间已经超过 5GB，因为除了 AI 模型本体，还包括：

- 缓存文件
- 模型更新包
- 相关依赖库

更尴尬的是，Google 官方表示用户可以在设置里关闭设备端 AI。但现实情况却是，有些用户根本看不到这个选项。也就是说，你甚至没法正常关闭。

## Edge 浏览器也一样

很多人以为"我不用 Chrome，我只用 Edge"就能躲过一劫。但问题是，微软 Edge 同样会自动下载本地 AI 模型，因为微软也在推进设备端 AI。

其功能同样包括：

- Copilot 本地模式
- 智能搜索建议
- 网页内容理解

甚至很多用户根本不用 Edge，但由于 Windows 自带 Edge，只要浏览器偶尔被打开，它就可能开始后台下载模型。

## 如何查看 Chrome 是否偷偷下载了 AI 模型？

如果你用的是最新版的 Chrome，可以在设置中心看到这个选项，但是无法直接通过关闭按钮删除模型。我们需要进入到指定文件夹下进行手动删除。

![20260509045947 686631](https://cdn.gooo.ai/web-images/5361a2d537ea294638e00a58f6051e33949c5e3166bdc63cb64cf9b3c0d91349)

## 删除步骤（Windows 用户）

### 1. 手动删除已下载的模型文件

进入这个路径：

```plaintext
C:\Users\你的用户名\AppData\Local\Google\Chrome\User Data\OptGuideOnDeviceModel\
```

找到文件：**weights.bin**，这就是 Chrome/Edge 浏览器偷偷下载的模型，总共 4G 左右大小。

![20260509050559 122539 scaled](https://cdn.gooo.ai/web-images/ef0ed9820f17f79911d01330a83d7d4b7b90491821c42652631a6fda37f279bb)

**注意：** 如果 chrome://flags 找不到相关选项，就选择下方更彻底的禁止方法！

## Windows 用户：彻底禁止下载的方法（推荐）

Windows 用户可以直接通过注册表禁用。以管理员身份打开 CMD，然后执行：

### 禁用 Chrome 设备端 AI

```plaintext
reg add "HKLM\SOFTWARE\Policies\Google\Chrome" /v "GenAILocalFoundationalModelSettings" /t REG_DWORD /d 1 /f
```

### 禁用 Edge 设备端 AI

```plaintext
reg add "HKLM\SOFTWARE\Policies\Microsoft\Edge" /v "GenAILocalFoundationalModelSettings" /t REG_DWORD /d 1 /f
```

以上命令中的注册表键值 `1` 代表禁用设备端 AI 功能。如果后续你想重新启用，只需要将命令最后的 `1` 改为 `0` 后再次执行即可。

另外，通过注册表或组策略进行修改后，浏览器"关于"页面可能会出现"由你的组织管理"之类的提示。这个只是系统提示，用于说明浏览器策略被修改，并不会影响浏览器的正常使用，也不会对个人账号造成影响。

## Mac 用户如何查看和删除？

Mac 用户可以打开终端执行：

```plaintext
du -sh ~/Library/Application\ Support/Google/Chrome/optimization_guide_model_store
```

如果这里显示有几个 GB 的占用，那说明 Chrome 已经下载了本地 AI 模型。

### Mac 如何删除 Chrome 本地 AI 模型？

首先，彻底退出 Chrome：

```plaintext
pkill Chrome
```

然后删除模型：

```plaintext
rm -rf ~/Library/Application\ Support/Google/Chrome/optimization_guide_model_store
```

建议连下面这个一起删除：

```plaintext
rm -rf ~/Library/Application\ Support/Google/Chrome/OnDeviceHeadSuggestModel
```

## 如何防止 Chrome 再次自动下载？

打开 Chrome 地址栏输入：

```plaintext
chrome://flags
```

搜索：

- optimization guide
- on device

把相关选项全部改成：**Disabled**

尤其是：**#Enables optimization guide on device** 这个最好直接关闭，否则浏览器后面可能会重新下载。

### 进阶防护（让文件无法被重写）

如果你想更彻底地防止模型被重新下载，可以锁定文件：

**macOS:**

```plaintext
chmod 444 weights.bin && chflags uchg weights.bin
```

**Linux:**

```plaintext
chmod 444 weights.bin && sudo chattr +i weights.bin
```

## 为什么浏览器会越来越"重"？

其实现在浏览器的发展方向已经变了。以前浏览器只是"网页查看工具"，而现在 Chrome、Edge、Safari 都在朝"AI 操作系统入口"发展。

未来：

- AI 助手
- 本地大模型
- 智能工作流
- 自动化脚本

可能都会直接内置在浏览器里。而这些功能最终都需要本地 AI 模型支持。所以未来，浏览器占用几十 GB，可能都会慢慢变成常态。

## 到底该不该关闭本地 AI？

其实分两种情况。

### 建议保留的人

如果你经常使用：

- AI 辅助写作
- 智能翻译
- 网页内容总结

那么本地 AI 确实有优势，响应更快，而且数据不需要上传云端，隐私更有保障。

### 建议关闭的人

如果你：

- 硬盘空间紧张（256GB / 512GB 用户）
- 从来不用浏览器 AI 功能
- 更在意系统性能和空间

那关闭会更适合。尤其是 256GB / 512GB 用户，会明显感觉到空间压力。

## 总结

这次 Chrome 和 Edge 自动下载本地 AI 模型，其实只是一个开始。未来，浏览器、Windows、macOS、Office 可能都会默认部署 AI 模型。你的电脑，正在慢慢变成 AI 终端。问题只剩一个：你愿不愿意让它继续占用你的硬盘空间？

---

## 视频时间戳

- 00:00 你的电脑正在被 Google"征用"？
- 01:15 什么是设备端本地 AI 模型？为什么浏览器要偷偷下载？
- 02:40 最离谱的问题：你根本找不到关闭按钮！
- 03:30 Windows 用户：如何查看、手动删除 AI 模型？
- 04:50 Windows 用户：注册表彻底禁止下载方法（强烈推荐）
- 06:10 Mac 用户：终端一键查看与删除模型指令
- 07:20 通用进阶防护：修改 Chrome Flags 防止死灰复燃
- 08:30 到底该不该关闭本地 AI？总结建议

## 相关链接

- [YouTube 视频原地址](https://www.youtube.com/watch?v=KQck0xwjHAw)
- [原文来源 - 推特](https://x.com/wlzh/status/2053107201284436291?s=20)
- [更多教程访问博客主页](https://869hr.uk)
- [超过100T资料总站](https://doc.869hr.uk)
- [微信讨论群](https://qr.869hr.uk/aitech)
- [Telegram 群聊](https://t.me/tgmShareAI)
- [Twitter/X](https://x.com/gxjdian)
- [YouTube 频道](https://youtube.com/@gxjdian)

## VPS 主机推荐

- Claude 用的丽萨主机：https://lisahost.com/aff.php?aff=9424
- 按流量 VPS：https://www.lycheeip.com/home/ip?affId=1AwYIQ7BW8
- 一年 10 美元的多年保底小鸡：https://clients.zgovps.com/?affid=1207
- 各种云主机，主打性价比：https://my.racknerd.com/aff.php?aff=15809
- 美国的 VPS，一年 70 美金搞活动：https://app.cloudcone.com/?ref=13794
- 一年 8.5 美金的美国家宽，稳定靠谱：https://www.webshare.io/?referral_code=55vpv6waorud
- VPS DMIT：https://www.dmit.io/aff.php?aff=21728
- VPS VIRCS 家宽落地机：https://www.vircs.com/welcome?vcd=61a4aae4
- 家宽 IP 链接：https://ipfly.net/activity/OE5TWVlUUEI6TFZKOVhYQzM5NQ==
- 住宅 VPS 链接：https://www.voyracloud.com/?ref_code=5ZG4FHL8

## Gmail、Telegram 等账号购买、礼品卡

- https://accboy7gxjdian.acceboy.com/
- https://universalbus.cn/?s=bvDplWi2fZ
- https://www.gamsgo.com/partner/jGh24
- Claude、OpenAI Codex 等充值：https://bewild.ai?code=GXJDIAN

## eSIM 推荐

1. 三家 eSIM 让国产手机秒变 eSIM 手机，全方面优缺点对比：https://s.869hr.uk/mcc
2. 9eSIM 打 9 折（优惠码：maq）：https://www.9esim.com/?coupon=maq
3. ESTK 打 9 折（优惠码：GXJDIAN）：https://store.estk.me/zh?aid=16007
4. XeSIM 打 9 折（推荐码：gxjdian）：https://xesim.cc/?DIST=RE5FHg==
5. Wise 申请链接（推荐码：lizhiw12）：https://wise.com/invite/ihpc/lizhiw12
6. N26 申请链接（推荐码：lizhiw02766c）：https://youtu.be/HY9OD8rX89s?si=78REb8MyKSJB6cwQ
7. Bybit 支付卡申请链接：https://www.bybit.com/invite?ref=LGNQRG

## 短信及语音接码平台

- https://hero-sms.com/?ref=357885
- https://smspva.com/?ref=1307601

## 代理 IP 推荐

- 500M 试用，链接 https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN，85 折优惠
- 200M 试用，链接 https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码 GXJDIAN，9 折优惠

## YouTube 播放列表

- AI 产品与技术相关：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海 VPS 相关：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

## 关注我不迷路

如果你觉得这期视频对你有帮助，请务必：

- 点赞本视频
- 在评论区留下你的问题或成功注册的截图
- 订阅频道并打开小铃铛，获取最新硬核白嫖教程和科技前沿资讯！
- 微信公众号：搜"AI前沿的短裤哥"

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/chrome-edge-delete-local-ai-model/)
