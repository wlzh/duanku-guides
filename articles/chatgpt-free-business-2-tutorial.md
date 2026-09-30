# 免费领ChatGPT Business 2个月！美区优惠码+长连接脚本教程

免费ChatGPT 2个月 Business 领取 第二期，这次是美区，绑卡用SafePal或者bybit 免费领取ChatGPT Business 2个月

> 完整图文与持续更新版本：[免费领ChatGPT Business 2个月！美区优惠码+长连接脚本教程](https://869hr.uk/2026/tech/chatgpt-free-business-2-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/chatgpt-free-business-2-tutorial/
- 更新：2026-05-13
- 分类：技术
- 专题：技术、AI
- 关键词：ChatGPT、免费、Business、优惠码、AI
- 视频：https://www.youtube.com/watch?v=gQLkDdOIzQM
- 系列：[AI 产品与技术](../series/ai-products-and-technology.md)

## 正文

<!-- 文章摘要 -->
> 
免费ChatGPT 2个月 Business 领取 第二期，这次是美区，绑卡用SafePal或者bybit...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=gQLkDdOIzQM)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 0 分钟。

免费ChatGPT 2个月 Business 领取 第二期，这次是美区，绑卡用SafePal或者bybit

免费领取ChatGPT Business 2个月！第二期美区教程来了！

本期使用美区优惠码 STRIPEATLASGPT4BIZ050126，配合长连接脚本即可生成支付链接，绑卡用SafePal或Bybit即可。

第一期教程：https://869hr.uk/2026/tech/chatgpt-team--15-1-50--48--promo/

Bybit开卡视频：https://youtu.be/3sN7P2t_CeA

步骤：
1. 登录ChatGPT
2. 打开浏览器控制台
3. 运行长连接脚本
4. 点击生成的支付链接
5. 用SafePal或Bybit绑卡完成支付

## 优惠码链接

直接点击下方链接，使用优惠码 STRIPEATLASGPT4BIZ050126：

https://chatgpt.com/?promoCode=STRIPEATLASGPT4BIZ050126

## 长连接脚本

在 ChatGPT 页面按 F12 打开浏览器控制台，粘贴以下脚本并回车运行：

```javascript
(async function () {
    console.log("⏳ 正在获取凭证并请求生成链接...");
    try {
        // 1. 动态获取当前 Access Token
        const session = await fetch("/api/auth/session").then((r) => r.json());
        if (!session.accessToken) {
            throw new Error("无法获取 Token，请确保你已登录 ChatGPT");
        }

        // 2. 构造 Payload
        const payload = {
            plan_name: "chatgptteamplan",
            team_plan_data: {
                workspace_name: "myWorkspace",
                price_interval: "month",
                seat_quantity: 2
            },
            billing_details: {
                country: "US",
                currency: "USD"
            },
            cancel_url: "https://chatgpt.com/?promoCode=STRIPEATLASGPT4BIZ050126",
            promo_code: "STRIPEATLASGPT4BIZ050126",
            checkout_ui_mode: "hosted"
        };

        // 3. 发送请求
        const response = await fetch(
            "https://chatgpt.com/backend-api/payments/checkout",
            {
                method: "POST",
                headers: {
                    Authorization: `Bearer ${session.accessToken}`,
                    "Content-Type": "application/json",
                },
                body: JSON.stringify(payload),
            }
        );

        const data = await response.json();

        // 4. 输出结果
        if (data.url) {
            console.clear();
            console.log(
                "%c✅ 成功生成支付长链接：",
                "color: #10a37f; font-size: 20px; font-weight: bold; margin-bottom: 10px;"
            );
            console.log(data.url);
            console.log(
                "\n%c(你可以直接点击上面的链接，或者复制发给别人)",
                "color: gray;"
            );
        } else {
            console.error("❌ 生成失败，服务器响应如下：", data);
            if (data.detail) console.error("错误详情:", data.detail);
        }
    } catch (e) {
        console.error("❌ 执行出错:", e);
    }
})();
```

## eSIM 与支付卡推荐
- 注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有 🔗https://869hr.uk

## 短信及语音接码平台

- 或https://smspva.com/?ref=1307601

## 白嫖流量

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

## 关注与资源

如果你觉得这期视频对你有帮助，请务必：

👍 点赞本视频

💬 在评论区留下你的问题或成功注册的截图

🔔 订阅频道并打开小铃铛，获取最新硬核白嫖教程和科技前沿资讯！
#ChatGPT #免费 #Business #优惠码 #AI #ChatGPTBusiness #美区 #SafePal #Bybit #教程

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=gQLkDdOIzQM)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/chatgpt-free-business-2-tutorial/)
