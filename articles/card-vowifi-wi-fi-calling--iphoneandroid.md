# 【海外卡保号】海外 VoWiFi (Wi-Fi Calling) 开启全流程：iPhone、Android、代理规则

本视频严格依据论坛指南，为您带来亲测有效的 VoWiFi 开启全流程教程。涵盖美国卡、英国卡、德国卡、香港卡等不同地区的开启方法，iPhone 和 Android 设备实操，以及 Surge/Clash 代理规则配置。

> 完整图文与持续更新版本：[【海外卡保号】海外 VoWiFi (Wi-Fi Calling) 开启全流程：iPhone、Android、代理规则](https://869hr.uk/2026/tech/card-vowifi-wi-fi-calling--iphoneandroid/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/card-vowifi-wi-fi-calling--iphoneandroid/
- 更新：2026-05-05
- 分类：技术
- 关键词：VoWiFi、海外卡、教程
- 视频：https://www.youtube.com/watch?v=3lYgUUBEstI

## 正文

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=3lYgUUBEstI)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 3 分钟。严格依据论坛指南《海外 VoWiFi （Wi-Fi Calling）开启指南：iPhone、Android、代理规则》，为您带来亲测有效的 VoWiFi 开启全流程教程。

<!-- more -->

## 什么是 VoWiFi

很多海外电话卡、香港电话卡都支持 VoWiFi，也就是 Wi-Fi Calling。它可以让手机在蜂窝信号差、无服务，或者只连接 Wi-Fi 的情况下，继续使用运营商原生电话和短信。

但 VoWiFi 不是打开一个开关就一定成功。真正成功要看四件事：

1. 号码和套餐是否支持 Wi-Fi Calling
2. 手机系统是否允许打开 Wi-Fi Calling 开关
3. 手机区域是否符合手机系统及运营商要求
4. 当前网络环境是否能完成 IMS 注册

### 判断成功标准

| 设备 | 成功判断 |
|------|----------|
| iPhone | 状态栏出现 Wi-Fi Calling，并且"关于本机"里的 IMS 状态显示 Voice / SMS |
| Android | 状态栏出现 Wi-Fi Calling / WLAN Call，或 SIM 状态里的移动网络类型显示 IWLAN |
| 通用判断 | 飞行模式 + Wi-Fi 下，可以使用原生电话和短信 |

## 开始前的确认

操作之前，先确认这张卡本身支持 Wi-Fi Calling。

### 重点检查项目

| 项目 | 说明 |
|------|------|
| 套餐是否支持 Wi-Fi Calling | 有些运营商不是所有套餐都支持 |
| 号码是否正常 | 欠费、停机、未激活都可能失败 |
| 是否需要后台开通 | 有些运营商需要在 App 或官网里先打开 |
| 美国卡是否配置 E911 | 美国卡首次开启 Wi-Fi Calling 通常需要 E911 地址 |
| 香港卡是否有语音分钟 | 香港卡尤其重要，套餐里要包含语音通话分钟数 |

**香港卡特别注意**：套餐里必须包含语音通话分钟数。纯数据卡、上网卡、没有语音服务的套餐，不适合作为 VoWiFi 测试对象。

## 不同地区卡的开启要点

### 美国卡：重点是 E911

美国卡开启 VoWiFi 的核心难点通常是首次配置 E911 地址。

| 情况 | 操作 |
|------|------|
| 从未开通过 Wi-Fi Calling | 使用美国 IP，打开 Wi-Fi Calling 时配置 E911 |
| 已经配置过 E911 | 很多美国运营商后续可以漫游 VoWiFi，不一定每次都需要美国 IP |
| 换机 / 重置网络 / 重装系统 | 可能需要重新用美国 IP 配置 E911 |

**一句话总结**：首次配置 E911 通常需要美国 IP，日常 VoWiFi 注册不一定每次都需要美国 IP。

### 英国 / 欧洲卡：默认需要本地 IP

英国和欧洲卡不要直接套美国卡经验。美国卡很多支持漫游 VoWiFi，但英国和欧洲不少运营商并不支持、或不稳定支持漫游 Wi-Fi Calling。

**实操建议**：
- 英国卡用英国 IP
- 德国卡用德国 IP
- 法国卡用法国 IP
- 意大利卡用意大利 IP

也就是说，欧洲卡不要简单理解成"随便一个欧洲节点就行"，而是要尽量使用运营商所在国家的本地 IP。

### 德国 Vodafone：需要额外处理 ePDG DNS

德国 Vodafone 属于欧洲卡里比较特殊的一类。实测中，很多 DNS 无法正常解析它的 ePDG 域名，导致代理线路、UDP 500 / 4500 都配置好了，但手机仍然无法发起正常的 VoWiFi 注册。

