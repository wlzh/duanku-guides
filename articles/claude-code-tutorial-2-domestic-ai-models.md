# 【Claude Code 小白教程-第2期】接入国内大模型！GLM/通义千问配置，AICodeSwitch神器！

欢迎回来！Claude Code 小白教程第二期，手把手教你配置智谱 GLM、阿里通义千问，使用 AICodeSwitch 神器一键切换模型，还有免费大模型白嫖教程。

> 完整图文与持续更新版本：[【Claude Code 小白教程-第2期】接入国内大模型！GLM/通义千问配置，AICodeSwitch神器！](https://869hr.uk/2026/tutorial/claude-code-tutorial-2-domestic-ai-models/)

## 内容信息

- 原文：https://869hr.uk/2026/tutorial/claude-code-tutorial-2-domestic-ai-models/
- 更新：2026-04-22
- 分类：教程
- 专题：教程、AI
- 关键词：Claude Code、GLM、通义千问、AICodeSwitch、AI编程
- 视频：https://www.youtube.com/watch?v=ahyKIDcC6nk

## 正文

<!-- 文章摘要 -->
> 
欢迎回来！Claude Code 小白教程第二期，手把手教你配置智谱 GLM、阿里通义千问，使用 AICodeSwitch 神器一键切换模型，还有免费大模型白嫖教程。

## 视频教程

<div class="video-container">
[在 YouTube 观看视频](https://www.youtube.com/watch?v=ahyKIDcC6nk)
</div>

<!-- more -->

## 视频介绍

欢迎回来！这是系列教程的**【第二期】**。

在第一期，我们搞定了基础配置。这一期，我们将重点解决国内用户的痛点：如何安全、流畅地使用 Claude Code，并享受国内大模型带来的便利和优惠！

**频道**：短裤AI分享

## 视频章节

| 时间 | 章节 | 内容 |
|------|------|------|
| 00:00 | 开场介绍 | 封面图片、频道品牌标识、5个主题概述 |
| 01:19 | 为什么要选择国产模型 | 5大优势 + 5家国产模型供应商 |
| 03:47 | 配置 GLM | 注册、API密钥、3种配置方法、测试、模型映射 |
| 07:56 | 配置 通义千问 | 百炼平台、环境变量、6种模型变体 |
| 11:08 | AICodeSwitch 神器 | 安装、配置、模型切换、常见问题解答 |
| 13:05 | 免费模型 | OpenRouter、Ollama、ClaudeCodeRouter、完整设置 |
| 16:36 | 总结与订阅 | 总结、Subscribe 按钮、频道品牌标识 |

## 本期内容

我们将手把手带你完成进阶配置，实现"国内大模型自由"：

- ✅ **2.1 为什么选择国内大模型？**（核心逻辑与优势分析）
- ✅ **2.2 配置智谱 GLM 模型**（实操国内最强模型之一）
- ✅ **2.3 配置阿里通义千问模型**（大厂模型全面接入）
- ✅ **2.4 使用 AICodeSwitch 神器**（一键在多模型间无缝切换）
- ✅ **2.5 探索更多永久免费大模型**（手把手白嫖教程）

## 详细内容

### 为什么要选择国内大模型？

很多朋友可能会问，Claude 本身就很好用，为什么还要费劲去配置国内模型呢？原因有很多：

1. **访问速度**：国内模型的服务器部署在中国境内，响应时间更短，通常1到2秒就能得到回复，不受国际网络波动影响，稳定性好得多
2. **成本考虑**：国内模型的 API 调用费用普遍比海外模型低 30% 到 50%，很多还提供免费额度或试用机会，支付方式更方便，支持支付宝、微信支付
3. **中文处理能力**：国内模型对中文的理解和处理更加精准，能更好地理解中文语境和文化内涵，处理成语、俗语等特殊表达也更准确
4. **数据安全与合规**：使用国内模型数据存储在国内，符合数据安全法和个人信息保护法，不受跨境数据传输限制
5. **本地化服务支持**：中文客服、中文技术文档、线上线下技术交流活动，与国内主流开发工具和平台深度集成

**目前支持 Claude Code 的国内模型厂商：**

| 厂商 | 代表模型 | 特点 |
|------|----------|------|
| 智谱AI | GLM-4 | 中文理解能力强，代码生成质量高 |
| 通义千问 | Qwen Plus / Qwen Max | 多模态能力强，支持图像和代码 |
| DeepSeek | DeepSeek Coder | 专注于代码领域，代码生成准确率高 |
| 豆包 | Doubao | 用户界面友好，集成度高 |
| Kimi | Moonshot | 上下文窗口大，支持长文本处理 |

### 配置智谱 GLM 模型

GLM 是国内领先的大语言模型之一，由智谱AI 开发，中文理解能力非常出色。整个配置过程分为三个大步骤：注册获取 API → 配置 Claude Code → 测试连接。

**注册步骤：**
1. 访问智谱AI 开放平台（bigmodel.cn），点击注册
2. 输入手机号进行验证，完成注册
3. 完成实名认证（认证后可获得更多免费额度）
4. 新用户总共可获得 **500 万 tokens** 的免费额度（100万注册 + 400万实名认证）

**配置方式（三种）：**
- **方式一（推荐）**：自动化助手 — 在终端执行 `npx @anthropic-ai/ai-coding-helper`
- **方式二**：自动化脚本 — Mac/Linux 用 curl 下载脚本执行
- **方式三**：手动配置 — 编辑 Claude Code 的 settings.json，设置环境变量 `ANTHROPIC_AUTH_TOKEN` 和 `ANTHROPIC_BASE_URL`

**模型映射关系：**
- Claude Opus → GLM 4.7（最强大的模型）
- Claude Sonnet → GLM 4.7（平衡性能与速度）
- Claude Haiku → GLM 4.5 Air（快速响应模型）

### 配置阿里通义千问模型

通义千问是阿里巴巴推出的中文大模型，阿里云百练平台提供了与 Anthropic API 兼容的服务，可以方便地接入 Claude Code。

**开通步骤：**
1. 登录阿里云百练控制台
2. 开通服务，领取新人免费额度（有效期90天）
3. 创建 API Key
4. 配置环境变量 `ANTHROPIC_BASE_URL` 和 `ANTHROPIC_API_KEY`

**通义千问支持的模型变体：**

| 系列 | 特点 | 适用场景 |
|------|------|----------|
| Qwen3 Max | 最强大，支持思考模式 | 复杂任务 |
| Qwen Plus | 能力强，理解深入 | 大多数场景 |
| Qwen Flash | 响应速度快，成本低 | 性价比高 |
| Qwen Turbo | 响应最快，成本最低 | 新手使用 |
| Qwen3 Coder | 专为编程优化 | 代码任务 |
| Qwen VL | 支持视觉理解 | 图像+文本 |

### 使用 AICodeSwitch 神器

AICodeSwitch 是一个模型路由工具，可以集中管理多个 AI 模型的配置，内置模型适配器，甚至可以把 GPT 类的模型也作为 Claude Code 的驱动模型。

**安装：**
```bash
npm install -g aicodeswitch
# Mac/Linux 可能需要 sudo
```

**使用：**
1. 终端输入 `acos ui` 打开图形化界面
2. 配置供应商和路由
3. 激活对应的路由即可

**优势：**
- 一键切换不同的路由，根据任务类型自动选择合适的模型
- 不需要手动修改 Claude Code 的配置文件
- 切换模型不会影响对话历史
- 提供丰富的日志和使用统计信息

### 免费大模型使用指南

**方式一：OpenRouter**
- 聚合了多种大模型的平台，包含免费模型
- 注册后筛选 Free 模型（Llama3 8B、Mistral 7B、Gemma 7B 等）
- 创建 API 密钥即可使用

**方式二：本地搭建 Ollama**
- 在自己电脑上运行大模型，完全免费
- Mac/Windows/Linux 都支持
- 安装后运行 `ollama run llama3` 下载并启动模型
- 运行 `ollama serve` 启动 API 服务（本地 11434 端口）

**方式三：ClaudeCodeRouter**
- 将多种模型统一管理接入 Claude Code
- 安装后创建配置文件 `router_config.json`
- 运行 `ccr start` 启动服务
- 修改 Claude Code 配置指向 ClaudeCodeRouter 地址

## 本期总结

1. 了解了为什么要选择国内大模型（速度、成本、中文处理、安全、本地化）
2. 学会了配置智谱AI 的 GLM 模型
3. 学会了配置阿里云的通义千问模型
4. 掌握了 AICodeSwitch 模型切换工具
5. 了解了如何使用完全免费的大模型

## 相关教程推荐

- [Claude Code 小白教程-第1期](https://869hr.uk/2026/tutorial/claude-code-tutorial---1-how-to-usage/)
- [DeepSeek 相关传闻深度分析](https://869hr.uk/2025/tech/deepseek-20250208/)

## 视频信息

- **视频标题**：【Claude Code 小白教程-第2期】接入国内大模型！GLM/通义千问配置，AICodeSwitch神器！
- **UP主**：短裤AI分享
- **时长**：约 17 分 36 秒

## 参考链接

- [YouTube 原视频](https://www.youtube.com/watch?v=ahyKIDcC6nk)
- [869hr.uk 博客首页](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tutorial/claude-code-tutorial-2-domestic-ai-models/)
