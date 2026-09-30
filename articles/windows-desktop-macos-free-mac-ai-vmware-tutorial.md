# Windows电脑安装macOS系统完整教程，免费使用Mac专属AI软件VMware虚拟机手把手教学

介绍在 Windows 电脑中使用 VMware 安装 macOS 的准备条件、虚拟机配置、系统安装和常见故障排查，用于体验 Mac 专属软件。

> 完整图文与持续更新版本：[Windows电脑安装macOS系统完整教程，免费使用Mac专属AI软件VMware虚拟机手把手教学](https://869hr.uk/2026/tech/windows-desktop-macos-free-mac-ai-vmware-tutorial/)

## 内容信息

- 原文：https://869hr.uk/2026/tech/windows-desktop-macos-free-mac-ai-vmware-tutorial/
- 更新：2026-05-25
- 分类：技术
- 专题：技术、AI
- 关键词：VMware、macOS、Windows安装macOS、虚拟机、Mac专属AI软件
- 视频：https://www.youtube.com/watch?v=EToxhFmpbM0
- 系列：[基础软件与效率工具](../series/software-and-tools.md)

## 正文

<!-- 文章摘要 -->
> 
很多朋友没有mac电脑，可AI时代来了，这几年各种高级AI软件仅Mac支持的屡见不鲜，可mac电脑 又太贵，今天手把手教你windows电脑上安装macOS系统，让你用上mac电脑...

## 视频教程

<div class="video-container">[在 YouTube 观看视频](https://www.youtube.com/watch?v=EToxhFmpbM0)</div>

## 视频介绍

本视频由 短裤AI分享 制作，时长约 24 分钟。

## 1. 前言

很多朋友没有mac电脑，可AI时代来了，这几年各种高级AI软件仅Mac支持的屡见不鲜，可mac电脑 又太贵，今天手把手教你windows电脑上安装macOS系统，让你用上mac电脑
## 2. 下载所需文件

* **官方正版VMware下载（17 pro）**：**链接：https://pan.quark.cn/s/bcc5a3fa93c8?pwd=A3GW 提取码：A3GW**

* **下载系统镜像**：**链接：https://pan.quark.cn/s/e2e1c805bed2?pwd=Nr5F 提取码：Nr5F**

* **macOS-VMware补丁文件（提取码:qwdn）**：**链接: https://pan.baidu.com/s/1vMSmgN0bq7kM9LioeeHp6w?pwd=4j87 提取码: 4j87**

一共三个文件：（缺一不可）

* VMware安装包

* macOS镜像文件

* macOS-VMware补丁文件
## 3. 安装 VMware

请先移步此教程安装VMware再继续：
# VMware17Pro虚拟机安装教程(超详细)

***
## 1. 下载

* 下载地址：**链接：https://pan.quark.cn/s/bcc5a3fa93c8?pwd=A3GW 提取码：A3GW**
-image.png)

下载后长这样：
-f3b1fbdd95fa224d4fc42371114f0d2d.png)
## 2. 前期准备
-8b6ef78f8b52788a5a33a1a68cd8a17c.png)
### 2.1 创建 VMware 所需文件夹

先找一个磁盘空间比较充裕的盘符（不要无脑选C盘），比如我这里E盘空间比较大，我的一些工具、软件等等都会安装在这个盘符里。

那根据我们分类的原则，我们可以把 `VMware` 列为工具类。所以可以在 `Tools` 目录下新建一个 `VMwareTools` 文件夹。
-1d89f965623d8f56843f3ca6b6574778.png)

建好 `VMwareTools` 大的目录后，我们还需要在这个目录下创建 `VMware` 的 `安装目录` 和之后 `创建虚拟机的存放目录` （这个很）

* VMware： `VMware` 的 `安装目录`

* VMwareData： `创建虚拟机的存放目录`
-519f0abba78cc3230aa92f33ae3e9761.png)
## 3. 安装VMware

