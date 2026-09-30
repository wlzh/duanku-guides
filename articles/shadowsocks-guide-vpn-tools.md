# Shadowsocks 完全指南：从零开始掌握科学上网核心工具小白必看

从零解释 Shadowsocks 的工作方式、与传统 VPN 的差异、常用客户端和基础配置流程，并整理连接验证与常见故障排查。

> 完整图文与持续更新版本：[Shadowsocks 完全指南：从零开始掌握科学上网核心工具小白必看](https://869hr.uk/2026/tech/shadowsocks-guide-vpn-tools/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/shadowsocks-guide-vpn-tools/
- 更新：2026-08-02
- 分类：技术
- 专题：技术
- 关键词：Shadowsocks、VPN、小火箭、ClashX、Shadowrocket
- 视频：https://www.youtube.com/watch?v=NHCgLZNDvDw
- 系列：[出海网络搭建](../series/overseas-network.md)

## 正文

<!-- 文章摘要 -->
> 
Shadowsocks（小飞机/酸酸）是什么？怎么用？本视频从零开始，带你彻底搞懂科学上网的核心工具！...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=NHCgLZNDvDw)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 41 分钟。

## 小火箭 Shadowsocks 完全指南：从零开始掌握科学上网的核心工具

Shadowsocks 完全指南封面

须知**：本文专为完全零基础的小白用户撰写。你不需要任何网络技术背景，只要跟着文章一步步走，就能从“完全不懂”到“独立配置、熟练使用”。文中每一个概念都会在功能界面中出现时讲透，建议收藏后分章节阅读。

---

## 第一章 认识 Shadowsocks

### 1.1 什么是 Shadowsocks

Shadowsocks（简称**SS**，中文社区常叫它“酸酸”、“小飞机”、“纸飞机”）是一种开源的、轻量级的加密代理协议与工具。它的核心功能只有一句话：**在你本地的设备和一台远程服务器之间，建立一条加密隧道，让你的网络流量通过这条隧道中转出去，从而绕过网络审查与封锁。**

打个比方：你的网络流量就像一封信。你在中国寄一封信到国外，邮局（网络运营商/防火墙）会拆开检查信的内容，如果发现敏感内容就拦下。Shadowsocks 做的事情是——你在本地把这封信装进一个密码箱（加密），然后寄给你的海外朋友（远程服务器），你的朋友收到后用同样的密码打开箱子（解密），再帮你把信投递到真正的目的地。目的地回信时，也是先寄给你的海外朋友，朋友装进密码箱寄回给你，你打开后就能看到内容。

整个过程里，邮局只看到“你在和朋友之间来来回回搬运密码箱”，看不到箱子里面装的是什么。

### 1.2 为什么需要它：网络审查与信息自由

互联网虽然号称“全球互联”，但在很多地区，网络访问是受到限制的。以中国大陆为例，由于“防火长城”（Great Firewall，简称 GFW）的存在，大量国际网站和服务无法直接访问，包括但不限于：

-**搜索引擎**：Google Search

-**视频平台**：YouTube

-**社交媒体**：Twitter/X、Facebook、Instagram

-**工具服务**：Google Drive、Google Docs、ChatGPT、Claude

-**开发平台**：GitHub（部分时段不稳定）、Docker Hub

-**新闻媒体**：BBC、纽约时报、维基百科中文版

Shadowsocks 就是帮助你访问这些被封锁资源的技术工具之一。它不是唯一的工具，但由于其轻量、高效、开源、跨平台的特性，成为了最广为人知的代理协议之一。

### 1.3 Shadowsocks 的前世今生

你不需要记住这些历史，但理解一点很重要：**Shadowsocks 协议是基础**。后来出现的 V2Ray、Trojan、Clash 等工具，很多都兼容或基于 SS 协议。你在手机和电脑上用的那些“翻墙 App”——小火箭、ClashX、Clash Verge——底层都在处理 SS 协议（以及其他协议）。

Shadowsocks 发展时间线

### 1.4 核心术语速览表

在深入之前，先用一张表让你对所有术语有个印象。不用记住，后续每遇到一个都会详细展开：
| 术语 | 英文 | 一句话解释 |
| --- | --- | --- |
| 代理 | Proxy | 中间人帮你转发请求 |
| SOCKS5 | SOCKS5 | 一种代理协议标准，SS 基于它 |
| 加密 | Encryption | 把数据变成别人看不懂的密文 |
| 节点 | Node/Server | 远程中转服务器 |
| 协议 | Protocol | SSR 特有，增强数据校验和伪装 |
| 混淆 | Obfuscation | SSR 特有，把流量伪装成普通流量 |
| AEAD | AEAD | 现代加密方式，同时保证保密和完整 |
| 订阅 | Subscription | 一条 URL 自动获取多个节点 |
| 分流 | Routing/Split | 不同流量走不同路径 |
| PAC | PAC | 自动代理配置脚本 |
| 客户端 | Client | 你设备上运行的 App |
| 服务端 | Server | 远程节点上运行的程序 |
---

## 第二章 核心概念深度解析

这一章是全文的“地基”。后面每一章讲界面和操作时，都会回到这里的概念。如果你觉得某个概念一时理解不了，可以先跳过，等看到实际操作时回头来看就会豁然开朗。

### 2.1 代理（Proxy）：中间人转发**代理的本质是“中间人”**。你本来要直接访问目标网站，现在改成：你先把请求给代理服务器，代理服务器替你访问目标网站，拿到结果后再传回给你。

代理转发流程图**没有代理时**：你的设备 → 直接访问 → 目标网站。防火墙在中间拦截。**有代理时**：你的设备 → 代理服务器 → 目标网站。防火墙看到的是你和代理服务器之间的加密流量，不知道你到底访问了什么。

代理有两种常见类型：

-**HTTP 代理**：只处理网页（HTTP/HTTPS）请求

-**SOCKS5 代理**：更通用，能处理任何 TCP 网络流量（包括网页、邮件、游戏等）

### 2.2 SOCKS5 协议：Shadowsocks 的根基

SOCKS 是一种网络代理协议，SOCKS5 是它的第五版。它的工作在 OSI 模型的会话层（第五层），比 HTTP 代理更底层、更通用。**SOCKS5 的特点**：

- 支持 TCP 和 UDP

- 不关心你传输的是什么应用层协议（HTTP、FTP、SMTP 都行）

- 支持简单的认证（用户名密码）

- 支持 IPv4、IPv6、域名**Shadowsocks 对 SOCKS5 的改造**：标准 SOCKS5 是明文传输的——你的请求和代理服务器的响应都不加密，防火墙能看到全部内容。Shadowsocks 的核心创新在于：**把 SOCKS5 的实现拆成两半**——

-**ss-local（本地端）**：跑在你设备上，扮演 SOCKS5 服务器角色，接收你 App 的请求

-**ss-server（服务端）**：跑在海外节点上，扮演 SOCKS5 客户端角色，替你向目标网站发请求

中间 ss-local 和 ss-server 之间的通信，全部用你设定的加密算法加密。这就实现了“本地 SOCKS5 + 中间加密隧道”的架构。

### 2.3 加密（Encryption）：让流量变成密文

加密是 Shadowsocks 的核心安全机制。你可能会问：**为什么不直接用代理，要加密呢？** 因为如果不加密，防火墙只要看到你发往代理服务器的请求里有“google.com”，就知道你在翻墙，直接封锁你的代理服务器。加密后，防火墙只能看到一串随机字节，无法判断内容。

#### 加密算法的分类

Shadowsocks 支持的加密方法经历了从旧到新的演进：

SS加密方法分类图**什么是 AEAD？**

AEAD 全称 Authenticated Encryption with Associated Data（认证加密及关联数据）。传统的流加密只保证**保密性**（别人看不到内容），但不保证**完整性**——别人可以篡改你的密文，解密后变成乱码甚至被注入恶意数据。AEAD 同时保证：

