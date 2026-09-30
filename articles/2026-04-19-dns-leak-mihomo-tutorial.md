# 为什么加了节点还是被查到？一篇文章带你彻底了解Mihomo DNS查询工作方式，解决DNS泄露

本文深入讲解mihomo内核的DNS查询工作方式，详细分析Redir-host和Fake-IP两种DNS模式与SOCKS/HTTP和TUN两种入站方式的四种搭配下的DNS解析流程，找出DNS泄露的根本原因并给出完整的优化配置方案。适合零基础小白理解DNS泄露原理与防护。

> 完整图文与持续更新版本：[为什么加了节点还是被查到？一篇文章带你彻底了解Mihomo DNS查询工作方式，解决DNS泄露](https://869hr.uk/2026/%E7%BD%91%E7%BB%9C%E5%AE%89%E5%85%A8/2026-04-19-dns-leak-mihomo-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/%E7%BD%91%E7%BB%9C%E5%AE%89%E5%85%A8/2026-04-19-dns-leak-mihomo-tutorial/
- 更新：2026-04-19
- 分类：网络安全
- 关键词：VPN、网络安全、软件安装

## 正文

<!-- YouTube视频嵌入 -->
> 📺 视频教程：[为什么加了节点还是被查到？一篇文章带你彻底了解Mihomo DNS查询工作方式，解决DNS泄露](https://youtu.be/UFO-ZNHLXVw)

---

# 前言

这篇文章带你了解mihomo内核的DNS查询工作方式，解决DNS泄露。

很多人的DNS泄露教程只是怎么做，而鲜有人说明原理，便有了这篇教程。

我所有的教程都不是喂饭教程，而是原理讲解，需要抄作业可以直接退出，节省时间。

本篇教程为方便理解大量使用白话描述，请谅解部分位置的不严谨。

基于教程： [系统了解DNS](https://linux.do/t/topic/1897227) 后，我们继续了解。

---

# 一、DNS泄露的概念

并不是访问DNS测试网站，出现了国内的DNS服务器就是产生了DNS泄露。

而是DNS去到了不该去到的地方，比如解析 `www.google.com` ，我们希望解析该域名的DNS服务器是国外的，但是该域名的DNS解析被国内的DNS服务器响应，那么你访问该网站时、对于国内的DNS服务器产生了DNS泄露。

而我们访问 `www.bilibili.com` ，该域名是国内的主流网站，就应该由DNS处理解析来获得最好的解析结果与最快的速度，此时就不是DNS泄露，因为我们目的就是让国内网站使用国内DNS处理解析。

**DNS泄露是一个有前提条件的概念。**

---

# 二、mihomo内核的DNS解析流程

这里分为几个情况，按照各种入站协议和DNS模块的工作模式搭配，可以产生四个搭配结果：

- DNS模式为Redir-host，入站方式为socks/http服务器
- DNS模式为Fake-IP，入站方式为socks/http服务器
- DNS模式为Redir-host，入站方式为TUN虚拟接口
- DNS模式为Fake-IP，入站方式为TUN虚拟接口

这四种情况是我们作为一般客户端使用时，全部的四种情况。http代理服务器也是很多代理工具描述的"系统代理"使用的代理服务器协议。他们的DNS逻辑略有不同，所以我们逐一理解。

在此之前，我们先了解一下socks/http代理是什么。

## 1. socks与http代理简介

**SOCKS代理**

SOCKS 代理是一种通用的网络代理协议，他工作在会话层/传输层之间。

SOCKS代理并不能理解上层传输的应用是什么协议，什么HTTP，SMTP，SSH等协议SOCKS都不认识，他只会纯粹的拷贝和转发数据。

SOCKS代理最新的版本是5，也就是SOCKS5，SOCKS5开始，DNS请求可以被代理到服务器上进行，也可以选择在客户端本地解析，这取决于客户端的选择。

如果客户端选择SOCKS5代理DNS请求，客户端会把要访问的目标告诉SOCKS服务器，例如：

```bash
客户端：SOCKS代理，我想访问www.google.com:443，同时你帮我解析这个域名的DNS。
SOCKS：收到访问请求www.google.com:443，在我这边解析www.google.com的IP地址。
SOCKS：解析到www.google.com的IP地址，并且从目标处获得了数据，准备发给你客户端
客户端：收到了，完成访问
```

如果客户端选择SOCKS不代理DNS请求，客户端会在本地完成DNS解析后，把访问的目标IP地址告诉SOCKS服务器，例如：

```bash
客户端：我想访问www.google.com:443，我自己先解析一下www.google.com的IP地址。
客户端：我解析到www.google.com的IP地址是142.251.151.119。
客户端：SOCKS代理，我要访问142.251.151.119:443
SOCKS：收到访问请求142.251.151.119:443，从目标处获得了数据，准备发给你客户端
客户端：收到了，完成访问
```

**HTTP代理**

HTTP 代理是一种专门为 HTTP/HTTPS 设计的应用层代理。

HTTP代理可以理解HTTP中的请求和响应，并进行应用层代理和转发。

HTTP代理是必须由服务器进行DNS解析的，无法由应用本地发起DNS解析：

```bash
客户端：我想访问www.google.com:443，发给你HTTP代理。
HTTP代理：收到访问请求www.google.com:443，在我这边解析www.google.com的IP地址。
HTTP代理：解析到www.google.com的IP地址，并且从目标处获得了数据，准备发给你客户端。
客户端：收到了，完成访问。
```

**使用他们两个入口的原因**

因为socks/http代理是标准的代理服务器，受到各个主流操作系统和应用的支持，而我们使用的各种VLESS/Trojan等协议都不是标准的代理服务器，操作系统和应用不认识，所以我们需要一个介质把这些代理转换为socks/http代理供应用或系统接入，这个介质就是代理工具，比如mihomo。

mihomo等代理工具一端入口是socks/http代理，供各种应用和系统接入代理，一端是各种VLESS/Trojan等协议，负责真正出网传输连接到海外的代理服务器。

**为什么不直接使用socks/http代理服务器进行翻墙？**

因为这两个代理协议默认情况下都是不加密的，SOCKS规范里没有加密相关，HTTP代理可以选择使用TLS保护，也就是HTTPS代理。

但即使加密，这两种协议有明显的特征可供探测，无法抵抗GFW的检查，所以不能直接使用他们。

了解这两个代理协议后，我们回到主线讨论。

## 2. DNS模式为Redir-host，入站方式为socks/http服务器

工作流程如下：

- 用户准备访问 `www.google.com` ,浏览器准备
- 浏览器发现系统中配置了socks/http代理服务器（假设socks配置使用远程DNS）
- 浏览器直接把 `www.google.com` 的访问请求丢给代理服务器（注意，浏览器自身没有发起任何DNS解析）
- socks/http代理服务器（实际上就是mihomo内核）通过设置的入口：

```bash
port: 7890 //HTTP代理端口
socks-port: 7891 //SOCKS代理端口
mixed-port: 7892 //同时支持二者的混合端口
```

收到了客户端要访问 `www.google.com` 。

按照socks/http代理规范，作为服务端的mihomo不会主动进行DNS查询告知客户端，也就绕过了DNS模块中的Redir-host设置。

- mihomo直接用 `www.google.com` 这个访问目标开始匹配路由规则：

```bash
rules:
  - DOMAIN-SUFFIX,baidu.com,DIRECT
  - IP-CIDR,142.0.0.0/8,PROXY
```

第一条规则很显然并不能匹配，第二条规则是个IP规则，但是mihomo此时要匹配的目标是个域名，没法比对怎么办？

- mihomo看了看这个IP规则没有添加 `no-resolve` 禁止解析的指示，于是准备发起一个DNS解析查一查 `www.google.com` 的IP地址是多少，用来匹配这个IP规则。

- mihomo内核内部构造了一个 `www.google.com` 的DNS解析，于是来到mihomo的DNS模块中匹配DNS规则：

```bash
dns:
  enable: true
  listen: 0.0.0.0:1053
  ipv6: false
  enhanced-mode: redir-host
  use-hosts: true
  nameserver:
    - 223.5.5.5
    - 1.1.1.1
    - 8.8.8.8
```

- mihomo发现有三个可以使用的DNS服务器，于是直接把 `www.google.com` 的解析请求发给他们三个，谁的结果最快用谁。

- **很明显，DNS服务器中有223.5.5.5这个国内DNS，于是 `www.google.com` 的解析请求到了这个国内的DNS，造成了泄露。**

- mihomo收到了DNS结果后继续匹配，假设匹配成功，判断 `www.google.com` 需要走代理
- mihomo不采取规则匹配阶段得到的DNS结果，直接把 `www.google.com` 的请求发给节点服务器
- 节点服务器收到 `www.google.com` 的访问请求，在自己的网络环境下再次发起DNS解析获得 `www.google.com` 的IP地址，并访问网站，拿到数据后再把数据发回给客户端。

## 3. DNS模式为Fake-IP，入站方式为socks/http服务器

工作流程如下：

- 用户准备访问 `www.google.com` ,浏览器准备
- 浏览器发现系统中配置了socks/http代理服务器（假设socks配置使用远程DNS）
- 浏览器直接把 `www.google.com` 的访问请求丢给代理服务器（注意，浏览器自身没有发起任何DNS解析）
- socks/http代理服务器（实际上就是mihomo内核）通过设置的入口收到了客户端要访问 `www.google.com` 。

按照socks/http代理规范，作为服务端的mihomo不会主动进行DNS查询告知客户端，也就绕过了DNS模块中的Fake-IP设置。

- mihomo直接用 `www.google.com` 这个访问目标开始匹配路由规则
- mihomo看了看这个IP规则没有添加 `no-resolve` 禁止解析的指示，于是准备发起一个DNS解析
- mihomo内核内部构造了一个 `www.google.com` 的DNS解析，于是来到mihomo的DNS模块中匹配DNS规则：

```bash
dns:
  enable: true
  listen: 0.0.0.0:1053
  ipv6: false
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
  use-hosts: true
  nameserver:
    - 223.5.5.5
    - 1.1.1.1
    - 8.8.8.8
```

- 由于这是一个用于匹配IP规则的DNS解析，即使设置了fake-ip，mihomo也会忽略这个设置，去查询该域名的真实IP结果。

- **同样地，因为nameserver中有国内DNS服务器，解析请求又发给了国内的DNS，造成泄露。**

> 💡 **小结**：在使用SOCKS或HTTP入站的时候，无论你用Redir-host还是Fake-IP模式，只要nameserver里有国内DNS并且有IP规则被触发，都可能产生DNS泄露。

## 4. DNS模式为Redir-host，入站方式为TUN虚拟接口

工作流程如下：

- 用户准备访问 `www.google.com` ,浏览器准备
- 浏览器发现系统中没有配置任何有效的代理服务器，于是该请求准备直接发起
- 此时浏览器不知道 `www.google.com` 的IP地址，无法直接访问网站，于是准备构建一个DNS请求查询一下 `www.google.com` 的IP地址。
- 该条DNS请求直接被TUN虚拟接口捕获，并路由进入mihomo内核

mihomo内核发现这是一个DNS请求，于是导入DNS模块准备解析：

```bash
dns:
  enable: true
  listen: 0.0.0.0:1053
  ipv6: false
  enhanced-mode: redir-host
  use-hosts: true
  nameserver:
    - 223.5.5.5
    - 1.1.1.1
    - 8.8.8.8
```

- mihomo看了看自己的DNS模式为redir-host，于是准备发起DNS解析获得 `www.google.com` 的真实IP地址。
- mihomo发现有三个DNS可以使用，于是同时向他们三个发送了 `www.google.com` 的DNS解析请求
- **DNS列表中有223.5.5.5这个国内DNS，此时产生了DNS泄露。**
- DNS响应了结果，假设 `142.251.151.119` ，mihomo收到后直接把这个结果告诉浏览器，同时在内核内部维护一个映射表，标记 `142.251.151.119` 与 `www.google.com` 是对应的。
- 浏览器收到解析结果后，对着 `142.251.151.119` 发起访问请求
- 访问请求再次被TUN虚拟接口捕获，mihomo根据映射表还原域名，然后匹配路由规则决定走代理。
- mihomo在连接发出代理服务器之前，根据redir-host的映射表把目标 `142.251.151.119` 改成 `www.google.com` ，然后再发给节点服务器。

> ⚠️ 可以看到，TUN加Redir-host模式下，DNS查询发生的更早，泄露风险也更大。

## 5. DNS模式为Fake-IP，入站方式为TUN虚拟接口

工作流程如下：

- 用户准备访问 `www.google.com` ,浏览器准备
- 浏览器发现系统中没有配置任何有效的代理服务器，于是该请求准备直接发起
- 此时浏览器不知道 `www.google.com` 的IP地址，于是准备构建一个DNS请求
- 该条DNS请求直接被TUN虚拟接口捕获，并路由进入mihomo内核

```bash
dns:
  enable: true
  listen: 0.0.0.0:1053
  ipv6: false
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
  use-hosts: true
  nameserver:
    - 223.5.5.5
    - 1.1.1.1
    - 8.8.8.8
```

- mihomo看了看自己的DNS模式为Fake-IP，于是准备直接从配置的fake-ip地址池 `198.18.0.1/16` 中挑选一个IP返回给浏览器。
- 假设挑选了一个IP `198.18.0.232` ，mihomo把这个请求告诉浏览器，同时在内核内部维护的一个Fake-IP映射表中记录下 `198.18.0.232` 与 `www.google.com` 是对应的。
- 浏览器收到解析结果后，对着 `198.18.0.232` 发起访问请求。
- 访问请求再次被TUN虚拟接口捕获，mihomo根据映射表还原回这个连接的原始目标为 `www.google.com` 。
- 连接来到路由规则，匹配到IP规则时，mihomo还是需要查询真实IP来判断是否匹配。
- **这时它又会向包含国内DNS的服务器列表查询，导致泄露。**

> 💡 **结论**：Fake-IP模式虽然减少了DNS查询的次数，但并不能完全避免泄露。

---

# 三、原因总结与改进思路

如果你自己阅读并理解了上述的四种工作流程，你就可以知道DNS产生意外的位置无非是如下：

1. **使用SOCKS代理时**，SOCKS客户端没有配置代理DNS，导致DNS根本没有进入mihomo内核，从应用直接发出。
2. **路由规则中存在IP规则且被匹配**，同时DNS模块的DNS服务器分流与并发设计不合理。
3. **TUN接口对上层应用的工作逻辑影响**。
4. **Windows系统对DNS的特殊逻辑**（多宿主DNS解析）。

我们逐一解决：

## 解决方案一：确保SOCKS5代理DNS

只需要确保使用SOCKS5代理协议的客户端勾选"代理DNS"即可。（不同工具的配置描述可能不一致，请自行寻找类似位置）

## 解决方案二：优化路由规则顺序

mihomo的路由规则是自上而下匹配的，因此我们需要确保基于域名的规则放置在基于IP规则的前面，并定期维护域名列表，确保常用的域名都可以直接被域名规则匹配，即可大大减少DNS查询的发生概率。

```bash
rules:
  - DOMAIN-SUFFIX,google.com,PROXY
  - DOMAIN-SUFFIX,baidu.com,DIRECT
  - IP-CIDR,142.0.0.0/8,PROXY
```

这样当 `www.google.com` 请求到来时，会第一个域名规则会直接命中，不再匹配后续的IP规则，那么就不会产生DNS解析。

也可以给IP规则加 `no-resolve` 标识：

```bash
rules:
  - DOMAIN-SUFFIX,google.com,PROXY
  - DOMAIN-SUFFIX,baidu.com,DIRECT
  - IP-CIDR,142.0.0.0/8,PROXY,no-resolve
```

但是加 `no-resolve` 会导致域名目标完全依赖域名规则的匹配，如果域名规则不够完善，可能会导致分流效果下降，而且解决不了Redir-host+TUN模式下的DNS逻辑问题，更解决不了DNS逻辑不够高效导致的网站速度慢。

## 解决方案三：DNS模块优化（推荐）

因此，这里我更推荐进行DNS模块的改进，将DNS解析按照规则区分，不同目标使用不同DNS服务器和出口解析，兼顾IP规则的必要性，且无论使用Fake-IP还是Redir-Host，都可以保证DNS的一致安全性：

```bash
dns:
  enable: true
  listen: 0.0.0.0:1053
  ipv6: false
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
  use-hosts: true
  default-nameserver:
    - '223.5.5.5#DIRECT'
    - '119.29.29.29#DIRECT'
  proxy-server-nameserver:
    - 'https://dns.alidns.com/dns-query#DIRECT'
  nameserver:
    - "https://cloudflare-dns.com/dns-query#PROXY"
  nameserver-policy:
    "+.google.com": "https://cloudflare-dns.com/dns-query#PROXY"
    "+.bilibili.com": "https://dns.alidns.com/dns-query#DIRECT"
```

### 配置详解

**default-nameserver** - 用于解析加密DNS域名本身：

```bash
default-nameserver:
    - '223.5.5.5#DIRECT'
    - '119.29.29.29#DIRECT'
```

`#DIRECT` 是代表这个DNS服务器使用 `DIRECT` 这个出口进行连接，也就是直连。使用直连的目的是确保DNS系统和节点的起始连接可以正常完成，防止出现死循环问题：想要连接DNS需要通过节点，但是节点连接需要先进行DNS解析。

**proxy-server-nameserver** - 用于解析节点服务器中存在的域名：

```bash
proxy-server-nameserver:
    - 'https://dns.alidns.com/dns-query#DIRECT'
```

在没有解析出节点的入口之前，节点是不能使用的，所以这个也建议使用直连。

**nameserver-policy** - 按域名分流DNS服务器：

```bash
nameserver-policy:
    "+.google.com": "https://cloudflare-dns.com/dns-query#PROXY"
    "+.bilibili.com": "https://dns.alidns.com/dns-query#DIRECT"
```

- 当访问 `www.google.com` 时，会使用PROXY，也就是节点，并通过 Cloudflare 加密DNS解析。
- 当访问 `www.bilibili.com` 时，会使用DIRECT，也就是直连，通过阿里加密DNS解析，提升国内网站的解析速度。

**nameserver** - 默认DNS服务器：

```bash
nameserver:
    - "https://cloudflare-dns.com/dns-query#PROXY"
```

此处规则没有匹配到的DNS解析请求，将会使用默认DNS服务器进行解析，通过代理并使用 Cloudflare 处理。

> ✅ **这样就保证了**：国内DNS只能知道我们在访问哔哩哔哩，而不知道我们访问了Google。同时，对于我们没有覆盖到的域名，全部走节点代理的DNS解析，确保绝对不会对国内DNS产生泄露。

## 解决方案四：Windows多宿主DNS解析问题

这个问题只有TUN模式下会遇到，来源是Windows的一个功能：**多宿主DNS解析**。

这个功能目的是加快DNS解析速度和成功率，当系统中有应用发起DNS解析后，Windows会把该DNS解析发送到系统上所有可用的网络接口上。

问题就在这里：

- Windows系统把DNS请求同时发送给了物理网卡和TUN虚拟接口
- 一边被TUN接口捕获并路由进入mihomo内核
- **一边直接从物理网卡发出去**

即使我们mihomo的DNS配置的再好，有一个直接从物理网卡出去的DNS请求根本没有经过mihomo内核，那么也导致了DNS泄露。

### 方案一：组策略关闭多宿主DNS解析

位置在：本地组策略编辑器 - 计算机配置 - 管理模板 - 网络 - DNS客户端 - 禁用智能多宿主名称解析

进入策略参数，改为已启用即可。

### 方案二：TUN严格路由（推荐）

mihomo的TUN接口使用了sing-tun的代码，也带来了sing-tun的严格路由功能。

TUN严格路由就是，未经过TUN接口传输的数据全部都丢弃掉，也就让Windows的多宿主解析失去效果。

```bash
tun:
  enable: true
  stack: system
  auto-route: true
  auto-detect-interface: true
  strict-route: true  # 严格路由，设置为true即为启用
  dns-hijack:
    - any:53
```

> ⚠️ **提示**：严格路由可能会导致计算机物理网卡的传入连接受到影响，可能会影响一些局域网发现功能，比如很多手机的设备互联等，因此两种方案按需选择。

---

# 四、为什么要在乎DNS泄露问题

2025年，对于代理的环境压力逐渐加大，国内通报加剧，机场被买订阅泄露入口针对打击，甚至很多人访问YouTube等网站后立刻收到了属地反诈短信或电话提醒，包括很多学校的学生说自己翻墙被查到。

其实很多情况下并不是协议不安全，无论是最初的Shadowsocks，还是后来的Trojan，VMess，再到如今的VLESS+REALITY（VLESS本身没有加密，必须依赖TLS或REALITY做安全层加密），Hysteria等，他们的共同能力都是对内层数据的绝对加密保护，在密钥/密码没有泄露的情况下，你的内层访问目标是完全无法由中间人看见的。

**那么对于你的访问习惯，最直观最快速最精准的统计方式就是DNS。**

试想一下，你使用校园网/国内的DNS查询了 `www.google.com` 的IP地址是多少，然后紧接着对着一个服务器发送了一堆看不懂的加密数据，这种时序特征就是一个明显的信号 - 你在访问不合规的网站且疑似使用代理。

**很多情况往往是使用者的问题，而不是开发者的问题。**

当然，也要警惕某些受管理的公司网络/校园网络所使用的接入客户端，也许会在你的设备上注入证书来暗中MITM加密流量，当然这是另一种情况，不是DNS话题。

---

# 五、潜在的问题与提示

很多人并不会直接使用mihomo内核加载配置文件，而是使用基于mihomo内核开发的图形客户端代理软件，如Clash Verge Rev，Clash Party等，这些代理软件会使用其默认参数覆盖原始配置文件的部分字段，导致我们写好的配置文件遭到篡改并失去原始逻辑。

而他们的覆写是按照能够正常启动工具功能的逻辑去编写的，并不是最优选择，甚至有一些工具写的很差很烂。

**因此使用这些工具时，确保他们的一切覆写功能完全关闭，或无需求干脆不要使用他们。**

---

# 六、相关资源

> 📺 视频教程：[为什么加了节点还是被查到？一篇文章带你彻底了解Mihomo DNS查询工作方式，解决DNS泄露](https://youtu.be/UFO-ZNHLXVw)

## 短信及语音接码平台

- https://hero-sms.com/?ref=357885

## 白嫖流量

- 500M试用：https://ipfly.net/zh-cn/activity/GXJDIAN （优惠码 GXJDIAN，85折）
- 200M试用：https://dashboard.talordata.com/reg?inviter_code=gxjdian （优惠码 GXJDIAN，9折）

## 社群及链接

1. 微信讨论群：https://qr.869hr.uk/aitech
2. 超过100T资料总站网站：https://doc.869hr.uk
3. Telegram群聊：https://t.me/tgmShareAI
4. 微信公众号：搜"AI前沿的短裤哥"
5. 视频的文字博客：https://869hr.uk
6. 推特：https://x.com/gxjdian
7. Youtube：https://youtube.com/@gxjdian

## VPS主机

- Claude用的丽萨主机：https://lisahost.com/aff.php?aff=9424
- 按流量VPS：https://www.lycheeip.com/home/ip?affId=1AwYIQ7BW8
- 一年10美元多年保底小鸡：https://clients.zgovps.com/?affid=1207
- 各种云主机，主打性价比：https://my.racknerd.com/aff.php?aff=15809
- 美国VPS一年70美金：https://app.cloudcone.com/?ref=13794
- 一年8.5美金美国家宽：https://www.webshare.io/?referral_code=55vpv6waorud

## 家宽IP及住宅VPS

- 家宽IP：https://ipfly.net/activity/OE5TWVlUUEI6TFZKOVhYQzM5NQ==
- 住宅VPS：https://www.voyracloud.com/?ref_code=5ZG4FHL8

## Gmail、Telegram等账号购买、礼品卡

- https://accboy7gxjdian.acceboy.com/
- https://universalbus.cn/?s=bvDplWi2fZ
- https://www.gamsgo.com/partner/jGh24

## AI产品充值

- Claude、OpenAI Codex等充值：https://bewild.ai?code=GXJDIAN

## eSIM

1. 三家eSIM对比：https://s.869hr.uk/mcc
2. 9eSIM（优惠码：maq）：https://www.9esim.com/?coupon=maq
3. ESTK（优惠码：GXJDIAN）：https://store.estk.me/zh?aid=16007
4. XeSIM（推荐码：gxjdian）：https://xesim.cc/?DIST=RE5FHg==

## 银行卡/支付卡

5. Wise申请（推荐码：lizhiw12）：https://wise.com/invite/ihpc/lizhiw12
6. N26申请（推荐码：lizhiw02766c）：https://youtu.be/HY9OD8rX89s
7. Bybit支付卡：https://www.bybit.com/invite?ref=LGNQRG

## YouTube播放列表

- AI产品和技术相关：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海VPS：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

---

> 💡 **关注我不迷路**：如果你觉得这篇文章对你有帮助，请关注我的YouTube频道 [短裤AI分享](https://youtube.com/@gxjdian)，点赞视频，在评论区留下你的问题。订阅频道并打开小铃铛，获取最新硬核教程和科技前沿资讯！

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/%E7%BD%91%E7%BB%9C%E5%AE%89%E5%85%A8/2026-04-19-dns-leak-mihomo-tutorial/)