找到刚刚下载的 `VMware` 的 安装程序 ，在安装程序上鼠标右键点击，选择 `以管理员身份运行` ：
-8d0012575ed605d87d56d73f2a93347a.png)

弹出，确认选择是
-ef932a854cb384fca46be8daca41cf4d.png)

点完 `是` 以后这里需要稍微等待一会，才会显示安装界面：
-704d7ccc6560df2fd0378f6026a592ff.png)

接收许可 协议 以后，点击 `下一步` ：
-df70127f204076494658fd886ebc592e.png)

点完 ‘下一步’ 以后可能会出现下面这个界面，也可能不会出现，因人而异。如果出现了就勾选 `自动安装 Windows Hypervisor Platform (WHP)` ，然后 `下一步` 即可。 **如果没有出现就跳过这一步。**
-23be72c8f56c2672e8932aaa717dece2.png)

这里一定要点击 `更改...` ，来更改安装位置。

不要无脑选择C盘！！！不要无脑选择C盘！！！不要无脑选择C盘！！！
-0ae031e493430a96c8453ecc23864fbd.png)

选择我们刚刚创建的 `VMware的安装目录` ，然后点击 `确定` ：
-ef3a19f155d74ac87d1df77c3365230a.png)

选择安装目录，点击下一步
-a387ee8fcffbe32c8db060353d7a4701.png)

如果出现这个弹窗直接点 `确定` ，如果没有出现直接跳过这一步。
-24ab935e30dd7b755cd29838ef757a1a.png)

将 `启动时检查产品更新` 和 `加入 VMware 客户体验提升计划` 取消勾选，然后点击 `下一步` ：
-6594a253834d76ea3b24efc3835d79ec.png)

选择生成快捷方式，点击下一步
-8188d0e696c85b6f9ac37cf713ab3141.png)

准备好安装，点击安装
-58338101720bf1e50619e10198572728.png)

等待进度条跑完，安装完成：
-f5bfbfd6f9b6bd8b2ed95217f7a14694.png)

安装完成后会显示下面这个界面，直接点 `完成` 即可：

（从17.5.2版本开始博通官方已宣布 [workstation-和-fusion-对个人使用完全免费 ](https://blogs.vmware.com/china/2024/05/16/workstation-%E5%92%8C-fusion-%E5%AF%B9%E4%B8%AA%E4%BA%BA%E4%BD%BF%E7%94%A8%E5%AE%8C%E5%85%A8%E5%85%8D%E8%B4%B9%EF%BC%8C%E4%BC%81%E4%B8%9A%E8%AE%B8%E5%8F%AF%E8%BD%AC%E5%90%91%E8%AE%A2%E9%98%85/)，新版只有完成按钮，点完成即可）

建议直接用新版，不要再用老版本了！！！免费了！！！
-db2dcb21e0ee77ac6d2b9bcd09e5fb90.png)

这样就安装完成了。
-ad1e658361989ec80052d6344c08f86f.png)
## 4. 修改创建的 虚拟机 默认存放位置

这一步也很。后期创建虚拟机的时候会让你选择虚拟机存放位置，如果这一步没有做的话，那你每次创建虚拟机的时候都要手动的去选择存放位置。

有些小白同学甚至看都不看直接就存到了C盘，导致C盘越来越臃肿！***

首先在 `VMware工具栏` 点击 `编辑` ，然后点击 `首选项` ：
-7dd5f8ab704a39cff054ef250e1a4b37.png)

在左侧侧边栏，点击 `工作区` ，然后就能看到 `虚拟机的默认位置(D)` 的选项了，我们点击 `浏览` ，将默认位置改为我们刚刚创建的 `VMwareData` 目录。
-5bcfbbc8911d8b134a0192fdf8e5826d.png)

选择安装位置
-a6cd27876333206043fcd31fc98bd887.png)

确认安装位置
-f4e8fe8e0d1d0a7b0df2b021207bb120.png)

这样的话，我们在创建虚拟机的时候，就会默认存放在我们设置的目录中了。

