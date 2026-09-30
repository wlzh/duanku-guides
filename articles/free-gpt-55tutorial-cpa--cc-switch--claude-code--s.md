# 免费畅玩 GPT-5.5！小白手把手教程：CPA + CC-Switch + Claude Code 完整搭建攻略

从零开始搭建 CPA + CC-Switch + Claude Code 完整环境，免费使用 GPT-5.5 和 Codex，包含 VPN 配置、CPA 部署、CC-Switch 设置、Claude Code 整合的完整教程，以及 Codex 免费 Plus 申请指南

> 完整图文与持续更新版本：[免费畅玩 GPT-5.5！小白手把手教程：CPA + CC-Switch + Claude Code 完整搭建攻略](https://869hr.uk/2026/tech/free-gpt-55tutorial-cpa--cc-switch--claude-code--s/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/free-gpt-55tutorial-cpa--cc-switch--claude-code--s/
- 更新：2026-05-07
- 分类：技术
- 关键词：教程、AI工具、VPN、VPS
- 视频：https://www.youtube.com/watch?v=cEdCN_cY8mI

## 正文

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=cEdCN_cY8mI)</div>

## 写在前面：新人入坑避坑指南

作为一名 AI 社区的新人，在配置 CPA + CC-Switch 并成功使用 Codex 的路上走了不少弯路。在此特别鸣谢社区大佬卢哥和王子哥的手把手教导，吃水不忘挖井人！

今天我将我的学习过程整合分享出来，这是一份专为小白准备的完整全流程手把手教程，希望能帮助大家告别迷茫，轻松上手！同时这也是我的一份学习笔记，供大家参考交流。感谢 Ansonkkk、Jason_Xu 等社区成员的贡献，这份笔记希望能帮到大家！

## 教程核心亮点

- 👉 **小白手把手**：从 VPN 安装到 Claude Code 整合配置，每一步都清晰演示
- 👉 **无需高昂 OpenAI Key**：利用现有 Codex 兼容接口，畅享高性能模型
- 👉 **全流程搭建**：涵盖 VPN、CPA (CliProxyAPI)、CC-Switch 及其与 Claude Code 的完美融合
- 👉 **0 成本体验**：无需信用卡绑定，合理利用资源

## 所需工具 & 预备知识

1. VPN 客户端（教程推荐 Clash Verge - GitHub）
2. CPA (CliProxyAPI)（GitHub 项目）
3. CC-Switch（GitHub 项目）
4. Claude Code 桌面端（需启用开发者模式）
5. Codex/GPT-5.5 兼容账号（教程建议用 Plus 以上账号，免费账号有代入电话限制）

## 分步操作指南

### 一、VPN 配置

- 正确配置 VPN 畅快访问外网
- 建议选择美国节点
- 使用 Clash Verge，默认端口 7897

### 二、CPA (CliProxyAPI) 搭建 & 配置

1. 从 GitHub 下载程序，解压至 D 盘根目录
2. 创建桌面快捷方式
3. 复制 `config.example.yaml` 为 `config.yaml`
4. 用记事本修改 `config.yaml` 中的 `secret-key` 为 `123456`（并记下 CPA 端口 8317）
5. 运行 CPA
6. 浏览器打开 `http://127.0.0.1:8317/management.html`
7. 输入密码，生成新 API 密钥（记下此 sk- 密钥）
8. 在系统配置设置代理 URL 为 `http://127.0.0.1:7897`
9. 点击 OAuth 登录并授权 Codex 账号（建议 Plus 账号）
10. 查看额度确认配置成功

### 三、CC-Switch 配置

1. 从 GitHub 下载并安装 CC-Switch
2. 选择 Codex，启用高级配置
3. 填入 API 请求地址：`http://127.0.0.1:8317/v1`
4. 填入刚才在 CPA 生成的 API Key
5. 写入自定义配置（例如 `model_provider="custom"`, `model="gpt-5.5"` 等，详见视频）
6. 映射模型配置，测试链接，启用并开启路由

### 四、Claude Code 整合

1. 启用开发者模式（Troubleshooting → Enable Developer Mode）
2. 选择 config third party
3. 设置 base-url 为 `http://127.0.0.1:15721`
4. 设置 API-KEY 为 `PROXY_MANAGED`
5. 映射模型配置，重启

现在就可以在 Claude 里畅享 GPT 的高性能啦！

---

## Codex 申请免费 Plus 的正确姿势

小白手把手教程，从域名申请到免费订阅，全流程教学。

### 一、手动注册企业邮箱

#### 1. 进入阿里云万网，点击域名注册

#### 2. 选择 .asia 域名

首年 8 元，如果你连 8 元都不舍得，可以不用往下看了。

#### 3. 输入域名并查询

