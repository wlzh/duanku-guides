# Gmail搞免费GPT账户｜K12空间白嫖ChatGPT Plus全流程 喂饭级教程

多了登录gpt会报错，脚本中的空间ID现在人数人多，可以自己找最新的gmail的K12空间id，进行替换，linuxdo等很多站很多分享的

> 完整图文与持续更新版本：[Gmail搞免费GPT账户｜K12空间白嫖ChatGPT Plus全流程 喂饭级教程](https://869hr.uk/2026/tech/chatgpt-gmail-free-gpt-k12-plus-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/chatgpt-gmail-free-gpt-k12-plus-tutorial/
- 更新：2026-07-03
- 分类：技术
- 专题：技术、AI
- 关键词：ChatGPT、免费GPT、K12空间、Gmail别名、ChatGPT Plus
- 视频：https://www.youtube.com/watch?v=tuPU2TQXNbI

## 正文

<!-- 文章摘要 -->
> 
【K12 】通过Gmail 搞免费GPT账户 - 喂饭级教程，不适合小白...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=tuPU2TQXNbI)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 6 分钟。

【K12 】通过Gmail 搞免费GPT账户 - 喂饭级教程，不适合小白

写在前面

因为很多人拿到GPT空间id不知道怎么用

辛苦做的视频，防止又被人说刷流量

说三编！！！不适合完全没概念的小白，不适合完全没概念的小白，不适合完全没概念的小白

一个gmail支持创建5个别名邮箱

多了登录gpt会报错，脚本中的空间ID现在人数人多，可以自己找最新的gmail的K12空间id，进行替换，linuxdo等很多站很多分享的

注意每个账号

开无痕登录账号，登录后不要退出账号，直接关闭页面，再开无痕再登录新的账号

注意outlook的不适用

得是gmail的空间id才行，大家有新的gmail空间id也欢迎评论区留言进行分享，分享给更多小伙伴

操作步骤
1.打开GPT官网 使用 gmail 账号进行登录

如图 使用邮箱别名注册，会转发到你的gmail邮箱
2.到邮箱输入验证码

完成账号创建
3.F12开启控制台

输入如下脚本内容，回车，等待脚本运行成功，空间ID有的话可以替换脚本中的，目前现在脚本中的实测可用