大功告成！！
-f1f718a79f8101b42452d4fcc0fd2fe1.png)
## 5. 安装后界面变成英文的解决方法

有的同学可能装系统的时候电脑时区选择的有问题，导致VMware的界面变成了英文界面。

不想乱研究乱折腾的话，直接用这个方法：
1. 先关闭VMware
2. 在我们电脑桌面右击VMware快捷方式图标
3. 然后选择 `属性`
4. 找到 `快捷方式` （默认打开的就是快捷方式如果不是自行切换）
5. 在打开的弹窗中找到 `目标(T)` 这一栏
6. 然后在这一栏的最后面添加下面这行代码：
7. （⚠️注意：-- 的前面有一个空格）

```plaintext
--locale zh_CN
AI生成项目
```

* 然后点 `应用` 按钮

* 最后点击 `确定` 按钮即可
## 4. 安装macOS-VMware补丁文件
### 4.1 解压macOS-VMware补丁文件

解压 `unlocker424.zip`
-7c2eb42f56b6d51ca73edc9fc3f17056.png)
### 4.2 结束VMware相关进程

在任务栏上 右键—— 任务管理器 ——详细 信息 ，找到VMware相关的进程全部结束掉。
-6a63590d77df22327673ae3e7ae2d6da.png)

杀死如图的进程 1
-f9709c80c334addb941907a502d44cae.png)

杀死如图的进程 2
-427ca2ad404096b07bc8a959954536df.png)

杀死如图的进程 3
-8095694997e5b8ad47896dabd762d2a0.png)

杀死如图的进程 4
-df55fd91bb9f8c0d04a136049fdf6a32.png)

杀死如图的进程 5
-586b50f4b7819f8299bdff7be93e6b5b.png)

杀死如图的进程 6
-b748cee3c6be4863f7c465af457ced9c.png)
### 4.3 运行补丁包

找到补丁包解压目录后进入 `windows` 目录，双击运行 `unlock.exe`
-00292f515435f2ecb02e1441ac062d90.png)

如果提示如下弹出：
-20cb60444bb1d26f9b2611b57492f183.png)

点击 `更多信息` ：
-6f005b503315a94a1c9fb1ed47d87dab.png)

仍要运行：
-da4c783b72087b1c716b9ec3d3d7d371.png)

然后点击 是 ，就会显示如下弹窗，按下 `回车` 即可
-b38ef1fd7c3bfa6186870c490d416269.png)

完成如图，点击回车，继续
-3042cbbb2c249cca350419e620f64bfc.png)
## 5. 安装macOS
### 5.1 新建虚拟机

直接点击 `创建新的虚拟机` ，或者在左侧 `库` 栏内右键 `新建虚拟机` ，或者点击左上角 `文件` — `新建虚拟机` ：
-6af76be782f9c35251b16b308bba8b1e.png)

选择 `自定义(高级)(C)` 后，点击 `下一步` ：
-8fc2686b6ec541425104adf757600692.png)

继续点击 `下一步` ：
-5f34a9ce9bb007db3eb750496b90217d.png)

选择 `稍后安装操作系统(S)。` 后，点击 `下一步` ：

现在我们就相当于买电脑，先把电脑配置整好。什么 Cpu 啊内存条啊硬盘啊什么乱七八糟的，先不着急装系统。
-7bf958f4d1f0c822efc52f5ad9eb758f.png)

选择 `Apple Mac Os X(M)` 后，在下方 `版本(V)` 中选择我们安装系统版本:

（不在第四步骤安装补丁不显示这个选项哈）
-5fb0724f1ff20afc2f89f418395854e9.png)

该选择的选择好以后，点击 `下一步` ：
-6ddb41b32eefe1f11653f326f5c68286.png)

这里是要我们给虚拟机起个名字，你可以根据自己的实际需求起名，比如 `recreation01` ,意为娱乐第01个虚拟机。

