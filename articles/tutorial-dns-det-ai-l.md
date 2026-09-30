# 【零基础教程】系统了解DNS查询全过程：从根域到权威，详解DNS工作原理与安全防篡改！

这期视频带你零基础系统全面地了解DNS域名系统的查询全过程，从根域到权威详解DNS工作原理与安全防篡改

> 完整图文与持续更新版本：[【零基础教程】系统了解DNS查询全过程：从根域到权威，详解DNS工作原理与安全防篡改！](https://869hr.uk/2026/tutorial/tutorial-dns-det-ai-l/)

## 内容信息

- 原文：https://869hr.uk/2026/tutorial/tutorial-dns-det-ai-l/
- 更新：2026-04-19
- 分类：教程
- 专题：教程
- 关键词：VPN、网络工具、域名、教程
- 视频：https://www.youtube.com/watch?v=mAD591hkUAA
- 系列：[出海网络搭建](../series/overseas-network.md)

## 正文

<!-- 文章摘要 -->
> 
这篇文章带你了解DNS查询的过程和工作方式，系统全面地掌握DNS（域名系统）的查询全过程，从根域到权威，详解DNS工作原理与安全防篡改。

## 视频教程

<div class="video-container">
[在 YouTube 观看视频](https://www.youtube.com/watch?v=mAD591hkUAA)
</div>

<!-- more -->

## 前言

这篇文章带你了解DNS查询的过程和工作方式。

## 一、DNS的概念

DNS中文名称 **域名系统**，是一种可以将域名（例如 `www.google.com` ）翻译为计算机友好的IP地址的服务，这样人类可以不需要记住IP地址，而是可以通过更好记的域名访问Internet服务。

计算机之间进行网络传输数据只认识IP地址，而不认识域名，DNS正是做这种"翻译"工作。

DNS多数情况下做域名 → IP地址的解析工作，但也可以做IP地址 → 域名的解析工作，后者被称为rDNS（反向DNS）。

## 二、域的分类

域按照层级，可以分为根域、顶级域、二级域和子域。

### 1. 根域

根域是DNS树的最顶端，写作 `.` 。

它本身没有任何名字，就是一个 `.` ，在解析器中也一般是隐式存在的。

比如说， `www.google.com.` 的最后一个 `.` 就是根域的标志。

任何域最后都一定属于根域。

### 2. 顶级域

顶级域（TLD）是位于根域下的一级域名。

比如说 `.com` , `.org` , `.net` 等。

`www.google.com.` 的顶级域就是 `.com` 。

### 3. 二级域

注册在顶级域下面的域名，这也是我们付费注册的内容。

`google.com` 的二级域就是 `google` 。

`google.co.jp` 的二级域是 `co` ，但是 `.co.jp` 是一个整体的域名注册单位，是依附于顶级域 `.jp` 下面的一个二级域注册单位。

二级域在网络空间，搜索引擎中的SEO是独立存在的，有各自不同的内容与表现。

### 4. 子域

在二级域下面进一步划分的域名，用于区分同一个二级域下面的不同服务，不需要单独注册，二级域所有者使用DNS自行划分即可。

`www.google.com` 中的 `www` 就是 `google.com` 这个二级域下面的一个子域。

## 三、DNS的种类

DNS根据工作位置和作用的不同，分为五种DNS服务器：

- DNS转发器
- 递归DNS服务器
- 根DNS服务器
- TLD权威服务器
- 权威DNS服务器

我们在平时能够接触到的是前两种，DNS转发器和递归DNS。

### 1. DNS转发器

DNS转发器最常见于我们的设备通过DHCP获得的IP地址，比如路由器的IP地址。

路由器会在自身的UDP 53端口上运行一个简易的DNS转发器，设备将DNS请求发送给路由器后，路由器按照自己配置的上游DNS（一般是运营商PPPoE下发的DNS服务器）直接转发。

DNS转发器大量见于局域网内的DNS设备，或个人兴趣搭建的私有DNS；运营商的区域/市级网络也会部署用于边缘缓存，减轻骨干网DNS压力。

DNS转发器是一种非常无脑的解析器，它自己什么都不知道，只会把收到的DNS解析请求转发给设置的上游DNS，自己只是进行简单的缓存控制或准入控制等，它不会真正去查询域名的信息。

### 2. 递归DNS服务器

这种DNS也非常常见，我们很常见的 `1.1.1.1` ， `8.8.8.8` ， `223.5.5.5` 等都属于递归DNS，并且他们对公众开放使用，所以他们也叫公共递归DNS，我们一般简称叫他们公共DNS。

他们不同于DNS转发器，递归解析器是DNS系统中的核心节点，负责真正接受DNS查询请求。

递归DNS知道完整的DNS查询流程，知道根DNS的信息，并逐级递归根DNS，TLD DNS，权威DNS，直到查询到域名的DNS信息，这也是递归DNS的名称来源。

同时递归DNS一般具备缓存能力，用于加快DNS查找速度。

### 3. 根DNS服务器

根DNS（Root Name Server）是整个互联网最高级别的服务器，它是一切DNS查询的起点，记录着顶级域（TLD）的权威DNS服务器地址，并引导递归DNS下一步查询的TLD DNS地址。

同时，根DNS还是DNSSEC的信任起始锚点，DNSSEC所有的签名都从根DNS开始，逐级建立信任链。

可以理解为，根DNS是整个互联网DNS的"图书馆"。

根DNS在全球范围内一共有13个逻辑标识，按照字母，从A到M。

注意，这并不代表根DNS服务器只有13台，根DNS服务器的IP地址使用Anycast技术，同一个IP广播到很多地区的多个机房上，因此根DNS实际上由上千个节点和全球网络构成，极大提升其负载能力与灾备，并有效对抗针对根DNS服务器的攻击。

递归DNS会预置一个根提示文件，该文件中就包含上述列表的内容，用于提示起始的根DNS服务器域名与IP地址，从而让递归DNS能够找到DNS查询的起点。

根DNS只有13个逻辑标识，是因为DNS协议基于UDP传输，UDP协议根据RFC 1035，规定最大报文长度是512字节，13 个是最大可放入报文的 IPv4 地址数量，因此导致根DNS只有13个逻辑标识和IP地址，但是因为使用了Anycast，实际物理服务器可以无限多。

根DNS还管理着所有的TLD权威服务器分配与他们的粘性记录（Glue record），根DNS会存储TLD权威服务器的IP地址，避免DNS查询进入依赖循环问题（即查询前必须知道TLD权威服务器的IP却要先查询TLD权威服务器的IP问题）。

### 4. TLD权威服务器

TLD权威服务器（TLD DNS）是位于根DNS后的二级DNS服务器，它记录着各自的顶级域下的所有域名的权威DNS记录（比如 `.com .net .org .io` 等)，当递归DNS解析具体网站时，TLD DNS负责帮递归解析器找到该网站的权威DNS服务器。

比如 `.com` 顶级域的TLD DNS就记录着所有以 `.com` 结尾域名的权威DNS记录，比如 `www.google.com` ， `www.bilibili.com` 等。

### 5. 权威DNS服务器

权威DNS是负责存储和管理特定域名实际解析记录的最终来源。

当用户使用递归DNS进行某个域名的DNS查询时，最终就由该域名设置的权威DNS进行结果响应。

权威DNS是相对于域名而言的，每个域名的权威DNS可以是不一样的，其直接决定了域名解析的内容是什么。

## 四、DNS的一般工作流程

首先我们设定一个前置条件：

用户设备配置了一个DNS转发器 `192.168.31.1` ，DNS转发器配置的上游递归DNS服务器是 `1.1.1.1` ，请求解析的域名是 `www.google.com` 。

具体工作流程如下：

- 用户对 `192.168.31.1` 这个DNS转发器询问 `www.google.com` 的IP地址是多少
- `192.168.31.1` 这个DNS转发器也不知道解析结果，于是直接把这个DNS请求转发给了自己配置的上游递归DNS服务器 `1.1.1.1` 。
- 1.1.1.1收到了解析 `www.google.com` 的请求，但是自己也不知道 `www.google.com` 的解析结果是什么，于是查看自己的根提示文件，选择了其中一个或多个根DNS服务器，询问 `www.google.com` 域名的DNS怎么解析。

- 根DNS并不会直接回复 `www.google.com` 怎么解析，而是返回 `.com` 这个顶级域的权威服务器列表：

```bash
.com.  NS  a.gtld-servers.net
.com.  NS  b.gtld-servers.net
...
```

同时根DNS服务器会带上这些TLD权威服务器的粘性记录（Glue Record），避免查询进入死循环：

```bash
a.gtld-servers.net. A 192.5.6.30
b.gtld-servers.net. A 192.33.14.30
...
```

- `1.1.1.1` 这个递归DNS收到了 `.com` 的TLD权威服务器地址和对应的IP，于是继续问TLD权威服务器： `www.google.com` 怎么解析？
- TLD权威服务器也不会直接回复 `www.google.com` 怎么解析，而是开始查找 `google.com` 配置的权威DNS服务器是什么，也就是 `google.com` 的NS记录：

```bash
google.com.  NS  ns1.google.com
google.com.  NS  ns2.google.com
...
```

- 由于NS服务器是 `google.com` 这个域的子域，这属于同域NS，因此TLD权威服务器会直接把Glue Record一并告知，防止出现查询死循环：

```bash
ns1.google.com. A 216.239.32.10
ns2.google.com. A 216.239.34.10
```

- 1.1.1.1知道了 `www.google.com` 的权威DNS服务器，于是继续询问权威DNS服务器： `www.google.com` 怎么解析？
- `www.google.com` 的权威DNS服务器告知递归DNS， `www.google.com` 的A记录，TTL（生存时间）等信息：

```bash
www.google.com. 3600 IN A 142.251.150.119
www.google.com. 3600 IN A 142.251.153.119
```

- 递归DNS收到响应，按照TTL时间，把这个解析结果缓存下来，同时把响应返回给请求的客户端
- 于是，我们一次DNS解析完成了。
- 下次其他客户端再问 `1.1.1.1` ， `www.google.com` 的A记录是多少， `1.1.1.1` 发现缓存没有过期，于是直接返回

```bash
www.google.com. 3600 IN A 142.251.150.119
www.google.com. 3600 IN A 142.251.153.119
```

不再继续递归查询，节省时间。

## 五、DNS支持的解析记录

事实上，DNS远远不止可以解析IP地址，还可以承载多种记录。如下是我整理的一份列表。

可供参考：

| 记录类型 | 全称 | 主要用途 / 说明 | 分类 |
| --- | --- | --- | --- |
| **A** | Address | IPv4 地址映射，用于域名 → IPv4 | 基础 |
| **AAAA** | IPv6 Address | IPv6 地址映射，用于域名 → IPv6 | 基础 |
| **CNAME** | Canonical Name | 域名别名记录，指向另一个域名（不能与 A/AAAA 同时存在） | 基础 |
| **DNAME** | Delegation Name | 子域别名，作用范围比 CNAME 大，影响整个子域 | 基础 |
| **NS** | Name Server | 指定权威 DNS 服务器 | 基础 |
| **MX** | Mail Exchange | 邮件服务器路由 | 邮件 |
| **PTR** | Pointer | 反向 DNS，用 IP → 域名 | 基础 / 反向 |
| **SOA** | Start of Authority | 区域起始记录，包含管理员邮箱、序列号、刷新时间等 | 基础 |
| **TXT** | Text | 任意文本信息，可用于验证、SPF、DKIM、DMARC 等 | 基础 / 验证 |
| **SPF** | Sender Policy Framework | 邮件发送策略，实际上是 TXT 记录的一种格式 | 邮件 |
| **SRV** | Service | 指定服务位置（协议+端口），如 SIP、XMPP、LDAP | 服务发现 |
| **CAA** | Certification Authority Authorization | 指定哪些 CA 可为该域签发证书 | 安全 / 证书 |
| **NAPTR** | Naming Authority Pointer | 高级服务重定向，常配合 SRV 使用（SIP/ENUM） | 服务发现 |
| **DS** | Delegation Signer | DNSSEC，用于验证下级域签名 | DNSSEC |
| **RRSIG** | DNSSEC Signature | DNSSEC 签名，保证数据完整性 | DNSSEC |
| **DNSKEY** | DNSSEC Key | DNSSEC 公钥，用于验证 RRSIG | DNSSEC |
| **NSEC / NSEC3** | Next Secure | DNSSEC 证明某记录不存在 | DNSSEC |
| **CDS / CDNSKEY** | Child DS / Child DNSKEY | DNSSEC 子域自动更新签名 | DNSSEC |
| **TLSA** | TLS Authentication | 与 DANE 协议结合，指定证书校验 | 安全 / DANE |
| **SMIMEA** | S/MIME Certificate | 邮件加密证书，用于 S/MIME | 邮件 / 安全 |
| **SSHFP** | SSH Fingerprint | 存储 SSH 公钥指纹，用于验证 SSH 连接 | 安全 |
| **LOC** | Location | 域名地理位置信息 | 其他 |
| **URI** | Uniform Resource Identifier | 指向某个 URI，部分服务使用 | 服务发现 / 网络 |
| **OPENPGPKEY** | OpenPGP Public Key | 发布 OpenPGP 公钥 | 安全 / 邮件 |
| **IPSECKEY** | IPSEC Key | 用于 IPsec 公钥定位 | 安全 / VPN |
| **SVCB** | Service Binding | 新型服务绑定记录（比HTTPS记录更具拓展能力） | 服务发现 / HTTPS |
| **HTTPS** | HTTPS Service Binding | HTTPS 服务端点信息，RFC 8484 | 服务发现 / HTTPS |

## 六、DNS拓展能力

### 1. DNSSEC

域名系统安全扩展 (DNSSEC) 是添加到 DNS 记录中的加密签名。

由于DNS协议设计之初，并没有提供任何可靠性的安全保护措施，DNS记录可以被攻击者篡改，并导致最终用户访问到错误的目标，因此DNSSEC应运而生。

DNSSEC可以保护DNS记录不被篡改，信任基于信任链进行，从根DNS服务器开始，直到最终域名的权威DNS服务器。

DNSSEC需要全链路的DNS服务器，以及客户端支持，任何一个不支持，都会导致DNSSEC失效，降级为普通DNS，不进行任何验证。

DNSSEC的工作流程：

- 客户端向递归DNS发起查询 `www.google.com` 的 `A` 记录是什么
- 递归DNS不知道 `www.google.com` 的 `A` 记录，于是查询根DNS服务器， `www.google.com` 的 `A` 记录是什么。
- 根DNS服务器不会直接回复，而是返回 `.com` TLD 权威服务器列表 + Glue（IP），以及根区域的 `DNSKEY` 和 `RRSIG` 。
- 递归解析器收到了上述内容，由于自己支持DNSSEC，内部预埋了根区域的本地信任锚（Root DNSKEY），递归解析器会使用此信任锚验证根服务器返回的RRSIG签名。
- 一旦验证通过，递归解析器就会信任 `.com` TLD 权威服务器列表 + Glue（IP）信息，同时信任根DNS服务器返回的最新 `DNSKEY` 记录。
- 递归解析器继续查询TLD权威服务器， `www.google.com` 的 `A` 记录是什么
- TLD权威服务器也不会直接回复，而是 `google.com` 权威DNS服务器的NS列表+ Glue（IP），以及TLD的 `RRSIG` ，以及指向到 `google.com` 这个子域的 `DS` 记录。
- 递归解析器收到后，会使用根DNS服务器的DNSKEY验证TLD权威服务器的 `RRSIG` ，验证通过后，会信任 `google.com` 权威DNS服务器的NS列表+ Glue（IP），以及指向到 `google.com` 这个子域的 `DS` 记录，从 `DS` 记录中获得子域的 `DNSKEY` 指纹，准备验证子域。
- 递归解析器继续查询 `google.com` 这个域名的权威DNS服务器， `www.google.com` 的 `A` 记录是什么。
- `google.com` 这个域名的权威DNS服务器会直接回复 `www.google.com` 的A记录，对A记录的 `RRSIG` 签名信息以及 `google.com` 域的DNSKEY，以及对 `DNSKEY` 的 `RRSIG` 签名。
- 递归解析器会使用从TLD权威服务器那获得的指向到 `google.com` 这个子域的 `DS` 记录中的 `DNSKEY` 指纹与获得的 `DNSKEY` 做比对，如果验证通过， `DNSKEY` 被信任。
- 递归解析器使用已通过信任的 `DNSKEY` 验证A记录的 `RRSIG` ，验证通过后A记录也被信任。
- 结果被信任后，递归解析器会给此条响应附加 `DNSSEC` 已验证通过的标志，并将 `A` 记录与标志位返回给客户端。
- 客户端查看 `DNSSEC` 状态标志位，发现验证已通过，于是采纳该 `A` 记录。
- 本次解析结束。

### 2. 加密DNS

传统的DNS协议是明文的，这意味着任何人都可以查看并且审计DNS查询请求信息，且可以针对性劫持或篡改DNS响应。

因此诞生了加密DNS，加密DNS目前主流的两种便是 **DNS-over-TLS 和 DNS-over-HTTPS (DoH)。**

- **DNS-over-TLS (DoT)**

通过 TLS 对 DNS 查询进行加密，使用 TCP 853 端口

在进行DNS传输前，双方先进行TLS握手，在TLS的加密隧道中传输DNS内容。

常见格式：

```bash
tls://dns.google
```

- **DNS-over-HTTPS (DoH)**

通过HTTPS协议传输的DNS，从外部来看这就是正常的HTTP请求，不仅带来了加密和防篡改，同时带来了一定的伪装性。

常见格式：

```bash
https://dns.google/dns-query
```

注意，DoH是有默认的请求路径的，为 `/dns-query` ，使用时务必注意。

有些软件不支持自定义DoH路径，实际上就是上述的默认路径。

### 3. EDNS

传统的DNS响应报文上限是512字节，EDNS（Extension Mechanisms for DNS）为DNS报文长度带来了拓展，使其可以超过512字节，承载更多的内容，并支持添加拓展字段参数。

比如携带客户端子网信息（EDNS Client Subnet）进行的DNS查询就依赖EDNS拓展能力。

### 4. DANE（实验性）

RFC 6698中添加了一项DNS-based Authentication of Named Entities，简称DANE，主要是结合 DNSSEC，验证 TLS/SSL 证书绑定作用，目前仍在实验阶段，可以关注后续发展。

## 七、DNS常见问题

### 1. DNS记录更新速度慢

如果你仔细阅读了上面的全部内容，不难发现，DNS传播是递归且存在缓存的，因此DNS的解析内容更新会有一定的生效时间，这是完全正常的。

### 2. Cloudflare上托管域名的NS问题

我们在Cloudflare或其他DNS提供商上托管域名的DNS解析时，会观察到让我们前往域名注册商处修改域名的NS服务器。

实际上就是设置域名的权威DNS服务器为他们的NS服务器，这样Cloudflare或其他DNS服务商的DNS服务器就变成了我们域名的权威DNS服务器，负责应答我们域名的一切DNS解析内容，且负责管理此域名的DNS解析内容。

修改域名NS服务器不同于修改域名的其他DNS记录，NS记录修改是位于域名注册商处，必须由域名注册商同步到TLD的权威服务器，而提交到TLD并进行同步通常至少有30分钟，最长24小时的时间，因此域名修改权威DNS服务器（NS记录）的时间会比修改其他DNS记录生效时间更久，这也是正常现象。

### 3. DNS反射攻击

Internet现行的TCP/IP协议一直有一个没有解决的问题：IP是可以伪造的。

攻击者可以伪装自己的IP是攻击目标的IP地址，给大量Internet上开放的公共DNS服务器发送一个指定的DNS解析请求，这个请求是特制的，请求一个会携带大量数据的TXT或SRV记录的域名。

攻击者需要很少的数据量，伪装受害者IP请求公共DNS服务器，而公共DNS服务器会回复一个超大的响应给真正的受害者，导致受害者的网络不得不处理这些自己根本不需要的垃圾DNS数据，严重就会拖慢甚至击垮受害者的网络。

这就是DNS反射攻击。

加密DNS可以一定程度上规避这种问题，因为加密DNS使用的TLS握手要求双方必须完成后才会传输DNS响应，伪造的IP是完成不了握手的。

### 4. 二级域中可以为某一个子域继续设置NS服务器

假设google.com的权威DNS服务器是 `ns1.google.com` 。

我们可以在 `google.com` 这个二级域中继续为某一个子域添加NS记录，假设 `music.google.com` 的NS记录为 `alice.ns.cloudflare.com` ，那么 `music` 这个子域本身，以及其下面的更多子域，假设 `hk.music` 的DNS记录将由 `alice.ns.cloudflare.com` 这个NS提供并管理，而不是 `ns1.google.com` 。

递归解析器发现子域存在NS服务器时会继续递归查询。

## 八、后话

希望能够对DNS有所理解。

---

## 相关教程推荐

<!-- 推荐链接：Cloudflare/域名系列 -->
- [Cloudflare Tunnel + Docker 内网穿透教程](https://869hr.uk/2026/tutorial/cloudflare-tunnel-docker-tutorial/)

## 视频信息

- **视频标题**: 【零基础教程】系统了解DNS查询全过程：从根域到权威，详解DNS工作原理与安全防篡改！
- **YouTube链接**: https://youtu.be/mAD591hkUAA
- UP主: M.

## 参考链接

- [YouTube 原视频](https://www.youtube.com/watch?v=mAD591hkUAA)
- [869hr.uk 博客首页](https://869hr.uk)

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tutorial/tutorial-dns-det-ai-l/)
