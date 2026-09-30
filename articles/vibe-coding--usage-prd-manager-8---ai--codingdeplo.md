# 编程小白Vibe Coding 必看：使用 prd-manager 8 种文档，一个想法指导 AI 准确 Coding到上线部署全部到位

这篇文章完整整理 prd-manager v2.0.0 的 8 类文档、版本治理、测试驱动和运维支持，帮助你用结构化方式提升 AI Coding 准确性。

> 完整图文与持续更新版本：[编程小白Vibe Coding 必看：使用 prd-manager 8 种文档，一个想法指导 AI 准确 Coding到上线部署全部到位](https://869hr.uk/2026/tech/vibe-coding--usage-prd-manager-8---ai--codingdeplo/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/vibe-coding--usage-prd-manager-8---ai--codingdeplo/
- 更新：2026-05-05
- 分类：技术
- 专题：技术、AI
- 关键词：教程、AI工具、Skills、Claude
- 视频：https://www.youtube.com/watch?v=O9MM4SnGyTc
- 系列：[AI 产品与技术](../series/ai-products-and-technology.md)

## 正文

> 
这是一篇围绕 prd-manager v2.0.0 的完整整理稿，保留了视频标题与详情里的核心信息，并补成适合博客阅读的排版版本。你可以先看视频，再顺着本文了解它如何把需求、设计、开发、测试、运维、版本记录串成一条更适合 AI 协作的工作流。

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=O9MM4SnGyTc)</div>

## 视频介绍

【深度教程】Vibe Coding 的正确姿势：prd-manager v2.0.0 结构化需求到运维全流程。

如果你在用 AI 进行 Vibe Coding 时，常常遇到这些问题：

- 零散的想法让 AI 生成的代码错误百出
- 项目文档缺失，每次沟通都像从零开始
- 难以在需求、代码、测试之间建立有效关联
- 项目迭代时，难以维护历史版本文档

那这套方法正好适合你。

prd-manager v2.0.0 是一个专为辅助 Vibe Coding 设计的 Skill 工具。它不是单纯给你一个模板，而是通过生成一套结构化的版本需求文档，来更精准地指导 AI Coding，从而显著提升 AI 生成代码的准确性和质量。

## 这期视频会讲什么

本视频会带你完整理解 prd-manager v2.0.0 的核心能力，包括：

- 完整的文档生命周期管理：覆盖从零开始的完整项目文档链路，提供 8 种文档类型，满足项目全周期需求
- 语义化版本策略：自动识别变更类型（Major / Minor / Patch），自动更新版本号与 `CHANGELOG.md`
- 测试驱动开发（TDD）：强制 PRD ↔ Code 双向验证，确保每一项需求都能被测试和验收
- 运维自动化支持：提供完整的部署、监控、故障排查、回滚流程文档
- 事故复盘与记录：提供事故记录模板与 5 Why 分析框架，帮助团队沉淀经验、防止重复踩坑
- AI 协作增强：通过 `CLAUDE.md` 给 AI 助手补足项目上下文与元规则，提升协作稳定性

## 内容大纲

### 1. prd-manager 简介与核心价值

它的定位不是“帮你多写几份文档”，而是把模糊想法整理成结构化项目文档，再把这些文档变成 AI 可以稳定理解和持续执行的上下文。

### 2. v2.0.0 核心更新与流程优化

这个版本已经不只是模板集合，而是更完整的流程工具。它把需求、设计、开发、计划、测试、运维、变更记录与 AI 协作说明接到了一起。

### 3. 八大结构化文档详解

围绕 Boundaries，也就是“每份文档只回答一个问题”的原则，拆清楚每份文档各自负责什么。

### 4. 实战：如何高效使用 prd-manager 进行版本治理

视频里会结合模式 A / 模式 B 的目录适配思路，说明怎么在不同项目里落地。

### 5. 事故复盘模板使用演示

不仅要能开发，也要能记录问题、分析原因、留下改进依据。

### 6. 安装指南与总结

从下载安装到如何开始用，都有完整说明。

## prd-manager v2.0.0 的核心能力

## 完整的文档生命周期管理

它覆盖的是完整项目链路，而不是单点文档输出。典型文档包括：

- `prd.md`
- `design.md`
- `dev.md`
- `plan.md`
- `ops.md`
- `test.md`
- `CHANGELOG.md`
- `CLAUDE.md`