下面的 `位置(L)：` 如果你没有按照 `步骤3.3` 修改默认位置，那你肯定是C盘，不建议大家放到C盘，会让C盘越来越臃肿！如果你显示的位置是在C盘，请回去看 `步骤3.3` 。

名字起好，位置选好，就可以点击 `下一步` 了：
-c6e3e2943faef451dd1d1b2b8fb4eb32.png)

选处理器数量和内核数量建议根据自身处理器情况来。首先我们在 `底部任务栏` 右键选择 `任务管理器` ：（Win10、Win11一样）

然后选择 `性能` — `CPU` ，就可以看到 `物理核心数` 和 `逻辑核心数` 了。
-a6f949d5699f0fd7207d12a543331f5e.png)

根据自己的需要选择核心数，但是切记不能等于或超过 物理机 的 实际核心数！！！
-bc0be8d3190a60f2767775b2f5390b21.png)

内存也是根据大家自身情况选择，物理机内存大小从 `任务管理器` — `性能` — `内存` 中查看，我是32GB内存我这里就选个8GB了（不能等于或超过物理机）：
-e3ee2ab9288d4457eb6120bf46d4c018.png)

选择 `使用网络地址转换(NAT)(E)` 后，点击 `下一步` ：
-fc4f538e96834f0593e76e67a51ecff9.png)

默认推荐，点击 `下一步` ：
-c2761d1aefed3702935db64dd75850ea.png)

默认推荐，点击 `下一步` ：
-a6d6b225992d14b4a200a873fb972bd5.png)

默认第一个，点击 `下一步` ：
-c5774bc0b7ff1180018cbc8d30c9fb64.png)

最大磁盘默认就行了，学习测试使用完全够用，最后点击 `下一步` ：

**（注意：不是说给了多少GB磁盘大小就少了多少GB，而是最大磁盘大小，用多少少多少）**
-789a719f2b7762d14e50a047a95ab290.png)

直接点击 `下一步` ：
-ffd0c40f136d2a359aaecf38ac3396c4.png)

到这里虚拟机就创建好了，相当于我们把电脑配好了，一会该去装系统了，如果你觉得不满意，还可以点击 `自定义硬件(C)` 去修改，满意可以直接点 `完成` ：
-e466edfbf536e4807307ece1afe512dc.png)
### 5.2 修改虚拟机配置

找到我们刚刚创建的虚拟机保存位置，然后找到后缀名位 `.vmx` 的文件：
-1a296d3e92bd6ec64c9a04285bab8262.png)

右键用记事本编辑或其他文本编辑工具打开：

在最后面加入： `smc.version = "0"`
-2318ec9832437537ab25fe2b76a99a7b.png)
### 5.3 安装操作系统
#### 5.3.1 选择 ISO 映像文件

在左侧双击我们刚刚创建的虚拟机，然后在右侧点击 `编辑虚拟机设置` ：
-8e277b5d73f277802f6bfbfcfe74c535.png)

在 `硬件` 这栏，点击 `CD/DVD (IDE)` ，然后选择 `使用 ISO 映像文件(M):`
-d8b1cbc00c77dcad9d25eed20f4d16d8.png)

点击 `浏览` 按钮，选择我们下载的系统镜像：

（这里选择的是 `步骤2` 中下载的系统镜像）
-298c55bf8f0a01e2d8892c67f95b5410.png)

最后点击 `确定` ：
-c3ebc563415340bcbfe99051929f5836.png)
#### 5.3.2 开启虚拟机

在左侧双击我们刚刚创建的虚拟机，然后在右侧点击 `开启此虚拟机` ：
-5ef59cde1b2c5d9958fc1c70835a3dc2.png)

等待进度条完成：
-d1d1e205955b78010cf47bf0a2e3ed12.png)
#### 5.2.3 选择语言
-0a8445f0d3371dc6e9bf8e51119a37ff.png)
#### 5.2.4 磁盘工具设置
-0cc2d800e72b396e3f35a61dd518af75.png)

