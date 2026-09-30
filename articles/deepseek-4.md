# DeepSeek放出一头黑鲸！同一个模型干活成本差4倍，答案全在模型外面

本期拆解DeepSeek Harness黑鲸开源智能体运行系统：一切皆插件架构、四种运行模式、Composio实测同一模型成本差4倍、MIT协议可自部署。

> 完整图文与持续更新版本：[DeepSeek放出一头黑鲸！同一个模型干活成本差4倍，答案全在模型外面](https://869hr.uk/2026/tech/deepseek-4/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/deepseek-4/
- 更新：2026-08-16
- 分类：技术
- 关键词：DeepSeek Harness、DeepSeek、AI Agent、智能体、一切皆插件
- 视频：https://www.youtube.com/watch?v=80u2rwxpTqA

## 正文

<!-- 文章摘要 -->
> 
8月13日DeepSeek开源了DeepSeek Harness，代号「黑鲸」，MIT协议。它不是模型，而是模型外面的一整套智能体运行系统：模型、工具、技能、沙箱、Agent循环甚至UI都是插件，官方一句话：一切皆插件。...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=80u2rwxpTqA)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 19 分钟。

## DeepSeek 放出一头「黑鲸」：同一个模型，干活成本差4倍，答案全在模型外面

事情是这样的。8月13日，DeepSeek 开源了一个新东西。

不是模型。是一整套让模型干活的基础设施，叫 DeepSeek Harness，MIT 协议，直接开源。他们还专门给它开了个微信公众号，头像是一头黑色的鲸鱼，跟 DeepSeek 模型产品那条蓝色鲸鱼明显区分开。

这头「黑鲸」不是模型，它是模型外面的一整套智能体运行系统。模型、工具、技能、会话、沙箱、存储、Agent 循环、任务调度，连用户界面，全都能作为插件加载、卸载、替换。

DeepSeek 给这套架构憋了一句特别容易传播的话：「一切皆插件」。

DeepSeek Harness 黑鲸

## 一个反常识的事：决定 AI 能不能干活的，真不是模型

要理解 Harness 为什么重要，得先接受一个反常识的事：在 Agent 时代，决定一个 AI 能不能干活的，绝不只是模型。

大模型本身只负责生成「下一步内容」。而一个能读写文件、运行命令、调用外部服务、派出子 Agent、还能根据执行结果继续干活的智能体，还需要一套持续运转的控制系统。Anthropic 曾把 Agent 的基础单元概括为「经过检索、工具和记忆增强的大模型」。但一旦进入长程任务，Harness 这一层要干的活就多了：上下文管理、权限控制、状态保存、错误恢复、循环停止条件，全归它管。

模型是灵魂，工具是身体

2026年4月，Anthropic 在讨论 Managed Agent 时说了句挺狠的话：Harness 里包含了「开发者对模型自身做不到什么的判断」，而这些判断会随着模型能力提升而过时。

这话其实点出了 Harness 设计的长期矛盾——框架要提供足够多的控制，又不能用过度固定的流程把模型框死。同一个模型放进不同的 Harness，最终表现可能差得很明显：系统提示词怎么组织、工具定义清不清晰、上下文什么时候压缩、失败后能不能重试，都会影响任务成功率、Token 消耗和运行时间。

## 一组扎心数据：同一个模型，成本差出4倍

光讲道理没意思，看数据。

智能体工具公司 Composio 在8月6日和11日做了两次测试：把同一个 DeepSeek V4-Flash 接入八种不同的 Harness，让它们分别完成三十项多步骤任务。

注意，这些不是简单问答。任务要求 Agent 真正进入 Gmail、Google Calendar、GitHub、Slack 这些真实应用，调用工具并改变应用状态，每项最长跑十五分钟，全部检查通过才算成功。

结果差距不小：完成最多的 Pi Agent 通过了二十项，最少的 OpenCode 只通过十四项。八种 Harness 总共跑了二百四十次，只有一百二十九次成功。三十项任务里，只有六项被所有 Harness 完成。

成本方面的差异更夸张：同样完成十六项任务，Claude Code、Codex 和 DeepAgents 每完成一项成功任务的估算成本分别约为 0.195 美元、0.081 美元和 0.045 美元。

同一个模型。差了四倍还多。