这 8 类文档分别承载不同职责，避免所有信息都堆在一个地方，导致 AI 和人都越看越乱。

## 语义化版本管理

prd-manager 支持按照语义化版本规则推进迭代：

- **Major**：不兼容的 API 变更、架构重构、破坏性变更
- **Minor**：向下兼容的新功能、新模块扩展
- **Patch**：向下兼容的问题修复、性能优化、文档更新

同时它还会配合 `CHANGELOG.md` 维护版本变化，帮助团队和 AI 在后续迭代时快速理解“为什么改”“改了什么”“影响到哪里”。

## 测试驱动开发（TDD）

它强调需求、代码、测试之间要形成可追踪关系，而不是需求写在文档里、代码改在仓库里、测试最后再补。通过 PRD ↔ Code 双向验证，可以让需求与实现更一致，也方便验收。

## 运维自动化支持

很多团队在需求和开发阶段写得很细，到了上线时反而靠记忆。prd-manager 会把以下内容一起纳入文档体系：

- 环境变量
- 部署步骤
- 监控告警
- 故障排查
- 回滚流程

这样项目不是“只会写代码”，而是真正可部署、可验证、可维护。

## 事故复盘与记录

它内置事故记录模板与 5 Why 分析思路，不只是为了留档，更是为了把问题原因、过程、改进动作沉淀下来，减少同类事故再次发生。

## AI 协作增强

通过 `CLAUDE.md` 记录项目上下文、技术栈、开发规范、关键决策和元规则，AI 在参与项目时就不必每次都从零猜测背景，协作稳定性会明显更高。

## 为什么这套方法适合 Vibe Coding

很多人一开始用 AI 写代码，最大的问题不是不会写 prompt，而是没有把问题整理成结构化输入。

常见情况包括：

- 需求一句话丢给模型，结果方向跑偏
- 代码写出来了，但测试缺失
- 文档和代码对不上
- 上线流程依赖个人记忆
- 出事故之后没有形成沉淀

prd-manager 的价值，就在于把这些容易散掉的环节，重新组织成一条稳定的工作流。AI 不是凭感觉“猜项目”，而是基于已经确认过的上下文一步步往下推进。

## 事前确认流程

默认按以下顺序推进：

`prd.md（确认） → design.md / dev.md（确认） → plan.md → ops.md / test.md → CHANGELOG.md / CLAUDE.md → docs/prd/README.md`

这个流程里有两个关键确认点：

- `prd.md` 生成后先确认需求，避免方向错
- `dev.md` 生成后再次确认技术方案，避免实现路径错

后面再进入计划、测试、运维与版本维护阶段。这样做的好处是：AI 不是一开始就写到底，而是在关键节点收敛上下文、减少返工。

## 能力范围

### 生成模式

从零产出完整项目文档链路，覆盖：

- `prd.md`
- `design.md`
- `dev.md`
- `plan.md`
- `ops.md`
- `test.md`
- `CHANGELOG.md`
- `CLAUDE.md`

### 管理模式

维护已有 `docs/prd/<version>/` 文档，支持查看、扩展、对比、搜索、归档。

### 迭代模式

支持语义化版本管理，自动识别 major / minor / patch 变更类型，并同步维护版本号。

### 测试驱动

要求代码变更同步更新测试，支持 PRD ↔ Code 双向验证。

### 运维支持

提供部署、监控、故障排查、回滚等流程文档。

### 事故记录

提供事故记录模板，帮助沉淀团队经验。

### 索引维护

同步更新 `docs/prd/README.md`，保持版本摘要倒序展示。

## 安装方式

如果你通过 Skill 目录安装，可以参考：

```bash
git clone https://github.com/wlzh/prd-manager ~/.claude/skills/prd-manager
```

## 适用场景

prd-manager 适合这些场景：

- **从零建文档**：为新项目或新版本初始化完整 PRD 文档链路
- **增量补需求**：在已有版本上新增需求，并同步补设计、计划或技术文档
- **版本治理**：查看版本状态、维护摘要索引、归档旧版本
- **版本对比**：对比不同版本之间的需求、优先级和计划变化
- **跨版本检索**：按主题搜索历史需求，比如认证、支付、通知
- **前后端协作**：让 `prd.md`、`design.md`、`plan.md`、`dev.md` 各自聚焦单一职责
- **测试驱动开发**：让需求、代码、测试之间保持双向映射
- **运维自动化**：让部署、监控、故障排查流程也进入文档体系
- **事故复盘**：沉淀经验，避免重复出错
- **AI 协作**：用 `CLAUDE.md` 给 AI 补齐上下文