选择 `VMware Virtual SATA Hard Drive Media` ，然后点击上方的 `抹掉` ：
-bb28b8b703ae5a4cc93bb6ad760197f0.png)

起个名字，比如： `macOS hard disk` ，然后点 `抹掉` :
-c7ad455b92b6af5aa32b8b31d015e514.png)

抹掉完成后，点击 `完成` ：
-c0396cc1b9e95f5f08bb8049b88d8861.png)

最后叉掉这个磁盘工具界面：
-41adf2326b64c6950fd5379dd33baa9e.png)
#### 5.2.5 安装 macOS
-74e6e2d7206ed13593c35c33024c02ed.png)

选择继续
-a7482ada4f82650daf7a3acf83985504.png)

选择同意协议
-b04170446dbfa06c77caf91d38357d37.png)

选择同意
-44bbaed91b15ebf7236d2032afff2ef8.png)

选择确认安装磁盘，点击继续
-fcc162ad26787eef9471986299552e66.png)

最后等待完成：
-099a7c5ea19f6d5ac18dd77176eaa692.png)

中会出现这个白苹果界面，不用担心，耐心的等待即可。

会出现多次，第一次下方会显示时间，后面的只有进度条。
-d22f8e789ed1e64e7286c6db94fd8f6f.png)

完成后会出现选择国家地区的界面：
-e0c01bf062d6b125ef75f528c2cf56a3.png)
#### 5.2.6 完成配置进入系统

翻到最后选择 `中国大陆` ，然后点击 `继续` ：
-7b06912ecbb3c84ba267499b4f32136b.png)

选择输入法，点击继续
-4e3db4e094f27ec2342d9b17d6484ac8.png)

辅助功能，点击以后
-b8b70ec5545288a52d36e2e8dc044948.png)

选择不接入互联网，点击继续
-71e905171a64923d9a98da1dabc878d9.png)

点击确认不连入互联网，继续
-4086a3519ba2f6ca4a1b779373a5dd14.png)

点击继续
-bdb84530910fa4ce673897f6e8b5ab7f.png)

迁移助理，选择以后
-565f8879909735c33f5f36bfedf96c18.png)

点击同意
-daeed0bec790ce49b7445d18007668e8.png)

点击条款同意按钮
-cf1f05c22bacd28f7aa1bef69baf2064.png)

设置账户名、密码等，然后点 `继续` ：
-fb6553df6b2eb6828bc268555aa1e2a3.png)

选择启用定位，点击继续
-f1a3211dd6bc436586070d619f1310ea.png)

取消分析，点击继续
-e0f3a99f5973f494dcb22ee9edcfea8c.png)

屏幕使用时间，点击稍后设置
-0ecbbebbf92f8b66cad2eec5bcd1573d.png)

外观，随便选适合自己的，以后设置中都能改，点击继续
-0968d1f675883fd8826ecdf0f5beb48e.png)

这样就进入系统了：
-7a2048e2284e49c05d4ebe9c86602a98.png)

看一下信息：
-f6741ed2bafd8e7339741fed8451cd8c.png)
#### 5.2.7 联网

先关机：
-eb9b935e709b2399efc40f7256cbaeee.png)

搜索 `服务` ，点击 `打开` ：
-8385a19876f753703c9d5aceaa274355.png)

找到 `VMware DHCP Services` ，点击启动：
-3a215ec30d430b76d1a47213e179dcc3.png)

找到 `VMware NAT Services` ，点击启动：
-94274e69b2ce7d1e6b92e53407fa882c.png)

回到VMware，重新开启虚拟机，进入系统验证是否联网：

网络已连接
-a74516e76d3a3cf5a4eb87ee4adfcb7b.png)

然后百度也可以打开了。
#### 5.2.8 解决系统窗口过小的问题

桌面上有一个光盘一样的东西，叫做 `Install macOS Ventura` ，在这个东西上面右键，选择 `推出“Install macOS Ventura”` ：
-9e352bb56da441fcfc55921f1ca4470a.png)

