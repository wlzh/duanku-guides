# 小白手把手自建纯净家宽节点+中转站全流程：DMIT配合VIRCS部署CPA，彻底解决AI风控！

基于"第一性原理"构建的自建纯净家宽节点与中转站完整流水线教程 由于当前各大 AI 模型（如 Claude、ChatGPT 等）风控日益严格，普通机场 IP 经常面临降智、封号或频繁弹验证码的问题

> 完整图文与持续更新版本：[小白手把手自建纯净家宽节点+中转站全流程：DMIT配合VIRCS部署CPA，彻底解决AI风控！](https://869hr.uk/2026/tech/dmitvircsdeploycpa-ai/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/dmitvircsdeploycpa-ai/
- 更新：2026-05-05
- 分类：技术
- 关键词：教程
- 视频：https://www.youtube.com/watch?v=Nigo_YH4SGE

## 正文

<!-- 文章摘要 -->
> 
基于"第一性原理"构建的自建纯净家宽节点与中转站完整流水线教程 (@gxjdian)...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=Nigo_YH4SGE)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 10 分钟。

基于"第一性原理"构建的自建纯净家宽节点与中转站完整流水线教程。由于当前各大 AI 模型（如 Claude、ChatGPT 等）风控日益严格，普通机场 IP 经常面临降智、封号或频繁弹验证码的问题。本期视频将带你从0到1搭建一套"毕业级"的跨国网络架构：利用优质线路机进行低延迟中转，配合纯净的住宅家宽 IP 作为落地出口，兼顾极速网络与绝对的安全性。

## 视频流水线大纲

⚙️ **架构原理解析**：为什么我们需要"线路机 (DMIT) + 落地机 (VIRCS)"的组合？

**VPS 基础加固**：修改 SSH 端口、配置 UFW 防火墙、禁用 Root 登录，保障服务器安全。

**线路机配置 (入口)**：安装 3x-ui 面板、配置 VLESS-Reality 协议、SSL 证书申请。

**落地机配置 (出口)**：IP 纯净度检测、使用 sing-box 部署更轻量的 Shadowsocks 协议。

**中转路由打通**：在 3x-ui 中配置出站规则，实现线路机流量无缝转发至家宽落地机。

**客户端无缝集成**：Clash Verge 节点转换技巧，以及如何利用扩展脚本将自建节点丝滑混入现有机场订阅组。

**CPA 进阶部署 (附加)**：零基础 Docker 部署 CLI Proxy API (CPA) 配合 Nginx 反代，实现 AI 接口的高效管理与调用。

## 线路机（DMIT）配置

### 一、登录VPS

#### 1. 连接VPS

工具推荐 FinalShell，新建连接：输入VPS的IP，端口22，使用公钥方式登录，用户名root，选择DMIT提供的私钥。

#### 2. 更新系统

```bash
apt update -y && apt upgrade -y && apt install sudo curl -y
```

### 二、VPS加固

#### 1. 创建普通用户并授权

```bash
# 创建用户
useradd -m -s /bin/bash wahaha

# 设置密码
passwd wahaha

# 复制 root 的 ssh 密钥以允许新用户登录
cp -r /root/.ssh /home/wahaha/
chown -R wahaha:wahaha /home/wahaha/.ssh

# 允许 wahaha 用户免密执行 sudo
echo 'wahaha ALL=(ALL) NOPASSWD: ALL' | tee /etc/sudoers.d/wahaha-nopasswd
chmod 0440 /etc/sudoers.d/wahaha-nopasswd
```

新开本地终端测试：

```bash
ssh wahaha@你的服务器IP
sudo whoami # 输出 root，无需输入密码
```

#### 2. 修改SSH端口号并配置 UFW 防火墙

```bash
# 修改 SSH 端口（此处以 8866 为例）
sudo sed -i 's/^#Port 22/Port 8866/' /etc/ssh/sshd_config
sudo sed -i 's/^Port 22/Port 8866/' /etc/ssh/sshd_config

# 验证配置语法是否正确
sudo sshd -t

# 安装并重置 UFW 防火墙
sudo apt update && sudo apt install -y ufw
sudo ufw reset # 输入 y 确认

# 设置默认进出站规则
sudo ufw default deny incoming
sudo ufw default allow outgoing

# 放行新的 SSH 端口
sudo ufw allow 8866/tcp
# 放行 80 与 443 端口
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

# 重启 SSH 服务
sudo systemctl restart ssh

# 启用防火墙
sudo ufw enable # 输入 y 确认

# 检查状态
sudo ufw status
```

**注意**：此时不要关闭当前的终端窗口！新开一个本地终端测试连接：

```bash
ssh wahaha@你的服务器IP -p 8866
```

验证连接成功后，再继续后续步骤。

#### 3. 禁用 Root 登录

确认新用户和新端口登录成功后，彻底关闭 Root 远程权限：

```bash
# 修改 SSH 配置，禁止 root 登录
sudo sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin no/' /etc/ssh/sshd_config

# 禁止密码登录
sudo sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication no/' /etc/ssh/sshd_config

# 检查配置语法并重启 SSH 服务
sudo sshd -t
sudo systemctl restart ssh
```