同一个模型不同Harness对比

说白了：模型划定的是能力上限，但 Harness 决定这份上限最终能兑现多少、要花多少钱去兑现。一项长任务跑下来，执行系统要不停地做判断：上下文里留什么丢什么、什么时候调哪个工具、工具报错了是重试还是换一个、模型说完工了该不该信。任何一步处理不好，模型就算思路全对，也可能在真正改文件、提交代码那一步功亏一篑。

## 为什么 DeepSeek 非要自己做 Harness

从这个角度看，DeepSeek 的动机就不难理解了。

一家靠低价和模型能力立足的公司，如果任务交付、失败反馈和开发者入口长期挂在别人的系统里，就算价格再有优势，也决定不了一个任务究竟会烧掉多少 Token、要重试几次、什么时候才算真正完成。

模型能力再强，如果「兑现能力」的钥匙握在别人手里，就永远只是别人生态里的一个零件。

## 「一切皆插件」：把 Agent 拆成乐高

DeepSeek Harness 建立在 Cordis 插件系统之上。根据官方文档，模型适配器、工具注册表、会话日志，乃至 Agent 循环本身，都属于插件。开发者不需要修改 Harness 的主体代码，就能通过插件替换或扩展具体能力。

Cordis 把这种能力叫做「时空可组合性」。时间上，插件卸载后，它注册过的服务、事件和副作用能够随之撤销；空间上，插件可以声明依赖，并在其他组件变化时重新建立协作关系。

一切皆插件的模块化架构

这种拆分对开发者有三类直接价值。

第一，模型和运行环境可以分离。你可以保留同一套会话工具和权限体系、只替换模型适配器；也可以固定模型，比较不同上下文管理或 Agent 循环的效果。这对模型评测特别有意义——有助于分辨能力提升到底来自模型本身，还是来自工程优化。

第二，企业可以保留自己的基础设施。沙箱、存储、审批、凭证和遥测数据都能作为插件存在，减少被单一 Agent 产品绑定的程度。

第三，Agent 能力可以形成独立生态。开发者不需要维护分叉版本，只需要发布插件。

当然，开放程度越高，治理成本也越高：插件来源验证、权限边界、依赖冲突、版本兼容和供应链安全，都会成为生态能否进入生产环境的前提。

## 四种运行模式，同一个宿主

官方提供了四种预设运行模式。它们不是换了个提示词风格，而是基于同一套 Harness 宿主、装配不同的工具和运行时能力。

四种运行模式

**标准模式**：提供相对完整的工具集合，面向日常 Agent 任务。**极简模式**：只保留 Shell 和文件编辑工具，主要用于基准测试，让评测更接近对模型自主规划和终端操作能力的直接观察。**程序化工具调用（PTC）模式**：让模型先生成一段代码，再由代码组织多轮工具调用，减少模型和工具之间的反复往返。但它给了模型更强的调度能力，对沙箱隔离和权限控制的要求也更高。**创造模式**：最有实验性。Agent 可以检查当前运行时，在内存中试验 Cordis 插件，再组合出新的运行模式。官方提供了一个 Cordis 演示，允许 Agent 检查和修改正在运行的插件环境，但距离稳定的自我进化还有很长的工程路径。

有个重要限制要注意：会话一旦产生内容，就不能切换模式了。因为中途切换会导致新工具集无法解释旧的工具调用，破坏会话的可复现性。

## 会话日志只能追加：「模型可见，即已记录」

DeepSeek Harness 另一项核心设计，是仅追加（append-only）的会话日志。

一个会话由按顺序追加的事件构成，是 Agent 全部交互历史的唯一事实来源。模型消息历史由这份日志推导生成，不再单独保存；恢复和回放也从同一组事件重新构建。系统提示词、思维链、工具调用及结果、子 Agent 调度和上下文注入，都会被记录下来，可以在轨迹视图中按来源查看。

官方文档把这条原则概括为「模型可见，即已记录」。上下文压缩不会删除原始历史，只是用替换事件改变模型此后看到的表象。

这么做的价值很直接：当 Agent 在第几十步做错决定时，开发者可以回到当时模型真正看到的上下文，确认问题到底来自模型判断、工具返回、提示词变化，还是错误注入。