-**保密性**：内容加密，外人看不到

-**完整性**：一旦密文被篡改，解密会失败，你能发现

-**真实性**：只有持有正确密钥的人才能生成有效密文

>**小白建议**：如果你在客户端里看到加密方法的选择，优先选 `chacha20-ietf-poly1305`（移动设备）或 `aes-256-gcm`（桌面设备）。如果是新协议节点，选 `2022-blake3-aes-256-gcm`。绝不选 `rc4-md5` 或 `none`。

#### 加密在界面中的位置

在 Shadowrocket 添加节点时，你会看到一个“加密”（method）选项：

```plaintext
┌─────────────────────────────┐
│  添加节点                    │
│                             │
│  类型:    Shadowsocks       │
│  地址:    1.2.3.4           │
│  端口:    8388              │
│  密码:*******-        │
│  加密:    chacha20-ietf-... │ ← 这里选加密方法
│                             │
└─────────────────────────────┘
```

这个加密方法**必须和服务端配置完全一致**，否则连接失败。这是新手最常踩的坑——客户端和服务端的加密方法不一致，连不上。

### 2.4 协议（Protocol）：SSR 的安全增强层**注意**：协议插件是 ShadowsocksR（SSR）特有的概念，原版 SS 没有。但很多客户端（如 Shadowrocket）为了兼容性也支持 SSR 协议。

如果说加密是给数据上锁，**协议插件**就是在锁的基础上加了防篡改和流量整形功能。它的主要作用：

1.**数据完整性校验**：加密只防偷看，协议插件还能防篡改——有人在中间改了你的数据包，服务端能检测到并丢弃

2.**包长度混淆**：原始 SS 的数据包长度有特征，容易被识别。协议插件会填充随机长度的数据，打乱包长度特征

3.**限制客户端数量**：服务端可以限制一个账号同时多少个设备连接

常见的协议插件：
| 协议插件 | 安全性 | 特点 |
| --- | --- | --- |
| `origin` | 基础 | 原版 SS 协议，无额外保护 |
| `auth_sha1_v4` | 较高 | SHA1认证，包长度混淆 |
| `auth_aes128_md5` | 高 | AES128认证+MD5校验 |
| `auth_aes128_sha1` | 高 | AES128认证+SHA1校验 |
| `auth_chain_a/b/c/d` | 最高 | 链式认证，抗检测最强 |
>**小白建议**：现代环境下，如果你用的是 SSR 节点，协议选 `auth_chain_a` 或 `auth_chain_d` 最安全。但说实话，现在大多数机场（节点服务商）已经迁移到 SS-2022 或 V2Ray 协议，SSR 的协议和混淆你了解即可，实际配置时按服务商给的参数填就行。

### 2.5 混淆（Obfuscation）：流量伪装

混淆插件同样是 SSR 特有的概念。**加密让内容看不懂，混淆让流量“看起来不像代理流量”**。

防火墙不仅看内容，还会看流量的“特征”。比如标准 SS 虽然加密了内容，但流量模式（连接时间、包大小分布、握手特征）仍然有代理的影子。混淆插件的作用是把流量伪装成其他正常协议的样子：
| 混淆插件 | 伪装成什么 | 适用场景 |
| --- | --- | --- |
| `plain` | 不伪装 | 协议已是 auth_chain 时不需混淆 |
| `http_simple` | 普通 HTTP 网页浏览 | 公司/学校内网封锁环境 |
| `http_post` | HTTP 上传请求 | 同上，与 http_simple 兼容 |
| `tls1.2_ticket_auth` | TLS 1.2加密连接 | 最像正常 HTTPS 流量，推荐 |**混淆参数（obfs_param）**：可以进一步指定伪装成访问哪个网站。比如填 `www.bing.com`，防火墙看到的就是你在访问必应。但大多数服务商不建议手填参数，而是让节点自带域名，客户端直接用域名作为伪装目标。

### 2.6 插件（Plugin / SIP003）：可插拔传输

Shadowsocks 有一个标准叫 SIP003，定义了“可插拔传输”机制。简单说就是：你可以挂一个外部程序来处理流量传输，让 SS 流量变成任意样子。

最常见的插件是 `obfs-local`（simple-obfs），功能类似 SSR 的混淆插件，但是是原版 SS 的实现。还有 `v2ray-plugin`、`kcptun`、`cloak` 等更高级的插件。

在客户端界面中，插件通常长这样：

```plaintext
┌─────────────────────────────┐
│  插件:    obfs-local        │
│  插件参数: obfs=tls;...     │
└─────────────────────────────┘
```

>**小白建议**：如果你的节点 URL 里有 `/?plugin=...`，说明这个节点用了插件。不用手动配置，复制 URL 导入即可，客户端会自动处理。

### 2.7 节点 URL 的完整格式

理解了上面所有概念，我们来看一个完整的 SS 节点 URL，这是你从机场订阅或分享链接中会看到的东西：**原版 SS URL（Base64 编码）**：

```plaintext
ss://YWVzLTI1Ni1nY206cGFzc3dvcmQ=@1.2.3.4:8388#节点名称
```

解码后是：

```plaintext
ss://加密方法:密码@服务器地址:端口#节点名称
```**SS-URI 标准格式（较新）**：

```plaintext
ss://aes-256-gcm:password@server.example.com:8388/?plugin=obfs-local%3Bobfs%3Dtls#MyNode
```**SSR URL**：

```plaintext
ssr://base64编码的配置
```

解码后的 SSR 配置：

```plaintext
server:1.2.3.4:port:protocol:method:obfs:password_base64/?params
```

各个字段含义：

- `server` = 服务器 IP 或域名

- `port` = 端口号

- `protocol` = 协议插件（如 auth_chain_a）

- `method` = 加密方法（如 aes-256-gcm）

- `obfs` = 混淆插件（如 tls1.2_ticket_auth）

- `password` = 密码

你不需要手动解析这些 URL。复制后粘贴到客户端，或扫描二维码，客户端会自动解析所有参数。但理解了格式，当连接失败时你就知道去检查哪些参数是否和服务端一致。

---

## 第三章 工作原理图解

### 3.1 整体架构：客户端-服务器模型

SS整体架构图**关键理解**：

1.**本地端（ss-local / 客户端 App）** 在你设备上启动一个 SOCKS5 代理服务，监听本地端口（通常是 1080）。你的浏览器/App 配置为使用这个本地代理。

2.**服务端（ss-server / 远程节点）** 在海外服务器上运行，负责接收加密流量、解密、然后向真正的目标网站发请求。

3.**中间的加密隧道** 是 ss-local 和 ss-server 之间的通信，全程加密，防火墙只看到密文。

4.**目标网站** 看到请求来自 ss-server 的 IP，不知道你的真实 IP。

### 3.2 一次请求的完整数据流

以你打开 `https://www.google.com` 为例，完整流程如下：

整个过程看起来步骤很多，但实际执行只需要几十到几百毫秒。增加的延迟主要来自两个地方：

-**地理距离**：你的设备到海外节点的网络延迟

-**加密/解密计算**：现代 CPU 上几乎可忽略，但在移动设备上可能有轻微影响

一次请求数据流时序图

### 3.3 Shadowsocks 与 VPN 的区别

新手经常混淆 SS 和 VPN。虽然都能翻墙，但技术原理完全不同：