**ePDG 域名**：
```
epdg.epc.mnc002.mcc262.pub.3gppnetwork.org
```

如果普通 DNS 解析不出 IP，可以自己做 DNS 重定向，或者直接改 hosts，将它映射到以下 IP 之一：
- 139.7.117.168
- 139.7.117.169
- 139.7.117.170

**hosts 示例**：
```
139.7.117.168 epdg.epc.mnc002.mcc262.pub.3gppnetwork.org
```

## iPhone 开启要点

iPhone 不能只关闭定位。实际操作中，还要处理 Apple 的地区检测。

建议把下面这个域名加入代理规则：
```
gspe1-ssl.ls.apple.com
```

并根据当前要开启 VoWiFi 的运营商切换代理线路。

### 查看 IMS 状态

设置 → 通用 → 关于本机 → 找到"运营商"字段 → 点按一下 → 切换到 IMS 状态

| IMS 状态 | 含义 |
|----------|------|
| Voice & SMS | 语音和短信都注册，最理想 |
| Voice | 语音注册，短信需要单独测试 |
| SMS | 短信注册，语音不一定成功 |
| 空白 / Not Registered | 未成功 |

**注意**：如果你的主要用途是收验证码，不能只看到 Voice 就认为完全成功，最好实际测试 SMS 接收。

## Android 开启要点

Android 的难点是系统经常不显示 Wi-Fi Calling 开关，或者开关能打开但无法注册。

如果系统里没有 Wi-Fi Calling 开关，可以使用：
- **Pixel IMS + Shizuku**

它的作用是强制打开 Android 被隐藏的 IMS / VoWiFi 开关。

**注意**：Pixel IMS 只是让 Wi-Fi Calling 开关出现或保持开启，不代表一定注册成功。最终还是要看状态栏是否出现 Wi-Fi Calling，或者移动网络类型是否变成 IWLAN。

### 查看是否成功

设置 → 关于本机 → SIM 卡状态 → 移动网络类型

如果显示 **IWLAN**，通常说明 VoWiFi 已经注册成功。

也可以尝试拨号输入：`*#*#4636#*#*`

## 通用开启流程

### 第一步：确认基础条件

1. 确认号码和套餐支持 Wi-Fi Calling
2. 美国卡确认 E911 地址是否已经配置
3. 香港卡确认套餐里包含语音通话分钟数
4. 确认号码状态正常，没有欠费、停机或未激活

### 第二步：准备地区环境

1. 关闭系统定位
2. iPhone 将 `gspe1-ssl.ls.apple.com` 加入代理规则
3. 根据当前运营商切换对应地区代理线路
4. 确认代理是全局规则、路由器规则或 TUN 模式
5. 确认 DNS、IPv6、UDP 规则没有泄漏
6. 德国 Vodafone 额外确认 ePDG 域名是否能解析

**代理线路建议**：

| 运营商 | 代理线路 |
|--------|----------|
| 美国卡首次配置 E911 | 美国 |
| 美国卡日常 VoWiFi | 不一定必须美国，失败时再切美国 |
| 英国卡 | 英国 |
| 欧洲其他卡 | 对应国家本地 IP |
| 澳洲卡 | 澳洲 |
| 香港卡 | 香港 |

### 第三步：先打开 Wi-Fi Calling 开关

在清理网络状态之前，先让系统保存 Wi-Fi Calling 开关状态。

**iPhone**：设置 → 蜂窝网络 → 对应号码 → Wi-Fi 通话 → 打开

**Android**：设置 → SIM 卡 → 对应 SIM → Wi-Fi Calling → 打开

### 第四步：拔卡及飞行模式重启

**实体 SIM**：
1. 确认 Wi-Fi Calling 开关已经打开
2. 拔出 SIM
3. 开启飞行模式
4. 保持飞行模式重启手机
5. 重启后不要关闭飞行模式

**eSIM**：
1. 确认 Wi-Fi Calling 开关已经打开
2. 关闭该 eSIM，或保持飞行模式
3. 重启手机
4. 重启后继续保持飞行模式
5. 后面再启用 eSIM

### 第五步：重新连接 Wi-Fi 和代理

重启后继续保持飞行模式，然后：
1. 手动打开 Wi-Fi
2. 连接已经走代理的 Wi-Fi
3. 确认代理规则或全局规则已经生效
4. 确认当前出口 IP 是目标地区
5. 确认 iPhone 的 `gspe1-ssl.ls.apple.com` 也走目标地区
6. 确认代理工具没有排除系统流量
7. 如果是德国 Vodafone，确认 ePDG 域名已经正确解析或映射

### 第六步：插卡并等待注册

网络环境准备好后：

