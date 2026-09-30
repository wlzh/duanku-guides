# 论文去AI味神器！baibaiAIGC开源工具完整教程｜多轮降AIGC痕迹 支持docx和txt

介绍 baibaiAIGC 开源工具的安装、API 配置、模型选择、docx 与 txt 处理流程，并说明多轮改写、切块校验和常见报错排查。

> 完整图文与持续更新版本：[论文去AI味神器！baibaiAIGC开源工具完整教程｜多轮降AIGC痕迹 支持docx和txt](https://869hr.uk/2026/tech/ai-baibaiaigc-tools-aigc-docx-txt-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/ai-baibaiaigc-tools-aigc-docx-txt-tutorial/
- 更新：2026-07-11
- 分类：技术
- 专题：技术、AI
- 关键词：baibaiAIGC、AI去味、论文降AIGC、AIGC检测、中文论文
- 视频：https://www.youtube.com/watch?v=wQJ25YhmxGk

## 正文

<!-- 文章摘要 -->
> 
baibaiAIGC https://github.com/poleHansen/baibaiAIGC...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=wQJ25YhmxGk)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 11 分钟。

baibaiAIGC https://github.com/poleHansen/baibaiAIGC

本仓库支持四种使用方式：
1. 对话 skill 模式：
- 在聊天中按 `SKILL.md` 约束执行单轮改写
- 安装本仓库作为 skill 后即可直接使用。
2. 脚本 API 模式：通过 `scripts/run_aigc_round.py` 执行单轮分段处理，并按需调用外部 OpenAI 兼容接口。
3. Web 模式：启动本地后端和前端页面，在浏览器中完成上传、配置、执行和导出。
4. app：安装app可直接使用
## 适用场景

适合以下任务：

* 中文论文去 AI 味

* 多轮降低 AIGC 痕迹

* 对长文档进行分段改写并保留原有结构 不适合以下任务：

* 长文件建议使用脚本，直接在聊天框效果不佳
## 效果

中文论文去 AI 味

多轮降低 AIGC 痕迹 对长文档进行分段改写并保留原有结构 基于 \`.docx\` 和 \`.txt\` 的论文处理工作流

一次性把两轮规则混合执行

把整篇长文一次性整体重写 为了“过检测”而随意改动事实或专业内容

安装依赖：

pip install -r requirements.txt

Web 前端依赖安装：

当前依赖非常少：

* `python-docx` ：用于 `.docx` 文本提取和回写
## 使用建议

* 推荐使用 web 端，然后是脚本；如果要作为 skill 使用，直接安装本仓库根目录即可。
## 快速开始
### 1. 准备输入文件

把待处理文件放到 `origin/` 目录，或在聊天 / Web 上传后让系统自动保存到 `origin/chat-uploads/` 。

示例：

* `origin/毕业论文.docx`

* `origin/毕业论文_原始_utf8.txt`
#### 模式 A：使用app（点击下方链接）

https://github.com/poleHansen/baibaiAIGC/releases
#### 模式 B：Web 模式

适合在浏览器中完成模型配置、文件上传、轮次执行和导出。

后端入口是 [scripts/web\_app.py ](https://github.com/poleHansen/baibaiAIGC/blob/main/scripts/web_app.py)，前端入口位于 [app/package.json ](https://github.com/poleHansen/baibaiAIGC/blob/main/app/package.json)。
### 一键安装并启动前后端

如果你只是想把 Web 前后端环境一次性装好并启动，可以直接在仓库根目录运行：

这条命令会自动完成：

* 创建根目录 `.venv` Python 虚拟环境（如果还没有）

* 安装后端依赖 `requirements.txt`

* 安装前端依赖 `app/package.json`

* 分别启动后端 Flask 和前端 Vite 开发服务器

启动成功后可访问：

* 前端： `http://127.0.0.1:1420`

* 后端： `http://127.0.0.1:8765`

如果依赖已经装好，只想跳过安装、直接启动，可以运行：

powershell -ExecutionPolicy Bypass -File .\scripts\start\_web\_dev.ps1 -SkipInstall
#### 模式 C：脚本 API 模式

适合用脚本做单轮批处理。

特点：

脚本入口是 [scripts/run\_aigc\_round.py ](https://github.com/poleHansen/baibaiAIGC/blob/main/scripts/run_aigc_round.py)。
#### 模式 D：对话 skill 模式

适合直接在聊天中执行当前应进行的一轮改写。

特点：

* 不需要你手动配置 `API Key / Model / Base URL` skill 入口和约束见 [SKILL.md ](https://github.com/poleHansen/baibaiAIGC/blob/main/SKILL.md)。
## Web 端运行方式二（自己安装环境运行）

先启动 Python 后端：

python scripts/web\_app.py

再启动前端开发服务器：

启动后按 Vite 终端输出中的本地地址在浏览器访问，前端会调用本地 Flask API。

Web 模式下可完成以下操作：

* 上传 `.txt` 或 `.docx` 文件后自动保存到 `origin/chat-uploads/`

* 配置并测试模型连接

* 按当前记录继续执行第 1 轮或第 2 轮

* 读取历史输出并导出 `.txt` 或 `.docx` 到 `finish/web_exports/`
## 脚本 API 模式用法
### 必填参数

运行单轮处理：

python scripts/run\_aigc\_round.py \<doc\_id> \<round> \<input\_path> \<output\_path> \<manifest\_path> \[--chunk-limit 850]

* `output_path` ：本轮输出文本路径

* `manifest_path` ：本轮切块结构输出路径
### 配置模型 API

* `api_key`

* `model`

* `base_url`

可以通过环境变量提供：

$env:BAIBAIAIGC\_API\_KEY="your\_api\_key"$env:BAIBAIAIGC\_MODEL="your\_model"$env:BAIBAIAIGC\_BASE\_URL="https://your-endpoint/v1"

也可以通过命令行参数提供：

python scripts/run\_aigc\_round.py origin/毕业论文\_原始\_utf8.txt 1 origin/毕业论文\_原始\_utf8.txt finish/intermediate/毕业论文\_原始\_utf8\_round1.txt finish/intermediate/毕业论文\_原始\_utf8\_round1\_manifest.json --api-key your\_api\_key --model your\_model --base-url https://your-endpoint/v1
### 第 1 轮示例

python scripts/run\_aigc\_round.py origin/毕业论文\_原始\_utf8.txt 1 origin/毕业论文\_原始\_utf8.txt finish/intermediate/毕业论文\_原始\_utf8\_round1.txt finish/intermediate/毕业论文\_原始\_utf8\_round1\_manifest.json --prompt-profile cn --chunk-limit 850
### 第 2 轮示例

python scripts/run\_aigc\_round.py origin/毕业论文\_原始\_utf8.txt 2 finish/intermediate/毕业论文\_原始\_utf8\_round1.txt finish/intermediate/毕业论文\_原始\_utf8\_round2.txt finish/intermediate/毕业论文\_原始\_utf8\_round2\_manifest.json --prompt-profile cn --chunk-limit 850

如果暂时不想调用模型，可以使用 `--dry-run` ：

python scripts/run\_aigc\_round.py origin/毕业论文\_原始\_utf8.txt 1 origin/毕业论文\_原始\_utf8.txt finish/intermediate/毕业论文\_原始\_utf8\_round1.txt finish/intermediate/毕业论文\_原始\_utf8\_round1\_manifest.json --chunk-limit 850 --dry-run --echo-prompt-inputs

这个模式下：

* 不会调用模型

* 输出文本与输入文本一致

* 可用于检查切块、prompt 拼接和 manifest 结构
## 对话 skill 模式用法

对话模式建议优先使用 [SKILL.md ](https://github.com/poleHansen/baibaiAIGC/blob/main/SKILL.md)和 [scripts/skill\_round\_helper.py ](https://github.com/poleHansen/baibaiAIGC/blob/main/scripts/skill_round_helper.py)中的规则。
1. 将原始文件放入 `origin/` ，或直接上传附件由系统自动保存到 `origin/chat-uploads/`
2. 在对话中触发降 AIGC skill
3. skill 读取记录，判断当前应执行的轮次
4. 若输入是 `.docx` ，先提取为中间 `.txt`
5. 按最多 850 字切块逐块改写
6. 写回本轮输出到 `finish/intermediate/`
7. 依据 `references/checklist.md` 做本轮评分

8. 更新记录，等待下一次新对话继续下一轮

注意：

* 对话 skill 模式不要求额外提供环境变量

* 脚本 API 模式报缺少 API 配置，不等于对话模式不可用
## 常见问题
### 1. 为什么脚本执行时报缺少 API 配置？

因为 [scripts/run\_aigc\_round.py ](https://github.com/poleHansen/baibaiAIGC/blob/main/scripts/run_aigc_round.py)的自动改写依赖外部 OpenAI 兼容接口。

解决方法：

* 配置 `BAIBAIAIGC_API_KEY`

* 配置 `BAIBAIAIGC_MODEL`

* 配置 `BAIBAIAIGC_BASE_URL`

或者使用 `--dry-run` 只做切块校验。
## 说明

这个 README 面向后续使用者，目的是让使用方式、目录约定和执行边界一次说清。更严格的行为约束以 [SKILL.md ](https://github.com/poleHansen/baibaiAIGC/blob/main/SKILL.md)为准。

baibaiAIGC 是一款开源的中文论文去 AI 味工具，支持多轮降低 AIGC 痕迹，对长文档进行分段改写并保留原有结构。

本视频完整介绍 baibaiAIGC 的四种使用方式：
1. 对话 Skill 模式 — 在聊天中按 SKILL.md 约束执行单轮改写
2. 脚本 API 模式 — 通过 run_aigc_round.py 执行单轮分段处理，支持 OpenAI 兼容接口
3. Web 模式 — 启动本地后端和前端，在浏览器中完成上传、配置、执行和导出
4. App 模式 — 安装即用

核心特点：
- 基于 .docx 和 .txt 的论文处理工作流
- 按最多 850 字切块逐块改写
- 支持两轮规则：第一轮结构性改写，第二轮深度润色
- 保留原文结构不破坏专业内容
- Web 前端支持文件上传、模型配置、轮次执行和导出

GitHub: https://github.com/poleHansen/baibaiAIGC

📎 **本视频涉及资源**

GitHub 仓库: https://github.com/poleHansen/baibaiAIGC

App 下载: https://github.com/poleHansen/baibaiAIGC/releases

SKILL.md: https://github.com/poleHansen/baibaiAIGC/blob/main/SKILL.md

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

- [YouTube视频原地址](https://www.youtube.com/watch?v=wQJ25YhmxGk)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/ai-baibaiaigc-tools-aigc-docx-txt-tutorial/)