VPN与SS对比图
| 对比项 | VPN | Shadowsocks |
| --- | --- | --- |
| 工作层级 | 网络层（IP），接管全部流量 | 会话层（SOCKS5），按 App 配置 |
| 流量范围 | 整个设备所有流量 | 只有配置了代理的 App 流量 |
| 协议特征 | VPN 协议有明显特征，容易被识别 | SS 流量伪装为随机/普通流量 |
| 封锁难度 | 常见 VPN 协议易被封 | 难以识别，需高级流量分析 |
| 性能 | 封装开销大，稍慢 | 轻量，更快 |
| 配置复杂度 | 系统级配置 | App 级配置，灵活 |
| 分流能力 | 较弱，通常全局 | 强大，可按域名/IP 分流 |**简单说**：VPN 是“你的所有流量都走加密通道”，SS 是“你指定的流量走加密通道”。这使得 SS 更灵活——你可以让国内网站直连（快），国外网站走代理（能访问）。

### 3.4 SS / SSR / V2Ray / Trojan / Clash 的关系

代理协议家族关系图**你需要知道的关键点**：

-**SS 是基础协议**，最轻量最快，但抗封锁能力相对弱

-**SSR 是 SS 的增强版**，加了协议和混淆，但已逐渐被淘汰

-**V2Ray 是更强大的平台**，支持更多伪装方式（WebSocket+TLS+CDN 等）

-**Trojan 伪装成 HTTPS**，是目前抗封锁最强的方案之一

-**Shadowsocks-2022** 是 SS 的新一代规范，用更现代的加密

-**Clash 系客户端是“前端壳”**——它们不发明新协议，而是统一支持上述所有协议，给你一个统一的管理界面

>**小白结论**：你用的 Shadowrocket 或 ClashX，本质上是一个“代理协议管理器”。它支持 SS、SSR、V2Ray、Trojan 等多种协议。你从机场拿到的节点链接，会自动识别是什么协议并配置。你只需要会操作客户端即可。

---

## 第四章 下载与安装

苹果生态下，Shadowsocks 相关客户端的获取是新手第一个门槛。因为中国大陆 App Store 已下架大部分代理软件，你需要一些技巧。

### 4.1 macOS 客户端

macOS 平台的主流 SS/代理客户端：
| 客户端 | 协议支持 | 费用 | 推荐度 | 系统要求 |
| --- | --- | --- | --- | --- |
|**ClashX Pro** | SS/SSR/V2Ray/Trojan | 免费 | ★★★★★ | macOS 10.15+ |
|**Clash Verge Rev** | SS/SSR/V2Ray/Trojan | 免费 | ★★★★★ | macOS 11+ |
|**ShadowsocksX-NG** | SS/SSR | 免费 | ★★★ （已停更） | macOS 10.11+ |
|**V2RayU** | SS/V2Ray | 免费 | ★★★ | macOS 10.14+ |
|**Surge 5** | 全协议 | 付费$49.99 | ★★★★ | macOS 12+ |
#### ClashX Pro 下载（推荐首选）

ClashX Pro 是 macOS 上最流行的免费代理客户端，开源，支持几乎所有主流协议。**下载途径**：

1.**GitHub 官方发布页**（需科学上网或镜像站）：

 - 仓库地址：`https://github.com/yichengchen/clashX`

 - 在 Releases 页面下载最新的 `.dmg` 文件

2.**国内镜像/网盘**：

 - 很多中文导航站（如 shadowsocksool.com、linuxsss.com）提供 ClashX 的镜像下载，搜索“ClashX 下载”即可找到

3.**Homebrew 安装**（如果你用 Homebrew）：

 ```bash
   brew install --cask clashx
   ```**安装步骤**：

ClashX安装步骤流程图

>**注意**：首次打开 ClashX 时，macOS 会弹出“无法打开，因为来自身份不明的开发者”的安全提示。这是正常的——因为 ClashX 没有苹果开发者签名。解决方法：在 Finder 中找到 ClashX.app，**右键点击 → 选择“打开” → 在弹窗中再次点“打开”**。只需操作一次，之后正常启动。

#### Clash Verge Rev 下载（新锐推荐）

Clash Verge Rev 是 Clash Verge 的社区接力维护版，界面更现代，功能更全。

- GitHub 仓库：`https://github.com/clash-verge-rev/clash-verge-rev`

- 下载最新的 `.dmg` 安装包

### 4.2 iOS / iPad 客户端

iOS 平台因为苹果的封闭生态，App 只能从 App Store 获取，而中国大陆 App Store 已下架所有代理软件。

#### 客户端对比
| 客户端 | 费用 | 协议支持 | 推荐度 | 备注 |
| --- | --- | --- | --- | --- |
|**Shadowrocket （小火箭）** | $2.99 | 全协议 | ★★★★★ | iOS 最经典，推荐 |
|**Quantumult X** | $7.99 | 全协议 | ★★★★ | 功能强大但配置复杂 |
|**Stash** | $3.99 | Clash 格式 | ★★★★ | 现代界面 |
|**Potatso Lite** | 免费 | SS/SSR | ★★★ | 免费但功能有限 |
|**Surge 5 iOS** | $49.99 | 全协议 | ★★★★ | 专业级，价格高 |
#### Shadowrocket 下载教程（重点）

Shadowrocket（小火箭）是 iOS 上最经典的代理客户端，性价比最高。但它需要非中国大陆 Apple ID 才能下载。**获取非国区 Apple ID 的方法**：

获取非国区AppleID流程图**详细步骤**：

1.**退出 App Store 的中国区账号**（注意：是 App Store，不是 iCloud!）
 - 打开“设置” → 最上方你的名字 → “媒体与购买项目” → “退出登录”

 - 或者直接打开 App Store → 右上角头像 → 下滑到底部 → “退出登录”

2.**登录非国区 Apple ID**
 - 打开 App Store → 右上角头像位置 → 滚动到底部 → 登录

 - 输入美区/港区/日区 Apple ID 和密码

3.**搜索 Shadowrocket**

 - 在 App Store 搜索框输入 `Shadowrocket`

 - 找到图标是纸飞机的应用

4.**购买下载**

 - 如果 Apple ID 已有余额（礼品卡），直接购买

 - 如果没有支付方式，需要先充值或绑定海外支付方式

 - 一些共享 ID 提供已购买的 Shadowrocket，可直接下载

>**重要安全提示**：
>
> - 共享 Apple ID 只在**App Store** 登录，**绝不要在 iCloud 登录**！在 iCloud 登录别人账号可能导致你的手机被锁。
>
> - 购买独立 Apple ID 比共享更安全，推荐自己注册或购买独立号。
>
> - 注册非国区 Apple ID 的方法网上有很多教程，搜索“美区 Apple ID 注册”即可。

### 4.3 国内用户获取渠道汇总

国内用户获取渠道汇总图

>**鸡生蛋蛋生鸡问题**：下载客户端需要翻墙，翻墙需要客户端。怎么破？
>
> - macOS 客户端从中文导航站下载，不需要翻墙
>
> - iOS 用非国区 Apple ID 从 App Store 下载，不需要翻墙
>
> - GitHub 访问可能不稳定，但不是完全封锁，多刷新或用镜像站

---

## 第五章 界面功能详解

这一章是全文核心。我们会逐个界面、逐个按钮、逐个设置项地讲解。以**Shadowrocket（iOS）** 和**ClashX（macOS）** 为主要示例，因为它们是最主流的客户端。

### 5.1 Shadowrocket（小火箭）界面全解析

Shadowrocket 的主界面底部有 5 个 Tab：

Shadowrocket底部导航结构图

#### 首页（Home）详解