### 三、网络测试

```bash
# 切换到 root 环境
sudo -i
# 运行融合怪脚本
bash <(curl -sL https://run.NodeQuality.com)
```

脚本跑完大概10几分钟，可以看到IP质量、网络质量等信息，该说不说大妈的三网优化真的不错。

**IP质量检测工具：**

- https://ping0.cc/ - 看ASN+原生/广播IP，纯净度纯娱乐
- https://ippure.com/ - 看IP纯净度
- https://ipdata.co/ - 看滥用标记
- https://scamalytics.com/ - 看欺诈得分
- https://radar.cloudflare.com/ - 跳盾检测，看机器人与人类流量占比
- https://chatgpt.com/ - 是否无人机验证、无需登录即可对话
- https://claude.ai/login - 是否跳验证码
- https://ip.net.coffee/dns/ - DNS泄漏测试
- https://ip.net.coffee/claude/ - Claude风险监测

### 四、安装 3x-ui 面板

```bash
# 安装/更新 3x-ui
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```

一路回车，安装完成后会输出以下信息，保存下来。

输入 `x-ui` 回车，开启BBR加速：输入 24，回车，1，回车。

使用 `ufw allow 面板端口/tcp` 放行面板的端口。

### 五、配置 3x-ui 面板

访问 Access URL，输入用户名和密码登录。

入站列表：添加入站
- 协议：vless
- 传输：TCP
- 安全：Reality
- Target：samsung.com:443
- SNI：samsung.com,www.samsung.com
- Get New Cert
- 创建

到这里一个订阅节点就创建完成了。

### 六、Cloudflare添加DNS

进入Cloudflare，点击域名，DNS-添加记录，填写名称、VPS的IP地址、关闭代理状态，保存，等待5分钟解析生效。

### 七、SSL 证书申请与自动续期

使用 acme.sh 申请证书，并将其安装到 x-ui 指定目录。

```bash
# 申请 ECC 证书
~/.acme.sh/acme.sh --issue -d 名称.域名 --standalone -k ec-256

# 创建证书存放目录
mkdir -p /etc/x-ui/ssl

# 安装证书并配置重载命令
~/.acme.sh/acme.sh --install-cert -d 名称.域名 --ecc \
--key-file /etc/x-ui/ssl/privkey.key \
--fullchain-file /etc/x-ui/ssl/fullchain.pem \
--reloadcmd "systemctl restart x-ui"
```

面板设置-证书，修改公钥文件路径和密钥文件路径，保存并重启。

## 落地机（VIRCS）配置

### 一、配置IP白名单

将线路机的IP加入到白名单，保证只有线路机IP才能登录。

### 二、登录VPS

同线路机

### 三、VPS加固

同线路机

### 四、网络测试

VIRCS家的家宽IP质量毋庸置疑，贵有贵的道理。

### 五、sing-box脚本一键生成订阅

```bash
# 切换到 root 用户
sudo -i
# 运行安装脚本
bash <(wget -qO- -o- https://github.com/233boy/sing-box/raw/main/install.sh)
```

默认生成的是 VLESS-REALITY 协议，但落地机作为出口节点，主要追求速度和稳定性，所以改为 Shadowsocks。

输入 `sb`，出现 sing-box 面板，输入 2 回车，1 回车，1 回车，8 回车，回车，输入密码，回车。

```bash
# 放行端口 7599
sudo ufw allow 7599/tcp
```

### 六、在线路机的3x-ui面板配置中转

Xray设置 → 出站规则 → 添加出站 → JSON → 粘贴落地机的ss链接 → 添加出站

点击测试按钮

路由规则 → 添加规则
- Inbound Tags：选入站节点名称
- Outbound Tag：选出站节点名称

保存-重新启动Xray（别忘了）

## 使用节点

工具推荐 Clash Verge

### 1. 节点转换

推荐猫佬的 https://linuxdo.icmpmiao.cc/

将转换后的链接导入到订阅中，选择对应的节点，进入 https://ping0.cc/ 测试。

### 2. 将家宽节点加入到机场中（可选）

通过全局扩展脚本，将自建节点加入到现有机场的节点组中，这样就可以灵活切换机场/自建节点。

可以将风控较高的网站单独做一个策略组，将家宽节点配置到这个策略组中，实现访问其他网站走机场节点，访问高风控网站走家宽节点。

## 安装CPA

线路机部署Nginx，落地机部署CPA，线路机作为入口，反向代理到落地机。

### 一、落地机

#### 1. 安装docker

```bash
# 卸载系统原有冲突 Docker 相关包
sudo apt remove $(dpkg --get-selections docker.io docker-compose docker-doc podman-docker containerd runc | cut -f1)

# 官方一键脚本安装 Docker
curl -fsSL https://get.docker.com | sh

# 把当前用户加入 docker 用户组
sudo usermod -aG docker $USER

# 立即生效
newgrp docker

# 测试
docker run hello-world
```

#### 2. 部署CPA

