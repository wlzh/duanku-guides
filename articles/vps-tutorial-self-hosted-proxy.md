# 从购买服务器到自建节点的全流程保姆级教程

从服务器选购到节点搭建的全流程保姆级教程，涵盖线路选择、IP质量、安全加固、节点搭建、中转分流等内容。

> 完整图文与持续更新版本：[从购买服务器到自建节点的全流程保姆级教程](https://869hr.uk/2026/tutorials/vps-tutorial-self-hosted-proxy/)

## 内容信息

- 原文：https://869hr.uk/2026/tutorials/vps-tutorial-self-hosted-proxy/
- 更新：2026-04-18
- 分类：教程
- 关键词：VPS、VPN、ip属性
- 视频：https://www.youtube.com/watch?v=FU-9MXyEuJw

## 正文

<!-- 文章摘要 -->
> 
不知不觉就注册一个月了，在我刚注册两天的时候，分享过一个经验贴广受佬友们的好评。而最近据说机场过的不太平，我一直以来使用自建节点，也发过节点的拼车，那么我再给大家分享一下从服务器选购到节点搭建的全流程。

## 视频教程

<div class="video-container">
[在 YouTube 观看视频](https://www.youtube.com/watch?v=FU-9MXyEuJw)
</div>

<!-- more -->

> **本教程不包含任何aff和推广。**

* [刚注册两天，但已经在L站与I站逛了一两个月了，把自己全部的所学与经验分享给大家](https://linux.do/t/topic/1809325)

学AI，上L站。学服务器可以上I站：[IDC Flare - 域名、主机等信息集散地](https://idcflare.com/latest)

推荐了解一些名词来更好地阅读文章：[机圈黑话/专有名词扫盲（持续更新ing）](https://idcflare.com/t/topic/16977)

---

## 1. 选择服务器

我们搭建节点选择服务器无非就看两件事：**机器线路** 与 **IP质量**。

### 1.1 机器线路是什么？

机器线路就是你与服务器进行网络通信时数据包"赶路"所经历的路径：

* **去程**：你发送请求给服务器的路。
* **回程**：服务器把数据（如视频、网页）传回给你的路。

我们搭建代理节点原理就是这样。中间走不同的网络线路对于传播延迟与丢包等肯定有非常大的影响。

一般来说，我们走的线路都是 163、4837、CMI 这样的普通骨干网，一到晚高峰，延迟和丢包率显著上升导致连接服务器的体验不佳。

因此，很多服务商提供了针对中国大陆连接优化的线路机，这些线路机走一些运营商精品线路如CN2、9929、CMIN2 等，让你即使在高峰也不用去挤大家都在用的骨干网，体验自然就上升了，当然成本也是随之提高。

各个运营商关于线路的情况不同，对于线路科普想深入了解的请看：

* [常见各种线路和网络的科普](https://linux.do/t/topic/1235548)

### 1.2 IP质量是什么？

我们使用代理服务器上网，访问网站用的IP就是我们代理服务器的IP。代理服务器的IP质量决定了网站对我们的风控。

* **原生 IP**：IP 注册地址与服务器机房物理位置一致。
* **广播 IP**：商家通过技术手段，把别的地方的 IP 广播到另一个地方用。
* **机房 IP**：绝大多数 VPS 厂商提供的都是机房 IP。
* **住宅 IP**："家宽"，固定的运营商IP，就像真正的居民一样。

购买服务器大概了解这些类型的IP就可以，一般来说原生IP > 广播IP，住宅IP >> 机房IP。

**流媒体解锁：** IP是否能够解锁了一些流媒体如netflix、tiktok等，IP是否能够访问一些AI服务如chatgpt、claude等，IP是否被google标记为中国地区（即"送中"）。

一般来说，普通的科学上网用正常的机房IP就可以，如果有特殊需求如AI、tiktok等，可以选择解锁比较好的原生机房IP或者家宽IP。如有运营养号需求（如claude、tiktok、电商等）建议使用家宽IP，想让AI不降智不一定非要用家宽IP，好一点的机房IP也可以。

对于IP质量的深度检测与科普请看：

* [VPS IP质量检测完全指南：从小白到精通的实用教程](https://idcflare.com/t/topic/18792)

### 1.3 如何选购服务器？

选购服务器搭建节点前，请明确自己的需求，除非你一定要AI养号或者电商运营，不要一上来就追求线路机+家宽IP组合拳，大部分的需求好一点的机房IP就可以做到了。

本人因为大量使用AI，是 **DMIT 线路机 + AI与google服务落地Frontier静态家宽** 的组合。

对于各种地区类型服务器厂商的详细推荐与评测请看猫猫佬帖子：

* [常见地区VPS推荐](https://meowvps.com/blog/resrec/)

或者上 IDC flare 多逛逛看看别人的测评与推荐。

服务器系统选择 **debian 12** 或 **ubuntu 22.04**。

---

## 2. 服务器安全初始化

**以下是服务器厂商没有自动生成ssh密钥对和没有服务器防火墙面板的情况，如果有可以跳过或更改对应的秘钥生成或防火墙配置步骤。有问题可以直接问AI发生了什么。**

未安装sudo的服务器请先在root下使用 `apt update && apt install -y sudo` 安装sudo。

### 2.1 生成密钥对

本地终端窗口执行

```bash
# 生成 ed25519 密钥对，邮箱仅标识可以随意更换，连续按 3 次回车（不设置密钥密码，使用默认路径）
ssh-keygen -t ed25519 -C "your_email@example.com"

# 查看本地公钥内容
cat ~/.ssh/id_ed25519.pub
```

### 2.2 初始连接与公钥上传

本地终端窗口执行

```bash
# 使用 root 密码登录服务器
ssh root@你的服务器IP

# 创建.ssh目录并设置权限
mkdir -p /root/.ssh
chmod 700 /root/.ssh

# 写入公钥（替换为你复制的公钥内容）
echo "你复制的完整公钥内容" >> /root/.ssh/authorized_keys
# 设置文件权限
chmod 600 /root/.ssh/authorized_keys
```

新开一个本地终端窗口执行

```bash
ssh root@你的服务器IP
```

成功：不需要输入密码直接登录

### 2.3 创建免密 sudo 新用户

连接服务器终端执行

```bash
# 创建新用户，可以替换 deer 为你喜欢的名字
useradd -m -s /bin/bash deer
# 设置用户密码
passwd deer

# 复制 SSH 密钥给 deer 用户
cp -r /root/.ssh /home/deer/
chown -R deer:deer /home/deer/.ssh

# 配置免密sudo权限
echo 'deer ALL=(ALL) NOPASSWD: ALL' | tee /etc/sudoers.d/deer-nopasswd
chmod 0440 /etc/sudoers.d/deer-nopasswd
# 验证sudo配置语法
visudo -c -f /etc/sudoers.d/deer-nopasswd
```

新开一个本地终端执行

```bash
ssh deer@你的服务器IP
sudo whoami
```

成功：输出 root，不需要输入密码

### 2.4 关闭 root 登录和密码登录

连接服务器终端执行

```bash
# 开启公钥认证
sudo sed -i 's/^#\?PubkeyAuthentication.*/PubkeyAuthentication yes/' /etc/ssh/sshd_config

# 禁止root登录
sudo sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin no/' /etc/ssh/sshd_config

# 禁止密码登录
sudo sed -i 's/^#\?PasswordAuthentication.*/PasswordAuthentication no/' /etc/ssh/sshd_config

# 验证配置语法（无任何输出：语法正确）
sudo sshd -t

# 重启 SSH 服务
sudo systemctl restart sshd
```

每条指令新开一个本地终端执行

```bash
# 测试deer用户登录
ssh deer@你的服务器IP

# 测试root登录被拒绝
ssh root@你的服务器IP

# 测试密码登录被拒绝
ssh -o PreferredAuthentications=password deer@你的服务器IP

# 如果仍然可以密码登录，说明配置被云服务器厂商默认配置覆盖，先查看，可以看到有 Yes
sudo grep -r "PasswordAuthentication" /etc/ssh/sshd_config.d/
# 更改所有的配置文件的密码登录为 no
sudo sed -i 's/PasswordAuthentication yes/PasswordAuthentication no/g' /etc/ssh/sshd_config.d/*.conf
# 重启 SSH 服务，再次进行密码登录测试
sudo systemctl restart sshd
```

### 2.5 更换 SSH 端口并配置 UFW 防火墙

连接服务器终端执行（**严格按照顺序**）

```bash
# 修改 SSH 端口配置（端口自选，自行替换）
sudo sed -i 's/^#Port 22/Port 26547/' /etc/ssh/sshd_config
sudo sed -i 's/^Port 22/Port 26547/' /etc/ssh/sshd_config
# 验证配置语法
sudo sshd -t

# 安装并重置 UFW
sudo apt update
sudo apt install -y ufw
# 输入y确认
sudo ufw reset
# 设置默认规则，禁止一切入站，允许一切出站
sudo ufw default deny incoming
sudo ufw default allow outgoing

# 放行新 SSH 端口
sudo ufw allow 26547/tcp
# 重启 SSH 服务
sudo systemctl restart sshd
# 启用防火墙
sudo ufw enable
# 查看防火墙状态，只能看到 26547/tcp 被允许
sudo ufw status
```

**别关这个终端**，新开一个本地终端执行

```bash
# 测试连接
ssh deer@你的服务器IP -p 26547
```

连接成功！

### 2.6 本地 SSH config 配置

编辑本地 `~/.ssh/config` 文件，添加以下内容：

```bash
Host myserver #服务器别名，可自行更改
  HostName xx.xx.xx.xx #你的服务器IP
  User deer # 你的用户名
  Port 26547 # 你更改的 ssh 端口
  IdentityFile ~/.ssh/id_ed25519 #请改为你的实际地址
```

本地终端窗口执行

```bash
# 测试别名登录
ssh myserver
```

成功：免密直接登陆。

**至此，我们完成了服务器安全加固并且能够方便地连接服务器了。**

---

## 3. 服务器网络与IP质量测评

这是我的两个服务器的测试帖子，当做样例：
- [【自用测评】DMIT-LAX.AN4.Pro.TINY 三网顶级线路 1000GB@1Gbps](https://idcflare.com/t/topic/77259)
- [【自用测评】AaITR 美国Frontier静态家宽 完美家宽IP](https://idcflare.com/t/topic/78295)

### 3.1 网络测试

**网络质量：**

可以使用 [GitHub - xykt/NetQuality: 网络质量检测脚本](https://github.com/xykt/NetQuality) 检测网络质量。

连接服务器终端执行

```bash
# 切换到 root 环境
sudo -i
# 运行测试脚本
bash <(curl -Ls https://Check.Place) -N
```

选择 **完整模式** 运行，可以看到全国各地连接到服务器的延迟怎么样。

**回程路由：**

运行同样的脚本，选择 **完整回程路由**，可以看到服务器回程走的具体是什么线路。

### 3.2 IP质量测试

**IP质量：**

可以使用 [GitHub - xykt/IPQuality: IP质量检测脚本](https://github.com/xykt/IPQuality) 检测IP质量。

连接服务器终端执行

```bash
# 切换到 root 环境
sudo -i
# 运行测试脚本
bash <(curl -Ls https://Check.Place) -I
```

可以看到各个常见IP库的检测情况和常见流媒体的解锁情况。

**流媒体解锁：**

可以使用 [GitHub - lmc999/RegionRestrictionCheck](https://github.com/lmc999/RegionRestrictionCheck) 检测详细的流媒体解锁情况。

连接服务器终端执行

```bash
# 切换到 root 环境
sudo -i
# 运行测试脚本
bash <(curl -L -s check.unlock.media)
```

选择对应的区域，得到详细的流媒体解锁结果。

```text
============[ Multination ]============
 Dazn:                                  Yes (Region: US)
 Disney+:                               Yes (Region: US)
 Netflix:                               Yes (Region: US)
 YouTube Premium:                       Yes (Region: US)
 Amazon Prime Video:                    Yes (Region: US)
 ChatGPT:                               Yes
 Google Gemini:                         Yes (Region: USA)
 Claude:                                Yes
=======================================
```

IP质量更深入的测试可以看上文贴的 VPS IP质量检测完全指南。

### 3.3 融合测试

一个个脚本一项项测试太麻烦了，我们可以直接用脚本进行融合测试。
[GitHub - LloydAsp/NodeQuality: 在沙箱环境中运行vps测试脚本，并排版测试结果](https://github.com/LloydAsp/NodeQuality)

```bash
# 切换到 root 环境
sudo -i
# 运行测试脚本
bash <(curl -sL https://run.NodeQuality.com)
```

测试结果可能5-10分钟较久，测试完成打开给出的nodequality结果网页，可以直接看到服务器的基本信息、IP质量、网络质量和回程路由四项测试结果。

**至此，我们基本完成了对服务器的质量测试。想要了解更多测试脚本的请看猫猫佬的帖子：**

* [常见脚本推荐](https://meowvps.com/blog/script/)

---

## 4. 节点搭建

**每搭建一个节点，请记得通过 `sudo ufw allow 端口/tcp` 放行对应的节点端口（UDP 协议放行UDP端口）！**

### 4.1 一键脚本搭建

对于自用，其实没必要上面板，直接使用一键脚本。
[GitHub - 233boy/sing-box 最好用的 sing-box 一键安装脚本 & 管理脚本](https://github.com/233boy/sing-box)

```bash
# 切换到 root 环境
sudo -i
# 运行安装脚本
bash <(wget -qO- -o- https://github.com/233boy/sing-box/raw/main/install.sh)
```

安装后会自动创建一个VLESS-REALITY的节点，我们可以看到节点的信息以及一个vless://开头的链接URL。

对于v2rayN：复制链接后在软件界面ctrl+v使用。
对于Clash系：需要将vless://开头的链接转换为clash的yaml配置文件，可以网上寻找转换工具，或者直接丢给AI让他帮你转换成配置文件即可。然后在clash订阅界面中拖入配置文件使用。

如果你需要管理节点可以输入 `sudo sb` 进入脚本菜单，有选项界面便捷好用。

### 4.2 3x-ui面板搭建

如果是多人使用或者想精细化管理等，可以使用 [3x-ui面板](https://github.com/MHSanaei/3x-ui) 来搭建节点。

#### 4.2.1 3x-ui面板安装

```bash
# 放行 80 与 443 端口
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
# 切换到 root 环境
sudo -i
# 安装3x-ui面板，连按四下回车
bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
```

安装完成后我们可以看到下面的信息：

```yaml
═══════════════════════════════════════════
     Panel Installation Complete!
═══════════════════════════════════════════
Username:    xxx
Password:    xxx
Port:        xxx
WebBasePath: xxx
Access URL:  https:x
═══════════════════════════════════════════
```

**某些系统安装会出现SSL证书的路径的错误BUG，需要通过http直接打开面板登录，在面板设置里面手动指定安装好的证书路径。出现问题不懂的直接去找AI帮你！**

使用 `ufw allow 面板端口/tcp` 放行面板的端口。
执行 `x-ui` ，选择 `6` 然后输入 `y` 更改我们的用户名和密码，然后连按两下回车。

现在访问我们的 `Access URL` ，输入用户名和密码，成功进入面板。

**如何用域名来访问面板和节点？**

你有一个域名，并且已经托管到了cloudflare：
* [保姆级教程：如何将域名无缝托管到 Cloudflare](https://idcflare.com/t/topic/68502)

打开cloudflare的域名DNS记录，名称随便你写，添加一条指向你服务器IP的 **仅DNS** 的解析记录，保存。

执行 `x-ui` ，选择 `19` ，然后选择 `1` ，输入刚才添加的解析记录子域名 `名称.你的域名.com` ，回车，选择 `y` ，option选择 `0` ，然后选择 `y` ，我们现在得到了新的用域名访问的 `Access URL` ，并且以后我们的节点地址也是我们的域名了。

#### 4.2.2 节点的搭建

点击 `入站列表` → `添加入站` → `协议 vless` → `安全 Reality` → `Get New Cert` → `创建` 。
这样我们得到了一个 vless + reality 节点。（记得放行端口）

点击二维码复制订阅链接。
点击菜单下的 `┇` → `编辑` 可以编辑节点信息，包括备注、端口、流量等等。

#### 4.2.3 节点的中转与分流

**在 `xray设置` 更改的设置都需要点击 `保存` 并 `重新启动 Xray` 。**

有些佬友可能买了家宽或者一些落地IP，直接访问的体验不好，可以通过线路机或者其他机器进行 **中转** 。

在中转机的3x-ui面板点击 `xray设置` → `出站规则` → `添加出站` → `JSON` ，粘贴你的落地节点的链接，然后点一下旁边的按钮解析。点击 `添加出站` 。

如果你是只想中转一下，所有访问都用落地的IP，那么点击 `路由规则` → `添加规则` ， `Inbound Tags` 选 `inbound-你的节点端口` ， `Outbound Tag` 选择你刚才添加的出站名称。
此时所用通过你选择的节点端口的流量都会转发给你的落地节点。

如果佬友们想正常服务就用中转机访问，只有 **AI以及谷歌服务等高风控场景** 才用落地或者家宽的节点来访问，可以 **添加分流**：

点击入站列表节点菜单下的 `┇` → `编辑` → `Sniffing` → `开启` 。
点击 `xray设置` → `高级配置` → `路由规则` ，在JSON文件后面添加分流规则（删除 `"inboundTag"` 就是所有节点都遵守分流）：

```json
{
    "type": "field",
    "inboundTag": [
      "inbound-你要分流的节点"
    ],
    "domain": [
      "geosite:google",
      "geosite:youtube",
      "domain:aistudio.google.com",
      "domain:googleapis.com",
      "domain:gstatic.com",
      "domain:ggpht.com",
      "domain:googlevideo.com",
      "domain:ytimg.com",
      "domain:youtubei.googleapis.com",
      "domain:gemini.google.com",
      "domain:ai.google.dev",
      "domain:deepmind.google",
      "domain:notebooklm.google",
      "domain:openai.com",
      "domain:chatgpt.com",
      "domain:oaistatic.com",
      "domain:oaiusercontent.com",
      "domain:anthropic.com",
      "domain:claude.ai",
      "domain:perplexity.ai",
      "domain:poe.com",
      "domain:huggingface.co",
      "domain:cohere.com",
      "domain:mistral.ai",
      "domain:x.ai",
      "domain:grok.com",
      "domain:groq.com",
      "domain:stability.ai",
      "domain:stability.com",
      "domain:midjourney.com",
      "domain:runwayml.com",
      "domain:runwayml.cloud",
      "domain:character.ai",
      "domain:elevenlabs.io",
      "domain:suno.com",
      "domain:replicate.com",
      "domain:cursor.com",
      "domain:cursor.sh",
      "domain:bolt.new",
      "domain:lovable.dev",
      "domain:replit.com",
      "domain:phind.com",
      "domain:you.com",
      "domain:ipdata.co",
      "geosite:figma",
      "domain:figma.com",
      "domain:figma.site",
      "domain:figmastatic.com"
    ],
    "outboundTag": "你的落地节点名称"
}
```

这个配置覆盖了一般的AI服务和所有google服务与youtube（防止google风控），使用的时候需要关闭google与metaai的定位防止送中。有其他想分流的域名和服务可以让AI继续给你加。

clash软件的中转和分流功能强大，自建节点脚本可以通过clash来分流：

* [[教程3.0] 草履虫也能学会的 Clash 配置：UI界面一键配置精确分流、链式代理](https://linux.do/t/topic/1398113)

---

## 5. 发车与拼车管理

线路机和家宽都很贵，一般都会拼几个人一同分担成本。

作为车主，你已经学会了3x-ui面板的搭建、节点的创建和管理、节点的中转与分流了，可以放心发车了，在发车前，打开记录日志防止纠纷（记得定期清理）：
点击 `xray设置` → `基础配置` → `访问日志` → `./access.log` 。
到时候可以通过AI分析日志看看是否有人滥用。

可以到我 IDC Flare 的主页看看我的发车模板，规则与价格一定要写清楚。
**不建议通过这个赚钱，只建议把这个作为分摊成本享受高质量自建节点的一种方法。**

作为车友，上车不要滥用，共同长久稳定地用节点对每个人都好。

---

## 相关链接

### 视频教程

本文配有视频教程，欢迎观看：

* YouTube 视频教程：[从购买服务器到自建节点的全流程保姆级教程](https://youtu.be/FU-9MXyEuJw)（上方可直接观看）

### VPS主机推荐

| 服务商 | 说明 | 链接 |
|--------|------|------|
| 丽萨主机 | Claude使用推荐 | [注册链接](https://lisahost.com/aff.php?aff=9424) |
| LycheeIP | 按流量VPS | [注册链接](https://www.lycheeip.com/home/ip?affId=1AwYIQ7BW8) |
| ZGOVPS | 一年10美元多年保底 | [注册链接](https://clients.zgovps.com/?affid=1207) |
| RackNerd | 各种云主机，主打性价比 | [注册链接](https://my.racknerd.com/aff.php?aff=15809) |
| CloudCone | 美国VPS，一年70美金活动 | [注册链接](https://app.cloudcone.com/?ref=13794) |
| Webshare | 一年8.5美金美国家宽 | [注册链接](https://www.webshare.io/?referral_code=55vpv6waorud) |

### 家宽IP

| 服务商 | 说明 | 链接 |
|--------|------|------|
| IPFly | 家宽IP | [注册链接](https://ipfly.net/activity/OE5TWVlUUEI6TFZKOVhYQzM5NQ==) |
| VoyraCloud | 住宅VPS | [注册链接](https://www.voyracloud.com/?ref_code=5ZG4FHL8) |

### 短信及语音接码平台

* [Hero SMS](https://hero-sms.com/?ref=357885)

### 白嫖流量

* 500M试用：[IPFly](https://ipfly.net/zh-cn/activity/GXJDIAN) 优惠码 `GXJDIAN`，85折优惠
* 200M试用：[Talordata](https://dashboard.talordata.com/reg?inviter_code=gxjdian) 优惠码 `GXJDIAN`，9折优惠

### Gmail、Telegram等账号购买、礼品卡

* [Accboy](https://accboy7gxjdian.acceboy.com/)
* [UniversalBus](https://universalbus.cn/?s=bvDplWi2fZ)
* [Gamsgo](https://www.gamsgo.com/partner/jGh24)

### Claude、OpenAI Codex等充值

* [Bewild](https://bewild.ai?code=GXJDIAN) 优惠码 `GXJDIAN`

### eSIM 推荐

| eSIM | 优惠 | 链接 |
|------|------|------|
| 9eSIM | 9折（优惠码：maq） | [注册链接](https://www.9esim.com/?coupon=maq) |
| ESTK | 9折（优惠码：GXJDIAN） | [注册链接](https://store.estk.me/zh?aid=16007) |
| XeSIM | 9折（推荐码：gxjdian） | [注册链接](https://xesim.cc/?DIST=RE5FHg==) |
| 三家eSIM对比 | 让国产手机秒变eSIM手机 | [对比文章](https://s.869hr.uk/mcc) |

### 出海银行卡/支付

| 服务 | 说明 | 链接 |
|------|------|------|
| Wise | 有身份证就可，推荐码：lizhiw12 | [申请链接](https://wise.com/invite/ihpc/lizhiw12) |
| N26 | 需要护照，推荐码：lizhiw02766c | [教程视频](https://youtu.be/HY9OD8rX89s) |
| Bybit支付卡 | 申请链接 | [注册链接](https://www.bybit.com/invite?ref=LGNQRG) |

### 社交媒体与社区

1. 微信讨论群：[加入群聊](https://qr.869hr.uk/aitech)
2. 超过100T资料总站：[doc.869hr.uk](https://doc.869hr.uk)
3. Telegram群聊：[t.me/tgmShareAI](https://t.me/tgmShareAI)
4. 微信公众号：搜「AI前沿的短裤哥」
5. 推特：[@gxjdian](https://x.com/gxjdian)
6. YouTube：[@gxjdian](https://youtube.com/@gxjdian)
7. 博客：[869hr.uk](https://869hr.uk)

### YouTube 专辑

* [AI产品&技术相关专辑](https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI)
* [出海收款、付款、银行卡、虚拟卡相关专辑](https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW)
* [出海手机号相关专辑](https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G)
* [出海网络搭建相关专辑](https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw)
* [出海VPS相关专辑](https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC)

---

以上都是个人摸索和使用的经验总结，如有错误欢迎佬友们批评指正！点个赞支持一下吧~

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tutorials/vps-tutorial-self-hosted-proxy/)