```plaintext
┌─────────────────────────────────────┐
│              首页 Home              │
│                                     │
│  ┌─────────────────────────────┐    │
│  │  未连接                      │    │
│  │  ───────────────            │    │
│  │  [●○○] 连接开关             │    │ ← 第一个操作：开关代理
│  └─────────────────────────────┘    │
│                                     │
│  全局路由:  [配置 ▼]                 │ ← 路由模式选择
│                                     │
│  ┌─────────────────────────────┐    │
│  │  当前节点                     │    │
│  │  🟢 美国-洛杉矶  120ms       │    │ ← 显示选中节点及延迟
│  └─────────────────────────────┘    │
│                                     │
│  [连通性测试]                        │ ← 测试所有节点延迟
│                                     │
│  ─────────────────────────          │
│  首页  节点  配置  规则  设置        │
└─────────────────────────────────────┘
```**每个元素详解**：**① 连接开关**：这是整个 App 最核心的按钮。打开=全局流量开始走代理，关闭=恢复直连。首次打开会弹出“添加 VPN 配置”的系统提示，需要你输入密码/Face ID 确认——这是因为 iOS 上代理必须通过系统的 VPN 接口实现，需要你的授权。**② 全局路由（路由模式）**：点击后弹出选项：

-**配置（Config）**：使用你下载的分流配置文件，按规则决定哪些走代理。**推荐日常使用这个模式**。

-**代理（Proxy）**：所有流量全部走代理，不分流。适合排查问题时临时使用。

-**直连（Direct）**：所有流量直连，不走代理。相当于关了代理但保持 App 运行。**③ 当前节点**：显示你选中的节点名称和延迟（毫秒）。点击可进入节点列表切换。**④ 连通性测试**：点击后会逐个测试所有节点的延迟，测完后每个节点右侧显示毫秒数。数值越小越快，`超时`表示连不上。

#### 节点（Servers）页详解

```plaintext
┌─────────────────────────────────────┐
│  节点                          [+]  │ ← 右上角加号添加节点
│                                     │
│  📂 订阅                             │
│  ├ 📁 我的机场           [🔄] [ℹ️]  │ ← 订阅链接，🔄更新，ℹ️设置
│  │  ├ 🟢 美国-洛杉矶   120ms        │
│  │  ├ 🟢 日本-东京     89ms         │
│  │  ├ 🟡 香港-01       156ms        │
│  │  └ ⚫ 新加坡-01      超时         │ ← 连不上的节点
│  │                                  │
│  ├ 📁 免费节点           [🔄] [ℹ️]  │
│  │  └ ...                           │
│  │                                  │
│  📂 手动添加                         │
│  └ 🟢 自建节点 1.2.3.4   200ms      │ ← 手动添加的节点
│                                     │
│  ─────────────────────────          │
│  首页  节点  配置  规则  设置        │
└─────────────────────────────────────┘
```**操作详解**：**① 添加节点 \[+\]**：点击后弹出添加方式选择：

-**扫码添加**：扫描节点二维码

-**粘贴节点链接**：复制了 `ss://` 或 `ssr://` 开头的链接，粘贴导入

-**手动输入**：逐项填写服务器地址、端口、密码、加密等**② 订阅管理 \[ℹ️\]**：点击订阅旁边的 ℹ️ 图标进入设置：

```plaintext
┌─────────────────────────────────┐
│  订阅设置                        │
│                                │
│  URL: https://example.com/sub  │ ← 订阅链接地址
│  备注: 我的机场                 │
│                                │
│  [✓] 打开时更新                 │ ← App启动时自动更新节点
│  [ ] 自动后台更新               │ ← 后台定时更新
│                                │
│  [更新]   [删除]                │
└─────────────────────────────────┘
```**③ 更新订阅 \[🔄\]**：手动触发从订阅 URL 重新获取节点列表。机场更新了节点或换了服务器时用。

#### 配置（Config）页详解

配置页是 Shadowrocket 的“分流大脑”。默认自带一个基础配置，你可以下载更全面的高级配置。

```plaintext
┌─────────────────────────────────────┐
│  配置                          [+]  │
│                                     │
│  ●  默认配置 (自带)                  │ ← 基础分流规则
│  ○  你下载的高级配置                  │ ← 需要自行添加
│                                     │
│  ─────────────────────────          │
│  首页  节点  配置  规则  设置        │
└─────────────────────────────────────┘
```**如何下载高级配置**：点击右上角 \[+\]，输入远程配置文件的 URL，App 会下载并导入。常用的开源配置文件地址在 GitHub 上可以搜到（搜索 `shadowrocket config`）。

#### 规则（Rules）页详解

规则页显示当前配置文件中的分流规则。每条规则的格式如下：

```plaintext
┌─────────────────────────────────────┐
│  规则                               │
│                                     │
│  DOMAIN-SUFFIX, google.com, PROXY   │ ← google走代理
│  DOMAIN-SUFFIX, apple.com, DIRECT   │ ← apple直连
│  DOMAIN-KEYWORD, facebook, PROXY    │ ← 含facebook走代理
│  IP-CIDR, 192.168.0.0/16, DIRECT    │ ← 局域网直连
│  GEOIP, CN, DIRECT                  │ ← 中国IP直连
│  FINAL, PROXY                       │ ← 以上都不匹配走代理
│                                     │
└─────────────────────────────────────┘
```**规则类型详解**：
| 规则类型 | 匹配什么 | 示例 |
| --- | --- | --- |
| `DOMAIN` | 精确域名 | `DOMAIN, www.google.com, PROXY` |
| `DOMAIN-SUFFIX` | 域名后缀 | `DOMAIN-SUFFIX, google.com, PROXY`（匹配 google.com 及其所有子域名） |
| `DOMAIN-KEYWORD` | 域名关键词 | `DOMAIN-KEYWORD, google, PROXY`（域名中含 google） |
| `IP-CIDR` | IP 段 | `IP-CIDR, 1.2.3.0/24, DIRECT` |
| `GEOIP` | 按国家 | `GEOIP, CN, DIRECT`（中国 IP 直连） |
| `USER-AGENT` | 浏览器标识 | `USER-AGENT, MicroMessenger, DIRECT` |
| `FINAL` | 兜底规则 | 匹配以上所有规则后剩下的流量怎么处理 |**策略（第三列）详解**：

- `PROXY`：走代理

- `DIRECT`：直连不走代理

- `REJECT`：拒绝连接（用于去广告）

>**小白理解分流的意义**：如果没有分流规则，你的所有流量都走代理。但访问国内网站也走代理的话，会绕一大圈反而更慢，而且国内服务可能因为你“在国外 IP”而限制。分流规则让“访问国内网站直连、访问国外网站走代理”，兼顾速度和可用性。

#### 设置（Settings）页详解

设置页有很多选项，挑最重要的讲：

```plaintext
┌─────────────────────────────────────┐
│  设置                               │
│                                     │
│  ── 代理 ──                         │
│  延迟测试方法:  [URL测试 ▼]          │ ← 改为URL测试更准确
│  延迟测试URL:  http://...           │ ← 测试用的目标网址
│                                     │
│  ── 路由 ──                         │
│  按路由规则绕过局域网:  [✓]          │ ← 局域网不走代理
│  按路由规则绕过大陆:  [ ]           │ ← 大陆IP不走代理
│                                     │
│  ── DNS ──                          │
│  DNS覆盖:  [✓]                      │ ← 使用自定义DNS
│  DNS服务器:  8.8.8.8, 1.1.1.1       │ ← 海外DNS
│                                     │
│  ── 其他 ──                         │
│  IPv6支持:  [ ]                     │
│  按需连接:  [ ]                     │
│  ICMP自动回复:  [✓]                 │
│                                     │
│  ── 服务器订阅 ──                    │
│  > 管理订阅...                       │
│                                     │
│  ── iCloud同步 ──                   │
│  iCloud同步:  [✓]                   │ ← 多设备同步配置
│                                     │
│  ── 关于 ──                         │
│  版本 2.2.10                        │
│                                     │
└─────────────────────────────────────┘
```**关键设置项详解**：**① 延迟测试方法**：默认可能是 TCP 测试（只测 TCP 连接速度），建议改为**URL 测试**（实际发 HTTP 请求测真实延迟），更准确但稍慢。**② 按路由规则绕过大陆**：勾选后，访问大陆 IP 时自动直连不走代理。和配置文件里的 `GEOIP, CN, DIRECT` 规则功能类似，这是 App 级别的开关。**③ DNS 设置**：这是影响连接成功与否的关键设置之一。如果 DNS 被污染（国内 DNS 返回错误 IP），即使代理配置正确也连不上。