很多人听到「一切皆插件」，第一反应是联想到 MCP 协议。但两者解决的问题不在同一层：MCP 是连接 AI 应用与外部数据和工具的开放标准，重点是统一连接方式；而 Harness 负责更上层的运行逻辑——什么时候把工具交给模型、调用前需不需要审批、结果如何写入会话、失败后是否重试、Agent 何时派出子任务、又在什么条件下停止。

所以 MCP 服务器可以成为 Harness 中的工具来源，而 Cordis 插件负责把模型、工具、状态、循环、界面和政策组合成一个可运行的 Agent。一个是连接标准，一个是运行系统，不打架。

## 230 个成员的「洞洞板」

工程规模上，DeepSeek Harness 仓库里已经包含超过 230 个 workspace 成员：文件系统、终端、子进程、伪终端（PTY）、语言服务器协议（LSP）、网页访问、技能、子智能体、工作流……几乎每一项能力都有自己的包。

如果把普通 Agent 项目比作一台装好的电脑，那 DeepSeek Harness 更像一块洞洞板——所有部件都可以插上，也可以拔下。它把典型能力拆成接口、实现和消费者三层：将来如果本地 Shell 要换成远程容器或云端沙箱，理论上只需替换实现层，不必重写模型工具和 Agent 循环。

插件化的架构通过 `cordis.yml` 配置文件实现，同一套代码可以组装成完全不同的产品形态：加入模型适配器、文件系统和 Bash，得到终端编程智能体；换成 Web 插件，就是浏览器应用；换成 ACP 或 JSON-RPC 协议，又能成为其他程序驱动的自动化服务。

## Agent 到底怎么跑：轮次、步骤与安全流水线

Harness 没有把核心简化成几行循环。一次用户输入开启一个轮次（Turn），一个轮次包含多个步骤（Step），一个步骤对应一次模型请求及后续工具执行。

工具调用安全流水线

工具调用要经过一整条流水线：前置策略、安全守卫、实际执行、后置处理、结果通知，一步不少。

工具可以声明并发安全性：只读任务并行执行，碰到修改状态的调用就作为屏障，等待前面的任务结束后再独占执行。它还认真处理了运行中消息的去向——区分排队消息、注入上下文和转向指令，并通过回执确认某条指令是否真正进入了某次模型请求。换句话说，它不只关心消息是否收到，还关心模型究竟在哪一步看到了它。

多智能体协作方面，主 Agent 可以把任务委派给子 Agent，每个 Agent 拥有独立的上下文层，可以配置不同工具和权限。子 Agent 有两种形态：`subagent` 是可以续跑的后台子 Agent，完成后结果自动送回父级会话；`subagent_fork` 是一次性子 Agent，继承当前上下文启动，做完就结束。

工作流引擎通过脚本确定性编排多个子 Agent，适合迁移、审计这类需要固定流程的任务。还有一种 Ralph 循环模式，每轮启动全新的子 Agent 执行同一个目标直到达成——比如把测试修到全部通过。

## 安全：默认收紧，失败即关闭

安全方面，Harness 的态度相当认真。

项目默认采用 workspace-write 模式，把命令执行和文件修改限制在当前工作区；更宽松的 danger-full-access 模式必须由部署方明确选择，不会被默认开启。三大桌面平台用了操作系统原生的隔离机制：Linux 用 bwrap 和 Landlock，macOS 用 Seatbelt，Windows 用 ACL。

有个细节我觉得挺讲究：沙箱后端如果只能覆盖部分承诺，会报告 partial 而非 full，不会虚报安全边界。

文件系统、Bash 和子进程共享同一套沙箱策略，避免「命令受限制、但文件工具可以绕过去」的漏洞。它还采用失败关闭原则：如果系统无法确认隔离机制真正生效，就拒绝执行，而不是悄悄退化为无保护运行。此外，密钥不进日志，数据默认留在本地。

## Code Mode：把几十次往返压成一次

程序化工具调用的技术基础叫 Code Mode。它把全部工具生成为一套 TypeScript 软件开发 SDK，模型通过 `run_code` 工具提交一段程序，在程序里直接调用各种工具，包括写循环、条件判断、并发执行。中间过程不占用模型上下文，只有最终打印或返回的内容才会进入上下文。