输入一个域名，可以随意输入，然后点击查询，查看这个域名价值 8 元，点击立即注册。

#### 4. 登录阿里云账号

跳出登录界面，登录阿里云账号，如果没有，点击立即注册进行注册。

#### 5. 购买域名

登录成功后，跳转到购买域名界面：
- 如果第一次注册，点击创建信息模板（个人的实名认证信息）
- 勾选同意
- 点击购买

#### 6. 支付

跳转到支付页面，选择一种支付方式，支付。

#### 7. 进入域名控制台

支付成功后，点击域名控制台。

#### 8. 查看域名状态

点击全部域名，查看域名状态，如果显示"未实名"，点击未实名。

#### 9. 实名认证

确保模板实名认证成功，邮箱验证成功，输入手机号，获取验证码，提交到注册局。

#### 10. 等待审核

提交到注册局后，耐心等待，成功后手机会收到短信提醒。

#### 11. 配置阿里邮箱

顶部输入"阿里邮箱"，点击阿里邮箱，解析邮箱。

#### 12. 一键设置

点击一键设置，10 分钟后生效。

#### 13. 管理邮箱

点击管理进入邮箱管理，可以在这里设置解析，设置管理员密码，跳转到登录地址。

#### 14. 登录邮箱

输入管理员名称和密码登录，完成身份验证。

#### 15. 确认域名解析

进入邮箱主界面，确保域名解析成功，如果解析不成功，不能收发邮件，需要耐心等待。

#### 16. 添加员工账号

点击左侧"组织与用户"，点击"员工账号"，添加员工账号。

到这里如果域名解析成功，添加我们的企业邮箱就成功了。这里我们就可以拿到企业员工邮箱。

### 二、下载模拟器

1. 搜索 bluestacks，点击官方链接
2. 点击下载模拟器并安装

### 三、安装 VPN 客户端

推荐使用 Clash Verge。

### 四、订购 VPN

这里我就不写链接了，不然会认为我推广。

### 五、安装 GoPay 和 WhatsApp

#### 1. 进入模拟器

系统应用，点击游戏商店。

#### 2. 搜索并安装

搜索 gopay 和 whatsapp 安装。

### 六、注册 gopay 和 whatsapp

这里就是傻瓜式一步一步按照官方直接用我们国内的手机号注册就可以。

### 七、使用企业员工邮箱注册 OpenAI

#### 1. 使用企业邮箱登录

使用企业邮箱登录 https://qiye.aliyun.com 方便接码。

#### 2. 无痕窗口访问 OpenAI

无痕输入 www.openai.com，点击试用。

#### 3. 免费注册

点击免费注册，输入企业员工邮箱点击继续。

#### 4. 设置密码

选择使用密码，输入密码继续。

#### 5. 验证邮箱

输入企业邮箱验证码继续。

#### 6. 生成美国地址

搜索"美国地址生成器"，随机生成一个美国地址。

#### 7. 填写用户信息

填入用户名和年龄，年龄随便写大于 18 岁。

#### 8. 跳过引导

跳过，点击继续，点击"好的开始吧"。

#### 9. 选择免费使用

点击免费使用。

#### 10. 切换地区

右下角美国点击，弹出下拉菜单，选择印度尼西亚。

#### 11. 选择 GoPay 支付

选择 gopay，输入全名，从美国地址生成器复制过来地址，会自动弹出州，邮政编码。如果不弹就删除再粘贴一次。

#### 12. 订阅

点击订阅会出错。

#### 13. 解决方案

VPN 节点切换到印度尼西亚，然后再点击订阅。跳转后输入 gopay 的手机号，第一次肯定不会有问题。

#### 14. 继续

点击继续。

#### 15. 验证

输入 whatsapp 的验证码，如果没有 whatsapp 也没关系，耐心等待 1 分钟，选择发送短信也可以，用手机接受短信就可以。

#### 16. 输入支付密码

输入 gopay 支付密码。

#### 17. 完成支付

继续，Pay now，输入密码一步一步，剩下的会自动跳转。

### 八、CPA 登录

输入密码就可以，不用再输入验证码。

### 九、第二次购买

**细节**：Gopay 注册成功默认有 1 块钱。支付后 GPT 会扣除 1 块验证账号。随后 10 分钟内会退回 1 块钱。我们一定要等这 1 块钱回来，因为 GPT 可能有这个环节，验证是否取消。

等这 1 块钱回来后，再取消 Unlink。

#### 取消步骤

1. 点击资料，点击账户
2. 点击 unlinked app
3. 点击 unlink 取消

### 十、高阶技巧

去 GitHub 下载插件，快捷注册 duck 等任意邮箱，然后使用选择日本节点，使用神秘代码 F12 浏览器控制台，按照提示输入 `allow pasting`。

