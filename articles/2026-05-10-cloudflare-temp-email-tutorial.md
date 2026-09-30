# 【2026最新】零成本自建Cloudflare临时邮箱！无限前缀域名邮箱，小白保姆级教程部署指南

2026最新Cloudflare临时邮箱搭建教程，零成本自建域名邮箱，支持无限前缀，D1数据库+KV缓存+Workers+Pages，小白20分钟搞定

> 完整图文与持续更新版本：[【2026最新】零成本自建Cloudflare临时邮箱！无限前缀域名邮箱，小白保姆级教程部署指南](https://869hr.uk/2026/uncategorized/2026-05-10-cloudflare-temp-email-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/uncategorized/2026-05-10-cloudflare-temp-email-tutorial/
- 更新：2026-05-10
- 分类：视频教程
- 关键词：教程、Cloudflare、开源项目、邮箱
- 视频：https://www.youtube.com/watch?v=Gf2c1TrqYuo

## 正文

注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有 🔗https://869hr.uk

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=Gf2c1TrqYuo)</div>

想要一个完全免费、支持无限前缀的自定义域名邮箱吗？本期视频将为你带来 2026 年最新版的 Cloudflare 临时邮箱（cloudflare_temp_email）保姆级搭建教程！完全不需要购买服务器，只需一个域名，利用赛博大善人 Cloudflare 的生态（D1 数据库、KV 缓存、Workers 和 Pages），小白也能在 20 分钟内搞定属于自己的高逼格域名邮箱！

无论你是需要注册各种平台防止主邮箱泄露，还是需要多个前缀分配给不同账号，这个方案都能完美解决。后续还可以扩展对接 Telegram 机器人和 Resend 发邮件功能哦！

## 视频目录 / 章节内容

- **第一部分**：域名准备与 Cloudflare 托管设置
- **第二部分**：配置电子邮件路由 (Catch-all)
- **第三部分**：创建 D1 数据库与 KV 缓存
- **第四部分**：部署后端 Workers 与环境变量配置
- **第五部分**：部署前端 Pages 与自定义域绑定
- **第六部分**：基础使用与创建账号测试

## 相关链接

- 原作者开源项目 GitHub 地址：https://github.com/dreamhunter2333/cloudflare_temp_email
- Cloudflare 官网：https://www.cloudflare.com/

---

## 图文教程（整合自 LINUX DO 社区文档）

> 本图文教程整合自 LINUX DO 社区文档共建帖子，原作者：小黄（XiaoHuang），项目原作者：awsl。原文链接：https://linux.do/n/topic/1666961

### 写在前面

这是一个 Cloudflare 临时邮箱的保姆级图文教程，2026 年最新版，针对 Cloudflare 页面更新和项目迭代做了全面翻新。

### 注意

此为临时邮箱，如果你会给你的域名一直续费，那么你可以一直用你自己的域名邮箱，如果你只是年抛域名（用了一年直接抛弃）**那么请不要拿它注册重要的平台**，因为很多域名二次续费很贵。

### 教程内容分两部分

- **第一部分**：教你如何把域名托管到 Cloudflare 并且配置如何用自己的域名接收邮件，转发到自己常用的邮箱
- **第二部分**：教你在 Cloudflare 上部署并配置 cloudflare_temp_email 项目

---

## 第一部分：将域名托管到 Cloudflare

### 开始前的准备

1. **域名准备** - 在腾讯云、阿里云等云服务商购买一个域名
2. **Cloudflare 账号** - 去 https://www.cloudflare.com/ 注册一个账号
3. **项目地址** - https://github.com/dreamhunter2333/cloudflare_temp_email ，记得给项目点个 star！

### 将域名交给 Cloudflare 托管（以腾讯云为例）

1. 登录 Cloudflare，先把语言设置成简体中文（右上角）
2. 点击**添加站点**，填入你的域名
3. 选择**免费计划**，完全够用
4. Cloudflare 会给你两个 DNS 服务器地址，记下来
5. 去域名注册商（如腾讯云）找到域名管理，修改 DNS 服务器
6. 把原来的 DNS 服务器替换成 Cloudflare 给的两个地址，保存
7. 回到 Cloudflare 点击**检查名称服务器**
8. 等待 5-15 分钟，看到绿色的**有效**状态就成功了

### 配置电子邮件路由

1. 点击左侧菜单的**电子邮件** → **电子邮件路由**
2. 在**目标邮箱**填写你的常用邮箱地址（如 Gmail）
3. 点击**创建并继续**，去邮箱完成验证
4. 配置 **Catch-all 规则**（捕获所有规则）：无论前缀是什么，统统转发到你的邮箱
5. 启用 Catch-all 并选择转发到你验证的邮箱地址

