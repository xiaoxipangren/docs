## 一: 主机环境

两种方案介绍

* 直接安装ubuntu 16.04 64位操作系统
* 使用win7 64位系统,虚拟机使用ubuntu 16.04 64位或者ubuntu 14.04 64位

资源包提供:ubuntu-14.04.3-desktop-amd64.iso,ubuntu-16.04.2-desktop- amd64.iso

## 二: 开发板套件提供的软件二进制包介绍

资源包提供:

* boot
* gxscpu.boot
* mcu.bin
* u-boot-spl.bin
* u-boot.img
* leo\_robot.dtb
* zImage
* root-brcm2708.tar.gz openwrt-brcm2708-bcm2709-rpi-2-ext4-sdcard.img

下面进行简单的说明  
boot: linux环境下运行的串口烧录工具  
gxscpu.boot:串口烧录工具boot使用的,进行烧录的片上运行程序mcu.bin:  
u-boot-spl.bin:将u-boot从flash拷贝到SDRAM中并运行的一个程序

u-boot.img:uboot,bootloader  
leo\_robot.dtb:系统设备树, linux kernel相关  
zImage:linux kernel  
root-brcm2708.tar.gz:根文件系统openwrt-brcm2708-bcm2709-rpi-2-ext4-sdcard.img:sd卡可烧录的根文件系统

## 三: 软件烧录和运行

我这里主要讲解开发工程师调试环境下的操作

第一步: 开发板串口接上CK uart端和PC端。开发板上电,这个时候win7系统会要 求我们安装usb串口驱动,使用资料包提供的“CH341SER-开发板串口驱动.zip”进行 安装

第二步: 使用PC端的串口工具,比如SecureCRT,发板串口接上CK uart端和PC端, 开发板上电,这个时候SecureCRT会有串口输出 。串口参数为115200,8N1

第三步: 切入到ubuntu虚拟机,设置虚拟机,识别到usb串口：![](/assets/USB serial.png)

## 第四步: 在linux下,通过mcu端的串口来烧写mcu.bin,uboot,leo\_robot.dtb

将boot工具拷贝到“/bin”目录下

> 例如: 执行:boot -b gxscpu.boot -d /dev/ttyUSB0 -c serialdown 0 mcu.bin

给出提示后,按下开发板reset键开始进行烧写， 烧写的先后顺序如下：

> mcu.bin:  
> boot -b gxscpu.boot -d /dev/ttyUSB0 -c serialdown 0 mcu.bin
>
> uboot:  
> boot -b gxscpu.boot -d /dev/ttyUSB0 -c serialdown 0x100000 u-boot-spl.bin
>
> boot -b gxscpu.boot -d /dev/ttyUSB0 -c serialdown 0x200000 u-boot.img
>
> dtb:  
> boot -b gxscpu.boot -d /dev/ttyUSB0 -c serialdown 0x300000 leo\_robot.dtb

## 第五步:通过TFTP加载linux kernel

Win7上运行资源包提供的tftpd32.exe\(Tftpd32\_cn\_bkill.com目录内\) 比如:TFTP服务器主机IP为192.168.1.188。开发板IP我们设置为192.168.1.211将zImage,leo\_robot.dtb放到TFTP目录上。

> 注意:开发板串口接上ARM uart端和PC端,开发板接上网线,然后开发板上电,这 个时候会通过串口工具看到uboot的打印,回车,进入uboot的命令模式![](/assets/uboot_screen.png)

这个时候,通过uboot进行开发板TFTP下载的网络设置 命令如下:

> 设置服务器： setenv serverip 192.168.1.188 
>
> 本机设置：setenv ipaddr 192.168.1.211
>
> 配置保存：saveenv

通过TFTP加载linux内核,命令如下:

> run netload

注意:这个命令是把linux内核加载到指定位置的内存上,但是并不会运行, 可以看到下载过程:![](/assets/download.png)

下载完毕后,显示如下:![](/assets/downlaod_done.png)

## 第六步:通过NFS加载root fs根文件系统

Linux环境下搭建NFS服务器

安装服务:

> sudo apt-get install nfs-kernel-server

配置: 编辑/etc/exports

/opt 192.168.\*\(rw,sync,crossmnt,no\_subtree\_check,no\_root\_squash\)以上配置使/opt目录及子目录可被192.168.\*网段的nfs客户端访问,可根据实际情况

配置: 重启nfs服务:

> sudo service nfs-kernel-server restart

将root-brcm2708.tar.gz解压到 ”/opt/rootfs”目录下 在开发板上通过uboot命令进行NFS启动的设置:

> setenv nfsboot "setenv bootargs console=ttyS0,115200 init=/init root=/dev/nfs rw nfsroot=192.168.1.161:/opt/rootfs/root-brcm2708 ip=192.168.1.211;bootz ${loadaddr} - ${fdt\_addr}"
>
> saveenv

然后开发板上执行:run nfsboot, 就可以看到linux kernel启动,并加载rootfs,最后启动demo程序。

注意:rootfs文件系统要修改下,否则网络会异常

