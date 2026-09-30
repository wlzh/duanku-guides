# MAS - 史上最简单Windows/Office一键激活工具 | 不报毒实测

推荐Microsoft Activation Scripts（MAS）这款开源Windows/Office激活工具，支持HWID/KMS38/在线KMS三种激活模式，实测不报毒且永久有效。本文提供PowerShell一键激活教程和传统安装方法，包含详细操作截图和安全验证指南。

> 完整图文与持续更新版本：[MAS - 史上最简单Windows/Office一键激活工具 | 不报毒实测](https://869hr.uk/2025/software/mas-software/)

## 内容信息

- 原文：https://869hr.uk/2025/software/mas-software/
- 更新：2025-03-05
- 分类：软件
- 关键词：软件安装、开源项目

## 正文

<!-- 文章摘要 -->
> 
还在为Windows/Office激活烦恼？微软工程师都在悄悄用的开源激活工具MAS（Microsoft Activation Scripts），支持一键获取数字许可证，实测不触发Windows Defender警报，永久激活稳定可靠。

## 工具特性解析
![工具特性](https://img.869hr.uk/PicGo/202503/7323218a77bfec75a69daf8bb3941c92.webp "MAS激活选项界面 | 支持HWID/KMS38/在线KMS三种模式")

### 技术原理说明
- **HWID模式**：通过硬件ID向微软服务器申请数字许可证（永久激活）
- **KMS38模式**：模拟KMS服务器激活至2038年（理论永久）
- **在线KMS**：连接公共KMS服务器激活180天（需定期续期）

> "MAS的精妙之处在于完全使用系统原生命令，这解释了它为何能绕过杀毒软件检测" —— 逆向工程师 @vposy

## 激活操作指南

### 方法一：PowerShell一键激活（推荐）
```powershell
irm https://massgrave.dev/get | iex
```
1. Win+X调出菜单选择**Windows终端(管理员)**
2. 粘贴上述代码回车执行
3. 按数字键选择激活模式：
   - `1` HWID永久激活Windows
   - `2` KMS38激活Office
4. 看到绿色"Successfully"提示即完成

### 方法二：传统本地激活
1. [GitHub下载地址](https://github.com/massgravel/Microsoft-Activation-Scripts/)
2. 解压后运行`MAS_AIO.cmd`
3. 界面化操作选择激活类型

![操作流程演示](https://img.869hr.uk/PicGo/202503/aa323a86631b1d6a45d2490fa8726b87.webp)

## 安全验证说明
- **开源验证**：代码托管在[GitHub](https://github.com/massgravel/Microsoft-Activation-Scripts)
- **杀毒检测**：VirusTotal[检测报告](https://www.virustotal.com/gui/url-analysis)显示0/62报毒
- **网络行为**：仅连接微软官方服务器

## 注意事项
1. **系统要求**：
   - Windows 7及以上（建议Win10/11）
   - Office 2013-2021/O365
   
2. **激活前准备**：
   - 关闭杀毒软件实时防护
   - 确保系统时间准确
   - 建议创建系统还原点

3. **激活后验证**：
```bash
slmgr /xpr  # Windows激活状态查询
cscript ospp.vbs /dstatus  # Office激活状态查询
```

## 常见问题解答
Q：激活后会被封吗？  
A：HWID激活获得的是微软官方数字权利，与正版无异

Q：支持LTSC版本吗？  
A：实测支持Windows 10/11 LTSC 2021/2024

Q：重装系统后需要重新激活吗？  
A：HWID激活绑定主板，重装自动激活

<!-- 参考链接 -->
## 参考链接
- [MAS官网](https://massgrave.dev/)
- [GitHub项目页](https://github.com/massgravel/Microsoft-Activation-Scripts)
- [微软激活技术白皮书](https://learn.microsoft.com/zh-cn/windows-server/get-started/kms-client-activation-keys)

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2025/software/mas-software/)
