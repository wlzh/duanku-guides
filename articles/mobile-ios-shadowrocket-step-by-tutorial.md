# 苹果手机iOS定位修改到世界任何地方｜Shadowrocket小火箭保姆级教程 无需越狱

本教程教你用 Shadowrocket（小火箭） 把 iPhone 的定位改到世界任何地方， 无需越狱、无需电脑、无需开发者账号 。跟着一步步做即可。

> 完整图文与持续更新版本：[苹果手机iOS定位修改到世界任何地方｜Shadowrocket小火箭保姆级教程 无需越狱](https://869hr.uk/2026/tech/mobile-ios-shadowrocket-step-by-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/mobile-ios-shadowrocket-step-by-tutorial/
- 更新：2026-07-11
- 分类：技术
- 关键词：iOS定位修改、Shadowrocket、小火箭、iPhone定位、虚拟定位
- 视频：https://www.youtube.com/watch?v=aQdeFAPeVM8

## 正文

<!-- 文章摘要 -->
> 
# 苹果手机iOS定位修改到世界任何地方 · 小白入门到进阶保姆级教程...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=aQdeFAPeVM8)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 12 分钟。

# 苹果手机iOS定位修改到世界任何地方 · 小白入门到进阶保姆级教程

本教程教你用 **Shadowrocket（小火箭）**** **把 iPhone 的定位改到世界任何地方，**无需越狱、无需电脑、无需开发者账号**。跟着一步步做即可。

***
## 准备条件

* 一台 iPhone或iPad

* **Shadowrocket（小火箭）App**（App Store 付费应用，需先买好装好）

* 能正常联网

* 项目链接，见评论区链接 https://github.com/mekos2772/ios-location-spoofer

***
## 第一步：导入模块
1. 打开**Shadowrocket**
2. 底部点**「配置」**
3. 找到**「模块」 **，点右上角**「+」**

* 选 **「来自 URL」**，粘贴下面这个地址：

```plaintext
https://raw.githubusercontent.com/mekos2772/ios-location-spoofer/main/ios-location-spoofer.sgmodule
```

* 保存。回到模块列表，确认这条 **「iOS Location Spoofer」前面是勾选/启用**状态（右侧有个 ✓）

✅ 模块导入完成。

***
## 第二步：打开 HTTPS 解密
1. 进入**「HTTPS 解密」 **页面。不同 Shadowrocket 版本入口可能不同：

* Shadowrocket iOS 2.2.88(3308) 实测路径：底部点 **「配置」**→ 找到当前正在使用的配置文件 → 点右侧 **「ⓘ」**→ 进 **「HTTPS 解密」**

* 旧版 / 部分界面：底部点 **「设置」**→ 进 **「HTTPS 解密」**

* 如果在「设置」里找不到「HTTPS 解密」，不代表没有这个功能，优先按第一条从配置文件右侧「ⓘ」进入。

* 把 **「HTTPS 解密」**开关打开（变蓝）

* 注意：有的版本这里只有 **一个**开关，那是正常的，它本身就是中间人解密。旧教程截图里多出的"HTTP/2 MitM"开关是可选项，没有不影响。

* 看中间的 **「域名」**列表，确认包含这四个（导入模块后通常会自动出现）：

```plaintext
gs-loc.apple.com
gs-loc-cn.apple.com
bluedot.is.autonavi.com
bluedot.is.autonavi.com.gds.alibabadns.com
```

* 如果没有，点绿色 **「+」**，把上面这串用逗号分隔粘进去， **再点右上角 ✓ 保存**。

✅ 解密开关和域名就绪。

***
## 第三步：安装并信任证书（最关键，别漏）

这一步分**三个小步骤 **，少一步定位就改不了。
### 3.1 生成并安装证书
1. 还在 HTTPS 解密页面，点**「证书」**
2. 点**「生成 CA 证书」 **→ 再点**「安装证书」 **→ 点**「确认」**

* 弹出"已下载描述文件"对话框，点 **「允许」**
### 3.2 去系统里安装描述文件
4. 打开 iPhone**设置 **App
5. 进**设置 → 通用 → VPN 与设备管理**
6. 找到 Shadowrocket 的描述文件 → 点进去 → 点**「安装」 **（输入锁屏密码）
### 3.3 信任证书⚠️（90% 的人漏这步）
7. 进**设置 → 通用 → 关于本机 → 证书信任设置**

8. 把**Shadowrocket 那个证书的开关打开 **（启用完全信任）

✅ 三步都做完，解密才能真正工作。***
## 第四步：开启代理
1. 回到 Shadowrocket **首页**
2. 把顶部的**总开关打开 **（变绿色 / 显示"已连接"）
3. 第一次会弹"是否允许添加 VPN 配置"，点**允许**

✅ 代理已开启，上方状态栏会出现 VPN 图标。***
## 第五步：设置你想去的坐标

默认定位是 **苹果总部（美国库比提诺）**。改成你想要的地点：
1. Shadowrocket → 配置 → 模块 → 点开 **「iOS Location Spoofer」**
2. 找到**`argument=` **那一行，改里面这两个数字：

* `latitude=` → 你的 **纬度**

* `longitude=` → 你的 **经度**
3.**保存**

几个常用坐标可直接抄：
| 地点 | latitude（纬度） | longitude（经度） |
| ----- | ------------ | ------------- |
| 北京天安门 | 39.9087 | 116.3975 |
| 上海外滩 | 31.2397 | 121.4900 |
| 广州塔 | 23.1066 | 113.3245 |
| 东京塔 | 35.6586 | 139.7454 |
### 顺手把海拔等参数也调一下（建议，别只改经纬度）

`argument=` 里除了经纬度，还有几个参数一起构成"完整的一次定位"。只改经纬度、海拔却停在默认的 530 米，跑到上海（近海平面）或拉萨（3600 米）时就会明显对不上、容易露馅。建议按目标地点顺手调一下：
| 参数 | 默认值 | 含义 | 建议 |
| -------------------- | ---- | --------------- | ------------------------------------------------------ |
| `altitude` | 530 | 海拔（米），支持负数 |**改成目标地点的真实海拔 **（下面教你查）。上海≈4、北京≈44、拉萨≈3650、吐鲁番可为负 |
| `horizontalAccuracy` | 39 | 水平精度（米），越小越"精准" | 想更像 GPS 可设**5\~15 **；保持 39 也正常 |
| `verticalAccuracy` | 1000 | 垂直精度（米） | 配了真实海拔后可调小到**10\~30 **，让海拔显得更可信 |**怎么查目标地点海拔 **：
- 浏览器搜"地名 海拔"，或用高德/Google 地图
- 也可以打开这个免费接口直接看（把经纬度换成你的）：

```plaintext
https://api.open-meteo.com/v1/elevation?latitude=31.2397&longitude=121.4900
```

改法和经纬度一样：在 `argument=` 那行找到对应参数改数字，保存即可。其余参数（ `motionActivityType` 等运动状态）一般不用动。***
## 第六步：让定位生效

改完坐标不会立刻生效，需要"逼" iPhone 重新向苹果请求定位。方法很简单：
1. 打开 **设置 → 隐私与安全性 → 定位服务**
2.**整个关掉，等 10 秒以上，再打开**
3. 打开**地图 **或**天气 **App 查看定位
4.**没变就重复关/开定位几次 **，多试几遍就会生效***
## 进阶（可选）
## 用网页地图选点，告别手动改参数

前面第五步是手动去模块里改 `latitude` / `longitude` / `altitude` 数字—— **偶尔换一次没问题，但经常换、还要每次查海拔就很烦**。

项目自带一个 **网页地图选点工具**（ `location-picker/server.js` ），把这些全自动化了：

* **手指点地图哪里，定位就到哪里**，不用手查经纬度

* **海拔按地形自动获取**（点哪自动填哪的真实海拔），不用自己查

* **水平精度 / 垂直精度**在网页上直接调，点「保存」即可

* 支持 **高德 / 卫星 / 国外地图**切换，自动处理国内地图偏移

* 搜索地名能列出 **多个候选**，像真地图一样选

* **一键"恢复真实定位"**：不用去关模块，网页点一下就让脚本放行、回到真实位置（再点一下恢复伪造）
### 用它需要什么

* 一台能 **长期运行的服务器 / VPS / NAS**（用来跑这个小工具）

* 有一点点动手能力（会用 SSH、systemd）
### 怎么装
1. 把项目里的 `location-picker/server.js` 上传到你的服务器运行（文件开头的注释写了启动命令，支持自带 https 复用已有证书）
2. 在 Shadowrocket 模块的 `argument=` **末尾追加**（前面的参数都保留）：

```plaintext
&configUrl=https://你的域名:端口/loc.json?token=你的密码
```

* 之后改定位就是： **打开网页 → 点地图 → 按第六步关开定位生效**
### 配置环境变量（必读）

`server.js` 通过环境变量控制，**`TOKEN` 不设进程会直接退出，不会用弱口令兜底 **——这是防呆设计，避免你部署完忘了改默认密码被人扫。
| 变量 | 是否必设 | 默认值 | 说明 |
| ------- | ------ | ------ | ---------------------------------------------------------------- |
| `TOKEN` |**必设** | 无 | 网页端和模块 `configUrl` 里的 `token=` 必须一致。建议 `openssl rand -hex 24` 生成 |
| `PORT` | 否 | `8080` | 监听端口；1024 以下需 root |
| `CERT` | 否 | 空 | HTTPS 证书 fullchain 路径；与 `KEY` 同时设置才走 https |
| `KEY` | 否 | 空 | HTTPS 私钥路径；与 `CERT` 同时设置才走 https |
启动示例：

\# http（先跑通流程，再用 https）TOKEN=$(openssl rand -hex 24) PORT=8080 node server.js# https（复用 acme.sh 证书，续期无需重启，进程每 12 小时自动热加载）TOKEN=$(openssl rand -hex 24) PORT=8443 \CERT=/root/cert/example.com/fullchain.pem \KEY=/root/cert/example.com/privkey.pem

ode server.js

然后模块 `argument=` 末尾的 `configUrl` 写成：

```plaintext
&configUrl=https://example.com:8443/loc.json?token=上面那个TOKEN
```

* 没带 `?token=` → 服务端返回 **401**`missing token`

* `?token=` 写错 → 服务端返回 **403**`bad token`

数据文件 `loc.json` 自动落在 `server.js` 同目录，记录当前坐标 / 海拔 / 精度；已写入 `.gitignore` ，不会污染仓库。

***
## 常见问题排查**Q：定位一直不变？ **按这个顺序查：
1.**证书信任设置里的开关有没有真的打开 **（第 3.3 步，最常见原因）
2. 模块是不是在「模块」里且**已启用 **（右侧有 ✓）
3. HTTPS 解密开关是否打开、四个苹果域名是否都在
4.**有没有多试几次关/开定位 **（苹果有缓存，往往要重复几遍才生效）
5. 把模块 `argument=` 里的 `debug=false` 改成 `debug=true` ，去 Shadowrocket「数据/日志」看有没有拦截到 `wloc` 请求——能看到说明拦截成功**Q：模块导入后域名没自动出现？ **手动在 HTTPS 解密页面把那四个域名加进去，记得点右上角 ✓ 保存。**Q：找不到「HTTPS 解密」入口？ **如果你使用的是 Shadowrocket iOS 2.2.88(3308)，实测入口在「配置」页中：找到当前正在使用的配置文件，点击右侧「ⓘ」，再进入「HTTPS 解密」。旧版或部分界面可能仍在底部「设置」里。**Q：可以恢复真实定位吗？ **可以。关掉模块（取消 ✓）或关掉 Shadowrocket 总开关，然后按第六步刷新一次定位即可恢复。**Q：Apple News / 依赖区域的服务还是判定我在原位置？ **Apple News 等部分应用不只读定位，还依赖 iOS 系统服务的多个开关。请打开**设置 → 隐私与安全性 → 定位服务 → 系统服务 **，把里面所有开关全部打开（特别是「基于位置的 Apple 广告」「地点」「iPhone 分析」「路由与流量」「提升地图准确性」等）。全部打开后再关开一次定位，Apple News 通常就能识别到新区域了。***
## 操作顺序速查

```plaintext
导入模块 → 开HTTPS解密+加域名 → 装证书并信任 → 开代理 → 改坐标保存
→ 关定位等10秒再开(没变就多试几次) → 打开地图验证
```

祝配置顺利。卡在哪一步，对照上面"常见问题排查"逐条检查即可。

本教程教你用 Shadowrocket（小火箭）把 iPhone 的定位改到世界任何地方。无需越狱、无需电脑、无需开发者账号，跟着一步步做即可。

教程覆盖完整六个步骤：
1. 导入 iOS Location Spoofer 模块
2. 打开 HTTPS 解密并添加四个苹果域名
3. 安装并信任证书（最关键的三小步）
4. 开启代理
5. 设置目标坐标（含海拔等参数调整）
6. 让定位生效（关开定位服务刷新）

进阶部分介绍网页地图选点工具：手指点地图即可改定位，海拔自动获取，支持一键恢复真实定位。

GitHub 项目: https://github.com/mekos2772/ios-location-spoofer

📎 **本视频涉及资源**

GitHub 项目: https://github.com/mekos2772/ios-location-spoofer

模块地址: https://raw.githubusercontent.com/mekos2772/ios-location-spoofer/main/ios-location-spoofer.sgmodule

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
7. Bybit支付卡申请链接 （推荐码：LGNQRG）https://youtu.be/3sN7P2t_CeA

8. YiKa虚拟卡实操开卡教程，不需KYC，一个邮箱开50张卡，订阅ChatGPT/Claude/推特蓝V出海必备 https://youtu.be/XaLeXKu4PTM

## YouTube 播放列表

- AI产品&技术相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海VPS相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=aQdeFAPeVM8)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/mobile-ios-shadowrocket-step-by-tutorial/)
