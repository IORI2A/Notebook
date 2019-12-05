# 下载 linux 操作系统

Ubuntu downloads
https://ubuntu.com/download

-> Ubuntu Desktop -> see our alternative downloads -> Past releases and other flavours (Past releases) -> old-releases.ubuntu.com -> Ubuntu 16.04.5 LTS (Xenial Xerus)

Ubuntu 16.04.1 LTS (Xenial Xerus)
http://old-releases.ubuntu.com/releases/xenial/

选择列表中的 ubuntu-16.04.5-desktop-amd64.iso

参考：
Ubuntu 16.04.5 LTS（Xenial Xerus）发布，该系列最后一个版本
https://www.linuxidc.com/Linux/2018-08/153339.htm


# 在虚拟机中安装 ubuntu 

ubuntu+eclipse开发环境搭建
http://www.emtronix.com/download/ubuntu_eclipse.pdf

虚拟机名 emtronix-linux
用户名 emtronix-linux
密码 AM**6688

# ubuntu+Qt 开发环境搭建

ubuntu+Qt开发环境搭建
http://www.emtronix.com/download/ubuntu_qt.pdf

## 交叉编译工具链安装

ESM6802-toolchain-x86_64.sh（主板产品光盘中获得，在产品光盘的“工具”文件夹中）

## Qt 安装

qt-unified-linux-x64-3.0.0-online.run（主板产品光盘中获得，在产品光盘的“工具”文件夹中）

官方下载 qt-unified-linux-x64-3.0.0-online.run
https://download.qt.io/archive/online_installers/3.0/

运行 ./qt-unified-linux-x64-3.0.0-online.run 报错：
bash: ./qt-unified-linux-x64-3.0.0-online.run: Permission denied

修改权限
chmod u+x qt-unified-linux-x64-3.0.0-online.run
再次执行
sudo ./qt-unified-linux-x64-3.0.0-online.run
要求输入用户密码

安装默认目录
/opt/Qt

在线下载太慢。
下载离线安装包 qt-opensource-linux-x64-5.8.0.run
安装默认目录 /opt/Qt5.8.0

参考：
qt linux下配置安装
https://www.cnblogs.com/haoyijing/p/5783537.html
