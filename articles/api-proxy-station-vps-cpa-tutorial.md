# 手把手教你搭建 API 中轉站：VPS+CPA+New API+Docker+Nginx+Cloudflare+SSL+域名配置 保姆級教程

從零開始搭建 API 中轉站完整教程，涵蓋 VPS 購買、CPA 配置、New API 部署、Docker Compose、Nginx 反向代理、Cloudflare DNS 與 SSL 證書配置

> 完整图文与持续更新版本：[手把手教你搭建 API 中轉站：VPS+CPA+New API+Docker+Nginx+Cloudflare+SSL+域名配置 保姆級教程](https://869hr.uk/2026/tutorial/api-proxy-station-vps-cpa-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tutorial/api-proxy-station-vps-cpa-tutorial/
- 更新：2026-05-10
- 分类：教程
- 专题：教程
- 关键词：教程、VPS、Docker、Cloudflare、建站
- 视频：https://www.youtube.com/watch?v=GxGQPcFOF6s

## 正文

> 
本視頻是一份全流程「保姆級」教學，手把手教你如何從零開始搭建一個對外 API 中轉站。相關視頻中的內容、命令、腳本、代碼，都在博客文章中 🔗https://869hr.uk

## 視頻教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=GxGQPcFOF6s)</div>

## 教程核心架構

VPS + CLI Proxy API (CPA) + NEW API + Docker + Nginx + Cloudflare + SSL + 域名配置

## 時間戳

| 時間 | 步驟 |
|------|------|
| 00:00 | 前提与 VPS 选择：騰訊雲最新活動頁面選擇與購買 |
| 01:30 | 伺服器連接：使用 FinalShell 連接到伺服器並查看 IP |
| 02:45 | 準備工作：創建資料夾結構 (/opt/proxy/...) |
| 04:00 | 配置 CPA：修改 cpa/config.yaml（⚠️ 請務必修改密碼與秘鑰） |
| 06:15 | 配置 Docker Compose：編寫 docker-compose.yml |
| 08:30 | 認證文件：將認證文件放進指定目錄 |
| 10:00 | 防火牆配置：Linux 防火牆與云伺服器安全組打開 3000 端口 |
| 11:45 | 執行與訪問：執行 docker compose 並訪問中轉站首頁 |
| 13:15 | New API 配置：登錄、渠道管理、添加渠道、測試 |
| 15:00 | 系統管理：設置模型價格、模型廣場 |
| 16:30 | 令牌配置：配置與測試令牌 |
| 18:00 | 本地連接測試：使用 CC Switch 進行本地測試 |
| 19:30 | 域名與 SSL (進階)：Cloudflare DNS 代理域名 |
| 21:30 | Nginx 配置：反向代理與安全增強 |
| 23:45 | SSL 證書：Cloudflare Origin Certificate |
| 25:15 | 最終安全性部署：更新防火牆與 Docker Compose |
| 27:30 | 重啟與驗證：最終啟動與域名訪問驗證 |

---

# 前提

# VPS选择

## 活动页 [腾讯云最新活动](https://cloud.tencent.com/act?Is=sdk-topnav)

## 购买完毕后进入控制台

## 查看服务器ip

## 使用FinalShell连接到服务器

# 对外中转站教程开始

## 一、准备工作

### 1、创建一个文件夹用于存文件，并进入该文件夹

```bash
mkdir -p /opt/proxy/{cpa/{logs,auths},newapi/{data,logs}} && cd /opt/proxy && touch docker-compose.yml cpa/config.yaml
```

```
/opt/proxy/
├── docker-compose.yml
├── cpa/
│   ├── logs/
│   ├── auths/
│   └── config.yaml
└── newapi/
    ├── data/
    └── logs/
```

### 2、cpa目录下的 config.yaml 文件

```yaml
# 服务器绑定主机/接口，默认空字符串同时绑定 IPv4/IPv6
# 使用 "127.0.0.1" 或 "localhost" 可限制仅本机访问
host: ""
# 服务器端口
port: 8317
tls:
# 是否启用 HTTPS
  enable: false
# 管理 API 设置
remote-management:
# 是否允许远程（非 localhost）访问管理接口。
# 为 false 时仅允许 localhost，仍需管理密钥。
# 留空则完全禁用管理 API（所有 /v0/management 路由返回 404）。
  allow-remote: true
# 管理密钥。若填写明文，启动时会自动哈希后生效。
# 所有管理请求（包括本地）都需要该密钥。
# 留空则完全禁用管理 API（所有 /v0/management 路由返回 404）。
  secret-key: "$2a$10$5dHykttqHWAU.WcYFg0qgOXhDoxC1P7wpZ7i2T8Kj9xqwvVRfTUm2"    # ⚠️ 请修改密码
# true 时禁用内置管理面板资源与路由。 默认 false
  disable-control-panel: false
# 认证目录（支持 ~ 展开为主目录）
auth-dir: "~/.cli-proxy-api"
# apikeys 自己设置
api-keys:
  - sk-8SGCShq021BAFgpBE  # ⚠️ 请修改秘钥
# 调试日志。 默认 false
debug: true
# 写入滚动日志文件而非 stdout。 默认false
logging-to-file: true
# 日志目录大小上限，0 表示不限制。
logs-max-total-size-mb: 100
# 403/408/500/502/503/504 时的重试次数。
request-retry: 3
# 冷却凭据等待秒数上限，超出即触发重试。
max-retry-interval: 30
routing:
# 多匹配凭据的选择策略：round-robin 或 fill-first。 默认round-robin
  strategy: "round-robin"
# 是否为 /v1/ws 启用认证。 默认false
ws-auth: false
# 为 false 时禁用内存用量统计聚合，默认false
usage-statistics-enabled: false
```

### 3、proxy目录下的 docker-compose.yml 文件

```yaml
# newapi docker-compose 配置参考：
# https://docs.newapi.ai/zh/docs/installation/config-maintenance/docker-compose-yml
# 启动的全部服务
services:
# 服务名
  new-api:
# 镜像名
    image: calciumion/new-api:latest
# 容器名
    container_name: new-api
# 退出时总是自动重启，确保服务意外挂掉后能恢复。
    restart: always
# 启动容器后，会执行这个自定义命令，它将应用的日志目录设置为 /app/logs
    command: --log-dir /app/logs
# 端口映射
    ports:
      - '3000:3000'  # ❓注意后面的3000不能修改，不然后面的healthcheck心跳检测，检测不到
# 卷挂载
    volumes:
      - ./newapi/data:/data
      - ./newapi/logs:/app/logs
# 环境变量
    environment:
      - SQL_DSN=postgresql://root:123456@postgres:5432/new-api # ⚠️ 请修改密码
      - REDIS_CONN_STRING=redis://redis
# 设置容器时区为上海
      - TZ=Asia/Shanghai
# 是否启用错误日志记录
      - ERROR_LOG_ENABLED=true
# 是否启用批量更新 batch update enabled
      - BATCH_UPDATE_ENABLED=true
# 定义启动顺序，它会等待 rpa、redis、postgres 容器启动后，再启动
    depends_on:
      - redis
      - postgres
      - cpa
# 心跳检查，在容器内检查，间隔30s，超时时间10s，重复机制3次
    healthcheck:
# test的内容是向本机（容器内）发送一个请求，如果在响应中找不到success关键字就报错
      test: [
          'CMD-SHELL',
          "wget -q -O - http://localhost:3000/api/status | grep -o '\"success\":\\s*true' || exit 1",
        ]
      interval: 30s
      timeout: 10s
      retries: 3

# 下面的同上，不同的参数我再做解释
  redis:
    image: redis:latest
    container_name: redis
    restart: always

  postgres:
    image: postgres:15
    container_name: postgres
    restart: always
    environment:
# 数据库用户名
      POSTGRES_USER: root # ❓ 设置用户名，改为你自己的
# 数据库密码
      POSTGRES_PASSWORD: 123456 # ⚠️ 设置密码，改为你自己的
# 数据库名
      POSTGRES_DB: new-api
    volumes:
      - pg_data:/var/lib/postgresql/data

# cpa服务
  cpa:
    image: eceasy/cli-proxy-api:latest
    container_name: cpa
    volumes:
      - ./cpa/config.yaml:/CLIProxyAPI/config.yaml # 配置文件输出
      - ./cpa/auths:/root/.cli-proxy-api # 认证文件 config.yaml 中的 ~ 代表主目录，在linux中就是 /root
      - ./cpa/logs:/CLIProxyAPI/logs # 日志文件输出
    restart: always

# 顶级挂载，避免文件权限问题，挂载地址：/var/lib/docker/volumes/pg_data
volumes:
  pg_data:
```

### 4、把认证文件放进 /opt/proxy/cpa/auths 目录下

### 5、去Linux的防火墙打开3000端口

先查看下防火墙状态：

```bash
# 看防火墙是否在运行
systemctl status firewalld
# 启动防火墙（不会断 SSH，放心）
systemctl start firewalld
# 设置开机自启
systemctl enable firewalld
# 看看当前默认放行了哪些服务
firewall-cmd --list-services
# 看开放了哪些端口
firewall-cmd --list-ports
```

如果防火墙没有开启，则不用执行下面的步骤，或者你要安全可以打开防火墙后执行下面命令：

```bash
firewall-cmd --zone=public --add-port=3000/tcp --permanent && firewall-cmd --reload && firewall-cmd --list-ports
```

### 6、打开云服务器的安全组

进入腾讯云控制台，选择服务器，点击防火墙选项卡，添加规则：来源选择全部，协议端口填写 3000。注意不要动系统默认的 SSH（22端口）规则。

## 二、执行docker compose文件

```bash
docker compose up -d
```

## 三、通过 http://ip:3000 访问中转站

默认用户名 root，默认密码 123456，登录后记得修改密码。

## 四、New API 配置

### 1、渠道管理

添加渠道 - 类型选择对应选项 - Base URL 填写 `http://cpa:8317`（Docker 内部网络用容器名访问）- 密钥填写 CPA 配置文件中的 API Keys 值

### 2、系统管理

设置模型价格（内部计费单位），配置完模型价格后渠道测试才能通过。

### 3、其他设置

系统设置中可配置可见菜单、签到功能、系统公告、API 信息、支付设置等。

### 4、配置令牌

创建令牌并复制密钥值，这就是用户调用 API 时需要的密钥。

### 5、本地连接测试（CC Switch）

在 CC Switch 中填入中转站地址和令牌，发送测试消息验证中转站正常工作。

## 五、域名与 SSL（进阶）

### 1、使用 Cloudflare 的 DNS 代理域名

1. 登录 Cloudflare，点击添加站点，输入域名
2. 选择免费计划
3. 到域名注册商（如阿里云）修改 NS 记录指向 Cloudflare 提供的地址
4. 等待 DNS 传播生效（通常几小时）

### 2、添加 Nginx 目录和文件

```bash
mkdir -p /opt/proxy/nginx/{ssl,logs,conf.d} && \
cd /opt/proxy && \
touch nginx/nginx.conf nginx/conf.d/api.conf nginx/ssl/api.pem nginx/ssl/api.key && \
chmod 600 ./nginx/ssl/api.key
```

```
/opt/proxy/
├── docker-compose.yml
├── newapi/
│   ├── data/
│   └── logs/
├── cpa/
│   ├── config.yaml
│   ├── auths/
│   └── logs/
└── nginx/
    ├── nginx.conf
    ├── conf.d/
    │   └── api.conf
    ├── ssl/
    │   ├── api.pem
    │   └── api.key
    └── logs/
```

#### nginx.conf

```nginx
user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log warn;
pid /var/run/nginx.pid;

events {
    worker_connections 1024;
    use epoll;
    multi_accept on;
}

http {
    include /etc/nginx/mime.types;
    default_type application/octet-stream;

    log_format main '$remote_addr - $remote_user [$time_local] "$request" '
                    '$status $body_bytes_sent "$http_referer" '
                    '"$http_user_agent" "$http_x_forwarded_for"';

    access_log /var/log/nginx/access.log main;

    sendfile on;
    tcp_nopush on;
    tcp_nodelay on;
    keepalive_timeout 65;
    types_hash_max_size 2048;
    client_max_body_size 100m;

    gzip on;
    gzip_vary on;
    gzip_min_length 1024;
    gzip_comp_level 6;
    gzip_types text/plain text/css text/xml text/javascript
               application/json application/javascript
               application/xml+rss application/rss+xml
               font/truetype font/opentype
               application/vnd.ms-fontobject image/svg+xml;

    include /etc/nginx/conf.d/*.conf;
}
```

#### api.conf

```nginx
# ==================== HTTP 重定向到 HTTPS ====================
server {
    listen 80;
    server_name api.wudike.online;                               # ⚠️ 你的域名

    return 301 https://$server_name$request_uri;
}

# ==================== HTTPS 主服务器 ====================
server {
    listen 443 ssl http2;
    server_name api.wudike.online;                               # ⚠️ 你的域名

    ssl_certificate /etc/nginx/ssl/api.pem;
    ssl_certificate_key /etc/nginx/ssl/api.key;

    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384;
    ssl_prefer_server_ciphers off;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;

    add_header Strict-Transport-Security "max-age=63072000" always;
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header X-XSS-Protection "1; mode=block" always;

    access_log /var/log/nginx/api-access.log main;
    error_log /var/log/nginx/api-error.log;

    client_max_body_size 100m;

    location / {
        proxy_pass http://new-api:3000;
        proxy_http_version 1.1;

        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Forwarded-Port $server_port;

        proxy_connect_timeout 300s;
        proxy_send_timeout 300s;
        proxy_read_timeout 300s;

        proxy_buffering off;
        proxy_cache off;
        proxy_cache_bypass $http_upgrade;
    }

    location /nginx-health {
        access_log off;
        return 200 "healthy\n";
        add_header Content-Type text/plain;
    }
}
```

#### SSL 证书

在 Cloudflare 的 SSL/TLS 设置页面，选择源服务器选项卡，点击创建证书。将证书内容复制到 `api.pem`，私钥内容复制到 `api.key`。

```bash
chmod 600 ./nginx/ssl/api.key
```

### 3、配置 DNS 解析

在 Cloudflare DNS 管理页面添加 A 记录：名称填写子域名（如 api），IPv4 地址填写 VPS 的公网 IP，确保代理状态开启（橙色云朵图标）。

### 4、打开防火墙

```bash
# 打开 443 和 80 端口，关闭 3000 端口
firewall-cmd --permanent --add-port=443/tcp && firewall-cmd --permanent --add-port=80/tcp && firewall-cmd --reload
firewall-cmd --permanent --remove-port=3000/tcp && firewall-cmd --reload
```

在云服务商安全组中同样开放 80/443，移除 3000。

### 5、修改 Docker Compose 添加 Nginx

```yaml
# newapi docker-compose 配置参考：
# https://docs.newapi.ai/zh/docs/installation/config-maintenance/docker-compose-yml
services:
  new-api:
    image: calciumion/new-api:latest
    container_name: new-api
    restart: always
    command: --log-dir /app/logs
    ports:
      - '3000'  # 改成 expose，不再对外暴露端口
    volumes:
      - ./newapi/data:/data
      - ./newapi/logs:/app/logs
    environment:
      - SQL_DSN=postgresql://root:123456@postgres:5432/new-api # ⚠️ 请修改密码
      - REDIS_CONN_STRING=redis://redis
      - TZ=Asia/Shanghai
      - ERROR_LOG_ENABLED=true
      - BATCH_UPDATE_ENABLED=true
    depends_on:
      - redis
      - postgres
      - cpa
    healthcheck:
      test: [
          'CMD-SHELL',
          "wget -q -O - http://localhost:3000/api/status | grep -o '\"success\":\\s*true' || exit 1",
        ]
      interval: 30s
      timeout: 10s
      retries: 3
    networks:
      - newapi-network

  redis:
    image: redis:latest
    container_name: redis
    restart: always
    networks:
      - newapi-network

  postgres:
    image: postgres:15
    container_name: postgres
    restart: always
    environment:
      POSTGRES_USER: root
      POSTGRES_PASSWORD: 123456 # ⚠️ 请修改密码
      POSTGRES_DB: new-api
    volumes:
      - pg_data:/var/lib/postgresql/data
    networks:
      - newapi-network

  cpa:
    image: eceasy/cli-proxy-api:latest
    container_name: cpa
    volumes:
      - ./cpa/config.yaml:/CLIProxyAPI/config.yaml
      - ./cpa/auths:/root/.cli-proxy-api
      - ./cpa/logs:/CLIProxyAPI/logs
    restart: always
    networks:
      - newapi-network

  # Nginx 反向代理服务 用于做SSL
  nginx:
    image: nginx:alpine
    container_name: nginx
    restart: always
    ports:
      - '80:80'
      - '443:443'
    volumes:
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
      - ./nginx/conf.d:/etc/nginx/conf.d:ro
      - ./nginx/ssl:/etc/nginx/ssl:ro
      - ./nginx/logs:/var/log/nginx
    depends_on:
      - new-api
    networks:
      - newapi-network

volumes:
  pg_data:

networks:
  newapi-network:
    driver: bridge
```

### 6、启动 Docker Compose

```bash
docker compose down
docker compose up -d
```

在浏览器中访问 `https://你的域名`，确认能看到 New API 登录页面且地址栏显示安全锁图标。

---

## 相關鏈接

- 騰訊雲最新活動：https://curl.qcloud.com/2Xh9Mh9l
- New API 部署文檔：https://docs.newapi.ai/zh/docs/installation/config-maintenance/docker-compose-yml

⚠️ **安全提示**：教程中涉及的所有密碼、秘鑰、隨機字符串，在實際部署時必須修改為您自己的內容！

## 日常鏈接

- 短信及语音接码平台 https://hero-sms.com/?ref=357885 或 https://smspva.com/?ref=1307601
- 白嫖流量 500M 試用：https://ipfly.net/zh-cn/activity/GXJDIAN 優惠碼 GXJDIAN，85 折
- 200M 試用：https://dashboard.talordata.com/reg?inviter_code=gxjdian 優惠碼 GXJDIAN，9 折

注意⚠️鏈接需複製到瀏覽器中才能打開！

## 關注我

1. 微信討論群：https://qr.869hr.uk/aitech
2. 超過100T資料總站：https://doc.869hr.uk
3. Telegram 群聊：https://t.me/tgmShareAI
4. 微信公眾號：搜「AI前沿的短褲哥」
5. 視頻的文字博客：https://869hr.uk
6. 推特：https://x.com/gxjdian
7. YouTube：https://youtube.com/@gxjdian

## VPS 主機推薦

- Claude 用的麗薩主機：https://lisahost.com/aff.php?aff=9424
- 按流量 VPS：https://www.lycheeip.com/home/ip?affId=1AwYIQ7BW8
- 一年 10 美元的多年保底小雞：https://clients.zgovps.com/?affid=1207
- 各種雲主機，主打性價比：https://my.racknerd.com/aff.php?aff=15809
- 美國的 VPS，一年 70 美金：https://app.cloudcone.com/?ref=13794
- 一年 8.5 美金的美國家寬：https://www.webshare.io/?referral_code=55vpv6waorud
- VPS DMIT：https://www.dmit.io/aff.php?aff=21728
- VPS VIRCS 家寬落地機：https://www.vircs.com/welcome?vcd=61a4aae4
- 家寬 IP 鏈接：https://ipfly.net/activity/OE5TWVlUUEI6TFZKOVhYQzM5NQ==
- 住宅 VPS 鏈接：https://www.voyracloud.com/?ref_code=5ZG4FHL8

## 賬號購買 & 充值

- Gmail、Telegram 等賬號購買、禮品卡：https://accboy7gxjdian.acceboy.com/
- https://universalbus.cn/?s=bvDplWi2fZ
- https://www.gamsgo.com/partner/jGh24
- Claude、OpenAI Codex 等充值：https://bewild.ai?code=GXJDIAN

## eSIM 推薦

1. 三家 eSIM 對比及開戶鏈接：https://s.869hr.uk/mcc
2. 9eSIM 打 9 折（優惠碼：maq）：https://www.9esim.com/?coupon=maq
3. ESTK 打 9 折（優惠碼：GXJDIAN）：https://store.estk.me/zh?aid=16007
4. XeSIM 打 9 折（推薦碼：gxjdian）：https://xesim.cc/?DIST=RE5FHg==
5. Wise 申請鏈接（推薦碼：lizhiw12）：https://wise.com/invite/ihpc/lizhiw12
6. N26 申請鏈接（推薦碼：lizhiw02766c）：https://youtu.be/HY9OD8rX89s?si=78REb8MyKSJB6cwQ
7. Bybit 支付卡申請鏈接：https://www.bybit.com/invite?ref=LGNQRG

## 相關播放列表

- AI 產品&技術相關：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、銀行卡：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手機號：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海網絡搭建：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海 VPS：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

## 參考文章

- [全平台 Docker 部署 CPA(CLIProxyAPI Plus) 靈活定制指南——接入Codex - 掘金](https://juejin.cn/post/7617781226364092450#heading-8)
- [【教程】2026版 小白也能看懂的自建Cloudflare臨時郵箱教程 - LINUX DO](https://linux.do/t/topic/1666961)

---

如果覺得這期視頻對你有幫助，請點贊、評論、訂閱頻道並打開小鈴鐺 🔔

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tutorial/api-proxy-station-vps-cpa-tutorial/)
