# Mac微信多开教程｜一键脚本实现双开到多开，支持Telegram、WhatsApp等所有APP

Mac上实现微信双开到多开的完整教程，使用终端命令复制程序、修改标识符、重新签名，配合Automator打包成一键启动应用。支持微信、Telegram、WhatsApp等所有Mac APP多开，无需第三方软件，可升级、纯原生。

> 完整图文与持续更新版本：[Mac微信多开教程｜一键脚本实现双开到多开，支持Telegram、WhatsApp等所有APP](https://869hr.uk/2026/tech/mac-telegram-whatsapp-app-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/mac-telegram-whatsapp-app-tutorial/
- 更新：2026-07-26
- 分类：技术
- 关键词：Mac微信多开、微信双开Mac、Mac多开微信、WeChat双开、macOS微信
- 视频：https://www.youtube.com/watch?v=NnfL-Uo3mHU

## 正文

<!-- 文章摘要 -->
> 
Mac上实现任意软件多开，以微信双开到多开为例，一键脚本即可实现。...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=NnfL-Uo3mHU)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 8 分钟。

Mac上实现任意软件多开，以微信双开到多开为例，一键脚本即可实现，不仅支持微信，支持Mac的Telegram、WhatsApp等各种APP

## 微信双开及多开方案，支持微信最新版本

1. 可升级！

2. 免安装 ！

3) 纯原生 ！

4) 够安全 ！

## 手把手操作

## 打开 terminal.app

安装cmd+空格，弹出的搜索框，输入terminal.all

安装 Xcode Command Line Tools

在命令行，输入安装命令 xcode-select --install

查看安装状态 xcode-select -p

如图所示说明安装成功

关闭微信

关闭所有已打开微信，也在微信窗口激活时可以使用快捷键 Command + Q 退出程序。

制作微信分身

删除旧的微信分身

如果之前通过别的方法制作过微信分身，请删除。

复制一份微信程序

使用 cp 命令进行文件复制， 在命令行输入 sudo cp -R /Applications/WeChat.app /Applications/<这里为目标应用名>.app

提示输入密码，直接输入自己的开机密码，这里终端中输入密码是不会显示任何字符的（盲打），请确保自己的密码输入正确，输入完成后直接回车。

检查 访达 → 应用程序 → <目标应用名>.app 是否存在。

唯一标识符

通过 /usr/libexec/PlistBuddy 程序来修改新复制的微信应用程序的唯一标识符（CFBundleIdentifier）， sudo /usr/libexec/PlistBuddy -c "Set :CFBundleIdentifier com.tencent.<这里为应用程序的唯一标识符>" /Applications/<这里为目标应用名>.app/Contents/Info.plist 。

比如：sudo /usr/libexec/PlistBuddy -c "Set :CFBundleIdentifier com.tencent.xinWeChatDual" /Applications/WechatDual.app/Contents/Info.plist

签名

对新复制的微信应用程序重新签名， sudo codesign --force --deep --sign - /Applications/<这里为目标应用名>.app

比如：sudo codesign --force --deep --sign - /Applications/WeChatDual.app

尝试双开
首先手动打开原始的微信应用程序，然后通过命令 nohup /Applications/<这里为目标应用名>.app/Contents/MacOS/WeChat >/dev/null 2>&1 &

在 terminal.app 中打开第二个复制的微信：
nohup /Applications/WeChatDual.app/Contents/MacOS/WeChat >/dev/null 2>&1 &

打包命令

每次输入命令打开非常不方便，可以参考以下打包命令教程

使用自动操作打包

自动操作（Automator）是Mac电脑上自带的一款软件，通过设置，可以实现电脑上的大部分操作自动进行，可以简单理解为一个更加硬核的快捷指令（Shortcuts）。

在启动台找到自动操作（Automator），点开打开。

选择新建文稿

选择新建文稿类型为应用程序

找到实用工具 → 运行 Shell 脚本，双击或者拖拽至右侧空白处。

复制代码至文本框，Shell 类型默认 /bin/zsh 或 /bin/bash 即可。

nohup /Applications/WeChatDual.app/Contents/MacOS/WeChat >/dev/null 2>&1 &

保存文件（Cmd+S），名称随意，位置选择应用程序（Applications），文件格式选择应用程序，存储即可。

打开启动台，图标出现，点击即可启动第二个微信。

## 嫌丑换图标

这个图标只是脚本启动APP的图标，脚本执行之后出现的第二个微信还是原版本的，如果还是嫌丑就改图标，自己设计或者去网上找一个心仪的图标。我喜欢这个黑白的，因为有植物大战僵尸里面模仿者（Imitater）的感觉。

复制（ Cmd + C ）下载好的图标文件。

在应用程序（Applications）文件夹里找到刚保存的脚本程序，右击图标，点击显示简介。

点击左上方的小图标，周围变蓝即可，然后粘贴（ Cmd + V ），即可完成。

## 效果展示及懒人包