**保持飞行模式 → Wi-Fi 已连接 → 代理已生效 → 插入 SIM**

然后等待：**30 秒到 2 分钟**

期间不要反复开关 Wi-Fi Calling，不要频繁切换代理节点，不要不断开关飞行模式。

### 第七步：确认是否成功

| 设备 | 成功表现 |
|------|----------|
| iPhone | 状态栏出现 Wi-Fi Calling，关于本机 IMS 显示 Voice / SMS |
| Android | 状态栏出现 Wi-Fi Calling / WLAN Call，SIM 状态显示 IWLAN |
| 实测 | 飞行模式 + Wi-Fi 下可以打电话、接电话、收发短信 |

**最后一定要实测**：
1. 原生电话拨打运营商电话
2. SMS 发送
3. SMS 接收

如果主要用途是收验证码，尤其要测试 SMS 接收，不要只测电话。

## Surge 代理规则示例

VoWiFi 常见会使用 UDP 500 和 UDP 4500。下面是一组简单的 Surge 规则示例：

```
# iPhone Apple 地区检测
DOMAIN,gspe1-ssl.ls.apple.com,VoWiFi地区节点

# 英国 VoWiFi / ePDG
AND,((GEOIP,GB),(AND,((PROTOCOL,UDP),(OR,((DEST-PORT,500),(DEST-PORT,4500))))))),英国节点

# 德国 VoWiFi / ePDG
AND,((GEOIP,DE),(AND,((PROTOCOL,UDP),(OR,((DEST-PORT,500),(DEST-PORT,4500))))))),德国节点

# 香港 VoWiFi / ePDG
AND,((GEOIP,HK),(AND,((PROTOCOL,UDP),(OR,((DEST-PORT,500),(DEST-PORT,4500))))))),香港节点

# 美国 VoWiFi / ePDG
AND,((GEOIP,US),(AND,((PROTOCOL,UDP),(OR,((DEST-PORT,500),(DEST-PORT,4500))))))),美国节点

# 瑞士 VoWiFi / ePDG
AND,((GEOIP,CH),(AND,((PROTOCOL,UDP),(OR,((DEST-PORT,500),(DEST-PORT,4500))))))),瑞士节点
```

## 香港 Android 的特殊绕过方法

香港卡在 Android 上难度较高。除了套餐必须包含语音通话分钟数之外，还可能遇到一个问题：

部分香港运营商配置要求开启定位后，才能打开 Wi-Fi Calling 开关。

但跨境使用时，又不希望一直打开定位。这时可以尝试使用 **实体 eSIM 卡切配置保留开关状态**。

### 操作流程

1. 插入实体 eSIM 卡
2. 切换到香港运营商配置
3. 打开系统定位
4. 进入 SIM 设置
5. 打开 Wi-Fi Calling 开关
6. 确认开关已经保持开启
7. 切换实体 eSIM 到其他配置
8. 关闭系统定位
9. 准备好 Wi-Fi、代理和飞行模式环境
10. 再切回香港卡配置
11. 检查 Wi-Fi Calling 开关是否仍然保持开启
12. 如果开关仍然开启，就等待 IMS 注册
13. 成功后不要手动关闭 Wi-Fi Calling 开关

## 难度分级

| 难度 | 类型 | 主要难点 |
|------|------|----------|
| ★★☆☆☆ | 美国 T-Mobile 系 MVNO | 首次 E911 配置 |
| ★★★☆☆ | 美国 AT&T / Verizon 系 | E911、设备白名单、账号授权 |
| ★★★★☆ | 英国 / 欧洲卡 | 通常不支持漫游 VoWiFi，建议使用当地 IP |
| ★★★★☆ | 德国 Vodafone | 德国 IP + ePDG DNS 映射 |
| ★★★★☆ | 香港 iPhone | 香港线路、套餐语音分钟 |
| ★★★★★ | 香港 Android | 语音套餐、定位限制、开关状态 |

## 失败时的排查方法

### 1. 先查套餐和账号

| 失败现象 | 优先检查 |
|----------|----------|
| 完全没有 Wi-Fi Calling 开关 | 套餐是否支持、系统是否隐藏、Android 是否需要 Pixel IMS |
| 美国卡打不开 | E911 是否配置、是否使用美国 IP |
| 英国 / 欧洲卡不注册 | 是否使用运营商本国 IP |
| 德国 Vodafone 不注册 | ePDG 域名是否能解析 |
| 香港卡无法使用 | 套餐是否有语音分钟、是否支持 Wi-Fi Calling |
| 开关打开后无反应 | IMS 是否注册、网络是否走对线路 |
| 能打电话不能收短信 | SMS over IMS 可能未注册，要单独测试短信 |

### 2. 再查系统状态

