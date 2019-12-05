**搜索关键字： 开源项目中的 configure 文件**

开源软件中的configure文件的作用及原理
http://blog.chinaunix.net/uid-25267728-id-3557835.html

configure的作用是利用这个configure的脚本来查看你的linux的运行环境。然后生成一个Makefile文件，你就可以通过makefile文件编译你的项目了。

configure配置安装详解
https://blog.csdn.net/u010977122/article/details/52959098

Configure脚本配置工具就是基础之一，它是autoconf的工具的基本应用。

configure它是个shell脚本，主要用于编译安装源代码库和软件。


**搜索关键字： QT configure 文件**

Qt 头文件、CONFIG
https://blog.csdn.net/tianshi_1988/article/details/48272109
其转自：
qmake 之 CONFIG 与 QT 乱谈
https://www.cnblogs.com/hnrainll/archive/2011/05/20/2052335.html

构建一个C++程序：无非是编译(包括编译预处理)、链接 这几步。
编译时，我们需要让预处理器能找到我们的头文件(即：指定头文件路径)
链接时，我们需要让链接器能找到我们需要的库

头文件路径 如：$QTDIR/include
库文件 如：QtCore4.lib(或相应的其他形式)

分别采用g++和msvc进行编译：
g++ main.cpp -Ie:\Qt\4.7.0\include -o main -Le:\Qt\4.7.0\lib -lQtCore4
或
cl main.cpp -ID:/Qt/4.7.0/include -Femain  -link -LIBPATH:D:/Qt/4.7.0/lib QtCore4.lib

在C++中，使用第三方库的过程，就是包含头文件、链接库文件的过程。

简单看一下Qt的头文件和库文件，然后看看qmake是如何处理的：为什么我们不需要在.pro文件内指定这些头文件路径和库文件

C、C++ 尖括号或双引号内就是一个头文件的文件名。

include<QString> 需要指定查找路径 $QTDIR/include/QtCore 
include<QtCore/QString> 需要指定查找路径 $QTDIR/include 
文件 D:\Qt\Qt5.8.0\5.8\mingw53_32\include\QtCore\QString 。该文件就是一个无后缀的头文件。
其内部内容，包含“实体”头文件：
```
#include "qstring.h"
```
这是否可以算是一种跳转技术？

include<QtCore> 这也是头文件，而不是指目录。（文件可以无后缀）
其位置在： $QTDIR/include/QtCore/QtCore
D:\Qt\Qt5.8.0\5.8\mingw53_32\include\QtCore\QtCore

感觉：
include<QtXXX> 
QT 会自动在 $QTDIR/include/ 下查找子目录 QtXXX 中的 QtXXX 文件。即路径： $QTDIR/include/QtXXX/QtXXX
而 QtXXX 中通过 include 语句来包含该模块涉及到的“实体”头文件。
这里的分析不对，头文件和库的路径、库名等信息是通过 .pro 文件来确定的。如下说明：

和头文件比起来，库文件似乎就比较简单了。因为它们直接在 $QTDIR/lib 。

库：
动态库(共享库)、静态库(归档库)
不同平台下有不同的后缀。 .dll, .so, .dylib, .lib, .a
带调试信息，不带调试信息的库
windows下的动态库需要引导库（.dll 对就的 .lib ，非静态库）

.pro 文件
默认会省略的内容(因为是默认值，所以可以不写)
CONFIG += qt 
QT += core

CONFIG += qt
将使得最终包含:
头文件路径 $QTDIR/include
库文件路径 $QTDIR/lib

QT += core
将对Qt相关的路径进一步细化
头文件路径中 $QTDIR/include/QtCore
链接需要的库 QtCore4.lib
编译预处理的宏 QT_CORE_LIB

现在头文件路径和库文件都有了，而且，无论头文件写成 QString 还是 QtCore/QString 都能被找到。

感觉：
QT += xxx
QT 增加头文件查找路径， $QTDIR/include/QtXxx 。
QT 增加引用库 QtXxx.lib 。