把双开启动软件放在dock栏，点击之后就可以实现微信双开，而且全程无终端打开，也不会出现其他方法中关闭终端，第二个微信就关闭的情况。

同样的，如果更改代码，也可以实现其他软件的双开，可以自行探索。

## 一键自动化脚本

如果你实在太懒了，不想一步步手工操作，那么下面的一件脚本可以使用，我们继续教程

如果Mac上已经安装python， 或者你会使用python运行脚本，把如下脚本保存成multi-wechat-mac.py文件

```python
#! /usr/bin/env python3
import argparse
import os
import subprocess
def run_cmd(cmdline: str):
    print(f"running cmd: {cmdline}")
    return subprocess.run(cmdline, shell=True, check=True)
def test_cmd(cmdline: str):
    print(f"testing cmd: {cmdline}")
    return subprocess.run(cmdline, shell=True, check=False).returncode == 0
def cli():
    parser = argparse.ArgumentParser(
        description="Multi WeChat Mac",
        formatter_class=argparse.ArgumentDefaultsHelpFormatter,
    )
    parser.add_argument("-n", "--name", default="WeChat2", help="Name for the new WeChat app")
    return parser.parse_args()
def main():
    args = cli()
    name = args.name
    step = 0
    print(f"Creating new WeChat app with name {name}")
    step += 1
    print(f"
Step {step}: Ensure Xcode Command Line Tools is installed")
    if test_cmd("xcode-select -p"):
        print("Xcode Command Line Tools is already installed, skip")
    else:
        run_cmd("xcode-select --install")
    step += 1
    print(f"
Step {step}: Ensure no WeChat instance is running")
    yes = input("Close any WeChat instance, then press y to continue: ")
    if yes != "y":
        print("Aborted")
        return
    step += 1
    print(f"
Step {step}: Copy WeChat app")
    path = f"/Applications/{name}.app"
    if os.path.exists(path):
        print(f"{path} already exists, skip")
    else:
        run_cmd(f"sudo cp -R /Applications/WeChat.app {path}")
    step += 1
    print(f"
Step {step}: Setting App Identifier for {path}")
    identifier = f"com.tencent.xin{name}"
    plist_path = f"{path}/Contents/Info.plist"
    if test_cmd(f"grep {identifier} {plist_path}"):
        print(f"App Identifier for {path} is already set to {identifier}, skip")
    else:
        cmdline = f'sudo /usr/libexec/PlistBuddy -c "Set :CFBundleIdentifier {identifier}" {plist_path}' 
        run_cmd(cmdline)
    step += 1
    print(f"
Step {step}: Signing {path}")
    cmdline = f"sudo codesign --force --deep --sign - {path}"
    run_cmd(cmdline)
    print(f"
Done! You can now run {name} from /Applications, enjoy!")
if __name__ == "__main__":
    main()
```

## if script is downloaded into this dir

cd \~/Downloads/

## create WeChat2 by default

python3 multi-wechat-mac.py

## create WeChat3

python3 multi-wechat-mac.py -n WeChat3

Mac上实现任意软件多开，以微信双开到多开为例，一键脚本即可实现。

不仅支持微信，还支持Mac上的Telegram、WhatsApp等各种APP多开！

本教程方案四大优势：

✅ 可升级 — 不修改原版微信，更新不受影响

✅ 免安装 — 使用系统自带工具，无需第三方软件

✅ 纯原生 — 复制+签名机制，macOS原生支持

✅ 够安全 — 本地操作，不涉及任何第三方账号

📋 教程内容：

1️⃣ 打开终端（Terminal.app）

2️⃣ 安装 Xcode Command Line Tools

3️⃣ 关闭已打开的微信

4️⃣ 复制微信程序（cp -R 命令）

5️⃣ 修改唯一标识符（PlistBuddy 修改 CFBundleIdentifier）

6️⃣ 重新签名（codesign 签名）

7️⃣ 使用 Automator 打包成一键启动应用

8️⃣ 自定义图标美化

9️⃣ Python 一键自动化脚本

🔗 核心命令：

sudo cp -R /Applications/WeChat.app /Applications/WeChatDual.app

sudo /usr/libexec/PlistBuddy -c "Set :CFBundleIdentifier com.tencent.xinWeChatDual" /Applications/WeChatDual.app/Contents/Info.plist

sudo codesign --force --deep --sign - /Applications/WeChatDual.app

nohup /Applications/WeChatDual.app/Contents/MacOS/WeChat )/dev/null 2)&1 &

适用于 macOS 所有版本，微信最新版本完美支持。

📎 本视频涉及资源
- macOS 终端 (Terminal.app) — 系统自带
- Automator (自动操作) — 系统自带
- Xcode Command Line Tools — xcode-select --install 安装
- Python 一键脚本 — 视频中已提供完整代码

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

- [YouTube视频原地址](https://www.youtube.com/watch?v=NnfL-Uo3mHU)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/mac-telegram-whatsapp-app-tutorial/)