| 设备 | 检查项 |
|------|--------|
| iPhone | 关于本机 → 运营商 → IMS 状态 |
| Android | 关于本机 → SIM 卡状态 → 移动网络类型是否 IWLAN |
| 香港 Android | Wi-Fi Calling 开关是否被定位限制 |

### 3. 再查代理和网络

| 问题 | 处理 |
|------|------|
| 地区不对 | 切换到运营商对应地区线路 |
| iPhone 地区检测失败 | 检查 `gspe1-ssl.ls.apple.com` 是否走代理 |
| DNS 异常 / 污染 | DNS 跟随代理；必要时做 DNS 重定向或 hosts |
| 德国 Vodafone DNS 失败 | 映射 ePDG 域名到指定 IP |
| 没有 UDP 500 / 4500 | 检查是否为全局 / TUN / 路由器代理，并确认节点协议支持 UDP |
| 规则命中但不注册 | 检查 SIM 状态、IMS 状态、套餐权限和本地 IP 是否正确 |

## 补充方案：VoHive

如果你的目标是海外卡保号、短信转发、实体 eSIM 管理，副机不一定非要是一台手机，也可以考虑 VoHive。

VoHive 是一个面向移远 4G 模组的管理平台，适合拿移远 EC20 这类 USB 模组做：
- 网页/Bot 收发短信
- 多卡统一管理
- 实体 ESIM/eUICC 管理（加卡，切卡，删卡）
- 基于手机卡流量的代理池
- TelegramBot / 飞书Bot / QQBot 远程控制
- 在条件满足时启用 VoWiFi
- 通过 /vocall 发起 VoWiFi 模拟外呼

## 总结

VoWiFi 成功的关键，不是简单打开 Wi-Fi Calling 开关，而是让手机在正确的系统状态和网络环境下完成 IMS 注册。

最实用的顺序是：

**确认套餐支持 → 关闭定位 → 配好代理和地区检测 → 先打开 Wi-Fi Calling 开关 → 拔卡进入飞行模式重启 → 手动打开 Wi-Fi → 确认代理生效 → 插卡 → 等待注册 → 查看 IMS / IWLAN**

不同卡的重点不同：

| 类型 | 重点 |
|------|------|
| 美国卡 | 首次配置 E911 通常需要美国 IP |
| 英国 / 欧洲卡 | 对应国家本地 IP |
| 德国 Vodafone | ePDG DNS 需要手动重定向或 hosts 映射 |
| iPhone | `gspe1-ssl.ls.apple.com` 和地区检测 |
| Android | Pixel IMS、Shizuku、IWLAN |
| 香港卡 | 套餐必须有语音分钟数，建议香港 IP |
| 香港 Android | 定位限制和实体 eSIM 卡切配置保留开关 |

## 相关资源

### 短信及语音接码平台
- https://hero-sms.com/?ref=357885
- https://smspva.com/?ref=1307601

### 白嫖流量
- 500M试用：https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN，85 折优惠
- 200M试用：https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码GXJDIAN，9 折优惠

### 联系方式
1. 微信讨论群：https://qr.869hr.uk/aitech
2. 超过100T资料总站网站：https://doc.869hr.uk
3. Telegram群聊：https://t.me/tgmShareAI
4. 微信公众号：搜"AI前沿的短裤哥"
5. 视频的文字博客：https://869hr.uk
6. 推特：https://x.com/gxjdian
7. Youtube：https://youtube.com/@gxjdian

### VPS主机推荐
- Claude用的丽萨主机：https://lisahost.com/aff.php?aff=9424
- 按流量VPS：https://www.lycheeip.com/home/ip?affId=1AwYIQ7BW8
- 一年 10 美元的多年保底小鸡：https://clients.zgovps.com/?affid=1207
- 各种云主机，主打性价比：https://my.racknerd.com/aff.php?aff=15809

### eSIM 推荐
1. 9eSIM打 9 折（优惠码：maq）：https://www.9esim.com/?coupon=maq
2. ESTK打 9 折（优惠码：GXJDIAN）：https://store.estk.me/zh?aid=16007
3. XeSIM打 9 折（推荐码：gxjdian）：https://xesim.cc/?DIST=RE5FHg==

### 视频专辑
- AI产品&技术相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海VPS相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=3lYgUUBEstI)
- [论坛原文](https://linux.do)
- [博客主站](https://869hr.uk)

---

如果你觉得这期视频对你有帮助，请务必：
👍 点赞本视频
💬 在评论区留下你的问题或成功注册的截图
🔔 订阅频道并打开小铃铛，获取最新硬核白嫖教程和科技前沿资讯！

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/card-vowifi-wi-fi-calling--iphoneandroid/)
