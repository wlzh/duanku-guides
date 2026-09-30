# ChatGPT Business 第三期｜澳大利亚48个月Team优惠码$17.8/月，4种支付含PayPal

本文介绍 ChatGPT Business 澳大利亚 Team 优惠的适用条件、价格与四种支付方式，并补充 PayPal 付款步骤和开通前核对事项。

> 完整图文与持续更新版本：[ChatGPT Business 第三期｜澳大利亚48个月Team优惠码$17.8/月，4种支付含PayPal](https://869hr.uk/2026/tech/chatgpt-business-48-team-17-8-4-payment-paypal/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/chatgpt-business-48-team-17-8-4-payment-paypal/
- 更新：2026-05-15
- 分类：技术
- 专题：技术、AI
- 关键词：ChatGPT Business、ChatGPT Team、ChatGPT 优惠码、ChatGPT 澳大利亚、ChatGPT 订阅
- 视频：https://www.youtube.com/watch?v=EJnGTrFy5Sk
- 系列：[AI 产品与技术](../series/ai-products-and-technology.md)

## 正文

<!-- 文章摘要 -->
> 
免费ChatGPT 2个月 Business 领取 第期，这次是澳大利亚，需要澳大利亚节点，优惠如图...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=EJnGTrFy5Sk)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 5 分钟。

免费ChatGPT 2个月 Business 领取 第期，这次是澳大利亚，需要澳大利亚节点，优惠如图

绑卡的话还是跟一期一样，SafePal或者bybit都可，这两个卡，https://869hr.uk的博客和油管频道里面都有讲过如何开卡，bybit开卡视频https://youtu.be/3sN7P2t_CeA

3、第三种支付办法，用YPT卡，绑到apple pay上，把长连接生成的stripe链接，复制到手机上支付也可

4、 第四种支付办法，如果你有Paypal，则使用如下脚本运行长连接生成支付链接，则打开的支付链接有Paypal支付方式

```javascript

(async function generateAUTeamLink() {

const DEFAULT_PROMO_CODE = "STRIPEATLASGPT4BIZ050126";

// 优先读取当前页面 URL 参数中的 promoCode，没有则使用默认值

const PROMO_CODE =

new URLSearchParams(location.search).get("promoCode")?.trim() ||

DEFAULT_PROMO_CODE;

console.log("正在获取 Session Token...");

let accessToken;

try {

// 获取当前登录 session

const sessionResp = await fetch("/api/auth/session", {

credentials: "include",

});

if (!sessionResp.ok) {

throw new Error(`Session 请求失败 HTTP ${sessionResp.status}`);

}

const session = await sessionResp.json();

accessToken = session?.accessToken;

if (!accessToken) {

throw new Error("accessToken 为空");

}

} catch (e) {

console.error("获取 Token 失败：", e.message);

return;

}

console.log("Token 获取成功");

// 构造支付请求参数

const payload = {

plan_name: "chatgptteamplan",

team_plan_data: {

workspace_name: `workspace-${Date.now()}`,

price_interval: "month",

seat_quantity: 2,

},

billing_details: {

country: "AU",

currency: "AUD", // 修复错误引号

},

cancel_url: `https://chatgpt.com/?promoCode=${encodeURIComponent(

PROMO_CODE

)}`,

promo_code: PROMO_CODE,

checkout_ui_mode: "hosted",

};

console.log("正在请求 Stripe 长链接...");

try {

const resp = await fetch(

"https://chatgpt.com/backend-api/payments/checkout",

{

method: "POST",

headers: {

Authorization: `Bearer ${accessToken}`,

"Content-Type": "application/json",

},

body: JSON.stringify(payload),

}

);

let data;

try {

data = await resp.json();

} catch {

data = null;

}

// 检查请求状态

if (!resp.ok) {

console.error(`请求失败 HTTP ${resp.status}`);

console.log("响应详情：", data);

return;

}

// 提取 Stripe Hosted Checkout URL

const hostedUrl =

data?.url ||

data?.stripe_hosted_url ||

data?.checkout_url ||

null;

if (!hostedUrl) {

console.warn("未找到 Stripe 长链接，原始响应：", data);

return;

}

// 输出成功信息

console.log("=".repeat(60));

console.log("✅ ChatGPT Team 链接生成成功");

console.log("Checkout Session ID:", data?.checkout_session_id || "N/A");

console.log("计划:", "ChatGPT Team");

console.log(

"国家/币种:",

`${payload.billing_details.country}/${payload.billing_details.currency}`

);

console.log("席位:", payload.team_plan_data.seat_quantity);

console.log("优惠码:", PROMO_CODE);

console.log("Stripe 长链接:");

console.log(hostedUrl);

console.log("=".repeat(60));

} catch (e) {

console.error("网络异常：", e.message);

}

})();

```