```bash
mkdir -p ~/cpa && cd ~/cpa
cat <<EOF > config.yaml
host: "0.0.0.1"
port: 8317
auth-dir: "~/.cli-proxy-api"
request-retry: 3
quota-exceeded:
  switch-project: true
  switch-preview-model: true
api-keys:
  - "sk-cpa-$(tr -dc 'a-z0-9' </dev/urandom | head -c 32)"
remote-management:
  allow-remote: true
  secret-key: "mgt-cpa-$(tr -dc 'a-z0-9' </dev/urandom | head -c 32)"
  disable-control-panel: false
logging-to-file: true
usage-statistics-enabled: true
logs-max-total-size-mb: 100
EOF

echo "*** 请记录你的明文密钥 ***"
grep -E '(sk-cpa-|mgt-cpa-)' config.yaml
```

创建 docker-compose.yml 并启动：

```bash
cat <<'EOF' > docker-compose.yml
services:
  cli-proxy-api:
    image: eceasy/cli-proxy-api:latest
    pull_policy: always
    container_name: cli-proxy-api
    network_mode: host
    volumes:
      - ./config.yaml:/CLIProxyAPI/config.yaml
      - ./auths:/root/.cli-proxy-api
      - ./logs:/CLIProxyAPI/logs
    restart: unless-stopped
EOF

docker compose up -d
```

### 二、线路机

#### 1. 安装Nginx

```bash
sudo apt update
sudo apt install -y nginx
```

#### 2. 配置防火墙

```bash
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw reload
```

#### 3. 配置 Nginx

```bash
sudo tee /etc/nginx/sites-available/cpa >/dev/null <<'EOF'
server {
    listen 80;
    server_name 你的域名;

    location / {
        proxy_pass http://落地机IP:8317;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_http_version 1.1;
        proxy_set_header Connection "";
        proxy_buffering off;
        proxy_read_timeout 3600s;
        proxy_send_timeout 3600s;
    }
}
EOF

sudo ln -sf /etc/nginx/sites-available/cpa /etc/nginx/sites-enabled/cpa
sudo nginx -t
sudo systemctl reload nginx
```

#### 4. 加HTTPS

```bash
sudo apt install -y certbot python3-certbot-nginx
sudo certbot --nginx -d 你的域名
```

访问 `https://你的域名/management.html`，输入 mgt-cpa- 密钥登录。

## 常见问题

### 线路机和落地机有什么区别？

因为家宽机器几乎都不能直连，所以需要一个能直连的线路机中转。访问线路机就跟访问家宽机是一样的。

### 成本多少？

DMIT: 13$/月 + VIRCS: 36$/月

### 家宽VPS是什么？

国外运营商在公寓等住宅网络搭建的服务器，环境干净，风控度低，适合搭建中转站。

## VPS 推荐链接

**VPS DMIT**
https://www.dmit.io/aff.php?aff=21728

**VPS VIRCS（家宽落地机）**
https://www.vircs.com/welcome?vcd=61a4aae4

**短信及语音接码平台**
- https://smspva.com/?ref=1307601
- https://hero-sms.com/?ref=357885

**白嫖流量**
- 500M试用：https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN，85折优惠
- 200M试用：https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码 GXJDIAN，9折优惠

## 相关资源

**VPS主机推荐**
- Claude用的丽萨主机：https://lisahost.com/aff.php?aff=9424
- 按流量VPS：https://www.lycheeip.com/home/ip?affId=1AwYIQ7BW8
- 一年10美元保底小鸡：https://clients.zgovps.com/?affid=1207
- 性价比云主机：https://my.racknerd.com/aff.php?aff=15809
- 美国家宽：https://www.webshare.io/?referral_code=55vpv6waorud

**家宽IP链接**
- https://ipfly.net/activity/OE5TWVlUUEI6TFZKOVhYQzM5NQ==
- https://www.voyracloud.com/?ref_code=5ZG4FHL8

**账号购买、礼品卡、Claude充值**
- https://accboy7gxjdian.acceboy.com/
- https://universalbus.cn/?s=bvDplWi2fZ
- https://www.gamsgo.com/partner/jGh24
- https://bewild.ai?code=GXJDIAN

**eSIM推荐**
- 9eSIM（优惠码：maq）：https://www.9esim.com/?coupon=maq
- ESTK（优惠码：GXJDIAN）：https://store.estk.me/zh?aid=16007
- XeSIM（推荐码：gxjdian）：https://xesim.cc/?DIST=RE5FHg==

**金融服务**
- Wise（推荐码：lizhiw12）：https://wise.com/invite/ihpc/lizhiw12
- Bybit支付卡：https://www.bybit.com/invite?ref=LGNQRG

## 联系方式

1. 微信讨论群：https://qr.869hr.uk/aitech
2. 超过100T资料总站：https://doc.869hr.uk
3. Telegram群聊：https://t.me/tgmShareAI
4. 微信公众号：搜"AI前沿的短裤哥"
5. 视频的文字博客：https://869hr.uk
6. 推特：https://x.com/gxjdian
7. Youtube：https://youtube.com/@gxjdian

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=Nigo_YH4SGE)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/dmitvircsdeploycpa-ai/)
