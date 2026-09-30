# VPS安全加固完全指南：7招让你的服务器固若金汤

VPS安全加固7大核心策略详解，涵盖禁用Root登录、SSH密钥认证、Fail2ban防爆破、UFW防火墙、Docker安全配置，附一键自动化加固脚本

> 完整图文与持续更新版本：[VPS安全加固完全指南：7招让你的服务器固若金汤](https://869hr.uk/2026/tech/vps-security-hardening-skill-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/vps-security-hardening-skill-tutorial/
- 更新：2026-04-24
- 分类：技术
- 专题：技术
- 关键词：VPS、网络安全、教程、开源项目
- 视频：https://www.youtube.com/watch?v=-uqap0UClnY
- 系列：[出海 VPS](../series/vps.md)

## 正文

## 视频教程

<div class="video-container">
[在 YouTube 观看视频](https://www.youtube.com/watch?v=-uqap0UClnY)
</div>

## 为什么 VPS 安全加固如此重要

随着 AI 应用的大火，越来越多的开发者和技术爱好者开始购买 VPS 服务器。无论是部署 AI 应用、搭建个人网站，还是运行各类服务，VPS 已经成为许多人的必备工具。但是，你的 VPS 真的安全吗？

当你的服务器暴露在公网上的那一刻起，它就成为了黑客扫描和攻击的目标。根据安全研究机构的数据，一台新开通的 VPS，平均在上线后的几分钟内就会遭遇第一次扫描攻击。如果使用默认配置，你的服务器可能在几小时内就会被暴力破解。

特别是对于刚接触 VPS 的小白用户，往往会忽视最基本的安全措施：

- 使用 root 账户直接登录
- SSH 端口保持默认的 22
- 使用弱密码
- 没有配置防火墙
- 缺少防暴力破解机制

这些看似"方便"的做法，实际上是在给黑客敞开大门。

## 七大核心安全策略

今天要介绍的这套 VPS 安全加固方案，涵盖了从基础到进阶的七大核心防护策略，可以让你的服务器安全性提升数个量级。

### 1. 禁用 Root 密码登录

Root 账户拥有系统的最高权限，一旦被攻破，黑客可以对你的服务器为所欲为。而 root 又是所有 Linux 系统的默认管理员账户名，黑客只需要暴力破解密码即可。

操作步骤：

- 创建一个新的普通用户账户
- 赋予该账户 sudo 权限
- 禁止 root 账户通过密码远程登录
- 保留 root 本地登录能力（通过控制台）

这样做的好处是，即使有人知道了你的用户名，没有正确的密码和权限提升方式，也无法获取系统控制权。

### 2. 更改 SSH 默认端口

SSH 服务默认使用 22 端口，这是所有黑客都知道的常识。大量的自动化扫描工具会不停地扫描互联网上所有 IP 的 22 端口，尝试暴力破解。

将 SSH 端口改为一个非标准端口（如 3322、8822 等），可以有效避开大部分自动化扫描。虽然这不是绝对安全的措施，但可以大幅减少被攻击的频率。

需要注意：

- VPS 平台的安全组/防火墙已开放新端口
- 系统防火墙（UFW）已配置新端口
- 旧的 22 端口已关闭

### 3. 配置 Fail2ban 防暴力破解

Fail2ban 是一款优秀的入侵防御工具，它会监控系统日志，当检测到某个 IP 在短时间内多次登录失败时，会自动将该 IP 加入黑名单，禁止其继续访问。

典型配置：

- 5 分钟内失败 5 次，封禁 10 分钟
- 持续攻击者可延长封禁时间
- 支持邮件或其他方式通知管理员

这个机制可以有效防止暴力破解攻击，让攻击者的自动化工具失效。

### 4. 启用 SSH 密钥认证

密码认证的问题在于容易被暴力破解（尤其是弱密码），可能被键盘记录器窃取，人为因素导致泄露。

而 SSH 密钥认证使用的是非对称加密：

- 私钥保存在本地，永不传输
- 公钥放在服务器上
- 即使有人截获通信内容，也无法破解

一个 2048 位的 RSA 密钥，其安全强度相当于一个长度超过 600 位的随机密码。这种级别的安全性，即使是超级计算机也需要数百年才能破解。

### 5. SSH 登录通知（可选）

通过配置 SSH 登录通知，每当有人（包括你自己）登录服务器时，都会收到即时通知。这可以帮助你：

- 及时发现异常登录
- 追踪登录时间和来源
- 在被入侵的第一时间采取措施

可以通过企业微信、Telegram、邮件等多种方式接收通知。

### 6. 防火墙配置与端口管理

Ubuntu 系统自带的 UFW（Uncomplicated Firewall）是一个简单易用的防火墙工具。正确配置后，它可以只开放必要的端口、关闭所有不需要的服务端口、防止未授权访问。

端口管理策略：

- 开放新的 SSH 端口
- 删除旧的 22 端口规则
- 根据实际需求开放应用端口（如 80、443）
- 定期审查开放的端口列表

### 7. Docker 安全配置

很多人不知道，Docker 默认会直接操作 iptables 规则，这会绕过 UFW 防火墙的设置。这意味着即使你在 UFW 中关闭了某个端口，Docker 容器仍然可能将其暴露在公网上。

解决方案是在 Docker 配置文件中添加：

```json
{
  "iptables": false
}
```

这样可以防止 Docker 绕过 UFW，确保所有端口都受到防火墙的统一管理。

## 一键自动化加固方案

手动执行这些配置步骤不仅繁琐，还容易出错。为了让更多人能够轻松完成 VPS 安全加固，开源社区提供了自动化工具。

### 使用方法

只需要一条命令，就能完成所有配置：

```bash
./scripts/harden-vps.sh \
  --ip <vps_ip> \
  --root-pass <root_password> \
  --user <new_user> \
  --user-pass <new_user_password> \
  --port <ssh_port>
```

### 可选参数

- `--no-fail2ban` - 跳过 Fail2ban 安装
- `--with-notify` - 配置 SSH 登录通知

### 前置条件

在运行脚本之前，需要确保：

1. VPS 支持 root 密码登录（临时开启即可）
2. 本地安装了 sshpass 工具
3. VPS 平台的防火墙已开放新端口

如果你的 VPS 默认禁用了 root 密码登录，可以通过控制台执行以下命令临时开启：

```bash
sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication yes/' /etc/ssh/sshd_config
sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config
systemctl restart ssh
passwd root
```

### 执行流程

脚本会按照 10 个阶段依次执行：

1. **SSH 连接测试** - 验证 root 密码登录
2. **系统更新** - 更新软件包到最新版本
3. **安装依赖** - 安装 sudo、ufw、fail2ban 等工具
4. **创建 sudo 用户** - 创建新用户并配置权限
5. **SSH 安全配置** - 修改端口、启用密钥登录
6. **Fail2ban 配置** - 设置防暴力破解规则
7. **SSH 配置验证** - 检查配置文件正确性
8. **UFW 防火墙** - 配置防火墙规则
9. **重启服务** - 应用所有配置
10. **Docker 安全检查** - 检测并修复 Docker 配置

整个过程全自动完成，最后会生成一份详细的加固报告。

## 实战演示要点

在实际使用中，有几个关键点需要注意：

### 防火墙配置顺序

一定要先在 VPS 平台的安全组/防火墙中开放新的 SSH 端口，再执行加固脚本。否则可能会导致 SSH 连接中断，无法继续操作。

### 不同 VPS 平台的差异

不同的 VPS 提供商（如 AWS、Google Cloud、Oracle Cloud、阿里云等）在 SSH 配置上可能有细微差异。脚本已经针对常见情况做了兼容处理，但仍建议在测试环境先验证。

### 保存好新的登录凭证

加固完成后，记得保存：

- 新的 SSH 端口号
- 新用户的用户名和密码
- SSH 私钥文件（如果配置了密钥登录）

### 测试新配置

在断开原有 SSH 连接之前，先用新的端口和账户测试登录，确保一切正常。避免把自己锁在门外。

## 后续维护建议

完成初始加固后，还需要养成良好的安全习惯：

定期更新系统：

```bash
sudo apt update && sudo apt upgrade -y
```

监控登录日志，定期检查 `/var/log/auth.log`，关注异常登录尝试。

审查防火墙规则：

```bash
sudo ufw status numbered
```

确保只开放必要的端口。再安全的系统也可能遭遇意外，定期备份是最后的保险。即使配置了密钥登录，用户密码仍然很重要（用于 sudo 提权），建议使用密码管理器生成和保存强密码。

## 开源项目

这套 VPS 安全加固方案已经在 GitHub 开源，任何人都可以免费使用、修改和分享：

- **GitHub**: https://github.com/wlzh/skills/tree/main/vps-security-hardening
- **视频教程**: https://youtu.be/-uqap0UClnY
- **图文教程**: https://x.com/gxjdian/status/2033751314208059507

## 社群与资源

1. 微信讨论群：https://qr.869hr.uk/aitech
2. 超过100T资料总站网站：https://doc.869hr.uk
3. Telegram群聊：https://t.me/tgmShareAI
4. 微信公众号：搜"AI前沿的短裤哥"
5. 视频的文字博客：https://869hr.uk
6. 推特：https://x.com/gxjdian
7. Youtube：https://youtube.com/@gxjdian

## VPS主机推荐

- Claude用的丽萨主机：https://lisahost.com/aff.php?aff=9424
- 按流量VPS：https://www.lycheeip.com/home/ip?affId=1AwYIQ7BW8
- 一年 10 美元的多年保底小鸡：https://clients.zgovps.com/?affid=1207
- 各种云主机，主打性价比：https://my.racknerd.com/aff.php?aff=15809
- 美国的vps，一年 70 美金搞活动：https://app.cloudcone.com/?ref=13794
- 一年 8.5 美金的美国家宽，稳定靠谱：https://www.webshare.io/?referral_code=55vpv6waorud
- 家宽IP链接：https://ipfly.net/activity/OE5TWVlUUEI6TFZKOVhYQzM5NQ==
- 住宅VPS链接：https://www.voyracloud.com/?ref_code=5ZG4FHL8

## 账号购买与充值

- Gmail、Telegram等账号购买、礼品卡：https://accboy7gxjdian.acceboy.com/
- 通用数字商品：https://universalbus.cn/?s=bvDplWi2fZ
- 游戏与AI服务：https://www.gamsgo.com/partner/jGh24
- Claude、OpenAI Codex等充值：https://bewild.ai?code=GXJDIAN

## 相关专辑

- AI产品和技术相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海VPS相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

## 关注我不迷路

如果你觉得这期视频对你有帮助，请务必：

- 点赞本视频
- 在评论区留下你的问题或成功注册的截图
- 订阅频道并打开小铃铛，获取最新硬核白嫖教程和科技前沿资讯！

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=-uqap0UClnY)
- [Twitter图文教程](https://x.com/gxjdian/status/2033751314208059507)
- [GitHub开源项目](https://github.com/wlzh/skills)
- [更多教程和资源](https://869hr.uk)

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/vps-security-hardening-skill-tutorial/)
