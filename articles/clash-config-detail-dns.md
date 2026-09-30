# Clash配置文件详解｜从零搞懂DNS、策略组、分流规则附实战

逐项解析 Clash 配置文件中的 mixed-port、mode、DNS、策略组和分流规则，并结合示例说明常见配置错误与验证方法。

> 完整图文与持续更新版本：[Clash配置文件详解｜从零搞懂DNS、策略组、分流规则附实战](https://869hr.uk/2026/tech/clash-config-detail-dns/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/clash-config-detail-dns/
- 更新：2026-05-23
- 分类：技术
- 专题：技术
- 关键词：Clash、Clash配置、代理工具、分流规则、DNS配置
- 视频：https://www.youtube.com/watch?v=OT_tlDDMNB4

## 正文

<!-- 文章摘要 -->
> 
**教学背景**：Clash作为最常用的跨平台代理工具，相信是不少人的选择。然而无论是自建的节点还是机场的订阅链接，当我们要将其转换到代理工具中时，很多人对于其中的分流规则是茫然的。许多订阅转换网站或者机场自带的规则与我们想要的分流效果相去甚远，以至于对于想要访问的目标网站，我们无法随心所欲地控制它应该是选择直连还是代理。...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=OT_tlDDMNB4)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 11 分钟。

# 一、概述

**教学背景**：Clash作为最常用的跨平台代理工具，相信是不少人的选择。然而无论是自建的节点还是机场的订阅链接，当我们要将其转换到代理工具中时，很多人对于其中的分流规则是茫然的。许多订阅转换网站或者机场自带的规则与我们想要的分流效果相去甚远，以至于对于想要访问的目标网站，我们无法随心所欲地控制它应该是选择直连还是代理。

**教学对象**：此篇教学面向中初级用户，大佬还请无视本人拙劣的知识水平。

**教学内容**：本文将从配置文件入手，逐一说明每一个板块的作用以及应该如何设置，如果涉及没讲到的配置，那就是我自己觉得没必要配置的，如有大佬补充，请不吝赐教。

**适用软件**：
- 所有Clash系列软件，包括但不限于 **Clash Meta**
- 、 **Clash for Windows**
- 、 **Clash Verge**
- 、 **Clash Verge Rev**
- 、 **clash meta for android**
- 等
- Clash客户端。

**【温馨提示】**为方便阅读，配置文件和参数解析我都隐藏了，请按需展开。如果不想了解得特别详细的话，可以直接跳到实战演练。
# 二、Clash配置文件解析
## 2.1 简述配置文件

先贴出配置文件的简化版：

配置文件简化版

```yaml
mixed-port: 7890
allow-lan: true
bind-address: "*"
ipv6: false
mode: rule
log-level: info
external-controller: 127.0.0.1:9090
secret:""
dns:
proxies:
proxy-groups:
rules:
```

参数解析：

每个参数的作用
| 参数名称 | 作用 | 备注 |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------- |
| mixed-port | HTTP(S) 和 SOCKS4(A)/SOCKS5 代理服务共用一个端口 | 一般不需要将HTTP代理端口和SOCKS5代理端口分开，所以此处不修改 |
| allow-lan | 设置为 true 以允许局域网的连接（可用来共享代理） | 如没有局域网代理需求可关闭 |
| bind-address | 仅当 `allow-lan` 为 `true` 时有效<br>\*': - 绑定所有 IP 地址<br>- 192.168.122.11: 绑定单个 IPv4 地址<br>- “\[aaaa::a8aa:ff:fe09:57d8]”: 绑定单个 IPv6 地址 | 地址绑定，一般不需要修改 |
| ipv6 | 当设置为 false 时, 解析器不会将主机名解析为 IPv6 地址 | 因为我开启此选项老是出现解析错误，故我个人是选择关闭的 |
| mode | Clash 路由工作模式<br>rule: - 基于规则的数据包路由<br>- global: 所有数据包将被转发到单个节点<br>- direct: 直接将数据包转发到互联网 | 默认为规则模式，不需要更改 |
| log-level | 日志级别: info / warning / error / debug / silent | 为了平时方便调试我会设置为info |
| external-controller | RESTful Web API 监听地址 | 连接第三方Clash GUI的地址和端口，一般不需要修改 |
| secret | RESTful API 的口令(可选) | 连接第三方Clash GUI的密码，不需要可不填 |
| dns | DNS 服务设置 | 为防止DNS解析错误或DNS泄露，此部分需详细配置 |
| proxies | 代理节点 | 你的自建节点或者机场节点 |
| proxy-groups | 策略组 | 代理节点的分组 |
| rules | 分流规则 | 控制是否代理的规则 |
以上就是每个参数的大致设置和作用，可以看出，要想配置好分流规则，我们重点应该关注“ **dns**”、“ **proxy-groups**（策略组）”、“ **rules**（分流规则）”三个板块。下面我们再详述这三个参数。
## 2.2 DNS配置