```javascript
// ==UserScript==
// @name ChatGPT Workspace Join Request
// @namespace https://chatgpt.com/
// @version 4.0.0
// @description 子号自动从 /api/auth/session 获取当前登录账号 AT，向母号 workspace 发送加入申请（request）或接受邀请（accept）。只需 workspace ID，UI 可编辑保存。
// @author you
// @match https://chatgpt.com/*
// @run-at document-idle
// @grant none
// ==/UserScript==
(function () {
"use strict";
// ===================== 默认配置 =====================
const DEFAULTS = {
workspaceIds: "a0a16bc9-e1b1-45f0-b269-812b53f60121",
intervalMs: 1500,
maxRetries: 3,
retryBackoffMs: 5000,
sessionPollMs: 20000,
panelWidth: 400,
};
const STORE_KEY = "jr_config_v4";
function loadConfig() {
let saved = {};
try { saved = JSON.parse(localStorage.getItem(STORE_KEY) || "{}"); } catch (_) {}
return Object.assign({}, DEFAULTS, saved);
}
function saveConfig(cfg) {
try { localStorage.setItem(STORE_KEY, JSON.stringify(cfg)); } catch (_) {}
}
let CONFIG = loadConfig();
// ---------- 状态 ----------
const STATE = {
at: "",
session: null,
deviceId: crypto.randomUUID(),
autoRan: false,
running: false,
};
// ---------- /api/auth/session ----------
async function fetchSession() {
const res = await fetch("/api/auth/session", {
headers: { accept: "*/*" },
credentials: "include",
});
if (!res.ok) throw new Error(`session HTTP ${res.status}`);
return res.json();
}
function decodeJwt(at) {
try {
const p = at.split(".")[1];
const j = JSON.parse(atob(p.replace(/-/g, "+").replace(/_/g, "/")));
const auth = j["https://api.openai.com/auth"] || {};
const prof = j["https://api.openai.com/profile"] || {};
return {
account_id: auth.chatgpt_account_id || "",
email: prof.email || "",
plan_type: auth.chatgpt_plan_type || "",
exp: j.exp || 0,
};
} catch (_) { return {}; }
}
function fmtExp(exp) {
if (!exp) return "?";
const min = Math.round((exp * 1000 - Date.now()) / 60000);
if (min > 60) return `剩余 ${Math.round(min/60)} 小时`;
return `剩余 ${min} 分钟`;
}
async function refreshSession() {
try {
const s = await fetchSession();
const at = s.accessToken || "";
if (at && at !== STATE.at) {
STATE.at = at;
STATE.session = s;
const info = decodeJwt(at);
log(`子号 AT 已更新: ${info.email || "?"}`, "ok");
updateUserBar(info, "ok");
onATReady();
} else if (!at) {
updateUserBar(null, "warn");
}
} catch (e) {
log(`session 获取失败: ${e.message}`, "warn");
updateUserBar(null, "err");
}
}
// ---------- 发请求 ----------
async function sendOne(wsId, route, attempt) {
attempt = attempt || 0;
const url = `/backend-api/accounts/${wsId}/invites/${route}`;
const headers = {
accept: "*/*",
authorization: "Bearer " + STATE.at,
"content-type": "application/json",
"oai-device-id": STATE.deviceId,
"oai-language": navigator.language || "en-US",
};
log(`→ POST /accounts/${wsId.slice(0,8)}/invites/${route} (第 ${attempt+1} 次)`);
try {
const res = await fetch(url, {
method: "POST", headers, body: "", mode: "cors", credentials: "include",
});
const text = await res.text();
if (res.ok) {
log(`✓ ${wsId.slice(0,8)} HTTP ${res.status}: ${text}`, "ok");
return true;
}
log(`✗ ${wsId.slice(0,8)} HTTP ${res.status}: ${text.slice(0,180)}`, "warn");
if (res.status === 401 || res.status === 403) {
log("子号 AT 失效，刷新 session...", "warn");
STATE.at = "";
await refreshSession();
if (attempt < CONFIG.maxRetries) {
await sleep(2000);
return sendOne(wsId, route, attempt + 1);
}
return false;
}
if (attempt < CONFIG.maxRetries) {
await sleep(CONFIG.retryBackoffMs * (attempt + 1));
return sendOne(wsId, route, attempt + 1);
}
return false;
} catch (e) {
log(`网络错误: ${e.message}`, "err");
if (attempt < CONFIG.maxRetries) {
await sleep(CONFIG.retryBackoffMs);
return sendOne(wsId, route, attempt + 1);
}
return false;
}
}
function parseWorkspaceIds() {
return CONFIG.workspaceIds.split(/[
,]+/).map(s => s.trim()).filter(Boolean);
}
async function runAll(route) {
if (STATE.running) { log("正在运行中，请稍候", "warn"); return; }
if (!STATE.at) {
log("无可用 AT，刷新 session...", "warn");
await refreshSession();
if (!STATE.at) { log("仍未取到 AT，请先登录 chatgpt.com", "err"); return; }
}
const ids = parseWorkspaceIds();
if (!ids.length) { log("未配置 workspace ID", "err"); return; }
STATE.running = true;
setBtns(false);
log(`开始处理 ${ids.length} 个 workspace（${route}）`, "info");
let ok = 0;
for (const ws of ids) {
const r = await sendOne(ws, route);
if (r) ok++;
if (ids.length > 1) await sleep(CONFIG.intervalMs);
}
log(`完成：成功 ${ok}/${ids.length}`, ok === ids.length ? "ok" : "warn");
STATE.running = false;
setBtns(true);
}
function onATReady() {
if (!STATE.autoRan) {
STATE.autoRan = true;
runAll("request");
}
}
function sleep(ms) { return new Promise(r => setTimeout(r, ms)); }
// ---------- UI ----------
let panelBody, userBarEl, reqBtnEl, accBtnEl, wsInputEl, saveBtnEl, dirty = false;
function setBtns(enabled) {
[reqBtnEl, accBtnEl].forEach(b => {
if (b) { b.disabled = !enabled; b.style.opacity = enabled ? "1" :
- "0.5"
- }
});
}
function updateUserBar(info, status) {
if (!userBarEl) return;
const c = { ok: "#2f855a", warn: "#b7791f", err: "#c53030" };
if (info && info.email) {
userBarEl.innerHTML =
`<span style="color:${c.ok}">●</span> <b>${info.email}</b> · ${info.plan_type||"?"} · ` +
`<code style="background:
- #edf2f7
- padding:1px 4px
- border-radius:3px">${(info.account_id||"").slice(0,8)}</code> · ` +
`<span style="color:#718096">${fmtExp(info.exp)}</span>`;
} else {
const msg = status === "err" ? "session 获取失败，请确认已登录" : "未检测到 AT，等待登录...";
userBarEl.innerHTML = `<span style="color:${c[status]||c.warn}">●</span> ${msg}`;
}
}
function markDirty() {
dirty = true;
if (saveBtnEl) {
saveBtnEl.textContent = "保存 *";
saveBtnEl.style.background = "#d69e2e";
saveBtnEl.style.color = "#fff";
}
}
function markClean() {
dirty = false;
if (saveBtnEl) {
saveBtnEl.textContent = "已保存";
saveBtnEl.style.background = "#38a169";
saveBtnEl.style.color = "#fff";
}
setTimeout(() => {
if (!dirty && saveBtnEl) {
saveBtnEl.textContent = "保存";
saveBtnEl.style.background = "#edf2f7";
saveBtnEl.style.color = "#4a5568";
}
}, 1500);
}
function buildPanel() {
const css = `
.jr-panel{position:
- fixed
- top:14px
- right:14px
- width:${CONFIG.panelWidth}px
background:
- #fff
- border:1px solid #e2e8f0
- border-radius:14px
box-shadow:
- 0 12px 32px rgba(0,0,0,.16)
- z-index:99999
font:
- 13px/1.55 -apple-system,BlinkMacSystemFont,"Segoe UI",sans-serif
- color:#1a202c
- overflow:hidden}
.jr-head{padding:
- 11px 16px
- background:linear-gradient(135deg,#3182ce,#2b6cb0)
- color:#fff
display:
- flex
- justify-content:space-between
- align-items:center}
.jr-title{font-weight:
- 600
- font-size:13px
- letter-spacing:.3px
- display:flex
- align-items:center
- gap:6px}
.jr-title svg{width:
- 16px
- height:16px
- fill:#fff}
.jr-ver{font-size:
- 11px
- opacity:.85
- background:rgba(255,255,255,.2)
- padding:1px 6px
- border-radius:8px}
.jr-sub{padding:
- 9px 16px
- background:#f7fafc
- border-bottom:1px solid #edf2f7
- font-size:12px
- color:#4a5568
- min-height:22px}
.jr-sec{padding:
- 12px 16px
- border-bottom:1px solid #edf2f7}
.jr-label{display:
- flex
- justify-content:space-between
- align-items:center
- font-size:11px
- color:#718096
margin-bottom:
- 6px
- font-weight:600
- letter-spacing:.4px
- text-transform:uppercase}
.jr-label .jr-count{font-size:
- 10px
- color:#a0aec0
- font-weight:400
- text-transform:none
- letter-spacing:0}
.jr-ta{width:
- 100%
- box-sizing:border-box
- border:1px solid #e2e8f0
- border-radius:8px
padding:
- 8px 10px
- font:12px/1.5 monospace
- color:#2d3748
- background:#fff
- transition:.15s
- min-height:64px
- resize:vertical}
.jr-ta:
- focus{outline:0
- border-color:#3182ce
- box-shadow:0 0 0 3px rgba(49,130,206,.12)}
.jr-save-row{display:
- flex
- justify-content:flex-end
- margin-top:8px}
.jr-body{padding:
- 10px 16px
- max-height:36vh
- overflow:auto}
.jr-foot{padding:
- 10px 16px
- border-top:1px solid #edf2f7
- display:flex
- gap:8px
- justify-content:flex-end
- flex-wrap:wrap}
.jr-line{padding:
- 3px 0
- word-break:break-all
- border-bottom:1px dashed #f1f5f9}
.jr-line:last-child{border-bottom:0}
.jr-info{color:#2b6cb0}.jr-ok{color:#2f855a}.jr-warn{color:#b7791f}.jr-err{color:#c53030}
.jr-btn{cursor:
- pointer
- border:0
- border-radius:7px
- padding:7px 14px
- font-size:12px
- font-weight:500
- transition:.15s}
.jr-btn-primary{background:
- #3182ce
- color:#fff}.jr-btn-primary:hover{background:#2b6cb0}
.jr-btn-green{background:
- #38a169
- color:#fff}.jr-btn-green:hover{background:#2f855a}
.jr-btn-ghost{background:
- #edf2f7
- color:#4a5568}.jr-btn-ghost:hover{background:#e2e8f0}
.jr-btn:
- disabled{cursor:not-allowed
- opacity:.5}
.jr-hint{font-size:
- 11px
- color:#a0aec0
- padding:6px 0 0 0
- line-height:1.5}
`;
const style = document.createElement("style");
style.textContent = css;
document.head.appendChild(style);
const p = document.createElement("div");
p.className = "jr-panel";
p.innerHTML = `
<div class="jr-head">
<span class="jr-title">
<svg viewBox="0 0 24 24"><path d="M15 4l6 6-10 10H5v-6L15 4zm-1 1L7 12l5 5 7-7-5-5z"/></svg>
Workspace Join Request
</span>
<span class="jr-ver">v4.0</span>
</div>
<div class="jr-sub" id="jr-user">未检测到 AT，等待登录...</div>
<div class="jr-sec">
<label class="jr-label">
<span>母号 Workspace ID</span>
<span class="jr-count" id="jr-count">0 个</span>
</label>
<textarea class="jr-ta" id="jr-ws" placeholder="一行一个 UUID
acfb4e38-524c-4dc8-b4cf-fb3d0ce28b25"></textarea>
<div class="jr-save-row">
<button class="jr-btn jr-btn-ghost" id="jr-save" style="padding:5px 14px">保存</button>
</div>
<div class="jr-hint">只需子号 AT + workspace ID。request = 主动申请加入；accept = 接受已有邀请。</div>
</div>
<div class="jr-body" id="jr-body"></div>
<div class="jr-foot">
<button class="jr-btn jr-btn-ghost" id="jr-refresh">刷新 AT</button>
<button class="jr-btn jr-btn-green" id="jr-accept">Accept</button>
<button class="jr-btn jr-btn-primary" id="jr-run">Request</button>
</div>
`;
document.body.appendChild(p);
panelBody = p.querySelector("#jr-body");
userBarEl = p.querySelector("#jr-user");
reqBtnEl = p.querySelector("#jr-run");
accBtnEl = p.querySelector("#jr-accept");
wsInputEl = p.querySelector("#jr-ws");
saveBtnEl = p.querySelector("#jr-save");
const countEl = p.querySelector("#jr-count");
// 填入已保存值
wsInputEl.value = CONFIG.workspaceIds;
const updateCount = () => {
const n = wsInputEl.value.split(/[
,]+/).map(s=>s.trim()).filter(Boolean).length;
countEl.textContent = `${n} 个`;
};
updateCount();
// 编辑标记 dirty
wsInputEl.addEventListener("input", () => {
markDirty();
updateCount();
});
// 保存
saveBtnEl.addEventListener("click", () => {
CONFIG.workspaceIds = wsInputEl.value;
saveConfig(CONFIG);
markClean();
log("workspace 已保存", "ok");
});
// 按钮
reqBtnEl.addEventListener("click", () => runAll("request"));
accBtnEl.addEventListener("click", () => runAll("accept"));
p.querySelector("#jr-refresh").addEventListener("click", async () => {
log("手动刷新 session...", "info");
await refreshSession();
});
}
function log(msg, level) {
const styles = { info: "jr-info", ok: "jr-ok", warn: "jr-warn", err: "jr-err" };
const time = new Date().toLocaleTimeString();
console.log("%c[JoinReq]", "color:
- #3182ce
- font-weight:bold", msg)
if (panelBody) {
const line = document.createElement("div");
line.className = `jr-line ${styles[level] || "jr-info"}`;
line.textContent = `[${time}] ${msg}`;
panelBody.appendChild(line);
panelBody.scrollTop = panelBody.scrollHeight;
}
}
// ---------- 启动 ----------
function boot() {
buildPanel();
log("脚本已加载 v4.0", "info");
log("只需子号 AT + workspace ID", "info");
log("request = 主动申请 · accept = 接受邀请", "info");
refreshSession();
setInterval(refreshSession, CONFIG.sessionPollMs);
window.addEventListener("focus", () => { if (!STATE.running) refreshSession(); });
}
if (document.readyState === "loading") {
document.addEventListener("DOMContentLoaded", boot);
} else {
boot();
}
})();
```
4.运行成功后点击脚本的 accept 加入空间
5.刷新页面或新开页面

切换到空间，选中空间进行切换，不切换到空间的话，后续导出json会是Free，这里要注意
6.打开session链接

评论区获取 <https://chatgpt.com/api/auth/session>，获取session信息全选复制
7.打开session转换工具链接

评论区获取 [https://gpt.learnlicen.dpdns.org/ ](https://gpt.learnlicen.dpdns.org/)进行 session 转换，转换完成后导入账号使用

8.导入 cockpit tools 进行使用

导入token(可选，看自己习惯用哪个工具就用哪个)

9.导入完成进行使用

注意项

一定要用别名邮箱，别用自己的邮箱，不然后续封号就麻烦了，大家快蹬起来吧

通过Gmail邮箱别名+K12空间，免费白嫖ChatGPT Plus团队版。从注册GPT到一键加入workspace空间，再到导出session转换token，全流程保姆级实操演示。

⏱️ 时间轴

📎 本视频涉及资源

• ChatGPT官网: https://chatgpt.com/

• Session接口: https://chatgpt.com/api/auth/session

• Session转换工具: https://gpt.learnlicen.dpdns.org/

⚠️ 不适合完全没概念的小白，需要一定技术基础。每个Gmail支持创建5个别名邮箱，务必使用别名而非主邮箱。

注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有 🔗https://869hr.uk

## 短信及语音接码平台

- 或https://smspva.com/?ref=1307601

纯净住宅IP白嫖流量
- 500M试用， 链接 https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN ， 85 折优惠
- 200M试用，链接 https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码GXJDIAN， 9 折优惠
- eSIM各国纯净IP流量：https://www.redex.vip/zh?partnerId=31
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
7. Bybit支付卡申请链接 （推荐码：LGNQRG）https://youtu.be/3sN7P2t_CeA

8. YiKa虚拟卡实操开卡教程，不需KYC，一个邮箱开50张卡，订阅ChatGPT/Claude/推特蓝V出海必备 https://youtu.be/XaLeXKu4PTM

## YouTube 播放列表

- AI产品&技术相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海VPS相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=tuPU2TQXNbI)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/chatgpt-gmail-free-gpt-k12-plus-tutorial/)
