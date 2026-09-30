# 2026最新！用Gopay只需5分钟开通ChatGPT Plus，只需接两次码

log("💰 Plan : ChatGPT Plus（尝试使用 IDR / 印尼盾）"); console

> 完整图文与持续更新版本：[2026最新！用Gopay只需5分钟开通ChatGPT Plus，只需接两次码](https://869hr.uk/2026/tech/chatgpt-gopay-5-plus/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/chatgpt-gopay-5-plus/
- 更新：2026-05-31
- 分类：技术
- 专题：技术、AI
- 关键词：ChatGPT Plus、Gopay、GPT Plus 开通、ChatGPT 订阅、印尼支付
- 视频：https://www.youtube.com/watch?v=xf4uBgeK158

## 正文

<!-- 文章摘要 -->
> 
* 一个有免费试用的邮箱（微软或gmail邮箱更好）...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=xf4uBgeK158)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 11 分钟。

## 前置条件：

* Gopay APP

* 一个有免费试用的邮箱（微软或gmail邮箱更好）

* 日本节点

* hero-sms的印尼Gojek(只需接两次码，看后面焚诀)
## 准备好上面的，按下面步骤操作：

先用日本节点登录有免费试用的邮箱，如下图出现“免费试用”的就行

然后直接F12打开开发者模式选择控制台，粘贴神秘代码并回车拿到印尼长链接，神秘代码通过评论区博客文章中获取

获得支付长链接

神秘代码：

```javascript
(async function generatePlusHostedLink() {
console.log("⏳ [plus-link] 正在获取 Session Token...");
// ── 1. 获取当前登录的 Access Token ──────────────────────────────────────
let accessToken;
try {
const session = await fetch("/api/auth/session").then((r) => r.json());
accessToken = session?.accessToken;
if (!accessToken) {
throw new Error("accessToken 为空");
}
} catch (e) {
console.error("❌ [plus-link] 获取 Token 失败，请确保已登录 ChatGPT：", e.message);
return;
}
console.log("✅ [plus-link] Token 获取成功");
// ── 2. 构造请求 Payload ──────────────────────────────────────────────────
const payload = {
plan_name: "chatgptplusplan",
billing_details: {
country: "ID",
currency: "IDR",
},
cancel_url: "https://chatgpt.com/#pricing",
promo_campaign: {
promo_campaign_id: "plus-1-month-free",
is_coupon_from_query_param: false,
},
checkout_ui_mode: "hosted",
};
console.log("📦 [plus-link] 请求 Payload：");
console.log(payload);
// ── 3. 发送请求 ──────────────────────────────────────────────────────────
console.log("⏳ [plus-link] 正在请求 Stripe 长链接...");
let data;
let response;
try {
response = await fetch("https://chatgpt.com/backend-api/payments/checkout", {
method: "POST",
headers: {
Authorization: `Bearer ${accessToken}`,
"Content-Type": "application/json",
},
body: JSON.stringify(payload),
});
const text = await response.text();
try {
data = JSON.parse(text);
} catch {
console.error("❌ [plus-link] 返回内容不是 JSON：");
console.log(text);
return;
}
console.log("📨 [plus-link] HTTP 状态：", response.status);
console.log("📨 [plus-link] 原始返回：");
console.log(data);
if (!response.ok) {
console.error("❌ [plus-link] 请求失败，HTTP", response.status, data);
return;
}
} catch (e) {
console.error("❌ [plus-link] 网络请求异常：", e.message);
return;
}
// ── 4. 尝试提取 Stripe Hosted URL ────────────────────────────────────────
const hostedUrl =
data?.url ||
data?.stripe_hosted_url ||
data?.checkout_url ||
data?.redirect_url ||
data?.payment_url;
if (!hostedUrl) {
console.warn("⚠️ [plus-link] 未找到 Stripe 长链接。");
console.warn("可能原因：");
console.warn("1. OpenAI 后端没有返回 hosted checkout URL；");
console.warn("2. 当前账号地区不支持 IDR；");
console.warn("3. billing_details.currency 被后端忽略或校验失败；");
console.warn("4. promo_campaign_id 不适用于当前账号；");
console.warn("5. 返回字段名已经变化。");
console.log("📨 完整返回如下：");
console.log(data);
return;
}
console.log("─".repeat(60));
console.log("✅ [plus-link] 生成成功！");
console.log("");
console.log("📋 Checkout Session ID :", data.checkout_session_id);
console.log("🏢 Processor Entity :", data.processor_entity);
console.log("💰 Plan : ChatGPT Plus（尝试使用 IDR / 印尼盾）");
console.log("");
console.log("🔗 Stripe 长链接：");
console.log(hostedUrl);
console.log("─".repeat(60));
})();
```

* 跳转到支付页面后，按图片标注进行操作，填完账单信息不要点订阅！！！，先放着

*

*
## 现在去接码注册Gopay，我用hero-sms接码，也可以用别的

这里用Gojek的印尼号码注册去Gopay

服务选Gojek, 国家选印尼，费用选最便宜的即可，然后点击购买

购买后复制+62后面的号码，然后打开Gopay进行注册，按下面步骤注册就行

粘贴印尼号码，并继续

选择短信接码

这里是第一次接码

名字随意填写，点击创建账户

然后在这个界面，等一会，等印尼盾到账
## 注册好Gopay，1印尼盾到账后，我们进行下一步
## 现在回到刚刚GPT的支付界面 点击订阅

输入刚刚的+62后面的印尼号，如果粘贴的记得去掉括号和空格
### 重点来了！！！到下面这里先不要点绿色按钮，不然就要接三次码

*

*

现在我们回到Gopay,上面那里先放着，先去Gopay把PIN设置好

点击右下角profile，然后再点Account & app settings

进来后点Security settings

然后选Create PIN

*

自己输入6位PIN待会要用，输入完点继续

*

继续输入第一次的PIN，进行二次确认

*

注意到这里进行第二次的接码，默认会用whatsAPP接码，我们点击Try another method

*

换sms短信去接，不然接码平台收不到验证码

*

注意：第二次接码需要手动点一下刷新按钮

输入刚刚的验证码，验证过后就设置后PIN了
## 现在再点击刚才的支付界面的绿色按钮

*

点击后你会发现就不用接第三次码，第三次码也是等比较久的一个码,下面直接输入刚刚设置的PIN

*

这里直接点

这里能看到刚刚送的1rp，直接点pay now

*

这步直接点

这里需要再输一次PIN

这里直接点

*

到这里就已经成功了

*

等一会后就会看到成功订阅plus提示，大功告成！！！

邮件也会收到套餐订阅

*

2026年最新ChatGPT Plus开通教程！通过Gopay印尼支付，全程只需接两次验证码，5分钟搞定订阅。

📌 你将学到：
1. 如何用日本节点获取Stripe印尼支付链接
2. 用hero-sms接码平台注册Gopay账号
3. 只需两次接码设置PIN码的技巧
4. 用1印尼盾完成GPT Plus订阅

⚠️ 前置条件：
- Gopay APP
- 有免费试用的邮箱（微软或Gmail）
- 日本节点
- hero-sms的印尼Gojek接码服务

💡 本教程关键技巧：先在Gopay设置好PIN码，再点支付确认，这样可以省去第三次接码，大大节省时间！

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

- [YouTube视频原地址](https://www.youtube.com/watch?v=xf4uBgeK158)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/chatgpt-gopay-5-plus/)
