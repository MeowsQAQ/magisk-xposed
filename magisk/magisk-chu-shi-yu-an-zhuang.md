# Magisk 初识与安装

### **Magisk 是如何工作的？** <a id="ss-H2-1551071250826"></a>

在一些用户眼里，Magisk 与另一款名为 Xposed 的神器有着高度的相似性，部分群体当中甚至还存在着「Magisk 框架」这样的说法。

的确，二者的工作机制都是「拦截」。Xposed 通过劫持 Android 系统的 zygote 进程来加载自定义功能，这就像是半路截杀，在应用运行之前就已经将我们需要的自定义内容强加在了系统进程当中。

Magisk 则另辟蹊径，通过挂载一个与系统文件相隔离的文件系统来加载自定义内容，为系统分区打开了一个通往平行世界的入口，所有改动在那个世界（Magisk 分区）里发生，在必要的时候却又可以被认为是（从系统分区的角度而言）没有发生过。![](https://cdn.sspai.com/2019/02/25/82c9c372a64d21dce9d813c2fe9dbd7f.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)Xposed/Magisk 原理示意图

Magisk 的实现方式就像是一种魔法，当被挂载的 Magisk 分区被隐藏甚至被取消挂载时，原有系统分区的完整性丝毫未损，玩需要 root 验证的游戏、运行对设备认证状态有要求的应用甚至进行需要验证系统完整性的 OTA 更新**都没有任何问题**。![](https://cdn.sspai.com/2019/02/25/f9ba127eb6c341faadf8fbb3df725572.jpeg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)可通过 SafetyNet 认证并有针对性地隐藏 root

因此严格来说 Magisk 可以被看作是一种文件系统，这种文件系统通过巧妙的实现方式避开了对系统文件的直接修改，从稳定性上来看要优于以往任何一种系统框架，这也是当前它在玩机社区广受认可和好评的原因所在。

### 

### **它的魔力不止于 root** <a id="ss-H2-1551071255040"></a>

很多人对 Magisk 的初步认识可能是 root ——在 [SuperSU](https://sspai.com/post/27521) 销声匿迹之后，它自然而然就成为了当前 Android 社区用来获取 root 权限的主流方式。

不过 Magisk 特殊的运作机制还赋予了它相较于 Android 平台其他定制工具而言独一无二的特质——**systemless**。这种 systemless 特质让 Magisk 拥有了获取 root 权限之外的诸多优势：

**一方面，得益于独特的挂载机制，使用 Magisk 时我们可以有针对性地隐藏 root，甚至暂时隐藏 Magisk 本身**。

如此一来，不仅「root 模式下使用特定应用」成为了可能，就连无缝 OTA 更新这种「魔改党」们想都不敢想的事也变得不再遥远。在 Magisk Manager 应用的设置中，我们甚至还可以用随机包名对 Magisk 进行重新安装，让它从其他应用的眼皮底下彻底消失——多么具有魔法特质的高明手段！

![](https://cdn.sspai.com/2019/01/21/eb3e071124501d6c8fcd7a2aa7107693.jpeg?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

**另一方面，挂载系统的存在，也让 Magisk 拥有了多样的模块化生态系统。**  


既然用了「开外挂」的实现方式，那不妨就多挂载一些额外的东西，字体、音效、驱动……甚至 Xposed 本身。Magisk 提供了一个独立于系统分区以外的、可以随时隐形的「沙盒」，那自然不能将其才华禁锢于 root 这一件事上。在 Magisk 的模块仓库里，我们可以找到各式各样的模块（modules）来满足自己的定制化需求，借助这些模块，我们在 root 之后能做的事情其实也还有很多。

在这里的讨论语境下，Magisk 如何给人们留下「框架」这一认知误区的原因就浮出水面了。**只是功能方面好不逊色的 Magisk，稳定性和上手门槛对大部分用户来说都更加友好**。

### 

### **如何安装 Magisk** <a id="ss-H2-1551071306252"></a>

作为一套复杂的文件系统，Magisk 的安装步骤却是十分简单。

在电脑上配置好[ adb 环境 ](../other/windows-cao-zuo-xi-tong-xia-de-adb-huan-jing-pei-zhi.md)并解开 Bootloader 锁后，如果你的设备有来自 [TWRP](https://twrp.me/Devices/) 的官方支持，只需在打开 USB 调试后将手机与电脑相连，然后打开电脑端的命令行窗口：

1. 执行 `adb reboot bootloader` 进入 Bootloader 界面
2. 执行 `fastboot boot TWRP.img` 进入临时 TWRP 
3. 在 TWRP 中刷入你下载的 Magisk 安装包

没有官方 TWRP 支持的设备安装 Magisk 的步骤要稍微复杂一些：

1. 从你的刷机包中提取当前固件的 **boot.img** 文件，将它传入到安装了 Magisk Manager 的手机中
2. 进入 Magisk Manager —— 安装（install）—— install —— 修补 boot 镜像文件
3. 然后选择传入的 boot.img 文件进行生成，并将生成后的 Patchedboot.img （姑且这么命名） 传输到电脑上。

![](https://cdn.sspai.com/2019/02/25/d6c6262e70528a1126015ce8e993c26c.gif?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

随后我们使用 Magisk 应用对 boot.img 进行重新打包：

1. 打开命令行窗口
2. 执行 `adb reboot bootloader` 进入 Bootloader 界面
3. 执行 `fastboot boot Patchedboot.img` 来加载生成后的 boot 分区文件获取**临时 root**

此时进入系统，你会发现你已经成功安装了 Magisk（如果显示没有安装则为获取失败，请检查操作过程重新尝试），但这还不够，我们还得进入 Magisk Manager，选择安装（install）——install——Direct Install（直接安装）才能将临时 root 转换为永久 root。![](https://cdn.sspai.com/2019/02/25/410506b237682cbcde5545bc4d313bd4.gif?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)别忘了进行二次安装

[三星](https://topjohnwu.github.io/Magisk/install.html#samsung-system-as-root)、[华为](https://topjohnwu.github.io/Magisk/install.html#huawei)等特殊机型的 Magisk 安装方法参见 Magisk 官方帮助文档。

安装完 Magisk 后，我们就可以通过 TWRP 或者 Magisk Manager 刷入获取到的模块了。模块的获取方式可以是 Magisk Manager 自带的模块仓库，也可以是其他第三方论坛（如酷安、XDA 等）。  


卸载 Magisk 最为彻底的方式就是在 Magisk Manager 中点击「卸载」、「完全卸载」，应用会自动下载刷完 uninstall.zip 卸载包、自动卸载它自己、自动重启。如果你无法进入系统，在 TWRP 中手动刷入 uninstall.zip 卸载包即可。

