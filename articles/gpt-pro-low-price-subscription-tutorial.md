# GPT Pro 超低价手把手小白订阅教程 20x 150U / 5x 88U

OpenAI GPT Pro 20x 实付 149.55 美元约 1035 元，Pro 5x 实付 88 美元约 603 元。脚本免 IP 直达菲律宾区和埃及区低价支付页面，支持 Fiat24、N26 等卡种，小白也能轻松操作。

> 完整图文与持续更新版本：[GPT Pro 超低价手把手小白订阅教程 20x 150U / 5x 88U](https://869hr.uk/2026/AI/gpt-pro-low-price-subscription-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/AI/gpt-pro-low-price-subscription-tutorial/
- 更新：2026-05-02
- 分类：ai
- 关键词：ChatGPT、教程、跨境支付、AI工具
- 视频：https://www.youtube.com/watch?v=N5qh78XZXoI

## 正文

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=N5qh78XZXoI)</div>

## 视频介绍

本视频为您带来 OpenAI 官方订阅 GPT Pro (20x/5x) 的终极低价教程。不同于普通的 IP 换区方法，本方法采用进阶脚本，直接在控制台跳过 IP 限制，直达对应低价区的支付页面，既安全又高效。

## 核心价格（实测）

- **GPT Pro 20x**（通过菲律宾区计费）：实付仅需约 149.55 美元（约合 150U / 1035 元）。本教程包含避税技巧，无需支付额外的菲区 12% 税款。
- **GPT Pro 5x**（通过埃及区计费）：实付仅需 4736 埃及币（约合 88U / 603 元）。

## 核心卖点

- 免去复杂网络环境：不需要单独购买或开启菲律宾、埃及 IP，使用脚本直接跳转。
- 直连官方支付页面：通过脚本直达 OpenAI 官网的 low-cost 区计费页面，权威渠道。
- 小白一键进阶：无需代码基础，按照步骤在浏览器控制台复制粘贴即可。

## 支付卡实测情况（重要）

**支持的卡（亲测可行）：** Fiat24、N26、EtherFi、小红卡、Savo

**被拒的卡（请勿测试）：** 国内 Visa/MasterCard 单币信用卡、银联卡、Wise（实体/虚拟）、Revolut

其他卡种由于没有测试，请自行尝试。

## 教程步骤

1. 开启您的网络工具（推荐直连，之前的测试表明香港 IP 可能会导致支付不成功，但使用脚本可跳过此限制，具体免 IP 方法见视频演示）。
2. 登录 ChatGPT 官网（chatgpt.com）。
3. 按 F12 打开浏览器控制台（Console）。
4. 根据您想订阅的套餐（20x 或 5x），复制下方对应的脚本代码，粘贴到控制台并回车。

## VPN 方法详解

### Pro 20x（菲律宾区）

1. 开启菲律宾的网络环境
2. 打开浏览器，登录 ChatGPT 官网
3. 点击左下角升级套餐，选择 Pro 20x
4. 价格显示 9990 披索（而不是 200 美元）
5. **账单地址一定要选择美国**，选一个免税州（俄勒冈州、特拉华州、蒙大拿州等）
6. 用 Fiat24 或 N26 的卡支付
7. 最终实付 149.55 美元，省下约 50 美元

### Pro 5x（埃及区）

1. 把 VPN 切换到埃及节点
2. 登录 ChatGPT 官网，选择 Pro 5x 套餐
3. 价格显示为 4736 埃及镑，折合人民币约 603 元
4. 同样账单地址选美国
5. 用 Fiat24、N26、EtherFi 等卡支付

## 脚本方法（免 IP）

不需要 VPN，也不需要切换 IP，直接在浏览器控制台执行脚本即可跳转到对应国家的支付页面。

### 操作步骤

1. 用浏览器打开 chatgpt.com，确保已登录
2. 按 F12 打开浏览器控制台（笔记本电脑可能需要同时按住 Fn 键再按 F12）
3. 找到 Console 选项卡，点击它
4. 复制对应脚本，粘贴到控制台，按回车
5. 自动跳转到对应国家的支付页面
6. 账单地址选美国免税州，用卡支付即可

### GPT Pro 5x 脚本（埃及区）

复制如下脚本 → 打开 [chatgpt.com](http://chatgpt.com/) → F12 打开控制台 → 粘贴脚本回车

```javascript
javascript:(async function(){try{const t=await(await fetch("/api/auth/session")).json();if(!t.accessToken){alert("请先登录 ChatGPT！");return}const p={"entry_point":"all_plans_pricing_modal","plan_name":"chatgptprolite","billing_details":{"country":"EG","currency":"EGP"},"checkout_ui_mode":"custom"};const r=await fetch("https://chatgpt.com/backend-api/payments/checkout",{method:"POST",headers:{Authorization:"Bearer "+t.accessToken,"Content-Type":"application/json"},body:JSON.stringify(p)});const d=await r.json();d.checkout_session_id?window.location.href="https://chatgpt.com/checkout/openai_llc/"+d.checkout_session_id:alert("提取失败："+(d.detail||JSON.stringify(d)))}catch(e){alert("发生错误："+e)}})();
```

### GPT Pro 20x 脚本（菲律宾区）

```javascript
javascript:(async function(){try{const t=await(await fetch("/api/auth/session")).json();if(!t.accessToken){alert("请先登录 ChatGPT！");return}const p={"entry_point":"all_plans_pricing_modal","plan_name":"chatgptpro","billing_details":{"country":"PH","currency":"PHP"},"checkout_ui_mode":"custom"};const r=await fetch("https://chatgpt.com/backend-api/payments/checkout",{method:"POST",headers:{Authorization:"Bearer "+t.accessToken,"Content-Type":"application/json"},body:JSON.stringify(p)});const d=await r.json();d.checkout_session_id?window.location.href="https://chatgpt.com/checkout/openai_llc/"+d.checkout_session_id:alert("提取失败："+(d.detail||JSON.stringify(d)))}catch(e){alert("发生错误："+e)}})();
```

## 注意事项

1. 这个方法的核心是利用了 OpenAI 在不同国家的定价差异，价格差异可能随时变化，建议趁早操作。
2. 如果没有 Fiat24 或 N26 的卡，建议先去申请一张。
3. 如果支付被拒，可以试试换一张卡或者换一个浏览器再试。

## 参考链接

- YouTube 视频：https://youtu.be/N5qh78XZXoI
- 博客主页：https://869hr.uk
- 微信讨论群：https://qr.869hr.uk/aitech
- Telegram 群聊：https://t.me/tgmShareAI
- 推特：https://x.com/gxjdian
- YouTube 频道：https://youtube.com/@gxjdian

## 相关推荐

- [ChatGPT Plus 教程](https://869hr.uk/6-chatgpt-plus-tutorial/)
- [美国 IP 使用 Claude 和 ChatGPT](https://869hr.uk/8-usa-ip-50-claude-chatgpt/)
- [ChatGPT 降级教程](https://869hr.uk/chatgpt-downgrade/)

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/AI/gpt-pro-low-price-subscription-tutorial/)