DNS配置在站内也是老生常谈的内容了，相信也有不少佬友给出了自己的见解，我在这里就不对DNS泄漏以及其它原理做出过多论述了，大致讲一下我的配置逻辑即可。

先贴出DNS配置完整版文件：

DNS配置完整版文件

```plaintext
dns:
enable: true
prefer-h3: true
use-hosts: true
use-system-hosts: true
respect-rules: false
listen: 0.0.0.0:1053
ipv6: false
enhanced-mode: fake-ip
fake-ip-range: 198.18.0.1/16
fake-ip-filter:
- '*.lan'
- "+.local"
- localhost.ptlogin2.qq.com
default-nameserver:
- tls://1.12.12.12
- 223.5.5.5
- 119.29.29.29
nameserver-policy:
'www.baidu.com': '114.114.114.114'
'+.internal.crop.com': '10.0.0.1'
'geosite:cn,private':
- https://223.5.5.5/dns-query
- https://223.6.6.6/dns-query
nameserver:
- https://dns.alidns.com/dns-query
- https://doh.pub/dns-query
proxy-server-nameserver:
- https://dns.alidns.com/dns-query
- https://doh.pub/dns-query
fallback:
- tls://1dot1dot1dot1.cloudflare-dns.com
- tcp://1.1.1.1
- https://1.0.0.1/dns-query
- https://1.1.1.1/dns-query
fallback-filter:
geoip: true
geoip-code: CN
geosite:
- gfw
ipcidr:
- 240.0.0.0/4
- 0.0.0.0/32
- 127.0.0.1/32
domain:
- '+.google.com'
- '+.facebook.com'
- '+.youtube.com'
```

参数解析：