## 确认输出边界

下表是 prd-manager 最核心的约束之一：每份文档只回答一个问题。

| 文档 | 关注点 |
|------|--------|
| `prd.md` | 做什么、为什么：功能需求、用户故事、验收标准、业务目标 |
| `design.md` | 长什么样：页面结构、交互流程、组件清单、ASCII 原型 |
| `dev.md` | 如何实现：技术架构、数据模型、接口影响、文件变更 |
| `plan.md` | 何时做、谁来做：任务拆解、时间线、里程碑、风险 |
| `ops.md` | 如何部署和运维：环境变量、部署流程、监控告警、故障排查、回滚 |
| `test.md` | 如何测试和验证：测试策略、用例设计、自动化测试、验收标准 |
| `CHANGELOG.md` | 版本历史：变更记录、迁移指南、破坏性变更 |
| `CLAUDE.md` | AI 协作：项目上下文、技术栈、开发规范、关键决策、给 AI 的元规则 |

这套边界强调：

- 不把技术方案写进 `prd.md`
- 不把用户故事写进 `dev.md`
- 不把数据模型和接口定义写进 `plan.md`
- 不把部署流程写进 `dev.md`
- 不把测试用例写进 `prd.md`

这条规则看上去简单，但对 AI 协作特别关键。因为上下文一旦职责混乱，模型就很容易输出看似全面、实际上难以执行的结果。

## 项目类型适配

不同项目，文档重心也不同：

- **前端项目**：`design.md` 为必含文档，重点描述页面结构、交互与组件设计
- **后端项目**：`dev.md` 为核心文档，需要包含接口影响清单
- **涉及数据库变更**：建议补充独立 SQL 文件，如 `sql/DDL.sql` 与 `sql/DML_init.sql`
- **生产环境项目**：`ops.md` 和 `test.md` 应作为必含文档
- **团队协作项目**：`CLAUDE.md` 为必含文档，用于增强 AI 协作一致性

## 版本管理策略

### 语义化版本规则

- **主版本号（Major）**：不兼容 API 变更、架构重构、破坏性变更
- **次版本号（Minor）**：向下兼容的新功能新增、模块扩展
- **修订号（Patch）**：向下兼容的问题修复、性能优化、文档更新

### 迭代触发条件

| 变更类型 | 版本号变化 | 示例 |
|---------|-----------|------|
| 破坏性变更 | Major + 1 | v1.0.0 → v2.0.0 |
| 新增功能模块 | Minor + 1 | v1.0.0 → v1.1.0 |
| Bug 修复 | Patch + 1 | v1.0.0 → v1.0.1 |

## 目录结构支持

prd-manager 支持两种目录结构模式。

### 模式 A：版本优先

适合快速迭代项目：

```text
docs/
├── v1.0.0/
│   ├── prd.md
│   ├── design.md
│   ├── dev.md
│   ├── plan.md
│   ├── ops.md
│   └── test.md
├── v1.1.0/
│   └── ...
├── CHANGELOG.md
└── CLAUDE.md
```

### 模式 B：类型优先

适合文档驱动项目：

```text
docs/
├── prd/
│   ├── v1.0.0/
│   │   └── prd.md
│   └── v1.1.0/
│       └── prd.md
├── design/
│   └── v1.0.0/
│       └── design.md
├── dev/
│   └── v1.0.0/
│       └── dev.md
├── plan/
│   └── v1.0.0/
│       └── plan.md
├── ops/
│   └── v1.0.0/
│       └── ops.md
├── test/
│   └── v1.0.0/
│       └── test.md
├── CHANGELOG.md
└── CLAUDE.md
```

Skill 会自动识别项目当前使用的目录结构，再按对应模式生成文档，不需要你为了用它先大改项目目录。

## 输入示例

你可以把它当作一个“帮你把需求整理清楚”的工具来用，输入越具体，输出越稳定：