首先确保系统已经联网，然后在VMware软件上方点击 `虚拟机` ，然后点击 `安装 VMware Tools(T)...`
-1cba10c6c6367df547dddb97c8292a0a.png)

在弹出的小窗口中，双击 `安装 VMware Tools` ：
-c1cd84c48ae595cd087804706b1ac2e9.png)

开始安装VMware Tools安装器
-fe45a19cd2bdd9a4a6463b0131cb91cc.png)

点击安装
-3e478d86ee05d952891e2ad062c6217e.png)

输入密码，然后点击 `安装软件` ：
-94df920c4c0c061f4f65deed78468ebe.png)

选择安装器授权，是的
-79f0d35fbe0e9b7907c89a7242c9b441.png)

打开系统设置，授权
-08a238aa89c946995974f1d66fb2aa5b.png)

点击允许
-1a6dfa83b59f3fa58a5b513944a44318.png)

输入密码
-c181d324f71b9d0c9d650b7be247abcf.png)

点击重启机器
-844dc0f773f23b20e0cb772c4066fdb1.png)

重启完成后，就基于VMware全屏了：
-1d3e46065ca831709ebaeebfdd80e181.png)

大功告成！！！
-9d45664a41a4a9fa5a4f7225ee23413d.png)
## 6. 问题汇总
### 6.1 无限重启

一直重启，显示这个界面。

找到该虚机的vmx，在里面添加 `smc.version = "0"`
-41056f83ff5e03bacb04a77a5897a834.png)
## 6.2 AMD处理器无法正常启动看这个

找到该虚机的vmx，在里面添加

```bash
smc.version = "0"
cpuid.0.eax = "0000:0000:0000:0000:0000:0000:0000:1011"
cpuid.0.ebx = "0111:0101:0110:1110:0110:0101:0100:0111"
cpuid.0.ecx = "0110:1100:0110:0101:0111:0100:0110:1110"
cpuid.0.edx = "0100:1001:0110:0101:0110:1110:0110:1001"
cpuid.1.eax = "0000:0000:0000:0001:0000:0110:0111:0001"
cpuid.1.ebx = "0000:0010:0000:0001:0000:1000:0000:0000"
cpuid.1.ecx = "1000:0010:1001:1000:0010:0010:0000:0011"
cpuid.1.edx = "0000:0111:1000:1011:1111:1011:1111:1111"
smbios.reflectHost = "TRUE"
hw.model = "MacBookPro14,3"
board-id = "Mac-551B86E5744E2388"
keyboard.vusb.enable = "TRUE"
mouse.vusb.enable = "TRUE"
AI生成项目bash
```
## 7. 求关注

看在这么详细份上，点个关注吧！

没有Mac电脑也想用macOS专属AI软件？本教程手把手教你用VMware虚拟机在Windows电脑上安装macOS系统，全程超详细演示。

内容包括：
1. VMware 17 Pro下载安装
2. macOS-VMware补丁文件安装
3. 虚拟机创建与配置（CPU、内存、磁盘）
4. macOS系统安装全过程
5. 联网设置与窗口全屏
6. AMD处理器兼容方案

安装完成后，你就可以在Windows电脑上运行各种仅支持macOS的AI软件了，无需购买昂贵的Mac电脑。

所需文件：
- VMware 17 Pro安装包
- macOS系统镜像文件
- macOS-VMware补丁文件

三个文件缺一不可，下载链接在视频中有提供。

注意，相关视频中的内容，命令，脚本，代码，都在博客文章中会有 🔗https://869hr.uk

## 短信及语音接码平台

- 或https://smspva.com/?ref=1307601

纯净住宅IP白嫖流量
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

## 参考链接

- [YouTube视频原地址](https://www.youtube.com/watch?v=EToxhFmpbM0)
- [相关推荐](https://869hr.uk)

---

---

来源与反馈：[M. 的博客](https://869hr.uk) · [文章原页](https://869hr.uk/2026/tech/windows-desktop-macos-free-mac-ai-vmware-tutorial/)
