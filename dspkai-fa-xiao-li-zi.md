## Hello World!

创建Helloworld工程，编写main.c。然后按下图红色区域配置后，点击"Build Active"编译，点击"Run"运行。![](https://www.showdoc.cc/home/common/visitfile/sign/7dce3a4b25ac45d99b376ef398268afb?showdoc=.jpg)

## 命令行配置

为了方便在命令行使用编译工具，可以把工具链添加到系统PATH路径下。

~/.bashrc中添加：

`export PATH="$PATH:${XTENSA_PATH}/XtDevTools/install/tools/RF-2016.4-linux/XtensaTools/bin" #其中XTENSA_PATH为xtensa的安装路径`

在使用工具链时，需要指定core的名称和路径，可以通过环境变量来指定。

~/.bashrc中添加：

`export XTENSA_CORE=Hifi4_bd7_20161020_A`

`export XTENSA_SYSTEM=${XTENSA_PATH}/XtDevTools/install/builds/RF-2016.4-linux/Hifi4_bd7_20161020_A/config #其中XTENSA_PATH为xtensa的安装路径`

## IDE环境导入源代码编译运行

以fft\_demo为例，步骤如下

1. 新建工程，导入源代码

- 点击菜单"File" - "New" - "Xtensa C/C++ Project"

- "Project Name"中填写项目名称"demo"，"Import Source For Project"中选择fft\_demo源代码所在的目录，

- "Project Type"选择"Create an executable image"，点击"Finish"

2. 按下图红框配置好

![](https://www.showdoc.cc/home/common/visitfile/sign/e8f19f13f3a169b1bb00c475369ceed7?showdoc=.jpg)

3. 右键点击"Project Explorer"窗口中的"demo"工程，选择"Build Properties..."，“Include Paths"中点击"Add"图标，点击"File System..."选择所需要的头文件路径"~/xtensa/Xplorer-6.0.4-workspaces/workspace/HiFi4\_VFPU\_library/include"，点击"OK"，"Apply"，"OK"

4. 右键点击"Project Explorer"窗口中的"demo"工程，选择"Library Dependencies..."，在"Available libraries"中选择"HiFi4\_VFPU\_library"，点击"Add"，点击"Apply"，"OK"

5. 点击"Build Active"编译，点击"Run"运行