- 建议开启 DNS 覆盖

- DNS 服务器填海外 DNS：`8.8.8.8`（Google）、`1.1.1.1`（Cloudflare）

- 或填加密 DNS 地址**④ iCloud 同步**：开启后，你的节点、配置、规则会通过 iCloud 在 iPhone、iPad、Mac 之间同步。如果你多设备使用，强烈建议开启。

### 5.2 ClashX（macOS）界面全解析

ClashX 运行后在菜单栏显示一个小图标（猫或狗），点击展开菜单：

```plaintext
┌──────────────────────────────┐
│  ClashX 菜单                 │
│                              │
│  ✅ 出站模式: 规则            │ ← 当前路由模式
│    ├ 全局                    │ ← 所有流量走代理
│    ├ 规则                    │ ← 按规则分流（推荐）
│    └ 直连                    │ ← 所有流量直连
│                              │
│  Proxy  ▸                   │ ← 代理节点选择
│    ├ 🟢 美国-洛杉矶          │
│    ├ 🟢 日本-东京            │
│    └ ⚫ 新加坡-01             │
│                              │
│  Proxy Group  ▸              │ ← 策略组
│    ├ 🔄 Auto-Select          │ ← 自动选择最快节点
│    ├ 🇺🇸 美国               │ ← 美国节点组
│    └ 🌏 其他               │
│                              │
│  配置  ▸                    │ ← 配置文件管理
│    ├ ● 我的机场配置          │
│    ├ ○ 备用配置              │
│    └ 配置文件夹              │ ← 打开配置目录
│                              │
│  ─────────────               │
│                              │
│  ☐ 设置为系统代理            │ ← 关键开关！
│  ☑ 开机自启动                │
│                              │
│  ─────────────               │
│                              │
│  More  ▸                     │
│    ├ Dashboard               │ ← 打开Web面板
│    ├ Logs                    │ ← 查看日志
│    └ 更新配置                │
│                              │
│  ─────────────               │
│  Quit ClashX                 │
└──────────────────────────────┘
```**每个菜单项详解**：**① 出站模式（Outbound Mode）**：

-**全局（Global）**：所有流量走选中节点，不分流。简单粗暴。

-**规则（Rule）**：按配置文件中的规则分流。日常推荐。

-**直连（Direct）**：不走代理。相当于关闭代理。**② 设置为系统代理**：这是 ClashX 最关键的开关。勾选后，ClashX 会设置 macOS 系统的 HTTP/HTTPS 代理为 ClashX 的本地端口。**不勾选的话，即使 ClashX 在运行，浏览器也不会走代理**。很多新手启动了 ClashX 却上不了 google，就是这个没勾选。**③ Proxy 节点选择**：选择当前使用的节点。在规则模式下，只有 `Proxy` 组里选中的节点会被用作默认代理节点。**④ Proxy Group 策略组**：这是 Clash 比其他客户端强大的地方。你可以把节点分成不同组，每个组有不同策略：

-**Auto-Select**：自动测速选最快的

-**手动选择**：你自己选

-**按地区分组**：美国组、日本组等

-**链式代理**：A 节点的流量再经过 B 节点**⑤ 配置文件夹**：打开后是 Clash 的配置文件（YAML 格式）存放目录。你的机场订阅下载的配置文件就在这里。**⑥ Dashboard**：打开浏览器中的 Clash 控制面板，可以查看实时连接、流量统计、日志等。

#### Clash 配置文件结构

Clash 的配置文件是 YAML 格式，理解它的高级用户可以自定义一切。基本结构：

```yaml
## Clash 配置文件结构
port: 7890              # HTTP 代理端口
socks-port: 7891        # SOCKS5 代理端口
allow-lan: false        # 是否允许局域网设备连接
mode: rule               # 出站模式: rule/global/direct
log-level: info          # 日志级别
## DNS 设置
dns:
  enable: true
  nameserver:
    - 8.8.8.8
    - 1.1.1.1
## 代理节点列表
proxies:
  - name: "美国-洛杉矶"
    type: ss              # 协议类型
    server: 1.2.3.4       # 服务器地址
    port: 8388            # 端口
    cipher: aes-256-gcm   # 加密方法
    password: "xxxxx"     # 密码
  - name: "日本-东京"
    type: ss
    server: 5.6.7.8
    port: 8388
    cipher: chacha20-ietf-poly1305
    password: "yyyyy"
## 代理组
proxy-groups:
  - name: "Proxy"         # 策略组名
    type: select           # 手动选择
    proxies:
      - "美国-洛杉矶"
      - "日本-东京"
      - Auto-Select
  - name: "Auto-Select"
    type: url-test         # 自动测速
    url: http://www.gstatic.com/generate_204
    interval: 300           # 5分钟测一次
    proxies:
      - "美国-洛杉矶"
      - "日本-东京"
## 分流规则
rules:
  - DOMAIN-SUFFIX,google.com,Proxy
  - DOMAIN-SUFFIX,apple.com,DIRECT
  - GEOIP,CN,DIRECT
  - MATCH,Proxy            # 兜底规则(等同FINAL)
```

>**小白提示**：你不需要手写 YAML 配置文件。机场提供的订阅链接会自动生成配置文件，ClashX 导入订阅即可。但理解了结构，在排查问题时你就知道去哪里看。

---

## 第六章 节点配置详解

### 6.1 节点从哪里来

你有了客户端，但没有节点（远程服务器）是无法使用的。节点的来源主要有三类：

节点来源图**给小白的建议**：

1.**入门阶段**：先用免费节点试试手感，确认客户端能用

2.**日常使用**：购买一个口碑好的机场（月费 10-30 元就能用），稳定性和速度有保障

3.**进阶玩家**：自建 VPS，完全掌控，但需要技术能力

### 6.2 节点 URL 格式详解

机场给你的节点通常有两种形式：**形式一：订阅链接（推荐）**

一条 URL，包含所有节点信息。你只需在客户端里添加这一条 URL，就能自动导入所有节点：

```plaintext
https://api.airport.com/v1/client/subscribe?token=abc123def456
```**形式二：单个节点链接**

`ss://` 或 `ssr://` 或 `trojan://` 或 `vmess://` 开头的链接，每个链接是一个节点。**SS 链接格式**：

```plaintext
ss://base64(加密方法:密码)@服务器:端口#节点名称
```

举例（已解码）：

```plaintext
ss://aes-256-gcm:MyPassword123@server.example.com:8388#美国-洛杉矶
```

各部分：

- `aes-256-gcm` = 加密方法

- `MyPassword123` = 密码

- `server.example.com` = 服务器地址（域名或 IP）

- `8388` = 端口

- `美国-洛杉矶` = 节点显示名称**SSR 链接格式**：

```plaintext
ssr://base64(服务器:端口:协议:加密:混淆:base64(密码)/?参数)
```**Trojan 链接格式**：

```plaintext
trojan://密码@服务器:端口?参数#名称
```

### 6.3 在客户端中添加节点

#### Shadowrocket 添加节点

Shadowrocket添加节点流程图**详细操作步骤（以订阅链接为例）**：

1. 在你的机场网站复制订阅链接

2. 打开 Shadowrocket

3. 点击首页右上角**➕** 按钮

4. 在弹出窗口中，**类型** 选择 `Subscribe`（订阅）

5. 在**URL** 栏粘贴你的订阅链接

