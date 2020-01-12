# Windows 操作系统下的 ADB 环境配置

## Windows7-

不少 Pixel 和 Nexus 手机用户都接触过工厂镜像，在手动刷入工厂镜像的过程中，我们时不时总会遇到这样那样的问题——这其中的大部分问题都与 **ADB 环境的配置**有关。

因此，为了便于日后进行索引，这里分享一下 Windows 环境下进行 ADB 环境配置的正确操作。

（注：本文以 Windows 7 为例进行操作，Windows 10 同样适用，个别设置项位置可能会有所不同，请善用搜索）

### **下载 platform-tools** <a id="ss-H2-1503303176891"></a>

从今年年初开始，Google 开始在 Android Studio 官方网站上单独提供 platform-tools 下载。

platform-tools 是 Android SDK 的一部分，它能为我们架起在 Windows/Mac/Linux 平台上直接与 Android 进行交互的「桥梁」。大家在各大教程里经常见到的 `fastboot`、`adb` 等指令就必须依赖 platform-tools 才能正确执行。

下载地址：

* https://developer.android.com/studio/releases/platform-tools.html

### **配置环境变量** <a id="ss-H2-1503303183154"></a>

下载好 platform-tools 进行解压，定位至如下位置：请进行精确定位

![](https://cdn.sspai.com/2017/08/17/b1c39ade6e8d7067afc718170142ff81.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

复制该曾目录的路径备用，为行文方便，这里将目录记为 **A**。

电脑端，定位至 `控制面板\系统和安全\系统` 目录下，点击面板左侧的 `高级系统设置` 打开系统属性面板，在 `高级` 选项卡中找到 `环境变量`。这里以 Windows 7 为例

![](https://cdn.sspai.com/2017/08/17/aa93dcee6c6a839b1817d74a0a337b45.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

在 `环境变量` 面板下方的 `系统变量` 中找到名为 `Path` 的变量进行编辑。

![](https://cdn.sspai.com/2017/08/17/737b53587531a567aa40c22e01bd6677.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

遵循「半角引号+路径」的格式，在编辑窗口的 `变量值` 末尾加上我们前面复制的目录 **A**，即「;A」。![](https://cdn.sspai.com/2017/08/17/d4ba1ecdd45453cb09f51db90b503dd5.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)请严格按照格式添加路径

添加完成后保存，环境变量就配置好了。我们日后在使用的过程中可以「随时随地」调用 platform-tools 提供的 `adb`、`fastboot` 等指令；你也可以使用「Windows 徽标键 + R」、键入 `cmd` 并回车、然后输入 `adb version` 来检测环境是否配置正确。图为正确配置后的输出结果

![](https://cdn.sspai.com/2017/08/17/823918ebcddd1bbf1af9196e5b884212.png?imageView2/2/w/1120/q/90/interlace/1/ignore-error/1)

最后，如果 `platform-tools` 目录不小心被删除，按照上面的步骤重新下载并更新 Path 变量中的地址即可。

