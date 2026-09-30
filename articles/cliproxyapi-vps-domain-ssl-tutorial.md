# CLIProxyAPI 部署教程：VPS、域名、SSL 与远程调用完整配置

这篇教程围绕 CLIProxyAPI 的完整部署流程展开，涵盖 VPS 准备、IP 检测、一键部署、Systemd 守护进程、防火墙配置、域名解析、Nginx 反向代理、SSL 证书申请与自动续期的完整流程。

> 完整图文与持续更新版本：[CLIProxyAPI 部署教程：VPS、域名、SSL 与远程调用完整配置](https://869hr.uk/2026/tutorial/cliproxyapi-vps-domain-ssl-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tutorial/cliproxyapi-vps-domain-ssl-tutorial/
- 更新：2026-05-04
- 分类：教程
- 专题：教程、AI
- 关键词：开发工具、VPS、Cloudflare、OpenClaw、SSL证书
- 视频：https://www.youtube.com/watch?v=3KhDHeQ7MJs

## 正文

<!-- 文章摘要 -->
> 
想要畅快使用 OpenClaw 却苦于没有 Token？买 API 太贵，免费的又极度不稳定？本教程将手把手带你利用免费 VPS 服务器，从零开始部署 CLIProxyAPI，并通过 Cloudflare 配置域名解析与 SSL 证书，实现完美反代，从此获得永久免费的 Token！

## 视频教程

<div class="video-container">
[在 YouTube 观看视频](https://www.youtube.com/watch?v=3KhDHeQ7MJs)
</div>

本视频由 **短裤AI分享** 制作，时长约 **41 分 47 秒**。

### 视频核心内容速览

- ✅ 00:00 效果展示：为什么要部署 CLIProxyAPI？如何白嫖 OpenClaw？
- ✅ 01:30 第一步：SSH 连接服务器与 IP 解锁能力检测（附一键脚本）
- ✅ 03:15 第二步：一键脚本高速部署 CLIProxyAPI 及核心配置文件修改（划重点！）
- ✅ 05:40 第三步：配置 Systemd 守护进程与开机自启
- ✅ 07:10 第四步：防火墙设置（iptables/nft/ufw）与 8317 端口放行防坑指南
- ✅ 10:05 第五步：Cloudflare API Token 申请与 Certbot 自动签发 SSL 证书
- ✅ 13:20 第六步：Nginx 安装与反向代理配置（监听 443 转发 8317，支持 WebSocket）
- ✅ 16:45 最终测试：用自定义域名和免费 Token 成功运行 OpenClaw！

---

## 前置准备

默认已放开 22 端口，此时可以尝试用你的认证方式进行 SSH 连接。

## 第一步：检测 IP 解锁情况

首先使用下面的脚本测试 ChatGPT 等平台的解锁情况：

项目地址：[IPQuality - GitHub](https://github.com/xykt/IPQuality)

**一键检测命令：**

```bash
sudo -i
bash <(curl -Ls https://IP.Check.Place) -f
```

如果 ChatGPT 显示解锁，即可继续操作，否则需要更换服务器或配置代理。

检测结果示例：

![IP检测结果](https://img.869hr.uk/cliproxyapi/ip-check-result.png)

---

## 第二步：部署 CLIProxyAPI

根据 [CLIProxyAPI 官方文档](https://help.router-for.me/cn/) 在服务器上部署。

### 使用一键安装脚本

```bash
curl -fsSL https://raw.githubusercontent.com/brokechubb/cliproxyapi-installer/refs/heads/master/cliproxyapi-installer | bash
```

### 修改配置文件

服务器默认使用项目根目录的 YAML 配置文件（`config.yaml`）。可通过 `--config` 指定其他路径：

```bash
./cli-proxy-api --config /path/to/your/config.yaml
```

**重要配置项：**

我们需要修改配置文件的 `remote-management.allow-remote` 来允许远程访问（如果在自己电脑上部署则不需要）。同时，设置管理密钥（写明文即可，会自动转换成哈希）。

```yaml
# 服务器绑定主机/接口，默认空字符串同时绑定 IPv4/IPv6。
# 使用 “127.0.0.1” 或 “localhost” 可限制仅本机访问。
host: “”

# 服务器端口
port: 8317

# TLS 设置：启用后使用提供的证书与私钥监听 HTTPS。
tls:
  enable: false
  cert: “”
  key: “”

# 管理 API 设置
remote-management:
  # 是否允许远程（非 localhost）访问管理接口。
  # 为 false 时仅允许 localhost，仍需管理密钥。
  allow-remote: true
 
  # 管理密钥。若填写明文，启动时会自动哈希后生效。
  # 所有管理请求（包括本地）都需要该密钥。
  # 留空则完全禁用管理 API（所有 /v0/management 路由返回 404）。
  secret-key: “123456”
```

---

## 第三步：配置 Systemd 守护进程

### 安装 service 文件到 systemd

```bash
cd ~/cliproxyapi
sudo cp -f cliproxyapi.service /etc/systemd/system/cliproxyapi.service
sudo systemctl daemon-reload
```

### 检查服务状态

```bash
systemctl status cliproxyapi.service --no-pager
```

### 启动并设置开机自启

```bash
sudo systemctl enable --now cliproxyapi.service
systemctl status cliproxyapi.service --no-pager
```

### 查看日志

```bash
sudo journalctl -u cliproxyapi.service -e --no-pager
```

---

## 第四步：防火墙配置与端口放行

在 GCP 面板或服务器上放行端口。使用 `iptables` 命令操作。

### 放行 8317 端口

```bash
sudo iptables -A INPUT -p tcp --dport 8317 -j ACCEPT
```

### 查看 iptables 规则

```bash
sudo iptables -L -n -v
```

### 删除指定规则

```bash
sudo iptables -D INPUT <line-number>
```

### 查看端口监听状态

```bash
ss -lntp
```

参数含义：
- `l`：只看监听
- `n`：数字显示端口
- `t`：TCP
- `p`：显示进程

配合 `grep` 筛选端口：

```bash
ss -lntp | grep 8317
```

### nft/ufw 防火墙处理

如果还是不能访问，需要检查 nft/ufw 问题。

**查看规则集：**

```bash
sudo nft list ruleset
```

INPUT 链顺序是按规则写入顺序匹配的。如果有下面这样的规则：

```lua
counter packets 525 bytes 31692 reject with icmp type host-prohibited
```

它的含义是：**无条件拒绝所有走到这里的输入流量**，等价于逻辑伪代码：

```lua
if (前面的规则都没匹配) {
    REJECT 所有包
}
```

如果我们的放行规则在这样的规则后面，就不会生效。我们可以删掉旧 reject：

```bash
sudo nft delete rule ip filter INPUT handle 9
```

然后在最后插入一条新的 reject：

```bash
sudo nft add rule ip filter INPUT reject with icmp type host-prohibited
```

这样顺序就正确了。

---

## 第五步：域名访问配置

使用 Cloudflare 托管服务，配合 Let's Encrypt 实现 SSL 证书自动续期。假设你的域名为 `bbb.aaa.com`。

### 0）安装 Nginx

```bash
sudo apt update
sudo apt install -y nginx
```

启动并设为开机自启：

```bash
sudo systemctl enable --now nginx
```

检查状态：

```bash
systemctl status nginx
```

### 1）Cloudflare 侧准备：创建 API Token

进入 Cloudflare → **My Profile → API Tokens → Create Token**

选模板：**Edit zone DNS**（或自定义）

**权限最小化建议：**
- Permissions: `Zone / DNS / Edit`
- Zone Resources: 仅选择 `aaa.com` 这个 zone

创建后复制 Token（只会显示一次）

### 2）服务器安装 certbot + cloudflare 插件

```bash
sudo apt update
sudo apt install -y certbot python3-certbot-dns-cloudflare
```

### 3）保存 Cloudflare Token

```bash
sudo mkdir -p /root/.secrets/certbot
sudo nano /root/.secrets/certbot/cloudflare.ini
```

写入（把 TOKEN 换成你的）：

```ini
dns_cloudflare_api_token = YOUR_CLOUDFLARE_API_TOKEN
```

权限必须收紧（不然 certbot 拒绝用）：

```bash
sudo chmod 600 /root/.secrets/certbot/cloudflare.ini
```

### 4）签发证书（DNS 验证）

```bash
sudo certbot certonly \
  --dns-cloudflare \
  --dns-cloudflare-credentials /root/.secrets/certbot/cloudflare.ini \
  -d bbb.aaa.com \
  --preferred-challenges dns-01
```

成功后证书会在：
- `/etc/letsencrypt/live/bbb.aaa.com/fullchain.pem`
- `/etc/letsencrypt/live/bbb.aaa.com/privkey.pem`

### 5）Nginx 配置反向代理

```bash
sudo nano /etc/nginx/sites-available/cliproxyapi
```

粘贴配置（替换域名为你的）：

```nginx
server {
    listen 443 ssl http2;
    server_name bbb.aaa.com;

    ssl_certificate     /etc/letsencrypt/live/bbb.aaa.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/bbb.aaa.com/privkey.pem;

    ssl_protocols TLSv1.2 TLSv1.3;

    location / {
        proxy_pass http://127.0.0.1:8317; 

        proxy_http_version 1.1;
        proxy_set_header Host $host;

        # WebSocket 支持
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection “upgrade”;
                                
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

        proxy_read_timeout 300s;
    }
}
```

启用并重载：

```bash
sudo ln -s /etc/nginx/sites-available/cliproxyapi /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

### 6）自动续期配置

**检查系统定时任务：**

```bash
systemctl list-timers | grep certbot || true
```

Ubuntu 通常自带 `certbot.timer`。

**续期后自动 reload nginx（添加 deploy hook）：**

创建 hook：

```bash
sudo vi /etc/letsencrypt/renewal-hooks/deploy/reload-nginx.sh
```

写入：

```bash
#!/bin/sh
systemctl reload nginx
```

赋权：

```bash
sudo chmod +x /etc/letsencrypt/renewal-hooks/deploy/reload-nginx.sh
```

测试续期：

```bash
sudo certbot renew --dry-run
```

看到成功即可。

**Cloudflare 设置：**

在 Cloudflare 中选择 **Full (strict) 模式**，开启 **Always Use HTTPS**（即使源站没开 80 也没关系，CF 边缘重定向）。

在服务器安全组/iptables 需要放行：**443/tcp**。

### 7）为 CLIProxyAPI 启用 TLS

可以在 WebUI 中配置，或在配置文件中直接修改：

**证书文件路径：** `/etc/letsencrypt/live/bbb.aaa.com/fullchain.pem`

**私钥文件路径：** `/etc/letsencrypt/live/bbb.aaa.com/privkey.pem`

修改 `config.yaml`：

```yaml
# 服务器绑定主机/接口
host: “”

# 服务器端口
port: 8317

# TLS 设置
tls:
  enable: true
  cert: “/etc/letsencrypt/live/bbb.aaa.com/fullchain.pem”
  key: “/etc/letsencrypt/live/bbb.aaa.com/privkey.pem”

# 管理 API 设置
remote-management:
  allow-remote: true
  secret-key: “123456”
```

---

## 最终效果

配置完成后，你可以使用自定义域名访问 CLIProxyAPI，并通过注册机搞定 100 个 Codex 账号，实现 OpenClaw 自由！

![最终效果](https://img.869hr.uk/cliproxyapi/final-result.jpg)

---

## 小白避坑指南

1. **修改 config.yaml 时**，千万记得把 `allow-remote` 改为 `true`，并设置一个你记得住的 `secret-key`
2. **配置防火墙放行端口时**，注意排查有没有冲突的 reject 规则
3. **Cloudflare SSL/TLS 加密模式**记得一定要设置为 **Full (strict) 严格模式**

---

## 相关资源

### GCP 免费服务器教程

- [【第一期】GCP永久免费+每月领$10防坑教程](https://youtu.be/mb77KAfXOVg?si=iNJI_dexpyX2MbUL)
- [【第二期】GCP永久免费及节点搭建](https://youtu.be/Tml8qPNAELI)
- [【第三期】GCP永久免费及节点搭建](https://youtu.be/88gyLp02bbI?si=87cSUk2k796Ux1t3)

### 社群与资源

- 💬 Telegram 讨论群：[t.me/tgmShareAI](https://t.me/tgmShareAI)
- 💬 Twitter：[x.com/gxjdian](https://x.com/gxjdian)
- 💬 微信讨论群：[qr.869hr.uk/aitech](https://qr.869hr.uk/aitech)
- 🔗 超过100T免费资源下载站：[doc.869hr.uk](https://doc.869hr.uk)
- 🔗 博客（银行卡、手机号、VPS主机、IP测试等）：[869hr.uk](https://869hr.uk)

### eSIM 服务推荐

1. 三家eSIM对比及开户链接：[s.869hr.uk/mcc](https://s.869hr.uk/mcc)
2. 9eSIM 打9折（优惠码：maq）：[www.9esim.com](https://www.9esim.com/?coupon=maq)
3. ESTK 打9折（优惠码：GXJDIAN）：[store.estk.me](https://store.estk.me/zh?aid=16007)
4. XeSIM 打8折（推荐码：gxjdian）：[xesim.cc](https://xesim.cc/?DIST=RE5FHg==)

### 虚拟银行卡

- Wise 申请（推荐码：lizhiw12）：[wise.com/invite/ihpc/lizhiw12](https://wise.com/invite/ihpc/lizhiw12)
- N26 申请（推荐码：lizhiw02766c）：[教程视频](https://youtu.be/HY9OD8rX89s?si=78REb8MyKSJB6cwQ)

---

## 参考链接

- [CLIProxyAPI 官方文档](https://help.router-for.me/cn/)
- [IPQuality - GitHub](https://github.com/xykt/IPQuality)
- [Cloudflare 官网](https://www.cloudflare.com/)
- [YouTube 原视频](https://www.youtube.com/watch?v=3KhDHeQ7MJs)

---

⚠️ **免责声明**：本教程仅供网络优化与技术交流学习，请大家合理、合法使用相关网络技术。

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tutorial/cliproxyapi-vps-domain-ssl-tutorial/)
