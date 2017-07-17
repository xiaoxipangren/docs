# 构建开发环境

## 硬件配置

如下图构建开发环境：![](/assets/NFS开发环境2.001.png)

## 服务器准备

1. 安装[Ubuntu 16.04.2 LTS](https://www.ubuntu.com/download/desktop)，也支持Ubuntu 14.04 LTS。
2. 安装TFTP服务器：  
   `sudo apt-get install tftpd-hpa`  
   配置TFTP服务器： `sudo vim /etc/default/tftpd-hpa`  
   将原来的内容改为： `TFTP_USERNAME="tftp"`  
   `TFTP_ADDRESS="0.0.0.0:69"`  
   `TFTP_DIRECTORY="/opt/tftpboot" #服务器目录,需要设置权限为777,chomd 777 /opt/tftpboot`  
   `TFTP_OPTIONS="-l -c -s" # 这里是选项,-c是可以上传文件的参数，-s是指定tftpd-hpa服务目录，上面已经指定`  
   将zImage和leo\_robot.dtb拷入/opt/tftpboot  
   重启TFTP服务器  
   `sudo service tftpd-hpa restart`

3. 安装 NFS服务器  
   `sudo apt-get install nfs-kernel-server  
   `配置NFS服务器  
   `sudo vim /etc/exports  
   `添加以下条目：  
   `/opt/nfs *(rw,sync,no_all_squash,no_subtree_check,no_root_squash)  
   `重新启TFTP服务器  
   `sudo service nfs-kernel-server restart`