每个参数的作用
| 参数名称 | 作用 | 备注 |
| ----------------------- | ----------------------------------------------------------------------------------------------------------- | ------------------------------------------ |
| enable | 是否启动自定义dns模块 | 若为false，则使用系统 DNS 解析，我们需要自己配置DNS解析，因此选true |
| prefer-h3 | 是否优先使用 DOH 的 http/3 | 一种加密的基于 QUIC 协议实现的DNS 协议，据说查询速度很快，所以我打开了 |
| use-hosts | 是否查询配置中的 hosts，默认 true | 虽然我没有配置hosts，但是一般还是开启的 |
| use-system-hosts | 是否查询系统 hosts，默认 true | 同上 |
| respect-rules | dns 连接跟随 rules，需配置proxy-server-nameserver | 一般不需要，我个人选择关闭 |
| listen | DNS 服务监听，仅支持 udp | 保持默认就行 |
| ipv6 | 是否解析 IPV6, 如为 false, 则回应 AAAA 的空解析 | 因为我开启此选项老是出现解析错误，故我个人是选择关闭的 |
| enhanced-mode | DNS 处理模式<br>可选值 `normal` / `fake-ip` / `redir-host` ，默认normal | 不深入讲解，这里我选择fake-ip |
| fake-ip-range | fakeip 下的 IP 段设置，tun的默认 IPV4 地址 | 保持默认即可 |
| fake-ip-filter | fakeip 过滤，以下地址不会下发 fakeip 映射用于连接 | fake ip白名单列表，保持默认即可 |
| default-nameserver | 默认 DNS, 用于解析nameserver中的加密 dns | 此处必须为 IP, 可为加密 DNS，我设置为国内明文DNS |
| nameserver-policy | 指定域名查询的解析服务器，可使用 geosite, 优先于 nameserver/fallback 查询 | 保持默认就行 |
| nameserver | 默认的域名解析服务器，如不配置 `fallback/proxy-server-nameserver` , 则所有域名都由 nameserver 解析 | 我设置为国内加密dns |
| proxy-server-nameserver | 代理节点域名解析服务器，仅用于解析代理节点的域名 | 我设置为国内加密dns |
| fallback | 后备域名解析服务器，一般情况下使用境外 DNS, 保证结果可信<br><br>配置 fallback后默认启用 fallback-filter,geoip-code为 cn | 解析墙外域名的，因此不能使用国内DNS，我设置为国外加密 dns |
| fallback-filter | 后备域名解析服务器筛选，满足条件的将使用 `fallback` 结果或只使用 `fallback` 解析 | |
| geoip | 是否启用 fallback filter | 默认开启就行 |
| geoip-code | 可选值为 国家缩写，默认值为 CN<br>除了 geoip-code 配置的国家 IP, 其他的 IP 结果会被视为污染<br>geoip-code 配置的国家的结果会直接采用，否则将采用 fallback结果 | 默认CN就行 |
| geosite | 可选值为对于的 geosite 内包含的集合<br>geosite 列表的内容被视为已污染，匹配到 geosite 的域名，将只使用 fallback解析，不去使用 nameserver | 保持默认就行 |
| ipcidr | 书写内容为 IP/掩码<br>这些网段的结果会被视为污染，nameserver解析出这些结果时将会采用 fallback的解析结果 | 保持默认就行 |
| domain | 这些域名被视为已污染，匹配到这些域名，会直接使用 fallback解析，不去使用 nameserver | 保持默认就行 |
以上就是我针对DNS的全部设置，因本人对于DNS的运行逻辑只是一知半解，如果有佬友有更好的配置，后续会不断优化此短篇幅。
## 2.3 策略组

策略组是我们选择哪个网站选用什么方式连接的前置条件，简而言之就是给你的节点如何分流进行分组。

举一个最简单的策略组配置文件：

最简单的策略组配置文件

```yaml
proxy-groups:
- name: 🚀 节点选择
type: select
proxies:
- ♻️ 自动选择
- DIRECT
- 你的节点
- name: ♻️ 自动选择
type: url-test
url: http://www.gstatic.com/generate_204
interval: 300
lazy: true
timeout:5000
max-failed-times:5
tolerance: 50
proxies:
- 你的节点
- name: 🎯 全球直连
type: select
proxies:
- DIRECT
- 🚀 节点选择
- ♻️ 自动选择
- name: 🛑 全球拦截
type: select
proxies:
- REJECT
- DIRECT
- name: 🐟 漏网之鱼
type: select
proxies:
- 🚀 节点选择
- 🎯 全球直连
- ♻️ 自动选择
- 你的节点
```

每个参数的作用
| 参数名称 | 作用 | 备注 |
| ---------------- | --------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| name | 策略组的名字 | 用于区分策略组 |
| type | 策略组的类型<br>分为select、url-test、fallback、load-balance、relay。 | select： - 手动选择<br>- url-test：自动选择<br>- fallback：当前选择节点超时，则会按顺序切换到下一个可以节点<br>- load-balance：负载均衡<br>- relay：链式代理 |
| proxies | 引入代理节点或其他策略组 | 选择分流策略 |
| url | 健康检查测试地址 | 保持默认即可 |
| interval | 健康检查间隔，如不为 0 则启用定时测试，单位为秒 | 保持默认即可 |
| lazy | 懒惰状态，默认为 `true` ,未选择到当前策略组时，不进行测试 | 保持默认即可 |
| timeout | 健康检查超时时间，单位为毫秒 | 保持默认即可 |
| max-failed-times | 最大失败次数，超过则触发一次强制健康检查，默认 5 | 保持默认即可 |
| tolerance | 节点切换容差，单位 ms | 保持默认即可 |
以上就是针对策略组的简单介绍，高级玩家可自行定制属于自己的策略组，中初级玩家可直接套用大佬们的策略组方案。
## 2.4 分流规则

此项参数最终决定了哪个网站选用什么方式连接，通过不同的匹配策略自由地选择自己的分流规则。

我们直接来看官方文档给出的示例：

