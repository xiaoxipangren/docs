# GX8010 用户开发指南

## 简介

GX8010芯片是[杭州国芯科技股份有限公司](http://www.nationalchip.com/)（股票代码836173）为智能音箱开发研制的高度集成的单芯片方案，它具有如下的特点：

* 集成了ADC，支持多达8路麦克风输入（也可支持数字麦克风和PDM输入）；
* 集成了一颗用于语音处理的DSP，可运行自动增益控制、降噪、波束合成、寻向、回声消除、去混响、特征值提取等语音前处理算法；
* 集成了两颗用于语音识别的神经网络处理器（NPU），可运行[TensorFlow](https://www.tensorflow.org/)模型，实现激活词识别、语音识别、语音合成等深度神经网络算法；
* 集成了音频解码器，支持WAV/MP3/MP4/AAC/HE-AAC等大部分音频格式；
* 集成了ARM Cortex A7处理器，带有Neon浮点处理单元，最高主频1Ghz；
* 集成了1Gb DDR3内存；
* 集成了SDIO、USB Host、USB Slave、SPI、I2C、I2S、BT1120等扩展接口；
* 集成了动态功耗管理，和多级唤醒机制，实现低功耗待机；
* 可运行Linux和RTOS等主流嵌入式操作系统

为了帮助开发者了解和熟悉GX8010，特推出GX8010评估板，它具有如下的特点：

* 6+1路圆形麦克风阵列，信噪比 &gt; 65dB，灵敏度 &gt; -26dBV @ 94dB 1KHz；
* 12颗三色LED环，可调整亮度和色彩；
* 4个按钮开关；
* 板载802.11 b/g/n Wi-Fi模块（SDIO接口）和3dBi陶瓷天线，支持AirKiss；
* USB Host接口，可通过USB Hub连接更多的USB设备；
* USB Device接口，可实现UAC、UVC、MS、PTP等USB设备；
* 8MB SPI NOR Flash（可替换成128MB SPI NAND Flash）；
* TF卡插槽；
* 2路USB UART调试接口，连接MCU和ARM；
* 40脚扩展接口（兼容树莓派扩展板）；
* 尺寸与名片相仿（85mm x 56mm，双层PCB）；
* 支持USB供电；

随评估板提供的软件有：

* 工具链；
* Linux Kernel 4.4.25；
* [SenseFlow](https://github.com/NationalChip/SenseFlow)；
* 根文件系统（带有离线语音识别的演示程序）；

如需了解详情和订购评估板，欢迎联系我们：

* 电话：+86-15906608826（季先生）
* 电邮：jihw@nationalchip.com