举个例子：统计所有包中的 TODO 标记并汇总排序，常规方式需要几十次往返，而在 Code Mode 下，一段程序一次跑完。同时，每次工具调用仍然要走完整的安全流水线。

## 生态兼容：谁都能接进来

生态兼容性方面，Harness 相当开放：支持 MCP 协议，可以接入任何 MCP 服务器；支持 Claude Code 和 Codex 的钩子脚本；内置 ACP 服务端，可以让支持 ACP 的编辑器直接把 Harness 当后端用；Skills 技能包系统支持自建技能库。

模型接入方面，除了 DeepSeek 官方 API，还支持任意 OpenAI 兼容端点，默认可以接入 Kimi、OpenAI、Anthropic、Google 等近四十家大模型。

上手也简单：装好 Node.js 22 或 24 以上版本，一行 `npx` 命令就能启动 Web 界面，默认地址 `127.0.0.1:3080`。界面和 Codex 之类很像，默认带了 133 个插件，覆盖文件读写、内置 ripgrep 全文检索、命令执行、持久终端、LSP 语义查询、网页搜索等日常操作。

还有三个贴心设计：一个独立的策略插件，强制要求智能体必须先读过文件才能改它；搜索结果超出上限后会自动存盘，不截断；命令和子 Agent 都可以转入后台统一管理。

## 社区已经疯了：不好好内测，都跑去写插件

内测期间最好玩的一幕：开发者们基本都不好好内测，都跑去写插件了。

短短几天就出现几百个插件：有人改了整个界面做出各种皮肤，有人实现了跨会话长期记忆，甚至有人做了后台自我进化。这足以说明插件系统的自由度。

不过官方对版本状态也给出了明确提示：当前仍处于开发者预览阶段，后续可能出现破坏兼容性的变更。Harness 本身 MIT 协议免费开源，但运行 Agent 需要配置 API Key，会产生模型调用成本。作为早期预览版，它更适合让大家认识架构、试验插件和反馈问题，暂时还不适合直接放进生产环境。

## 结语：模型是大脑，Harness 是身体

如果只看 Web 界面，很容易把 DeepSeek Harness 理解成又一个编程助手。但从仓库结构和设计理念来看，它的目标明显更底层——成品 Agent 更像这套 SDK 的第一位客户。

过去几年，大模型公司之间的竞争主要卷在参数和跑分上。但进入 2026 年以来，头部模型的基础能力快速收敛，价格战愈演愈烈，单纯卖 Token 的天花板已经肉眼可见。行业慢慢想明白了一件事：AI 的核心价值不在模型输出，而在场景落地。同样的 Token 消耗，闲聊价值微薄，而修复一个 Bug 可以创造几倍的商业价值。也正因为如此，DeepSeek 正在从「卖算力」走向「交付结果」。

这条路并不好走。Claude Code 和 Codex 背靠 Anthropic 和 OpenAI，先发优势明显；插件生态能否持续繁荣、开发者是否敢把生产环境托付给 0.1 版本，这些都是悬而未决的问题。但从 R1 到 V4，从模型到 Harness，DeepSeek 走的每一步都踩在同一个方向上——把前沿能力压到可负担的成本，再把可负担的能力接入可落地的系统。

当模型能力逐渐接近，真正拉开差距的，可能不再是考试分数更高的大脑，而是谁能为它造出更好用的身体。在 Agent 运行时这个赛道上，开源插件生态最终能不能跑过闭源的垂直整合？

这头黑鲸，你打算第一时间下水试试吗？

---**以上，既然看到这里了，如果觉得不错，随手点个赞、在看、转发三连吧，如果想第一时间收到推送，也可以给我个星标⭐～****谢谢你看我的文章，我们，下次再见。**

> 作者：短裤哥

> 本文基于 DeepSeek Harness 开发者预览版发布的公开信息整理，核心事实参考 DeepSeek 官方公告、GitHub 仓库说明、The New Stack 报道及 Composio 公开测试数据。

---

## 欢迎关注

如果你喜欢这种「AI 行业动态 + 技术拆解」的内容，欢迎关注短裤哥：持续分享 AI 行业动态、技术分析与工具玩法。

二维码

