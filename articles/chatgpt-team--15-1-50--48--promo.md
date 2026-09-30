# 48个月半价Team优惠码 一个人50人民币， 英国优惠码（可能是目前最低的），手把手保姆教程

本视频实测成功开通 ChatGPT Team 计划，实现目前已知最低价格：15.21/人月付，平均一人每个月50人民币，使用英国优惠码codestonegb获得48个月半价优惠

> 完整图文与持续更新版本：[48个月半价Team优惠码 一个人50人民币， 英国优惠码（可能是目前最低的），手把手保姆教程](https://869hr.uk/2026/tech/chatgpt-team--15-1-50--48--promo/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/chatgpt-team--15-1-50--48--promo/
- 更新：2026-05-10
- 分类：技术
- 关键词：ChatGPT、跨境支付、教程
- 视频：https://www.youtube.com/watch?v=yv1HFb79Yus

## 正文

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=yv1HFb79Yus)</div>

注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有。

## 核心信息（实测数据）

- **最终开通金额：** $15.21/人（月付，从英镑折算），平均一人每个月 50 人民币
- **优惠：** 48 个月半价（使用英国 promo 码：codestonegb）
- **实测工具：** 英国节点、美国免税州地址生成器、SafePal Fiat24 银行卡
- **关键步骤：** 在浏览器控制台执行 JavaScript 代码，修改支付负载（Billing Country: GB, Currency: GBP, promo_code: codestonegb）来生成 Stripe 的托管支付链接

## 长连接 + Fiat24 + 非家宽英国节点 + 美国免税地址 开通成功

扣款 **$15.21**

注意，长连接要用下面代码，要换 GB + 新的优惠码

## 手把手小白教程（详细步骤）

### 第1步：准备工作（节点与账号）

1. `英国优惠码链接：https://chatgpt.com/?promoCode=codestonegb`，注册账户，并支付

![](<images/48个月半价Team优惠码 一个人50人民币， 英国优惠码（可能是目前最低的），手把手保姆教程-iShot_2026-05-10_10.28.15.png>)

- 英国节点，对纯净度没有要求，我使用的 Cloudflare 的 Warp 的英国 IP 顺利通过支付
- 美国地址生成器，免税州填写账单地址
- 使用 SafePal 的 Fiat24 银行卡支付成功，使用 bybit 卡或者 SafePal，之前都发过教程：https://youtu.be/3sN7P2t_CeA?si=i3B02mc-9nR3eNQN

### 第2步：获取美国免税地址

使用美国地址生成器，选择一个免税州（如 Delaware, Oregon）生成一个账单地址，备用。为什么要美国地址？因为 Stripe 支付会根据你的账单地址来计算税费，如果使用免税州的地址，就可以省掉额外的税费。

### 第3步：准备支付工具

我们实测使用 SafePal Fiat24 银行卡支付成功。请确保你的卡内有足够的英镑或等值货币。

### 第4步：控制台魔法（生成 Stripe 长连接）

登录 ChatGPT 后，在支付页面，按下浏览器 F12，打开 Console（控制台）。

长连接获取，浏览器中 F12，Console，如图

![](<images/48个月半价Team优惠码 一个人50人民币， 英国优惠码（可能是目前最低的），手把手保姆教程-image.png>)

通过执行下面代码，获取 Stripe 长连接 URL：

```javascript
(async function generateTeamHostedLink() {
  console.log("⏳ [team-link] 正在获取 Session Token...");

  let accessToken;
  try {
    const session = await fetch("/api/auth/session").then((r) => r.json());
    accessToken = session?.accessToken;
    if (!accessToken) throw new Error("accessToken 为空");
  } catch (e) {
    console.error("❌ [team-link] 获取 Token 失败，请确保已登录 ChatGPT：", e.message);
    return;
  }

  console.log("✅ [team-link] Token 获取成功");

  const payload = {
    plan_name: "chatgptteamplan",
    team_plan_data: {
      workspace_name: "MyTeam",
      price_interval: "month",
      seat_quantity: 2,
    },
    billing_details: {
      country: "GB",
      currency: "GBP",        // ← 关键修改
    },
    cancel_url: "https://chatgpt.com/#team-pricing",
    promo_code: "codestonegb",
    checkout_ui_mode: "hosted",
  };

  console.log("⏳ [team-link] 正在请求 Stripe 长链接...");
  let data;
  try {
    const response = await fetch(
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

    data = await response.json();

    if (!response.ok) {
      console.error("❌ [team-link] 请求失败，HTTP", response.status);
      console.error(data);
      return;
    }
  } catch (e) {
    console.error("❌ [team-link] 网络请求异常：", e.message);
    return;
  }

  const hostedUrl = data?.url || data?.stripe_hosted_url || data?.checkout_url;

  if (!hostedUrl) {
    console.warn("⚠️ [team-link] 未找到长链接，原始响应如下：");
    console.log(data);
    return;
  }

  console.log("─".repeat(60));
  console.log("✅ [team-link] 生成成功！codestonegb promo 已生效");
  console.log("📋 Checkout Session ID :", data.checkout_session_id);
  console.log("🏢 Plan : ChatGPT Team（codestonegb）");
  console.log("👥 Seats :", payload.team_plan_data.seat_quantity);
  console.log("");
  console.log("🔗 Stripe 长链接：");
  console.log(hostedUrl);
  console.log("─".repeat(60));
  console.log("💡 提示：打开后检查优惠是否生效");
})();
```