到这里，任何发到你域名的邮件都会被转发到你设置的常用邮箱。如果你只是想要一个能接收邮件的域名邮箱，到这里已经够用了。

---

## 第二部分：在 Cloudflare 上部署 cloudflare_temp_email 项目

### 创建 D1 数据库

1. 回到 Cloudflare 首页，左侧菜单找到 **Workers 和 Pages** → **D1 SQL 数据库**
2. 点击创建，给数据库起个名字（如 `TempEmailDB`）
3. 打开项目 GitHub 上的 `db/schema.sql` 文件，复制所有 SQL 语句
4. 回到 Cloudflare D1 控制台，粘贴 SQL 语句，点击**执行**
5. 回到概述刷新，表数量是 10 就代表成功

### 配置 KV 缓存

1. 左侧菜单 **Workers 和 Pages** → **KV**
2. 点击**创建命名空间**，起个名字（如 `TempMailKV`）

### 创建 Workers 部署后端

1. 点击**创建应用程序** → **创建 Worker**，起个名字（如 `TempMailAPI`）
2. 绑定 D1 数据库：变量名必须填 **DB**（大写），选择你创建的数据库
3. 绑定 KV 缓存：变量名必须填 **KV**（大写），选择你创建的 KV 命名空间

### 配置环境变量

以下是必须配置的 10 个参数：

| 参数名 | 类型 | 值 | 说明 |
|--------|------|-----|------|
| DOMAINS | JSON | `["你的域名.com"]` | 临时邮箱域名列表 |
| DEFAULT_DOMAINS | JSON | `[]` | 未登录用户可用域名（推荐留空） |
| DISABLE_ANONYMOUS_USER_CREATE_EMAIL | 文本 | `true` | 禁止匿名用户创建邮箱 |
| JWT_SECRET | 文本 | 在线生成的随机字符串 | JWT 签名密钥（在线生成：https://www.librechat.ai/toolkit/creds_generator） |
| ADMIN_PASSWORDS | JSON | `["你的密码"]` | 管理后台登录密码 |
| ENABLE_USER_CREATE_EMAIL | 文本 | `true` | 允许用户创建邮箱 |
| ENABLE_USER_DELETE_EMAIL | 文本 | `false` | 是否允许删除邮件 |
| USER_ROLES | JSON | 见下方示例 | 用户角色配置 |
| ADMIN_USER_ROLE | 文本 | `admin` | 管理后台角色名 |
| ENABLE_AUTO_REPLY | 文本 | `false` | 自动回复功能 |

USER_ROLES 示例：

```json
[
    {"domains": ["你的域名.com"], "prefix": "", "role": "vip"},
    {"domains": ["你的域名.com"], "prefix": "", "role": "admin"}
]
```

### 部署代码文件

1. 在 Worker 设置中找到**兼容性标志**，添加 `nodejs_compat`
2. 从 GitHub Releases 页面下载最新版 `worker.js`
3. 回到 Worker 编辑页面，把 `worker.js` 文件拖入代码编辑区域
4. 点击**保存并部署**
5. 刷新页面，显示 `ok` 就代表后端部署成功

### 配置自定义域

1. 在 Worker 设置中找到**触发器**或**自定义域**
2. 添加自定义域，格式建议：`apimail.你的域名.com`
3. 等待 DNS 生效，浏览器访问自定义域显示 `ok` 即成功

### 重新配置域名电子路由

如果你之前配了 Catch-all 到常用邮箱，必须改为转发到 Worker：

1. 回到 Cloudflare 首页 → 电子邮件路由
2. 把 Catch-all 目标从常用邮箱改为你的 Worker
3. 这样临时邮箱网站才能正常接收邮件

### 部署前端页面

1. 访问临时邮箱官方文档生成前端代码：https://temp-mail-docs.awsl.uk/zh/guide/ui/pages
2. 填入你的后端地址（如 `https://apimail.你的域名.com`），**必须用 https**
3. 下载生成的前端代码文件
4. 回到 Cloudflare → **创建应用程序** → **Pages** → **上传资产**
5. 把前端代码文件拖进去
6. **重要设置**：未找到处理改为 `single-page-application`（否则刷新会 404）
7. 添加自定义域，格式建议：`mail.你的域名.com`
8. 等待 DNS 生效，访问前端地址能看到登录页面就成功了

### 基本使用

1. 用管理员密码登录后台
2. 在用户管理页面创建用户，设置用户名、密码和角色
3. 把前端地址和登录信息发给朋友
4. 用户登录后可以创建邮箱地址，接收邮件