由于在 .pro 文件内 CONFIG 中默认包含 qt ，QT 中默认包含 core ，这使得变得更加隐藏

- 默认包含 Qt Core 和 Qt GUI 模块。
If you use qmake to build your projects, the Qt Core and Qt GUI modules are included by default. 
https://doc.qt.io/archives/qt-5.6/qtmodules.html
 
当启用一个模块时，
要么是修改 CONFIG 变量。
要么是细化 QT 变量。（会多定义 QT_XXX_LIB 这样一个宏）
而有的模块，两者均可。

理解：
- 头文件 + 库（或者源码）
- 头文件和源码文件**不一定非得是 .h .cpp 的后缀。**都可以不需要后缀，如STL中的头文件就没有后缀，比如 ：
  + #include <cstring> 文件位置 D:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\include\cstring 是一个文件。
- 目前安装 Qt5.8.0 ，组件全选，安装后得到的头文件（从QT CREATEOR中查找头文件得到的路径）和库的类似根的路径。
  + D:\Qt\Qt5.8.0\5.8\mingw53_32\include
  + D:\Qt\Qt5.8.0\5.8\mingw53_32\lib
- 头文件的妙用。
- QT 隐藏了很多细节。（一些未写出来的默认内容。）
- QtXXX 说明即有 QtXXX 模块（目录），也有 QtXXX 文件。 QXXX 说明有 QXXX 文件。
- incldue 语句，从设计上来说，仅说明文件名，可以显示包含文件路径。但不会自动根据文件名来自动补充同名路径，这在设计实现上麻烦也不清晰。路径由其它地方来指定，两者进行组合确定位置。在其下查找即可（不递归子目录，简单高效）。
- .pro 文件用来配置头文件查找路径，库查找路径和库名。

**windows 下 QT 的 configure 脚本是 configure.bat**

**搜索关键字： %~dp0**

Bat脚本中%cd%和%~dp0的区别
https://jingyan.baidu.com/article/c275f6ba34105ee33c756762.html

%cd%和 %~dp0在bat脚本中出现的频率比较高，两者有相似，也有不同，稍不留神就会出错。

使用范围：
%cd%：批处理脚本(bat脚本)、命令行窗口
%~dp0：批处理脚本(bat脚本)

bat脚本执行时，两者代表的值是否会变化:
%cd%：会。因为代表的是当前目录
%~dp0：不会。因为代表的是脚本文件在磁盘的位置


示例脚本cd-dp0.bat内容：
@echo off
echo this is %%cd%% : %cd%
echo this is %%~dp0 : %~dp0

在C:\Users\Administrator执行脚本
C:\Users\Administrator>f:\cd-dp0.bat

执行结果：
this is %cd% : C:\Users\Administrator
this is %~dp0 : f:\


**搜索关键字： errorlevel**

errorlevel与%errorlevel%的区别
https://blog.csdn.net/hudashi/article/details/7042260

errorlevel与%errorlevel%的区别，他们都是判断上个命令的返回值。
当使用if errorlevel 值 cmmand 句式时，它的含义是：如果返回的错误码值大于或等于值 的时候，将执行cmmand操作；
当使用if %errorlevel%==值 cmmand 句式时，它含义是：如果返回的错误码值等于值 的时候，将执行cmmand操作。
一般上一条命令的执行结果返回的值只有两个，"成功"用0 表示 "失败"用 1 表示，实际上，errorlevel 返回值可以在0~255 之间。

**搜索关键字： bat for %%C **

bat(续七)-for语句(循环结构)
https://www.cnblogs.com/lm002003/archive/2012/05/15/2502439.html

无开关的for语句能够对设定的范围内进行循环，是最基本的for循环语句。其命令格式为：
FOR %%variable IN (set) DO command
其中，%%variable是批处理程序里面的书写格式，在DOS中书写为%variable，即只有一个百分号(%)；set就是需要我们设定的循环范围；do后面的command就是循环所执行的命令，即循环体。