官方文档

```plaintext
rules:
- DOMAIN,ad.com,REJECT
- DOMAIN-SUFFIX,google.com,auto
- DOMAIN-KEYWORD,google,auto
- DOMAIN-REGEX,^abc.*com,PROXY
- GEOSITE,youtube,PROXY
- IP-CIDR,127.0.0.0/8,DIRECT,no-resolve
- IP-CIDR6,2620:0:2d0:200::7/32,auto
- IP-SUFFIX,8.8.8.8/24,PROXY
- IP-ASN,13335,DIRECT
- GEOIP,CN,DIRECT
- SRC-GEOIP,cn,DIRECT
- SRC-IP-ASN,9808,DIRECT
- SRC-IP-CIDR,192.168.1.201/32,DIRECT
- SRC-IP-SUFFIX,192.168.1.201/8,DIRECT
- DST-PORT,80,DIRECT
- SRC-PORT,7777,DIRECT
- IN-PORT,7890,PROXY
- IN-TYPE,SOCKS/HTTP,PROXY
- IN-USER,mihomo,PROXY
- IN-NAME,ss,PROXY
- PROCESS-PATH,/usr/bin/wget,PROXY
- PROCESS-PATH,C:\Program Files\Google\Chrome\Application\chrome.exe,PROXY
- PROCESS-PATH-REGEX,.*bin/wget,PROXY
- PROCESS-PATH-REGEX,(?i).*Application\\chrome.*,PROXY
- PROCESS-NAME,curl,PROXY
- PROCESS-NAME,chrome.exe,PROXY
- PROCESS-NAME,com.termux,PROXY
- PROCESS-NAME-REGEX,curl$,PROXY
- PROCESS-NAME-REGEX,(?i)Telegram,PROXY
- PROCESS-NAME-REGEX,.*telegram.*,PROXY
- UID,1001,DIRECT
- NETWORK,udp,DIRECT
- DSCP,4,DIRECT
- RULE-SET,providername,proxy
- AND,((DOMAIN,baidu.com),(NETWORK,UDP)),DIRECT
- OR,((NETWORK,UDP),(DOMAIN,baidu.com)),REJECT
- NOT,((DOMAIN,baidu.com)),PROXY
- SUB-RULE,(NETWORK,tcp),sub-rule
- MATCH,auto
```

以上规则匹配的优先级按照从上到下的顺序匹配，列表顶部的规则优先级高于其底下的规则。

