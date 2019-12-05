# Windows 平台
QT 编译64位程序。（为了对接 MYSQL 8.0.18.0 ，其libmysql是64位。）

QT 官方提供的 windows 平台上安装包(qt-opensource-windows-x86-mingw530-5.8.0.exe)仅支持32位。

使用32位安装包安装后得到的编译、运行工具 mingw53_32 。
编写一个32位下可编译运行的程序。

搜索关键字： QT 64

1. 首先考虑使用64位的 mingw 。

- **下载安装 mingw-w64**

MinGW (32)： http://mingw.org/
MinGW 64位 (MinGW-w64 - for 32 and 64 bit Windows)
项目主页： https://sourceforge.net/projects/mingw-w64/
官网： http://mingw-w64.org/doku.php/start

参考：
Qt+Mingw环境(32位+64位)
https://blog.csdn.net/baidu_40840693/article/details/81225571

下载 mingw-w64-install.exe 。

Version : 5.3.0
Architecture ： x86_64
Threads : posix
Exception : seh
Build revision : 0

C:\Program Files\mingw-w64\x86_64-5.3.0-posix-seh-rt_v4-rev0

配置mingw-w64执行程序环境变量(Path) 
C:\Program Files\mingw-w64\x86_64-5.3.0-posix-seh-rt_v4-rev0\mingw64\bin

使用 gcc -v 检测，最后包括输出
gcc version 5.3.0 (x86_64-posix-seh-rev0, Built by MinGW-W64 project)

- **配置使用 mingw-w64**

配置使用 mingw-w64 来编译mingw 32位下可编译运行的程序。

在 qt 中增加 mingw-w64 构建套件。
Tools->Options->Build&Run->Kits
配置对应 QT version 时，要求对应xx位。强制配置 Qt 5.8.0 MinGW 32bit 。
进行工程代码编译，报大多数标识符无法识别。

Qt Creator 工具是否是64位应当无关。主要是 Qt 各个库模块须要与位数匹配。











如何在Windows上编译64位QT
https://blog.csdn.net/hello_wyq/article/details/78166351


MinGW-w64构建64位Qt
https://zhuanlan.zhihu.com/p/40271922