---

## 对接 LINUX DO OAuth2 登录

### 修改后端参数

1. **DEFAULT_DOMAINS**：把域名加进去，让通过 LINUX DO 登录的用户有域名可用
2. **DISABLE_ANONYMOUS_USER_CREATE_EMAIL**：保持 `true`

### 配置 OAuth2

1. 在临时邮箱前端设置中启用 LINUX DO OAuth2 登录
2. 打开 https://connect.linux.do/ ，点击新建应用
3. 填写应用名称，回调地址填：`https://你的后端地址/api/oauth/callback/linuxdo`
4. 信任等级建议设为一级
5. 创建后获得 Client ID 和 Client Secret
6. 回填到临时邮箱的 OAuth2 配置中
7. 测试：打开临时邮箱网站，能看到 LINUX DO 登录按钮，点击授权后自动跳回登录成功

---

## 佬友们补充的教程

### Claude Code 部署方式

有佬友写了用 Claude Code + CLI 的形式去部署，思路是交给了 Claude Code，写得很详细：
https://linux.do/t/topic/1692459

### 自动部署脚本（macOS/Linux）

使用 CF 提供的 API 完成全自动化部署，支持配置子域名邮箱：
https://linux.do/t/topic/1783188

### Windows 版自动部署脚本

https://linux.do/t/topic/1801403

---

## 短信及语音接码平台

- https://hero-sms.com/?ref=357885
- https://smspva.com/?ref=1307601

## 白嫖流量

- 500M 试用：https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN，85 折
- 200M 试用：https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码 GXJDIAN，9 折

## 关注与资源

1. 微信讨论群：https://qr.869hr.uk/aitech
2. 超过100T资料总站网站：https://doc.869hr.uk
3. Telegram 群聊：https://t.me/tgmShareAI
4. 微信公众号：搜「AI前沿的短裤哥」
5. 视频的文字博客：https://869hr.uk
6. 推特：https://x.com/gxjdian
7. YouTube：https://youtube.com/@gxjdian

## VPS 主机推荐

- Claude 用的丽萨主机：https://lisahost.com/aff.php?aff=9424
- 按流量 VPS：https://www.lycheeip.com/home/ip?affId=1AwYIQ7BW8
- 一年 10 美元多年保底小鸡：https://clients.zgovps.com/?affid=1207
- 各种云主机，性价比之选：https://my.racknerd.com/aff.php?aff=15809
- 美国VPS年付70美金：https://app.cloudcone.com/?ref=13794
- 一年 8.5 美金美国家宽：https://www.webshare.io/?referral_code=55vpv6waorud
- VPS DMIT：https://www.dmit.io/aff.php?aff=21728
- VPS VIRCS 家宽落地机：https://www.vircs.com/welcome?vcd=61a4aae4
- 家宽IP：https://ipfly.net/activity/OE5TWVlUUEI6TFZKOVhYQzM5NQ==
- 住宅VPS：https://www.voyracloud.com/?ref_code=5ZG4FHL8

## Gmail、Telegram 等账号购买、礼品卡、AI 产品充值

- https://accboy7gxjdian.acceboy.com/
- https://universalbus.cn/?s=bvDplWi2fZ
- https://www.gamsgo.com/partner/jGh24
- Claude、OpenAI Codex 等充值：https://bewild.ai?code=GXJDIAN

## eSIM 推荐

1. 三家 eSIM 让国产手机秒变 eSIM 手机：https://s.869hr.uk/mcc
2. 9eSIM 打 9 折（优惠码：maq）：https://www.9esim.com/?coupon=maq
3. ESTK 打 9 折（优惠码：GXJDIAN）：https://store.estk.me/zh?aid=16007
4. XeSIM 打 9 折（推荐码：gxjdian）：https://xesim.cc/?DIST=RE5FHg==
5. Wise 申请链接（推荐码：lizhiw12）：https://wise.com/invite/ihpc/lizhiw12
6. N26 申请（推荐码：lizhiw02766c）：https://youtu.be/HY9OD8rX89s?si=78REb8MyKSJB6cwQ
7. Bybit 支付卡：https://www.bybit.com/invite?ref=LGNQRG

## YouTube 播放列表

- AI 产品&技术相关：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海 VPS 相关：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

---

喜欢这期教程的话，请务必点赞、订阅并打开小铃铛，你的支持是我持续更新的最大动力！有问题欢迎在评论区留言讨论。

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/uncategorized/2026-05-10-cloudflare-temp-email-tutorial/)