每个参数的作用
| 匹配方式 | 匹配内容 | 举例 |
| ------------------ | --------------------------------------------------------------- | --------------------------------------------------------- |
| DOMAIN | 匹配完整域名 | [ad.com](http://ad.com/) |
| DOMAIN-SUFFIX | 匹配域名后缀 | [google.com](http://google.com/) |
| DOMAIN-KEYWORD | 使用域名关键字匹配 | google |
| DOMAIN-REGEX | 域名正则表达式匹配 | ^abc.\*com |
| GEOSITE | 匹配 Geosite 内的域名 | youtube |
| IP-CIDR/IP-CIDR6 | 匹配 IP 地址范围<br>`IP-CIDR` 和 `IP-CIDR6` 效果是一样的， `IP-CIDR6` 只是一个别名 | 127.0.0.0/8<br>2620:0:2d0:200::7/32 |
| IP-SUFFIX | 匹配 IP 后缀范围 | 8.8.8.8/24 |
| IP-ASN | 匹配 IP 所属 ASN | 13335 |
| GEOIP | 匹配 IP 所属国家代码 | CN |
| SRC-GEOIP | 匹配来源 IP 所属国家代码 | cn |
| SRC-IP-ASN | 匹配来源 IP 所属 ASN | 9808 |
| SRC-IP-CIDR | 匹配来源 IP 地址范围 | 192.168.1.201/32 |
| SRC-IP-SUFFIX | 匹配来源 IP 后缀范围 | 192.168.1.201/8 |
| DST-PORT | 匹配请求目标端口范围 | 80 |
| SRC-PORT | 匹配请求来源端口范围 | 7777 |
| IN-PORT | 匹配入站端口,可用端口范围 | 7890 |
| IN-TYPE | 匹配入站类型 | SOCKS/HTTP |
| IN-USER | 匹配入站用户名，支持使用 / 分隔多个用户名 | linuxdo |
| IN-NAME | 匹配入站名称 | ss |
| PROCESS-PATH | 使用完整进程路径匹配 | D:\chrome.exe |
| PROCESS-PATH-REGEX | 使用进程路径正则表达式匹配 | \*bin/wget |
| PROCESS-NAME | 使用进程匹配，在Android平台可以匹配包名 | chrome.exe |
| PROCESS-NAME-REGEX | 使用进程名称正则表达式匹配，在Android平台可以匹配包名 | curl$ |
| UID | 匹配 Linux USER ID | 1001 |
| NETWORK | 匹配tcp或者udp | udp |
| DSCP | 匹配DSCP标记 (仅限 tproxy udp 入站) | 4 |
| RULE-SET | 引用规则集合，需配置rule-providers | providername |
| AND/OR/NOT | 逻辑规则，需要注意括号的使用 | ((DOMAIN, [baidu.com ](http://baidu.com/)),(NETWORK,UDP)) |
| SUB-RULE | 匹配至子规则,需要注意括号的使用 | (NETWORK,tcp) |
| MATCH | 匹配所有请求，无需条件 | |
备注：【no-resolve】 用于跳过目标IP的DNS解析

可以看出，分流配置是先进行匹配，再选择分流的规则（直连、拒绝还是代理）。中初级用户可能看着规则很多，觉得有点头晕目眩，其实我们用到的类型很少，并且不少大佬都已经为我们做好了现成的规则集。比如ACL4SSR佬为我们整理的 [本地/局域网地址合集 ](https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/LocalAreaNetwork.list)。【附一个 [ACL4SSR大佬的规则集 ](https://github.com/ACL4SSR/ACL4SSR/tree/master/Clash)Github地址。】

那么我们该如何应用这些合集地址，生成我们自己想要的配置文件呢，别着急我们慢慢讲。
# 三、远程配置文件解析

要想把节点转换成Clash能用的配置文件，订阅转换网站可以大幅降低中初级玩家的工作量，其大致的逻辑就是让“ **节点**”以“ **远程配置文件**”的规则形成“ **clash配置文件**”。

 

在订阅转网网站的远程配置一栏，可以看到ACL4SSR佬很贴心地为我们给出了不同的配置文件供我们选择，我们还是抽取一个文件举例说明。

我们以最齐全的 [ACL4SSR\_Online\_Full.ini ](https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_Full.ini)为例，解析有哪些内容。

ACL4SSR\_Online\_Full.ini

```plaintext
[custom]
;不要随意改变关键字，否则会导致出错
;acl4SSR规则
;去广告：支持
;自动测速：支持
;微软分流：支持
;苹果分流：支持
;增强中国IP段：支持
;增强国外GFW：支持
;设置规则标志位
ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/LocalAreaNetwork.list
ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/UnBan.list
ruleset=🛑 广告拦截,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/BanAD.list
ruleset=🍃 应用净化,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/BanProgramAD.list
ruleset=📢 谷歌FCM,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/GoogleFCM.list
ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/GoogleCN.list
ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/SteamCN.list
ruleset=Ⓜ️ 微软Bing,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Bing.list
ruleset=Ⓜ️ 微软云盘,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/OneDrive.list
ruleset=Ⓜ️ 微软服务,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Microsoft.list
ruleset=🍎 苹果服务,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Apple.list
ruleset=📲 电报消息,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Telegram.list
ruleset=💬 OpenAi,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/OpenAi.list
ruleset=🎶 网易音乐,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/NetEaseMusic.list
ruleset=🎮 游戏平台,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/Epic.list
ruleset=🎮 游戏平台,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/Origin.list
ruleset=🎮 游戏平台,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/Sony.list
ruleset=🎮 游戏平台,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/Steam.list
ruleset=🎮 游戏平台,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/Nintendo.list
ruleset=📹 油管视频,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/YouTube.list
ruleset=🎥 奈飞视频,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/Netflix.list
ruleset=📺 巴哈姆特,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/Bahamut.list
ruleset=📺 哔哩哔哩,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/BilibiliHMT.list
ruleset=📺 哔哩哔哩,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Ruleset/Bilibili.list
ruleset=🌏 国内媒体,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/ChinaMedia.list
ruleset=🌍 国外媒体,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/ProxyMedia.list
ruleset=🚀 节点选择,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/ProxyGFWlist.list
;ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/ChinaIp.list
ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/ChinaDomain.list
ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/ChinaCompanyIp.list
ruleset=🎯 全球直连,https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/Download.list
;ruleset=🎯 全球直连,[]GEOIP,LAN
ruleset=🎯 全球直连,[]GEOIP,CN
ruleset=🐟 漏网之鱼,[]FINAL
;设置规则标志位
;设置分组标志位
custom_proxy_group=🚀 节点选择`select`[]♻️ 自动选择`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇸🇬 狮城节点`[]🇯🇵 日本节点`[]🇺🇲 美国节点`[]🇰🇷 韩国节点`[]🚀 手动切换`[]DIRECT
custom_proxy_group=🚀 手动切换`select`.*
custom_proxy_group=♻️ 自动选择`url-test`.*`http://www.gstatic.com/generate_204`300,,50
custom_proxy_group=📲 电报消息`select`[]🚀 节点选择`[]♻️ 自动选择`[]🇸🇬 狮城节点`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇯🇵 日本节点`[]🇺🇲 美国节点`[]🇰🇷 韩国节点`[]🚀 手动切换`[]DIRECT
custom_proxy_group=💬 OpenAi`select`[]🚀 节点选择`[]♻️ 自动选择`[]🇸🇬 狮城节点`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇯🇵 日本节点`[]🇺🇲 美国节点`[]🇰🇷 韩国节点`[]🚀 手动切换`[]DIRECT
custom_proxy_group=📹 油管视频`select`[]🚀 节点选择`[]♻️ 自动选择`[]🇸🇬 狮城节点`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇯🇵 日本节点`[]🇺🇲 美国节点`[]🇰🇷 韩国节点`[]🚀 手动切换`[]DIRECT
custom_proxy_group=🎥 奈飞视频`select`[]🎥 奈飞节点`[]🚀 节点选择`[]♻️ 自动选择`[]🇸🇬 狮城节点`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇯🇵 日本节点`[]🇺🇲 美国节点`[]🇰🇷 韩国节点`[]🚀 手动切换`[]DIRECT
custom_proxy_group=📺 巴哈姆特`select`[]🇨🇳 台湾节点`[]🚀 节点选择`[]🚀 手动切换`[]DIRECT
custom_proxy_group=📺 哔哩哔哩`select`[]🎯 全球直连`[]🇨🇳 台湾节点`[]🇭🇰 香港节点
custom_proxy_group=🌍 国外媒体`select`[]🚀 节点选择`[]♻️ 自动选择`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇸🇬 狮城节点`[]🇯🇵 日本节点`[]🇺🇲 美国节点`[]🇰🇷 韩国节点`[]🚀 手动切换`[]DIRECT
custom_proxy_group=🌏 国内媒体`select`[]DIRECT`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇸🇬 狮城节点`[]🇯🇵 日本节点`[]🚀 手动切换
custom_proxy_group=📢 谷歌FCM`select`[]DIRECT`[]🚀 节点选择`[]🇺🇲 美国节点`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇸🇬 狮城节点`[]🇯🇵 日本节点`[]🇰🇷 韩国节点`[]🚀 手动切换
custom_proxy_group=Ⓜ️ 微软Bing`select`[]DIRECT`[]🚀 节点选择`[]🇺🇲 美国节点`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇸🇬 狮城节点`[]🇯🇵 日本节点`[]🇰🇷 韩国节点`[]🚀 手动切换
custom_proxy_group=Ⓜ️ 微软云盘`select`[]DIRECT`[]🚀 节点选择`[]🇺🇲 美国节点`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇸🇬 狮城节点`[]🇯🇵 日本节点`[]🇰🇷 韩国节点`[]🚀 手动切换
custom_proxy_group=Ⓜ️ 微软服务`select`[]DIRECT`[]🚀 节点选择`[]🇺🇲 美国节点`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇸🇬 狮城节点`[]🇯🇵 日本节点`[]🇰🇷 韩国节点`[]🚀 手动切换
custom_proxy_group=🍎 苹果服务`select`[]DIRECT`[]🚀 节点选择`[]🇺🇲 美国节点`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇸🇬 狮城节点`[]🇯🇵 日本节点`[]🇰🇷 韩国节点`[]🚀 手动切换
custom_proxy_group=🎮 游戏平台`select`[]DIRECT`[]🚀 节点选择`[]🇺🇲 美国节点`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇸🇬 狮城节点`[]🇯🇵 日本节点`[]🇰🇷 韩国节点`[]🚀 手动切换
custom_proxy_group=🎶 网易音乐`select`[]DIRECT`[]🚀 节点选择`[]♻️ 自动选择`(网易|音乐|解锁|Music|NetEase)
custom_proxy_group=🎯 全球直连`select`[]DIRECT`[]🚀 节点选择`[]♻️ 自动选择
custom_proxy_group=🛑 广告拦截`select`[]REJECT`[]DIRECT
custom_proxy_group=🍃 应用净化`select`[]REJECT`[]DIRECT
custom_proxy_group=🐟 漏网之鱼`select`[]🚀 节点选择`[]♻️ 自动选择`[]DIRECT`[]🇭🇰 香港节点`[]🇨🇳 台湾节点`[]🇸🇬 狮城节点`[]🇯🇵 日本节点`[]🇺🇲 美国节点`[]🇰🇷 韩国节点`[]🚀 手动切换
custom_proxy_group=🇭🇰 香港节点`url-test`(港|HK|hk|Hong Kong|HongKong|hongkong)`http://www.gstatic.com/generate_204`300,,50
custom_proxy_group=🇯🇵 日本节点`url-test`(日本|川日|东京|大阪|泉日|埼玉|沪日|深日|[^-]日|JP|Japan)`http://www.gstatic.com/generate_204`300,,50
custom_proxy_group=🇺🇲 美国节点`url-test`(美|波特兰|达拉斯|俄勒冈|凤凰城|费利蒙|硅谷|拉斯维加斯|洛杉矶|圣何塞|圣克拉拉|西雅图|芝加哥|US|United States)`http://www.gstatic.com/generate_204`300,,150
custom_proxy_group=🇨🇳 台湾节点`url-test`(台|新北|彰化|TW|Taiwan)`http://www.gstatic.com/generate_204`300,,50
custom_proxy_group=🇸🇬 狮城节点`url-test`(新加坡|坡|狮城|SG|Singapore)`http://www.gstatic.com/generate_204`300,,50
custom_proxy_group=🇰🇷 韩国节点`url-test`(KR|Korea|KOR|首尔|韩|韓)`http://www.gstatic.com/generate_204`300,,50
custom_proxy_group=🎥 奈飞节点`select`(NF|奈飞|解锁|Netflix|NETFLIX|Media)
;设置分组标志位
enable_rule_generator=true
overwrite_original_rules=true
clash_rule_base=https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/GeneralClashConfig.yml
;luck
```

每个参数的作用
| 参数名称 | 参数内容 | 备注 |
| -------------------------- | --------- | ------------------------ |
| ruleset | 规则集 | 设置对应的策略组里应该如何分流 |
| custom\_proxy\_group | 策略组 | 为不同的场景设置分组 |
| enable\_rule\_generator | 启用规则生成器 | 默认开启就行 |
| overwrite\_original\_rules | 覆盖原有规则 | 默认开启就行 |
| clash\_rule\_base | clash基础配置 | clash文件的配置，也就是我们上一章节讲的内容 |
ruleset我们按需选择自己需要的规则集，custom\_proxy\_group也是按需设置我们需要的策略组即可。

clash\_rule\_base的链接我们需要填写我们自己的clash配置文件地址。

远程配置文件相比Clash配置文件是不是要简单多啦，下面我们开始实战演练。
# 四、实战演练
## 4.1 上传配置
### 4.1.1 将clash基础配置上传到github

此前我们以及完成了clash配置文件的设置，这里贴一个完整版：

base.yml

```plaintext
mixed-port: 7890
allow-lan: true
bind-address: "*"
ipv6: false
mode: rule
log-level: info
external-controller: 127.0.0.1:9090
dns:
enable: true
prefer-h3: true
use-hosts: true
use-system-hosts: true
respect-rules: false
listen: 0.0.0.0:1053
ipv6: false
enhanced-mode: fake-ip
fake-ip-range: 198.18.0.1/16
fake-ip-filter:
- '*.lan'
- "+.local"
- localhost.ptlogin2.qq.com
default-nameserver:
- tls://1.12.12.12
- 223.5.5.5
- 119.29.29.29
nameserver-policy:
'www.baidu.com': '114.114.114.114'
'+.internal.crop.com': '10.0.0.1'
'geosite:cn,private':
- https://223.5.5.5/dns-query
- https://223.6.6.6/dns-query
nameserver:
- https://dns.alidns.com/dns-query
- https://doh.pub/dns-query
proxy-server-nameserver:
- https://dns.alidns.com/dns-query
- https://doh.pub/dns-query
fallback:
- tls://1dot1dot1dot1.cloudflare-dns.com
- tcp://1.1.1.1
- https://1.0.0.1/dns-query
- https://1.1.1.1/dns-query
fallback-filter:
geoip: true
geoip-code: CN
geosite:
- gfw
ipcidr:
- 240.0.0.0/4
- 0.0.0.0/32
- 127.0.0.1/32
domain:
- '+.google.com'
- '+.facebook.com'
- '+.youtube.com'
```

将其上传至github，存为base.yml
### 4.2.2 将远程配置上传到github

下面贴一个简单的远程配置文件作为示例：

远程配置.ini

```plaintext
[custom]
;不要随意改变关键字，否则会导致出错
;acl4SSR规则
;去广告：支持
;自动测速：支持
;微软分流：不支持
;苹果分流：不支持
;增强中国IP段：不支持
;增强国外GFW：不支持
ruleset=🎯 全球直连,rules/ACL4SSR/Clash/LocalAreaNetwork.list
ruleset=🛑 全球拦截,rules/ACL4SSR/Clash/BanAD.list
ruleset=🛑 全球拦截,rules/ACL4SSR/Clash/BanProgramAD.list
ruleset=🎯 全球直连,rules/ACL4SSR/Clash/GoogleCN.list
ruleset=🎯 全球直连,rules/ACL4SSR/Clash/Ruleset/SteamCN.list
ruleset=🚀 节点选择,rules/ACL4SSR/Clash/Telegram.list
ruleset=🚀 节点选择,rules/ACL4SSR/Clash/ProxyMedia.list
ruleset=🚀 节点选择,rules/ACL4SSR/Clash/ProxyLite.list
ruleset=🎯 全球直连,rules/ACL4SSR/Clash/ChinaDomain.list
ruleset=🎯 全球直连,rules/ACL4SSR/Clash/ChinaCompanyIp.list
;ruleset=🎯 全球直连,[]GEOIP,LAN
ruleset=🎯 全球直连,[]GEOIP,CN
ruleset=🐟 漏网之鱼,[]FINAL
custom_proxy_group=🚀 节点选择`select`[]♻️ 自动选择`[]DIRECT`.*
custom_proxy_group=♻️ 自动选择`url-test`.*`http://www.gstatic.com/generate_204`300,,50
custom_proxy_group=🎯 全球直连`select`[]DIRECT`[]🚀 节点选择`[]♻️ 自动选择
custom_proxy_group=🛑 全球拦截`select`[]REJECT`[]DIRECT
custom_proxy_group=🐟 漏网之鱼`select`[]🚀 节点选择`[]🎯 全球直连`[]♻️ 自动选择`.*
enable_rule_generator=true
overwrite_original_rules=true
clash_rule_base=你的base.yml的github地址
```

同样将其上传至github，存为你的远程配置名称.ini
### 4.3.3 使用你自己的远程配置

进入订阅转换网站，以我自己的为例。

网址： [https://sub.yuju.love](https://sub.yuju.love/)

 

填写你的远程配置名称.ini的github地址，如： <https://raw.githubusercontent.com/ACL4SSR/ACL4SSR/master/Clash/config/ACL4SSR_Online_Full.ini>

点击 **转换**。

复制到浏览器窗口检查。

 

**大功告成！完结撒花！**

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

- [YouTube视频原地址](https://www.youtube.com/watch?v=OT_tlDDMNB4)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/clash-config-detail-dns/)