- `/prd-manager 我这边想做一个 v0.3.0 的用户认证版本，你先帮我把需求整理成结构化 PRD。场景是一个后台管理系统，用户分普通员工和管理员；我现在明确想到的功能有账号密码登录、短信验证码登录、注册、找回密码、首次登录强制改密、异常登录提醒；P0 先保证登录注册闭环，P1 再补安全设置和登录风控。`
- `/prd-manager 我现在脑子里只有一个大方向，想做会员订阅功能，你帮我先把需求梳理清楚，只输出 prd.md 就行。这个功能主要面向 C 端用户，要包含套餐展示、试用、开通会员、续费提醒、自动续费关闭、退款规则、权益说明；目标是提升付费转化，所以也请顺手把成功指标和验收标准整理出来。`
- `我想用 prd-manager 给 v0.2.4 加一个“视频播放器”需求，但我现在说得比较散。这个播放器主要用在课程详情页，用户是付费学员，至少要支持倍速、清晰度切换、字幕、播放记录、断点续播、试看限制；你帮我按场景、用户、功能、优先级整理一下，再告诉我要不要补 design.md 和 dev.md。`
- `/prd-manager 帮我看看当前项目所有 PRD 版本现在分别是什么状态。除了列版本号，我还想知道每个版本的目标是什么、已经有哪些文档、还缺哪些关键文档，帮我整理成一眼能看懂的摘要。`
- `用 prd-manager 帮我对比一下 v0.2.0 和 v0.3.0，我不想看原始 diff。我更想知道这两个版本到底业务上增加了什么需求、删掉了什么、哪些优先级变了、开发计划哪里有变化，最后再帮我总结一句这次版本升级的重点。`
- `/prd-manager 帮我把所有版本里跟认证相关的内容都找出来。我不仅要文件列表，还想让你顺手整理一下：哪些版本已经覆盖登录、注册、找回密码、权限控制，哪些版本只做了一部分，哪些地方还缺。`
- `我准备把 v0.1.0 收起来，用 prd-manager 先帮我检查这个版本的文档是不是整理完整了。比如 prd、plan、design、dev 有没有缺，README 索引有没有同步，确认没问题以后再帮我归档。`

## 目录结构一览

```text
.
├── SKILL_v2.md
├── assets/
│   ├── prd_template.md
│   ├── design_template.md
│   ├── dev_template.md
│   ├── plan_template.md
│   ├── ops_template.md
│   ├── test_template.md
│   ├── incident_template.md
│   ├── changelog_template.md
│   ├── claude_template.md
│   └── readme_template.md
├── references/
├── agents/
└── evals/
```

## 能力验证

`evals/evals.json` 已覆盖的核心场景包括：

- 新建版本
- 初始化缺失的 `docs/prd/`
- 版本冲突检测
- 按需只生成单个文档
- 查看版本状态
- 扩展已有版本
- 对比版本差异
- 搜索需求
- 归档版本
- 迭代版本管理（语义化版本）
- 测试驱动开发（PRD ↔ Code 双向验证）
- 运维文档生成（部署、监控、故障排查）
- 事故记录与复盘
- `CLAUDE.md` 项目记忆体维护

## 核心特性补充

### 1. 完整的文档生命周期管理

从需求分析到部署运维，覆盖项目全生命周期的 8 种文档类型：

- **需求阶段**：`prd.md`、`design.md`
- **开发阶段**：`dev.md`、`plan.md`
- **测试阶段**：`test.md`
- **运维阶段**：`ops.md`
- **迭代阶段**：`CHANGELOG.md`
- **协作阶段**：`CLAUDE.md`

### 2. 语义化版本管理

- 自动识别变更类型
- 自动更新版本号
- 自动维护 `CHANGELOG.md`
- 支持版本对比、搜索、归档

### 3. 测试驱动开发

- 要求代码变更同步更新测试
- 支持 PRD ↔ Code 双向验证
- 提供完整的测试策略、用例设计、自动化测试文档

### 4. 运维自动化

- 提供完整部署流程文档
- 提供监控告警配置
- 提供故障排查手册
- 提供回滚方案

### 5. 事故记录与复盘

- 提供事故记录模板
- 提供 5 Why 分析框架
- 提供预防措施清单

### 6. AI 协作增强

- 用 `CLAUDE.md` 给 AI 提供项目上下文
- 记录关键架构决策与技术债
- 维护给 AI 的元规则

### 7. 灵活的目录结构

- 支持版本优先模式
- 支持类型优先模式
- 自动识别项目当前使用的目录结构

## 项目链接

- GitHub: https://github.com/wlzh/prd-manager

## 关注与社区入口

感谢观看，也欢迎继续关注我的内容更新：

