# ChatGPT Team 第五期！买一送一持续48个月，墨西哥18美刀+西班牙+哥伦比亚三国优惠码教程

📺 往期教程： • 第一期：ChatGPT Team 基础注册教程 • 第二期：土耳其/尼日利亚低价区教程 • 第三期：澳大利亚48个月Team优惠码+4种支付方法 • 第四期：英国优惠码半价Team教程 如有任何疑问或不会的操作，请查看前面四期视频教程

> 完整图文与持续更新版本：[ChatGPT Team 第五期！买一送一持续48个月，墨西哥18美刀+西班牙+哥伦比亚三国优惠码教程](https://869hr.uk/2026/tech/chatgpt-team-48-18-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/chatgpt-team-48-18-tutorial/
- 更新：2026-05-25
- 分类：技术
- 专题：技术、AI
- 关键词：ChatGPT、ChatGPT Team、ChatGPT Business、promo code、优惠码
- 视频：https://www.youtube.com/watch?v=2OtHK26bujM
- 系列：[AI 产品与技术](../series/ai-products-and-technology.md)

## 正文

<!-- 文章摘要 -->
> 
这是ChatGPT Business 第五期，逛论坛发现新code，如果有任何疑问的，或者不会的操作，看前面四期...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=2OtHK26bujM)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 4 分钟。

这是ChatGPT Business 第五期，逛论坛发现新code，如果有任何疑问的，或者不会的操作，看前面四期

墨西哥（18刀）： <https://chatgpt.com/?promoCode=thinkiamx>

西班牙 ： <https://chatgpt.com/?promoCode=thinkiaes>

哥伦比亚： <https://chatgpt.com/?promoCode=thinkiaco>

支付时可使用真实美国免税地址免税

短链接支付不了的，可以试试下面从别的佬那里搞来的长链接，加工了好多次，缝缝补补的能用了

使用方法（ **注意修改promoCode和货币国家**）：

F12-> console-> CTRL-V-> allow pasting-> 粘贴后回车食用

手慢无，快冲！！！

```plaintext
(async function generateAUTeamLink() {
console.log("⏳ 正在获取B Session Token...");
// 自动获取登录凭证
let accessToken;
try {
const s = await fetch("/api/auth/session").then(r => r.json());
accessToken = s?.accessToken;
if (!accessToken) throw new Error("accessToken 为空");
} catch (e) {
console.error("❌ 获取 Token 失败：", e.message);
return;
}
console.log("✅ Token 获取成功");
const COUPON = "thinkiafr";
// ---- 以下为你提供的 Payload（仅修改 workspace_name 动态生成）----
const payload = {
plan_name: "chatgptteamplan",
team_plan_data: {
workspace_name: "workspace", // 可自行修改
price_interval: "month", // month 或 year
seat_quantity: 2, // 席位数量，Team 最少 2？1的话是另外种玩法，需要号
},
billing_details: {
country: "FR",
currency: "EUR"
},
cancel_url: "https://chatgpt.com/?promoCode=thinkiafr",
promo_code: COUPON, // 注意这里用的是 promo_code 字段
checkout_ui_mode: "hosted"
};
console.log("⏳ 正在请求 Stripe 长链接 (FR)...");
try {
const resp = await fetch(
"https://chatgpt.com/backend-api/payments/checkout",
{
method: "POST",
headers: {
Authorization: `Bearer ${accessToken}`,
"Content-Type": "application/json"
},
body: JSON.stringify(payload)
}
);
const data = await resp.json();
if (!resp.ok) {
console.error(`❌ 请求失败 HTTP ${resp.status}`);
console.log("📋 响应详情：", data);
return;
}
const hostedUrl = data?.url || data?.stripe_hosted_url || data?.checkout_url;
if (!hostedUrl) {
console.warn("⚠️ 未找到长链接，原始响应：", data);
return;
}
console.log("─".repeat(60));
console.log("✅ ChatGPT Team 链接生成成功！（美国）");
console.log("📋 Checkout Session ID :", data.checkout_session_id);
console.log("📌 计划 : ChatGPT Team (US/USD)");
console.log("💺 席位 :", payload.team_plan_data.seat_quantity);
console.log("🎟️ 优惠码 :", COUPON);
console.log("🔗 Stripe 长链接：");
console.log(hostedUrl);
console.log("─".repeat(60));
} catch (e) {
console.error("❌ 网络异常：", e.message);
}
})();
```

手慢无，快冲！！！

ChatGPT Business Team 第五期优惠码教程！本期带来墨西哥、西班牙、哥伦比亚三个国家的买一送一优惠码，持续48个月，折合每人每月最低18美刀。

📌 本期优惠码：

• 墨西哥（18美刀/月）：promoCode=thinkiamx

• 西班牙：promoCode=thinkiaes

• 哥伦比亚：promoCode=thinkiaco

💡 支付技巧：使用真实美国免税地址可免消费税。

🔧 本期新增：F12控制台JS脚本一键生成Stripe长链接，短链接支付不了的可以用长链接（脚本已内置在视频中，复制粘贴即可使用）。使用方法：F12 → Console → allow pasting → 粘贴脚本回车执行。

⚡ 手慢无，优惠码数量有限，先到先得！

📺 往期教程：

• 第一期：ChatGPT Team 基础注册教程

• 第二期：土耳其/尼日利亚低价区教程

• 第三期：澳大利亚48个月Team优惠码+4种支付方法

• 第四期：英国优惠码半价Team教程

如有任何疑问或不会的操作，请查看前面四期视频教程。

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

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=2OtHK26bujM)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/chatgpt-team-48-18-tutorial/)
