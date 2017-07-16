## Hardware Guide

### 框架图

![](/assets/diagram.png)

### 接口位置

* 正面  
  ![](/assets/top.png)

* 反面  
  ![](/assets/bottom.png)

### 接口说明

| 位号 | 说明 |
| :--- | :--- |
| J1 | MCU JTAG接口 |
| J2 | TF卡插座 |
| J4 | Wi-Fi陶瓷天线 |
| J5 | ARM调试串口（板载USB UART） |
| J6 | MCU调试串口（板载USB UART） |
| J9 | 扩展接口（40脚，兼容树莓派扩展板） |
| J10 | USB Device |
| J13 | USB Host |
| J14 | PCM OUT的MCLK的测试脚 |
| J23 | 3.5mm 音频输出接口 |
| J30 | 静音跳线 |
| J34 | DC 5V输入 |
| D2 | 电源输入指示 |
| D5 | 功能指示 |
| K1 | 复位按钮 |

### 扩展接口说明

| 功能 | 序号 | 序号 | 功能 |
| :---: | :---: | :---: | :---: |
| 3.3V | 1 | 2 | 5V |
| SDA1 | 3 | 4 | 5V |
| SCL1 | 5 | 6 | GND |
| GPIO2 | 7 | 8 | UART1 TX |
| GND | 9 | 10 | UART2 RX |
| GPIO3 | 11 | 12 | GPIO2 |
| GPIO5 | 13 | 14 | GND |
| GPIO8 | 15 | 16 | GPIO4 |
| 3.3V | 17 | 18 | GPIO10 |
| SPI\_MOSI/GPIO7 | 19 | 20 | GND |
| SPI\_MISO/GPIO9 | 21 | 22 | GPIO11 |
| SPI\_SCK/GPIO6 | 23 | 24 | GPIO17 |
| GND | 25 | 26 | GPIO18 |
| SDA2/GPIO13 | 27 | 28 | SCL2/GPIO14 |
| GPIO19 | 29 | 30 | GND |
| GPIO21 | 31 | 32 | GPIO20 |
| GPIO28 | 33 | 34 | GND |
| TDI/GPIO22 | 35 | 36 | TDO/GPIO23 |
| TMS/GPIO24 | 37 | 38 | TCK/GPIO25 |
| GND | 39 | 40 | TRST/GPIO26 |