获取到 URL，打开 URL，即可填写银行信息，及账单的美国免税地址

![](<images/48个月半价Team优惠码 一个人50人民币， 英国优惠码（可能是目前最低的），手把手保姆教程-image-1.png>)

就可以支付成功了。

![](<images/48个月半价Team优惠码 一个人50人民币， 英国优惠码（可能是目前最低的），手把手保姆教程-image-2.png>)

### 第5步：完成支付

使用 bybit 卡或者 SafePal，之前都发过教程：https://youtu.be/3sN7P2t_CeA?si=i3B02mc-9nR3eNQN

- 代码执行成功后，控制台会输出一个 Stripe 的长链接
- 复制这个链接并在浏览器中打开
- 在此页面填写你的银行卡信息，以及第 2 步准备的美国免税账单地址
- 确认金额无误（应为英镑折算后的低价），点击支付，即可开通成功

## 关键资源链接

- 英国优惠码链接：https://chatgpt.com/?promoCode=codestonegb

## 免责声明

本教程仅供技术交流和参考，请确保您的操作符合相关平台的用户协议。本操作涉及修改代码和跨境支付，请谨慎操作并自行承担风险。优惠信息可能随时发生变化，请注意实测。

---

## 短信及语音接码平台

- https://hero-sms.com/?ref=357885
- https://smspva.com/?ref=1307601

## 白嫖流量

- 500M 试用，链接 https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN，85 折优惠
- 200M 试用，链接 https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码 GXJDIAN，9 折优惠

---

## 关注与资源

1. 微信讨论群：https://qr.869hr.uk/aitech
2. 超过 100T 资料总站网站：https://doc.869hr.uk
3. Telegram 群聊：https://t.me/tgmShareAI
4. 微信公众号：搜「AI前沿的短裤哥」
5. 视频的文字博客（银行卡、手机号、VPS 主机、IP 测试等）：https://869hr.uk
6. 推特：https://x.com/gxjdian
7. YouTube：https://youtube.com/@gxjdian

## VPS 主机等

- Claude 用的丽萨主机：https://lisahost.com/aff.php?aff=9424
- 按流量 VPS：https://www.lycheeip.com/home/ip?affId=1AwYIQ7BW8
- 一年 10 美元的多年保底小鸡：https://clients.zgovps.com/?affid=1207
- 各种云主机，主打性价比：https://my.racknerd.com/aff.php?aff=15809
- 美国的 VPS，一年 70 美金搞活动：https://app.cloudcone.com/?ref=13794
- 一年 8.5 美金的美国家宽，稳定靠谱：https://www.webshare.io/?referral_code=55vpv6waorud

**VPS DMIT：** https://www.dmit.io/aff.php?aff=21728

**VPS VIRCS：** 家宽落地机 https://www.vircs.com/welcome?vcd=61a4aae4

- 家宽 IP 链接：https://ipfly.net/activity/OE5TWVlUUEI6TFZKOVhYQzM5NQ==
- 住宅 VPS 链接：https://www.voyracloud.com/?ref_code=5ZG4FHL8

## Gmail、Telegram 等账号购买、礼品卡、Claude 充值 AI 产品

- https://accboy7gxjdian.acceboy.com/
- https://universalbus.cn/?s=bvDplWi2fZ
- https://www.gamsgo.com/partner/jGh24

**Claude、OpenAI Codex 等充值：** https://bewild.ai?code=GXJDIAN

## eSIM 相关

1. 三家 eSIM 让国产手机秒变 eSIM 手机，全方面优缺点对比及开户链接 https://s.869hr.uk/mcc
2. eSIM 9eSIM 打 9 折（优惠码：maq）注册及购买链接 https://www.9esim.com/?coupon=maq
3. eSIM ESTK 打 9 折（优惠码：GXJDIAN）注册及购买链接 https://store.estk.me/zh?aid=16007
4. eSIM XeSIM 打 9 折（推荐码：gxjdian）注册及购买链接 https://xesim.cc/?DIST=RE5FHg==
5. Wise 的申请链接及教程链接（有身份证就可，推荐码：lizhiw12）
   - 教程链接：https://x.com/wlzh/status/19967997897...
   - 申请链接：https://wise.com/invite/ihpc/lizhiw12
6. N26 的申请链接及教程链接（需要护照，推荐码：lizhiw02766c）https://youtu.be/HY9OD8rX89s?si=78REb8MyKSJB6cwQ
7. Bybit 支付卡申请链接 https://www.bybit.com/invite?ref=LGNQRG，教程链接 https://youtu.be/3sN7P2t_CeA

## 相关专辑

- AI 产品&技术相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海 VPS 相关专辑：https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

---

## 关注我不迷路

如果你觉得这期视频对你有帮助，请务必：

- 点赞本视频
- 在评论区留下你的问题或成功注册的截图
- 订阅频道并打开小铃铛，获取最新硬核白嫖教程和科技前沿资讯

## 参考链接

- [YouTube 视频原地址](https://www.youtube.com/watch?v=yv1HFb79Yus)
- [博客主页](https://869hr.uk)

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/chatgpt-team--15-1-50--48--promo/)