8月13日DeepSeek开源了DeepSeek Harness，代号「黑鲸」，MIT协议。它不是模型，而是模型外面的一整套智能体运行系统：模型、工具、技能、沙箱、Agent循环甚至UI都是插件，官方一句话：一切皆插件。

本期拆解：
- Composio实测：同一个DeepSeek V4-Flash放进8种Harness，完成数14~20项，单任务成本0.045~0.195美元，差4倍
- Cordis插件系统：时空可组合性，插件卸载即撤销
- 四种运行模式：标准/极简/PTC程序化调用/创造模式
- 仅追加会话日志：模型可见即已记录
- 230个workspace成员的「洞洞板」架构
- 安全设计：workspace-write默认收紧、失败即关闭
- Code Mode：几十次往返压成一次
- 生态兼容：MCP、Claude Code/Codex钩子、ACP、近40家模型
- 社区几百个插件 涌现

模型是大脑，Harness是身体。当模型能力收敛，差距就在身体上。这头黑鲸你打算下水试试吗？

注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有 🔗https://869hr.uk

## 关注与资源

1. 微信讨论群：https://qr.869hr.uk/aitech
2. 超过100T资料总站网站：https://doc.869hr.uk
3. Telegram群聊：https://t.me/tgmShareAI
4. 微信公众号：搜“AI前沿的短裤哥”
5. 视频的文字博客(银行卡、手机号、VPS主机、IP测试等）：https://869hr.uk
6. 推特：https://x.com/gxjdian
7. Youtube：https://youtube.com/@gxjdian

## 短信及语音接码平台

- https://hero-sms.com/?ref=357885
- https://smspva.com/?ref=1307601

## 白嫖流量

- 500M试用， 链接 https://ipfly.net/zh-cn/activity/GXJDIAN 优惠码 GXJDIAN ， 85 折优惠
- 200M试用，链接 https://dashboard.talordata.com/reg?inviter_code=gxjdian 优惠码GXJDIAN， 9 折优惠
- eSIM各国纯净IP流量：https://www.redex.vip/zh?partnerId=31

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

1. Wise免出国极速开户全教程（身份证+国内手机号即可，完美平替香港卡！）https://youtu.be/AL8cOn49xG8 （申请链接https://wise.com/invite/ihpc/lizhiw12 推荐码：lizhiw12）
2. N26 的申请链接及教程链接 （需要护照， 推荐码：lizhiw02766c ） https://youtu.be/HY9OD8rX89s?si=78REb8MyKSJB6cwQ
3. Bybit支付卡申请链接 （推荐码：LGNQRG）https://youtu.be/3sN7P2t_CeA
4. YiKa虚拟卡实操开卡教程，不需KYC，一个邮箱开50张卡，订阅ChatGPT/Claude/推特蓝V出海必备 https://youtu.be/XaLeXKu4PTM
1. 三家eSIM 让国产手机秒变eSIM手机，全方面优缺点对比及开户链接🔗 https://s.869hr.uk/mcc
2. eSIM 9eSIM打 9 折（优惠码：maq）注册及购买链接 https://www.9esim.com/?coupon=maq
3. eSIM ESTK打 9 折（优惠码：GXJDIAN）注册及购买链接 https://store.estk.me/zh?aid=16007
4. eSIM XeSIM打 9 折（推荐码：gxjdian）注册及购买链接 https://xesim.cc/?DIST=RE5FHg==
5. eSIM卡免手机保号收发短信！几十块大疆4G模块爆改移远EC25，Mac UTM一键部署VoHive完整教程 https://youtu.be/PZRkoggXFco
6. 国行iPhone秒变eSIM！Xesim卡手把手喂饭教程，出国留学旅行必备 https://youtu.be/Mhd2KR8Ydo4

## YouTube 播放列表

- AI产品&技术相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYinOdd8WbQ_gbuSVMNgBLlI
- 出海收款、付款、银行卡、虚拟卡相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjEzCOqJh5ojUt8IQm6kYUW
- 出海手机号相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjukvk0xcEupXpgNaObcY-G
- 出海网络搭建相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYh3kMT-egNWr8Bba0jdyttw
- 出海VPS相关专辑 https://www.youtube.com/playlist?list=PLpBi3Wpk7OYjYV-Mz64Bzv3FxADmyKcsC

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=80u2rwxpTqA)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/deepseek-4/)
