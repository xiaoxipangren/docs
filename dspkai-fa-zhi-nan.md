# DSP开发指南

## Xtensa Development Tools 安装

Xplorer支持在Linux（官方推荐RedHat）和Windows上安装。

### 准备工作

由于Xplorer没有64bit版本，如果你的操作系统是Linux 64bit的，需要先安装32bit的兼容包。

以下操作在Ubuntu版本14.04.4 LTS，内核版本4.2.0-27-generic上验证成功。



`sudo dpkg --add-architecture i386`

`sudo apt-get update`

`sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386`

`sudo apt-get install libx11-6:i386`

`sudo apt-get install gtk2-engines:i386`

`sudo apt-get install lib32ncurses5 lib32z1`

`sudo apt-get install libxtst6:i386`

`sudo apt-get install libgtk2.0-0:i386`

`sudo apt-get install lib32ncurses5`

`sudo apt-get install libcanberra-gtk3-0:i386`



### 安装

在Linux上执行



`chmod +x Xplorer-6.0.4-linux-installer.bin`

`./Xplorer-6.0.4-linux-installer.bin`



按提示安装即可。

在Windows上双击Xplorer-6.0.4-windows-installer.exe，按提示安装。

### 添加License

点击菜单栏的 "Help" - "Xplorer License Keys"，在弹出的对话框上点击"Install Software Keys"，输入License Address \(请向国芯支持人员索取），点击"Finish"。

如果可以看到图中红框提示就表示添加成功。

![](https://www.showdoc.cc/home/common/visitfile/sign/7f7f2ce484c1ebb869221fd3644aeb6e?showdoc=.jpg)



### 添加CORE

我们目前使用的DSP processor core是Hifi4\_bd7\_20161020\_A，需要手动添加到Xplorer中。

右键点击"System Overview"窗口中的"Configurations"，选择"Find and Install a Configuration Build"，在弹出的窗口中点击"Browser"并选择configuration文件（linux为Hifi4\_bd7\_20161020\_AR\_linux\_redist.tgz，windows为Hifi4\_bd7\_20161020\_AR\_win32\_redist.tgz），点击"OK"。

添加完成后，可以在"System Overview“窗口的"Configurations"中找到刚添加的"Hifi4\_bd7\_20161020\_AR"，如下图红框所示。

![](https://www.showdoc.cc/home/common/visitfile/sign/ef23c119040c00ae4fddf79bf1494398?showdoc=.jpg)



### 添加工作区

可以把别人导出的工作区添加到我们的Xplorer中。

例如，添加HiFi4\_VFPU\_Library\_v3\_1\_0.xws，在Project Explorer窗口中点击右键，选择”Import”，下拉Xtensa Xplorer，选中Import Xtensa Xplorer Workspace，点击Next，点击Browser，选择xtensa/XtDevTools/downloads/RF-2016.4/libs下的HiFi4\_VFPU\_Library\_v3\_1\_0.xws文件，点击Next，选中HiFi4\_VFPU\_library，点击Finish