6. 在**备注** 栏填写一个你能认出的名字（如“我的机场”）

7. 点击右上角**保存**

8. App 会自动从 URL 获取节点列表，几秒后节点列表出现

9. 在节点列表中点击你想用的节点（建议先做连通性测试选最快的）

10. 回到首页，打开连接开关

11. 首次会弹出“添加 VPN 配置”提示，输入密码/Face ID 确认

12. 开关变绿，连接成功！

#### ClashX 添加节点

ClashX 的节点导入方式稍有不同，主要通过订阅链接：

1. 复制你的机场订阅链接

2. 点击菜单栏 ClashX 图标

3. 选择**配置 ▸ 配置文件夹**

4. 在打开的文件夹中，将订阅链接交给 ClashX 管理

更常见的方式是使用订阅转换：

1. 打开 ClashX 菜单

2. 选择**配置 ▸ 托管配置**

3. 或者直接在终端用 Clash 的 API 添加订阅

实际上，很多机场提供专门适配 Clash 的订阅链接，格式为：

```plaintext
https://api.airport.com/v1/client/subscribe?token=xxx&flag=clash
```

ClashX 导入订阅后，配置文件会自动下载到 `~/.config/clash/` 目录，节点列表自动出现在菜单的 Proxy 中。

### 6.4 节点参数完整说明

当你在 Shadowrocket 手动添加一个 SS 节点时，会看到以下参数：

```plaintext
┌─────────────────────────────────────┐
│  添加节点                            │
│ ─────────────────────────────────── │
│                                     │
│  类型:      Shadowsocks         [▼] │ ← 协议类型
│  地址:      server.example.com      │ ← 服务器地址(域名或IP)
│  端口:      8388                    │ ← 服务器端口
│  密码:      ••••••••                │ ← 连接密码
│  加密:      aes-256-gcm         [▼] │ ← 加密方法
│                                     │
│  ── SSR专用(如非SSR节点留空) ──      │
│  协议:      origin              [▼] │ ← 协议插件(SSR)
│  协议参数:                          │ ← 协议插件参数
│  混淆:      plain              [▼]  │ ← 混淆插件(SSR)
│  混淆参数:                          │ ← 混淆参数
│                                     │
│  ── SIP003插件(可选) ──              │
│  插件:                              │ ← 可插拔传输
│  插件参数:                          │ ← 插件参数
│                                     │
│  ── 其他 ──                         │
│  备注:      美国-洛杉矶              │ ← 节点显示名称
│  允许不安全:  [ ]                   │ ← 跳过证书验证(不推荐)
│                                     │
│              [保存]                  │
└─────────────────────────────────────┘
```**每个参数详解**：**① 类型**：选择协议类型。SS 节点选 `Shadowsocks`,SSR 选 `ShadowsocksR`,Trojan 选 `Trojan`,V2Ray 选 `VMess` 或 `VLESS`。**② 地址**：服务器地址，可以是域名（`server.example.com`）或 IP（`1.2.3.4`）。域名方式更灵活（服务商可换 IP 不用改配置），但需 DNS 解析。**③ 端口**：1-65535 的数字。常见端口有 8388、443、80 等。443 端口是 HTTPS 标准端口，用这个端口更不容易被识别为代理。**④ 密码**：连接密码，必须和服务端完全一致。**⑤ 加密**：加密方法，必须和服务端一致。现代推荐 `aes-256-gcm` 或 `chacha20-ietf-poly1305`。**⑥ 协议/混淆（SSR）**：只有 SSR 节点才需要填，SS 节点选 `origin` 和 `plain`（或留空）。**⑦ 插件（SIP003）**：可选。如果节点 URL 中有 `plugin=` 参数，这里要填对应插件名和参数。一般导入节点链接时会自动填好。

>**新手最重要的一条规则**：除非手动添加节点，否则不要改这些参数。从订阅链接导入的节点，参数都是服务商配好的，直接用即可。手动改参数是连接失败的第一大原因。

---

## 第七章 路由与分流详解

路由分流是代理工具最有价值的功能之一。理解了它，你就能做到“国内网站直连飞快、国外网站代理畅通”。

### 7.1 三种路由模式

三种路由模式图**三种模式的使用场景**：
| 模式 | 什么时候用 | 优点 | 缺点 |
| --- | --- | --- | --- |
| 全局 | 排查问题、全代理需求 | 简单，一定走代理 | 国内网站也走代理，慢 |
| 规则 |**日常使用（推荐）** | 智能分流，兼顾速度 | 需要好的规则配置 |
| 直连 | 临时关闭代理 | 不消耗代理流量 | 无法访问被封锁网站 |
### 7.2 分流规则的工作逻辑

分流规则是“从上到下逐条匹配”的。一个请求进来，从第一条规则开始检查，匹配到就执行对应策略，不再检查后面的规则。

分流规则工作逻辑图

### 7.3 PAC 与规则配置文件

PAC（Proxy Auto-Configuration）是一种自动代理配置脚本。本质上是一个 JavaScript 函数，浏览器调用它来判断“这个 URL 走代理还是直连”。

在 Shadowsocks 早期版本和系统中，PAC 文件是分流的主要方式。现代客户端（Shadowrocket、ClashX）更多使用内置规则引擎，但原理一样。**PAC 文件示例**：

```javascript
function FindProxyForURL(url, host) {
    // 国内域名直连
    if (shExpMatch(host, "*.cn")) return "DIRECT";
    if (shExpMatch(host, "*.taobao.com")) return "DIRECT";
    // 国外域名走代理
    if (shExpMatch(host, "*.google.com")) return "SOCKS5 127.0.0.1:1080";
    if (shExpMatch(host, "*.youtube.com")) return "SOCKS5 127.0.0.1:1080";
    // 默认直连
    return "DIRECT";
}
```

现代客户端已经很少直接让你编辑 PAC 了，但配置文件（Clash 的 YAML、Shadowrocket 的 conf）本质上做的就是这件事——定义一套分流规则。

### 7.4 推荐的分流策略

一个良好的分流配置应该做到：

推荐分流策略图

---

## 第八章 从零到能用：完整使用流程

这一章把前面所有知识串起来，给你一个完整的“从安装到第一次成功翻墙”的操作流程。

### 8.1 准备工作清单

准备工作清单图

### 8.2 iOS（Shadowrocket）完整使用流程

iOS完整使用流程图

**详细图文操作**：**步骤 1**：确保已从非国区 App Store 下载 Shadowrocket。App 图标是一个纸飞机。**步骤 2**：首次打开 Shadowrocket，系统会弹出“Shadowrocket 想要添加 VPN 配置”的提示。点击**允许**，然后输入设备密码或验证 Face ID。这是 iOS 系统级权限——代理 App 必须通过 VPN 接口接管网络流量。**步骤 3**：

1. 点击首页右上角**➕**

2. 在弹出页面，**类型** 选择 `Subscribe`

3. 在**URL** 栏粘贴你的订阅链接

4. 备注填一个名字，比如“我的机场”

5. 打开**“打开时更新”** 开关

6. 点右上角**保存****步骤 4**：保存后 App 会自动访问订阅 URL 获取节点列表。如果你的网络当前无法访问该 URL（有些订阅链接本身被墙），可能会获取失败。这时可以：

- 先用手机流量试试（有时 WiFi 网络更严格）

- 用机场提供的“Clash 订阅”链接格式可能有不同的可达性