BAT中
for %%C in (cl.exe icl.exe g++.exe perl.exe jom.exe) do set %%C=%%~$PATH:C
直接CMD中
for %C in (cl.exe icl.exe g++.exe perl.exe jom.exe) do set %C=%~$PATH:C
明显有一种换算：set perl.exe=D:\Perl64\bin\perl.exe

for %C in (cl.exe icl.exe g++.exe perl.exe jom.exe) do set %C=%~$PATH
没有明显的换算：set perl.exe=%~$PATH

for %C in (cl.exe icl.exe g++.exe perl.exe jom.exe) do set %C=~$PATH
没有明显的换算：set perl.exe=~$PATH

for %C in (cl.exe icl.exe g++.exe perl.exe jom.exe) do set %C=$PATH
没有明显的换算：set perl.exe=$PATH

for %C in (cl.exe icl.exe g++.exe perl.exe jom.exe) do echo %~$PATH:C
有明显的换算：echo D:\Perl64\bin\perl.exe

Path=D:\Perl64\site\bin;D:\Perl64\bin;C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem;C:\WINDOWS\System32\WindowsPowerShell\v1.0\;C:\Program Files (x86)\Microsoft SQL Server\100\Tools\Binn\;C:\Program Files\Microsoft SQL Server\100\Tools\Binn\;C:\Program Files\Microsoft SQL Server\100\DTS\Binn\;D:\Program Files\TortoiseSVN\bin;D:\Program Files\Microsoft SQL Server\110\DTS\Binn\;C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Binn\;D:\Program Files\Microsoft SQL Server\110\Tools\Binn\;C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Binn\ManagementStudio\;D:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\;C:\Program Files (x86)\Microsoft SQL Server\110\DTS\Binn\;C:\WINDOWS\System32\OpenSSH\;D:\Program Files\Git\cmd;C:\Program Files\Microsoft\Web Platform Installer\;C:\Program Files (x86)\Microsoft ASP.NET\ASP.NET Web Pages\v1.0\;C:\Program Files (x86)\Windows Kits\8.0\Windows Performance Toolkit\;C:\Program Files\MySQL\MySQL Shell 8.0\bin\;C:\Users\EDZ\AppData\Local\Microsoft\WindowsApps;;D:\Users\EDZ\AppData\Local\Programs\Fiddler;D:\Program Files\CMake\bin;C:\Users\EDZ\AppData\Local\Microsoft\WindowsApps

Path=
D:\Perl64\site\bin;
D:\Perl64\bin;
C:\WINDOWS\system32;C:\WINDOWS;
C:\WINDOWS\System32\Wbem;
C:\WINDOWS\System32\WindowsPowerShell\v1.0\;
C:\Program Files (x86)\Microsoft SQL Server\100\Tools\Binn\;
C:\Program Files\Microsoft SQL Server\100\Tools\Binn\;
C:\Program Files\Microsoft SQL Server\100\DTS\Binn\;
D:\Program Files\TortoiseSVN\bin;
D:\Program Files\Microsoft SQL Server\110\DTS\Binn\;
C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Binn\;
D:\Program Files\Microsoft SQL Server\110\Tools\Binn\;
C:\Program Files (x86)\Microsoft SQL Server\110\Tools\Binn\ManagementStudio\;
D:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\;
C:\Program Files (x86)\Microsoft SQL Server\110\DTS\Binn\;
C:\WINDOWS\System32\OpenSSH\;
D:\Program Files\Git\cmd;
C:\Program Files\Microsoft\Web Platform Installer\;
C:\Program Files (x86)\Microsoft ASP.NET\ASP.NET Web Pages\v1.0\;
C:\Program Files (x86)\Windows Kits\8.0\Windows Performance Toolkit\;
C:\Program Files\MySQL\MySQL Shell 8.0\bin\;
C:\Users\EDZ\AppData\Local\Microsoft\WindowsApps;;
D:\Users\EDZ\AppData\Local\Programs\Fiddler;
D:\Program Files\CMake\bin;
C:\Users\EDZ\AppData\Local\Microsoft\WindowsApps