编辑根目录下/etc/config/network,将以下参数屏蔽:

> \#config interface 'lan'
>
> \# \#option type 'bridge'
>
> \# option ifname 'eth0'
>
> \# option proto 'static'
>
> \# option ipaddr '192.168.111.136'
>
> \# option netmask '255.255.254.0'
>
> \# option ip6assign '60'



## 第七步:进入开发板的命令行 按q键退出demo程序

Demo测试语句:{

"dialog":\[ {

"pattern":\["\(早上\|下午\|晚上\|你\)好"\],

"answer":\["你也好啊"\] },{

"pattern":\["\(你\|萝卜头\)\(是谁\|叫什么名字\)"\],

"answer":\["我叫萝卜头,是一个萌萌哒的机器人"\] },{

"pattern":\["\(你\)?\(妈妈?\|爸爸?\)是谁","你从哪里来"\],

"answer":\["我来自杭州国芯科技,哈哈"\] },{

"pattern":\["\(你\)?\(能\|会\)\(干\|做\)\(些\)?什么","\(你\)?有\(些\)?\(什么\|哪些\)功能"\],

"answer":\["我会唱歌,跳舞,陪你聊天啊"\] },{

"pattern":\["再见","拜拜","关机"\],

"answer":\["拜拜"\] },{

"pattern":\["\(你\)?用\(的是?什么\|了谁的\|了什么\)芯片"\],

"answer":\["我装配了杭州国芯科技公司最新研发 的神经网络芯片,代号GX8010,它就是我的大脑"\]

},{  
 "pattern":\["\(你\)?\(可以\|能\)\(不联网\|离线\)工作\(吗\|嘛\)"\], "answer":\["我的芯片里有神经网络处理器,所以我可以离线进行

深度学习思考,是不是很厉害"\] },{

"pattern":\["\(你\)?\(支持\|有\)麦克风阵列吗","\(你\)?有几\(颗\|个\)

麦克风"\],

"answer":\["我有8通道数字麦克风和模拟麦克风接口,支持PDM和I方S接口,再加上最新的DSP处理器,可以做各种麦克风阵列处理哦"\]

},{  
 "pattern":\["\(芯片\|待机\)\(的\)?功耗怎么样"\], "answer":\["我采用了动态功耗调整和多级功耗唤醒技术,不仅运

行时功耗低,更可以超低功耗待机哦"\] },{

"pattern":\["芯片\(什么架构\|有几个核\)"\],

"answer":\["我的芯片采用的是多核异构模式,里面不仅有CPU还有DSP,更强大的是有两颗神经网络处理器哦"\]

},{  
 "pattern":\["\(哪里\|怎么\|怎样\)\(能\)?买\(到\)?\(这颗\)?芯片","芯

片多少钱"\],

"answer":\["这个要找我们小鸡哥哥了,他负责我们销售"\] },{

"pattern":\["\(小鸡哥哥\|他\)\(的\)?电话\(是\)?\(多少\|什么\)","电话 号码","手机号码\(是多少\)?"\],

"answer":\["小鸡哥哥电话是15906608826,快打给他吧"\] },{

"pattern":\["^萝卜头$"\],

"answer":\["我在啊","有事吗","有事您说话"\] },{

"pattern":\["明天天气\(怎么样\)?"\],

"answer":\["我猜明天应该是晴天"\] },{

"pattern":\["现在几点"\],

"answer":\["不好意思,今天没带表"\] },{

"pattern":\["一加一\(等于\)?\(几\|多少\)?"\],

"answer":\["当然等于二"\] }

\]

}

## 八: 软件运行的基本流程介绍

Linux kernel跑起来以后,将加载网络的nfs rootfs文件系统。 然后执行:/usr/bin/startapp

内容如下:

> \#!/bin/bash
>
> /home/gx/ai/ai.sh restart
>
> senseflow -c /usr/share/senseflow/sf/ai\_input\_vsp.sf -c /usr/share/senseflow/sf/ai\_output.sf

senseflow是我们的demo主程序。ai.sh将启动AI服务,进行skill的解析和对应动作的执行。

ai会运行三个python服务,ai是服务器的模式,这里相当于把它做到了本地端:

> ai service aiskills ai agent

senseflow在/usr/bin目录下。我们看下,在demo中,一个skill是如何运转的?

在文件系统\home\gx\ai\src\skills目录下可以看到许多我们实现好的skill我们demo使用的聊天skill是:chat\_local,唱歌skill是:music\_local

现在来说下,这个skill的运转流程：

通过senseflow,我们的声音被麦克风采集,内部进行ASR处理,转化为我们熟悉的文字格式。比如我说:“你是谁“,那么这个声音的波形被转化为文字形式的 “你是谁”。 这个文字数据最后传送到python服务的handler\_new\_chat\_intent函数中。（参考文件夹: chat\_local进行讲解,music\_local进行讲解。）

解释:handler\_new\_chat\_intent,gen\_speak\_action,get\_chat\_answer注意:先走默认的结巴分词方式,最后都不匹配才进入聊天模式