支付价格如下图

步骤不再详细讲了，看第一期视频，只是优惠码链接变了，及长连接脚本变了，看下面这两个
1. 澳大利亚优惠码链接 https://chatgpt.com/?promoCode=chieftnsau
2. 长连接脚本

```javascript

(async function () {

console.log(“

正在为 chieftnsau 生成澳大利亚版支付长链接…”);

try {

const session = await fetch(“/api/auth/session”).then((r) => r.json());

if (!session.accessToken) {

throw new Error(“无法获取 Token，请确保已登录 ChatGPT”);

}

const payload = {

plan_name: “chatgptteamplan”,

team_plan_data: {

workspace_name: “myWorkspace”,

price_interval: “month”,

seat_quantity: 2

},

billing_details: {

country: “AU”, // 澳大利亚专用

currency: “AUD” // 澳元

},

cancel_url: “https://chatgpt.com/?promoCode=chieftnsau”,

promo_code: “chieftnsau”,

checkout_ui_mode: “hosted”

};

const response = await fetch(

“https://chatgpt.com/backend-api/payments/checkout”,

{

method: “POST”,

headers: {

Authorization: Bearer ${session.accessToken},

“Content-Type”: “application/json”,

},

body: JSON.stringify(payload),

}

);

const data = await response.json();

if (data.url) {

console.clear();

console.log(“%c

成功生成带 chieftnsau 优惠的长链接：
- ”, “color: #10a37f
- font-size: 22px
- font-weight: bold
- ”)

console.log(data.url);

console.log(“

%c直接点开这个链接 → 应该能看到 AU$25 左右（2席位，48个月锁定）澳大利亚优惠价格”, “color:
- gray
- font-size: 16px
- ”)

} else {

console.error(“

生成失败，响应：”, data);

}

} catch (e) {

console.error(“

执行出错:”, e);

}

})();

```

通过Chrome浏览器里面，f12，进入console，输入长连接脚本，生成stripe的支付链接，拷贝出来，然后打开链接，填入银行卡进行支付，如果使用苹果手机，用apple pay支付的话，把链接，复制到手机上，用浏览器打开，

支付成功如下图

ChatGPT Business 第三期来了！这次是澳大利亚 48 个月 Team 订阅，优惠码可用，折合仅 $17.8/月。本期新增 PayPal 支付方式，达到共 4 种支付办法，上车更方便！

📌 优惠码链接：

https://chatgpt.com/?promoCode=chieftnsau

💰 本期亮点：

• 澳大利亚区域 48 个月 Team 订阅

• 仅需约 AU$25/2席位/月（折合 $17.8 美元）

• 4 种支付方式全支持

💳 4 种支付办法：

1️⃣ SafePal 或 Bybit 虚拟卡（前两期讲过开卡教程）

2️⃣ YPT 卡绑定 Apple Pay 支付

3️⃣ 长连接生成 Stripe 链接 → 手机 Apple Pay 支付

4️⃣ ✅ 新增：PayPal 支付（使用更新后的长连接脚本）

🔧 使用步骤：
1. 打开优惠码链接 https://chatgpt.com/?promoCode=chieftnsau
2. F12 打开浏览器控制台(Console)
3. 粘贴本期提供的长连接脚本
4. 生成的 Stripe 链接选择 PayPal 或银行卡支付
5. 支付成功后即可开通 ChatGPT Team

⚡ 优惠码：chieftnsau

📖 详细图文教程：https://869hr.uk

0:00 scene-01-开场介绍

1:00 scene-02-chatgpt-team澳大利亚区介绍

1:30 scene-03-4种支付方式总览

2:10 scene-04-脚本一-通用版stripe长连接生成

2:40 scene-05-优惠展示图

3:10 scene-06-使用专属优惠码chieftnsau

3:50 scene-07-脚本二-chieftnsau专用版

4:20 scene-08-支付价格与成功图

4:50 scene-09-资源汇总

5:10 scene-10-结尾总结

6:10 scene-11-关注与订阅

注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有 🔗https://869hr.uk

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

如果你觉得这期视频对你有帮助，请务必：

👍 点赞本视频

💬 在评论区留下你的问题或成功注册的截图

🔔 订阅频道并打开小铃铛，获取最新硬核白嫖教程和科技前沿资讯！
#ChatGPT #ChatGPTBusiness #ChatGPTTeam #AI #人工智能

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=EJnGTrFy5Sk)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/chatgpt-business-48-team-17-8-4-payment-paypal/)