- 找机场客服要一个“国内可直连”的订阅地址**步骤 5**：回到首页，点击**连通性测试**。App 会逐个测试每个节点的延迟。测试方法取决于你设置中的“延迟测试方法”——TCP 测试只测连接速度，URL 测试实际发请求更准确。等所有节点测完，每个节点右侧会显示延迟毫秒数或“超时”。**步骤 6**：在节点列表中，点击延迟最低且不是“超时”的节点。节点行变灰/打勾表示选中。**步骤 7**：回到首页，点击**全局路由**，选择**配置**（Config）。这会启用分流规则，国内网站直连、国外网站走代理。**步骤 8**：点击首页顶部的连接开关。开关滑动到右侧，变成绿色，表示代理已启动。状态栏会出现一个蓝色的“VPN”图标。**步骤 9**：打开 Safari 或 Chrome，访问 `https://www.google.com`。如果能正常加载 Google 首页，恭喜你，配置成功！

### 8.3 macOS（ClashX）完整使用流程

macOS完整使用流程图**ClashX 导入订阅的详细方法**：

ClashX 的订阅导入比 Shadowrocket 稍复杂一些。主流方法：**方法 A：通过托管配置（推荐）**

1. 点击 ClashX 菜单 →**配置 ▸ 配置文件夹**

2. 这会打开 Finder 到配置目录 `~/.config/clash/`

3. 回到 ClashX 菜单 →**配置 ▸ 托管配置**

4. 输入你的 Clash 格式订阅链接

5. ClashX 会下载配置文件并自动加载**方法 B：手动下载配置文件**

1. 在浏览器打开你的机场订阅链接（确保是 Clash 格式）

2. 下载的 YAML 文件放到 `~/.config/clash/` 目录

3. 在 ClashX 菜单的**配置** 列表中就能看到它**方法 C：订阅转换** 如果你的机场只提供 SS 格式的订阅链接，没有 Clash 格式，可以用订阅转换工具：

1. 访问订阅转换网站（搜索“Clash 订阅转换”）

2. 输入你的 SS 订阅链接

3. 选择目标格式为 Clash

4. 生成转换后的链接

5. 用这个链接在 ClashX 中导入

### 8.4 iPad 使用

iPad 和 iPhone 一样使用 Shadowrocket，操作完全相同。如果你在 iPhone 上已经购买并配置好：**方法一：App 同步**

- 在 iPad 的 App Store 用同一个非国区 Apple ID 下载 Shadowrocket

- 如果已购买，在 iPad 上是“已购买”状态，免费重新下载**方法二：iCloud 同步配置**

- 在 iPhone 的 Shadowrocket → 设置 → 开启 iCloud 同步

- 在 iPad 的 Shadowrocket → 设置 → 开启 iCloud 同步

- 配置、节点、规则会自动同步

---

## 第九章 系统设置详解

### 9.1 系统代理设置

#### macOS 系统代理

ClashX 勾选“设置为系统代理”后，实际上是修改了 macOS 的系统网络代理设置。你可以手动查看：**系统设置 → 网络 → Wi-Fi → 详细信息 → 代理**

你会看到：

- HTTP 代理：`127.0.0.1` 端口 `7890`

- HTTPS 代理：`127.0.0.1` 端口 `7890`

- SOCKS 代理：`127.0.0.1` 端口 `7891`

macOS系统代理流程图**为什么有些 App 不走系统代理？**

系统代理（HTTP/HTTPS 代理）只对“遵守系统代理设置”的 App 有效。大部分浏览器和很多 App 都遵守，但有些 App（如某些游戏、命令行工具）不读系统代理设置，它们直接发网络请求。

如果你需要所有流量都走代理，可以使用：

-**TUN 模式**（Clash Verge、Surge 支持）：创建虚拟网卡，接管全部流量

-**增强模式**（Shadowrocket 的选项）：类似 TUN 模式

#### iOS 系统代理

iOS 上 Shadowrocket 开启连接后，实际上是创建了一个系统级 VPN 配置。所有遵守 VPN 接口的流量都会走代理。这就是为什么首次使用需要你授权“添加 VPN 配置”。

在**设置 → VPN** 中可以看到 Shadowrocket 的 VPN 配置。

### 9.2 DNS 设置详解

DNS 是代理配置中最容易被忽视但又最关键的环节之一。**DNS 污染问题**：

DNS污染与解决方案图**Shadowrocket DNS 设置建议**：

- 设置 → DNS 覆盖 → 开启

- DNS 服务器填：`8.8.8.8, 1.1.1.1`（Google 和 Cloudflare 的公共 DNS）

- 或者用加密 DNS（DoH）地址**ClashX DNS 设置建议**： 在配置文件的 `dns` 部分设置：

```yaml
dns:
  enable: true
  enhanced-mode: fake-ip    # 虚假IP模式，最快
  nameserver:
    - https://dns.google/dns-query     # Google DoH
    - https://1.1.1.1/dns-query        # Cloudflare DoH
  fallback:
    - https://dns.google/dns-query
    - tls://8.8.8.8:853                # DNS over TLS
```

`fake-ip` 模式是 Clash 的特色功能：它给每个域名分配一个虚拟 IP，实际 DNS 解析在代理服务器端进行，彻底绕过本地 DNS 污染。

### 9.3 开机自启动**macOS ClashX**：

- 菜单 → 勾选“开机自启动”

- 或者在**系统设置 → 通用 → 登录项** 中添加 ClashX**iOS Shadowrocket**：

- iOS 没有开机自启动的概念（App 不后台常驻）

- 但 Shadowrocket 的 VPN 配置会在重启后保持，你可以在**设置 → VPN** 中手动开启

### 9.4 其他重要设置

#### 允许局域网连接（Allow LAN）

局域网共享代理图

如果你想让家里的 Apple TV、其他电脑通过你的 Mac 走代理，开启 `allow-lan: true`，并在其他设备的代理设置中填你 Mac 的局域网 IP 和 ClashX 端口。

#### TUN 模式（虚拟网卡）

TUN 模式创建一个虚拟网卡，接管系统所有网络流量，包括不遵守系统代理设置的 App。这是比“系统代理”更彻底的代理方式。

在 Clash Verge Rev 中可以开启 TUN 模式。开启后需要授予管理员权限。

TUN模式对比图

---

## 第十章 进阶技巧与故障排除

### 10.1 节点测速与选择策略

节点测速选择策略图**延迟 ≠ 速度**：延迟（ping）低不代表下载速度快。延迟只反映数据包往返时间，带宽才是下载速度的决定因素。测延迟快但看视频卡，说明带宽不够。实际使用需要两者都测。

### 10.2 链式代理（Chain Proxy）

Shadowrocket 支持链式代理——流量经过多个节点接力转发。

```plaintext
你的设备 → 节点A(日本) → 节点B(美国) → 目标网站
```

适用场景：

- 节点 A 直连目标网站被限制（如某些服务只允许美国 IP）

- 增加匿名性，多跳难以追踪

在 Shadowrocket 中配置链式代理：

1. 节点页 → 选中一个节点

2. 点击节点旁边的设置 → 前置代理 / 后置代理

3. 选择另一个节点作为链中的下一跳

### 10.3 常见故障排除

故障排除决策树

#### 常见问题 Q&A**Q: 打开连接开关后，所有网站都打不开了？** A: 可能是节点连不上 + 全局模式。切到“规则”模式，或换一个能连通的节点。如果所有节点都超时，检查订阅是否过期或账号是否欠费。**Q: Google 能打开但 YouTube 看不了视频？** A: 可能是节点带宽不够。换个节点，或检查规则是否把 YouTube 的视频 CDN 域名匹配到了直连。**Q: Mac 上 ClashX 运行了，但浏览器还是上不了 Google？** A: 99% 的可能是没勾选“设置为系统代理”。去 ClashX 菜单勾选它。**Q: iPhone 上 Shadowrocket 连接后，某些国内 App 不能用了？** A: 检查全局路由是否设为“配置”（规则模式）。如果是“代理”（全局），国内 App 也会走代理导致异常。**Q: 订阅链接导入后没有节点？** A: 可能是订阅链接格式不对或已过期。在浏览器打开那个链接看看返回什么。如果是机场，登录机场后台检查账号状态。**Q: 怎么清除 DNS 缓存？**