再次感谢原作者对以下神秘代码的贡献。虽然我不知道是谁搞出来的，但是觉得牛逼。

```javascript
(async function checkoutLinkOnly() {
try {
const session = await fetch('/api/auth/session').then((r) => r.json());
const accessToken = session?.accessToken;
if (!accessToken) {
console.log('accessToken: null');
return;
}

} catch (e) {
console.log('accessToken: null');
console.log('paymentLink: null');
}
})();
```

生成链接跳转。这个方法我自己在 5 月 5 日测试通过。但是这种号日存活。第二天就没了。

以上就是我现在使用 plus 的小技巧。

---

## 实用资源链接

### 短信及语音接码平台

- https://hero-sms.com/?ref=357885
- https://smspva.com/?ref=1307601

### 白嫖流量

- 500M 试用，链接 https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN，85 折优惠
- 200M 试用，链接 https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码 GXJDIAN，9 折优惠

### 社区链接

1. 微信讨论群：https://qr.869hr.uk/aitech
2. 超过 100T 资料总站网站：https://doc.869hr.uk
3. Telegram 群聊：https://t.me/tgmShareAI
4. 微信公众号：搜"AI 前沿的短裤哥"
5. 视频的文字博客（银行卡、手机号、VPS 主机、IP 测试等）：https://869hr.uk
6. 推特：https://x.com/gxjdian
7. Youtube：https://youtube.com/@gxjdian

### VPS 主机等

- Claude 用的丽萨主机：https://lisahost.com/aff.php?aff=9424
- 按流量 VPS：https://www.lycheeip.com/home/ip?affId=1AwYIQ7BW8
- 一年 10 美元的多年保底小鸡：https://clients.zgovps.com/?affid=1207
- 各种云主机，主打性价比：https://my.racknerd.com/aff.php?aff=15809
- 美国的 vps，一年 70 美金搞活动：https://app.cloudcone.com/?ref=13794
- 一年 8.5 美金的美国家宽，稳定靠谱：https://www.webshare.io/?referral_code=55vpv6waorud

### VPS DMIT

https://www.dmit.io/aff.php?aff=21728

### VPS VIRCS

家宽落地机：https://www.vircs.com/welcome?vcd=61a4aae4

### 家宽 IP 和住宅 VPS

- 家宽 IP 链接：https://ipfly.net/activity/OE5TWVlUUEI6TFZKOVhYQzM5NQ==
- 住宅 VPS 链接：https://www.voyracloud.com/?ref_code=5ZG4FHL8

### Gmail、Telegram 等账号购买、礼品卡，Claude 充值 AI 产品

- https://accboy7gxjdian.acceboy.com/
- https://universalbus.cn/?s=bvDplWi2fZ
- https://www.gamsgo.com/partner/jGh24

### Claude、OpenAI Codex 等充值

https://bewild.ai?code=GXJDIAN

### eSIM 相关

1. 三家 eSIM 让国产手机秒变 eSIM 手机，全方面优缺点对比及开户链接🔗 https://s.869hr.uk/mcc
2. eSIM 9eSIM 打 9 折（优惠码：maq）注册及购买链接 https://www.9esim.com/?coupon=maq
3. eSIM ESTK 打 9 折（优惠码：GXJDIAN）注册及购买链接 https://store.estk.me/zh?aid=16007
4. eSIM XeSIM 打 9 折（推荐码：gxjdian）注册及购买链接 https://xesim.cc/?DIST=RE5FHg==

### 银行卡相关

5. wise 的申请链接及教程链接（有身份证就可，推荐码：lizhiw12）（教程链接 https://x.com/wlzh/status/19967997897...）（申请链接 https://wise.com/invite/ihpc/lizhiw12）
6. N26 的申请链接及教程链接（需要护照，推荐码：lizhiw02766c）https://youtu.be/HY9OD8rX89s?si=78REb8MyKSJB6cwQ
7. Bybit 支付卡申请链接 https://www.bybit.com/invite?ref=LGNQRG，教程链接 https://youtu.be/3sN7P2t_CeA

### YouTube 专辑

- AI 产品&技术相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海 VPS 相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

---

## 关注我不迷路

如果你觉得这期视频对你有帮助，请务必：

- 👍 点赞本视频
- 💬 在评论区留下你的问题或成功注册的截图
- 🔔 订阅频道并打开小铃铛，获取最新硬核白嫖教程和科技前沿资讯！

## 参考链接

- [YouTube 视频原地址](https://www.youtube.com/watch?v=cEdCN_cY8mI)
- [博客主站](https://869hr.uk)

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/free-gpt-55tutorial-cpa--cc-switch--claude-code--s/)
