# macOS 微信最新版本(4.0.6.240版)双开及N开教程，主打免安装&原生&安全&可升级

本文详细介绍了在macOS系统上实现微信(4.0.6.240版)双开的方法，通过复制微信程序、修改唯一标识符、重新签名等步骤，让你轻松拥有多个微信账号，工作生活互不干扰。同时提供了打包命令教程，方便快捷地启动微信分身。适用于需要同时管理多个微信账号的用户。

> 完整图文与持续更新版本：[macOS 微信最新版本(4.0.6.240版)双开及N开教程，主打免安装&原生&安全&可升级](https://869hr.uk/2025/tutorial/wechat-dual-open/)

## 内容信息

- 原文：https://869hr.uk/2025/tutorial/wechat-dual-open/
- 更新：2025-08-17
- 分类：教程
- 关键词：微信、软件安装、教程、效率工具

## 正文

<!-- 文章摘要 -->
> 
还在为Mac上只能登录一个微信账号而烦恼吗？本文手把手教你如何在macOS上实现微信双开，甚至N开，让你的工作和生活互不干扰！

# &#x20;起因

今天更新了一下微信，发现打开报错，于是在网上整合了多个攻略，记录一下。

# &#x20;准备工作

## &#x20;安装 Xcode Command Line Tools

1. 打开 `terminal.app`

&#x20;

![](https://img.869hr.uk/PicGo/202508/2a924005fe5179fe65ecf21ee72b3f8a.(null))

2. 安装

输入安装命令 `xcode-select --install`

3. 查看安装状态

`xcode-select -p`

![](https://img.869hr.uk/PicGo/202508/ff679b8e5f3701f6cb802aee3a8f68cf.(null))

如图所示说明安装成功

## &#x20;关闭微信

关闭所有已打开微信，也在微信窗口激活时可以使用快捷键 Command + Q 退出程序。

# &#x20;制作微信分身

## &#x20;删除旧的微信分身

如果之前通过别的方法制作过微信分身，请删除。

## &#x20;复制一份微信程序

1. 使用 `cp` 命令进行文件复制， `sudo cp -R /Applications/WeChat.app /Applications/<这里为目标应用名>.app` 。

```shell
sudo cp -R /Applications/WeChat.app /Applications/WechatDual.app
```

2. 提示输入密码，直接输入自己的开机密码，这里终端中输入密码是不会显示任何字符的（盲打），请确保自己的密码输入正确，输入完成后直接回车。

3. 检查 `访达` → `应用程序` → `<目标应用名>.app` 是否存在。

![](https://img.869hr.uk/PicGo/202508/f3888536bdfe4c0bac2ac358093ed9e1.(null))

4. 通过 `/usr/libexec/PlistBuddy` 程序来修改新复制的微信应用程序的唯一标识符（CFBundleIdentifier）， `sudo /usr/libexec/PlistBuddy -c "Set :CFBundleIdentifier com.tencent.<这里为应用程序的唯一标识符>" /Applications/<这里为目标应用名>.app/Contents/Info.plist` 。

```shell
sudo /usr/libexec/PlistBuddy -c "Set :CFBundleIdentifier com.tencent.xinWeChatDual" /Applications/WechatDual.app/Contents/Info.plist
```

5. 对新复制的微信应用程序重新签名， `sudo codesign --force --deep --sign - /Applications/<这里为目标应用名>.app`

```shell
sudo codesign --force --deep --sign - /Applications/WeChatDual.app
```

6. 尝试双开

首先手动打开原始的微信应用程序，然后通过命令 `nohup /Applications/<这里为目标应用名>.app/Contents/MacOS/WeChat >/dev/null 2>&1 &` 在 `terminal.app` 中打开第二个复制的微信：

```shell
nohup /Applications/WeChatDual.app/Contents/MacOS/WeChat >/dev/null 2>&1 &
```

7. 每次输入命令打开非常不方便，可以参考以下打包命令教程

# &#x20;打包命令

## &#x20;使用自动操作打包

自动操作（Automator）是Mac电脑上自带的一款软件，通过设置，可以实现电脑上的大部分操作自动进行，可以简单理解为一个更加硬核的快捷指令（Shortcuts）。

1. 在启动台找到自动操作（Automator），点开打开。

&#x20;

![](https://img.869hr.uk/PicGo/202508/5827fcf59a6cc71a326bc8fa6d490a04.(null))

2. 选择新建文稿类型为应用程序。

&#x20;

![](https://img.869hr.uk/PicGo/202508/3f956cf0b29d12c48c25c7413aa4217c.(null))

3. 找到实用工具 → 运行 Shell 脚本，双击或者拖拽至右侧空白处。

&#x20;

![](https://img.869hr.uk/PicGo/202508/54b00e1b0cefabcf1995007b8e0cdb59.(null))

4. 复制代码至文本框，Shell 类型默认 /bin/zsh 或 /bin/bash 即可。

```shell
nohup /Applications/WeChatDual.app/Contents/MacOS/WeChat >/dev/null 2>&1 &
```

&#x20;

![](https://img.869hr.uk/PicGo/202508/860c29ac20140fa2ca640ee64271a06e.(null))

5. 保存文件（Cmd+S），名称随意，位置选择应用程序（Applications），文件格式选择应用程序，存储即可。

&#x20;

![](https://img.869hr.uk/PicGo/202508/ca68b520574b3ec651a513500bb519e5.(null))

6. 打开启动台，图标出现，点击即可启动第二个微信。

&#x20;

![](https://img.869hr.uk/PicGo/202508/3717a2e8e294b383e4679ccb348c1908.(null))

## &#x20;换图标

1. 复制（ Cmd + C ）下载好的图标文件。在应用程序（Applications）文件夹里找到刚保存的脚本程序，右击图标，点击显示简介。

&#x20;

![](https://img.869hr.uk/PicGo/202508/56f7e2a5e6888d0956934672bedad643.(null))

2. 点击左上方的小图标，周围变蓝即可，然后粘贴（ Cmd + V ），即可完成。

&#x20;

![](https://img.869hr.uk/PicGo/202508/f89a96a2cca7de1bc5dcbb275117ef96.(null))

&#x20;

![](https://img.869hr.uk/PicGo/202508/b7dd14d348bd3330459b97816d184111.(null))

# &#x20;N 开

重复以上操作，替换 <目标应用名> 和 <应用程序的唯一标识符> 即可制作第 N 个分身

# &#x20;参考文献

[dual-wechat](https://github.com/CLOUDUH/dual-wechat)
[mac版微信双开4.0.6.17版（最详细教程）](https://zhuanlan.zhihu.com/p/1924396537338922039)

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2025/tutorial/wechat-dual-open/)