- macOS：终端运行 `sudo dscacheutil -flushcache; sudo killall -HUP mDNSResponder`

- iOS：重启设备，或关闭再打开 Shadowrocket 的 DNS 覆盖

### 10.4 安全注意事项

安全注意事项图

>**最重要的安全提醒**：免费节点往往是最贵的——你付出的不是金钱，而是你的隐私和数据安全。免费节点运营者完全有能力记录你经过的所有流量（虽然有加密，但他们持有解密密钥）。对于涉及银行、支付、登录敏感账号的操作，要么用可信的付费节点，要么直连。

---

## 第十一章 全景总结

### 完整生态全景图

完整生态全景图

### 关键概念回顾

关键概念思维导图

### 新手快速上手 Checklist

- [ ] 已下载客户端（mac: ClashX / iOS: Shadowrocket）

- [ ] 已获取非国区 Apple ID（仅 iOS 需要）

- [ ] 已有节点来源（机场订阅 / 免费节点 / 自建）

- [ ] 已导入节点（订阅链接 / 扫码 / 粘贴 URL）

- [ ] 已做连通性测试并选择延迟低的节点

- [ ] 路由模式设为“规则”（Shadowrocket）或“Rule”（ClashX）

- [ ] macOS：已勾选“设置为系统代理”

- [ ] iOS：已授权 VPN 配置权限

- [ ] 已打开连接开关

- [ ] 已验证能访问 Google / YouTube

- [ ] 已配置 DNS（建议 8.8.8.8 + 1.1.1.1）

- [ ] 如多设备：已开启 iCloud 同步

---

## 附录：常用资源链接**协议规范与文档**：

- Shadowsocks 官方文档：`https://shadowsocks.org/`

- SS-2022 协议规范：`https://github.com/shadowsocks/shadowsocks-org/wiki/Shadowsocks-2022-Edition`

- SSR 协议文档：`https://github.com/shadowsocksrr/shadowsocks-rss/blob/master/ssr.md`**macOS 客户端**：

- ClashX:`https://github.com/yichengchen/clashX`

- Clash Verge Rev:`https://github.com/clash-verge-rev/clash-verge-rev`**iOS 客户端**：

- Shadowrocket（App Store）：`https://apps.apple.com/us/app/shadowrocket/id932747118`**中文导航站**（提供客户端镜像下载）：

- shadowsocksool.com（Shadowsocks 官网导航）

- linuxsss.com（Shadowsocks 中文网）

- itlanyan.com（SS 客户端整理）**订阅转换工具**（搜索在线工具）：

- 搜索关键词：“Clash 订阅转换” 或 “subconverter”

---

>**免责声明**：本文为技术科普与教育用途，介绍 Shadowsocks 代理协议的工作原理和使用方法。读者应了解并遵守所在地区的法律法规，合理合法使用网络工具。本文不鼓励也不协助任何违法活动。**如果你能跟着这篇指南走到这里，你已经从一个完全不懂的小白，变成了能独立配置和使用 Shadowsocks 的合格用户。** 剩下的就是在实际使用中积累经验——遇到问题回来查对应章节，多试几个节点和配置，你会越来越熟练。

科学上网不是目的，获取信息、拓展视野、连接世界才是。祝你在更广阔的互联网世界里，找到你需要的一切。🚀

Shadowsocks（小飞机/酸酸）是什么？怎么用？本视频从零开始，带你彻底搞懂科学上网的核心工具！

本视频专为完全零基础的小白用户制作。不需要任何网络技术背景，跟着视频一步步走，就能从"完全不懂"到"独立配置、熟练使用"。每一个概念都会在实际界面中出现时讲透，建议收藏后分章节观看。

📱 涵盖客户端：Shadowrocket（小火箭）、ClashX Pro、Clash Verge Rev

🔑 核心知识点：加密隧道、SOCKS5 代理、AEAD 加密、分流规则、DNS 设置、TUN 模式

🛠 实操内容：从下载安装到节点配置到首次成功连接的完整流程

⚠️ 免责声明：本视频为技术科普与教育用途。请遵守所在地区法律法规，合理合法使用网络工具。

📎**本视频涉及资源：**
- 相关链接: https://www.google.com`
- 相关链接: https://example.com/sub
- 相关链接: http://
- 相关链接: http://www.gstatic.com/generate_204
- 相关链接: https://api.airport.com/v1/client/subscribe?token=abc123def456
- 相关链接: https://api.airport.com/v1/client/subscribe?token=xxx&flag=clash
- 相关链接: https://dns.google/dns-query
- 相关链接: https://1.1.1.1/dns-query
- 相关链接: https://shadowsocks.org/`
- 相关链接: https://apps.apple.com/us/app/shadowrocket/id932747118`

注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有 🔗https://869hr.uk

## 关注与资源

1. 微信讨论群：https://qr.869hr.uk/aitech
2. 超过100T资料总站网站：https://doc.869hr.uk
3. Telegram群聊：https://t.me/tgmShareAI
4. 微信公众号：搜“AI前沿的短裤哥”
5. 视频的文字博客(银行卡、手机号、VPS主机、IP测试等）：https://869hr.uk
6. 推特：https://x.com/gxjdian
7. Youtube：https://youtube.com/@gxjdian

## 短信及语音接码平台

- https://hero-sms.com/?ref=357885
- https://smspva.com/?ref=1307601

## 白嫖流量

- 500M试用， 链接 https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN ， 85 折优惠
- 200M试用，链接 https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码GXJDIAN， 9 折优惠
- eSIM各国纯净IP流量：https://www.redex.vip/zh?partnerId=31

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

1. wise的申请链接及教程链接（有身份证就可，推荐码：lizhiw12） (教程链接https://x.com/wlzh/status/19967997897...) （申请链接https://wise.com/invite/ihpc/lizhiw12）
2. N26 的申请链接及教程链接 （需要护照， 推荐码：lizhiw02766c ） https://youtu.be/HY9OD8rX89s?si=78REb8MyKSJB6cwQ
3. Bybit支付卡申请链接 （推荐码：LGNQRG）https://youtu.be/3sN7P2t_CeA
4. YiKa虚拟卡实操开卡教程，不需KYC，一个邮箱开50张卡，订阅ChatGPT/Claude/推特蓝V出海必备 https://youtu.be/XaLeXKu4PTM
1. 三家eSIM 让国产手机秒变eSIM手机，全方面优缺点对比及开户链接🔗 https://s.869hr.uk/mcc
2. eSIM 9eSIM打 9 折（优惠码：maq）注册及购买链接 https://www.9esim.com/?coupon=maq
3. eSIM ESTK打 9 折（优惠码：GXJDIAN）注册及购买链接 https://store.estk.me/zh?aid=16007
4. eSIM XeSIM打 9 折（推荐码：gxjdian）注册及购买链接 https://xesim.cc/?DIST=RE5FHg==
5. eSIM卡免手机保号收发短信！几十块大疆4G模块爆改移远EC25，Mac UTM一键部署VoHive完整教程 https://youtu.be/PZRkoggXFco
6. 国行iPhone秒变eSIM！Xesim卡手把手喂饭教程，出国留学旅行必备 https://youtu.be/Mhd2KR8Ydo4

## YouTube 播放列表

- AI产品&技术相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海VPS相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=NHCgLZNDvDw)

## 延伸阅读

- [Clash 配置文件与 DNS 分流详解](https://869hr.uk/2026/tech/clash-config-detail-dns/)
- [VPS IP 质量检测与结果解读](https://869hr.uk/2026/tech/vps-ip-guide-tutorial/)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/shadowsocks-guide-vpn-tools/)