- 短信及语音接码平台：<https://smspva.com/?ref=1307601> 或 <https://hero-sms.com/?ref=357885>
- 白嫖流量 500M 试用：<https://ipfly.net/zh-cn/activity/GXJDIAN>，优惠码 `GXJDIAN`，85 折优惠
- 白嫖流量 200M 试用：<https://dashboard.talordata.com/reg?inviter_code=gxjdian>，优惠码 `GXJDIAN`，9 折优惠

### 社群与站点

1. 微信讨论群：<https://qr.869hr.uk/aitech>
2. 超过 100T 资料总站网站：<https://doc.869hr.uk>
3. Telegram 群聊：<https://t.me/tgmShareAI>
4. 微信公众号：搜“AI前沿的短裤哥”
5. 视频的文字博客（银行卡、手机号、VPS 主机、IP 测试等）：<https://869hr.uk>
6. 推特：<https://x.com/gxjdian>
7. Youtube：<https://youtube.com/@gxjdian>

### VPS 主机等

- Claude 用的丽萨主机：<https://lisahost.com/aff.php?aff=9424>
- 按流量 VPS：<https://www.lycheeip.com/home/ip?affId=1AwYIQ7BW8>
- 一年 10 美元的多年保底小鸡：<https://clients.zgovps.com/?affid=1207>
- 各种云主机，主打性价比：<https://my.racknerd.com/aff.php?aff=15809>
- 美国的 VPS，一年 70 美金活动：<https://app.cloudcone.com/?ref=13794>
- 一年 8.5 美金的美国家宽，稳定靠谱：<https://www.webshare.io/?referral_code=55vpv6waorud>

### 其他资源

- 家宽 IP 链接：<https://ipfly.net/activity/OE5TWVlUUEI6TFZKOVhYQzM5NQ==>
- 住宅 VPS 链接：<https://www.voyracloud.com/?ref_code=5ZG4FHL8>
- Gmail、Telegram 等账号购买、礼品卡、Claude 充值 AI 产品：
  - <https://accboy7gxjdian.acceboy.com/>
  - <https://universalbus.cn/?s=bvDplWi2fZ>
  - <https://www.gamsgo.com/partner/jGh24>
- Claude、OpenAI Codex 等充值：<https://bewild.ai?code=GXJDIAN>

### eSIM 相关

1. 三家 eSIM 让国产手机秒变 eSIM 手机，全方面优缺点对比及开户链接：<https://s.869hr.uk/mcc>
2. eSIM 9eSIM 打 9 折（优惠码：`maq`）注册链接：<https://www.9esim.com/?coupon=maq>
3. eSIM ESTK 打 9 折（优惠码：`GXJDIAN`）注册链接：<https://store.estk.me/zh?aid=16007>
4. eSIM XeSIM 打 9 折（推荐码：`gxjdian`）注册链接：<https://xesim.cc/?DIST=RE5FHg==>
5. wise 的申请链接及教程链接（有身份证就可，推荐码：`lizhiw12`）
   - 教程链接：<https://x.com/wlzh/status/19967997897...>
   - 申请链接：<https://wise.com/invite/ihpc/lizhiw12>
6. N26 的申请链接及教程链接（需要护照，推荐码：`lizhiw02766c`）：<https://youtu.be/HY9OD8rX89s?si=78REb8MyKSJB6cwQ>
7. Bybit 支付卡申请链接：<https://www.bybit.com/invite?ref=LGNQRG>
   - 教程链接：<https://youtu.be/3sN7P2t_CeA>

### 专辑入口

- AI 产品 & 技术相关专辑：<https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI>
- 出海收款、付款、银行卡、虚拟卡相关专辑：<https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW>
- 出海手机号相关专辑：<https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G>
- 出海网络搭建相关专辑：<https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw>
- 出海 VPS 相关专辑：<https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC>

## 结尾

如果你觉得这期视频对你有帮助，欢迎：

- 点赞本视频
- 在评论区留下你的问题或成功注册的截图
- 订阅频道并打开小铃铛，获取最新硬核白嫖教程和科技前沿资讯

## 参考链接

- [YouTube 视频原地址](https://www.youtube.com/watch?v=O9MM4SnGyTc)
- [prd-manager GitHub 仓库](https://github.com/wlzh/prd-manager)
- [作者博客](https://869hr.uk)

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/vibe-coding--usage-prd-manager-8---ai--codingdeplo/)
