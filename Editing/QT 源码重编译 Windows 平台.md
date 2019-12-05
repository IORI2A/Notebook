```
下载 QT 离线安装包。（可跳转下载历史版本）
https://www.qt.io/offline-installers
下载了 QT 5.8.0 安装包和源码包 QT 5.6.3 源码包
QT 5.6.3 是目前检索到官方支持WINCE的最后版本。

Official mirror of the qt-project.org qt/ git repositories
https://github.com/qt
```

# Qt for Windows
https://doc.qt.io/archives/qt-5.6/windows-support.html

- 开发编译源码的环境要求。
ensure that your development environment fulfills the requirements.

## Qt for Windows - Requirements
https://doc.qt.io/archives/qt-5.6/windows-requirements.html

- 在 Windows 平台上编译源码时需要的一些库和环境配置。
This page describes the required libraries and environment for Qt for Windows.

- 默认要求一些第三方库
  + ICU
  + ANGLE
  + 如果动态的从git获取源码进行编译的话，还需要 OPENSSL

**ICU**

ICU - International Components for Unicode
http://site.icu-project.org/

- 实现更完善的 UNICODE 的支持。

- 一些环境变量配置要求。
include and lib folders
INCLUDE and LIB environment variables
bin folder
PATH environment variable

- Qt 5.3 版本后， configure 不再默认将 ICU 库链接到 Qt Core 中。这将减少发布应用程序的大小。
From Qt 5.3 and onwards, configure does not link Qt Core against ICU libraries anymore by default. This reduces the size of a self-contained application package considerably.

- 使用 ICU 的一些好处。

- 显示指定在 Qt Core 中使用 ICU 。
To explicitly enable the use of ICU in Qt Core, pass -icu to configure:
configure -icu

**ANGLE （图形驱动）** 

- 其官网不可访问。需要翻墙？

- 此库将 OpenGL ES 2.0 API 调用转换为 DirectX 11 或 DirectX 9 调用（取决于可用性），无需在目标计算机上安装图形驱动程序。
This library converts OpenGL ES 2.0 API calls to DirectX 11 or DirectX 9 calls (depending on availability), removing the need to install graphics drivers on the target machines.

- ANGLE 在 DirectX 好实现了 OpenGL ES 。
ANGLE implements the OpenGL ES 2.0 API on top of DirectX 11 or DirectX 9. 

- 编译QT时，ANGLE 要求 DirectX SDK 已经安装好。
ANGLE requires that the DirectX SDK is installed when building Qt.

- 渲染后端
render backend

- Qt 5.4 引入的环境变量 QT_ANGLE_PLATFORM 可用于设置渲染端。
the environment variable QT_ANGLE_PLATFORM (introduced in Qt 5.4) can be used to control the render backend. Possible values are d3d11, d3d9 and warp.

- 使用自实现的 ANGLE , 需要设置 ANGLE_DIR 环境变量。
To use a custom version of ANGLE, set the ANGLE_DIR environment variable to point to the ANGLE source tree before building Qt.

- 如果想使用其它的图形驱动（OpenGL driver）代替 ANGLE 。configure 时指定 -opengl desktop 。
If you installed additional OpenGL drivers from your hardware vendor, then you may want to consider using this version of OpenGL instead of ANGLE. To use OpenGL, pass the command line options -opengl desktop to the configure script.
configure -opengl desktop

- 使用 OpenGL ES 仿真器贷款 ANGLE 。
To use an OpenGL ES 2.0 emulator instead of ANGLE, use the configure options: -opengl es2 -no-angle.
configure -opengl es2 -no-angle

- 除了编译时加载 OpenGL 驱动， Qt 也支持运行时加载 OpenGL 驱动。（动态加载）
In addition to the build time configuration, Qt supports choosing and loading the OpenGL implementation at runtime. To use this mode, pass -opengl dynamic to the configure script.
configure -opengl dynamic

- 官方使用的是动态加载，也推荐使用动态加载。
Note: As of Qt 5.5 this is the configuration used by the official, pre-built binary packages of Qt. It is strongly recommended to use it also in custom builds, especially for Qt binaries that are deployed alongside applications.

- 即使是静态编译， ANGLE 库也是无法链接入的，仅能通过共享库模式使用。
Note: Combining -opengl dynamic with -static is also possible, but be aware that ANGLE will not be statically linked into the applications in this case, it will still be built as a shared library.


**编译源码涉及到的工具 （运行时不一定使用）**

- 涉及使用到一些基础工具(其工具执行文件，在QT编译过程中要能够通过PATH路径获取得到。)
  + PERL
  + PYTHON

- ANGLE 还依赖 GnuWin32 和 Win flex-bison 工具。
ANGLE depends on these extra tools from the GnuWin32 and Win flex-bison projects

- 重命名 bison 和 flex
Note: If you are building qtbase outside of qt5.git, you will need to download win_bison and win_flex from the link above and rename them to bison and flex.


**SDK 和编译器要求**

- 选择使用 MinGW （32、64）来编译。
A MinGW toolchain with g++ version 4.7 or higher. Qt 5 is tested regularly with a 32 bit gcc 4.9.1 toolchain from the MinGW-w64 project.

mingw-w64 官网
GCC for Windows 64 & 32 bits
http://mingw-w64.org/doku.php

**Qt WebEngine**

- Qt WebEngine 的编译有其他一些要求。
Qt WebEngine has additional build requirements which are listed in the Qt WebEngine Platform Notes.


## Qt for Windows - Building from Source
https://doc.qt.io/archives/qt-5.6/windows-building.html

- 路径不能包含空格。
Note: The install path must not contain any spaces or Windows specific file system characters.

- 设置环境变量。将设置项编为脚本来执行。
This is done by creating an application link passing a .cmd file setting up the environment and the command line option /k (remain open) to cmd.exe.
```
快捷方式:
%comspec% /k ""D:\temp\qt5vars.cmd"" x86

D:\temp\qt5vars.cmd 内容：

@echo off
REM Set up \Microsoft Visual Studio 2013, where <arch> is \c amd64, \c x86, etc.
REM CALL "C:\Program Files (x86)\Microsoft Visual Studio 12.0\VC\vcvarsall.bat" <arch>
CALL "d:\Program Files (x86)\Microsoft Visual Studio 9.0\VC\vcvarsall.bat" x86
SET _ROOT=D:\temp\qt_wnd
SET PATH=%_ROOT%\qtbase\bin;%_ROOT%\gnuwin32\bin;%PATH%
REM Uncomment the below line when using a git checkout of the source repository
REM SET PATH=%_ROOT%\qtrepotools\bin;%PATH%
SET QMAKESPEC=win32-msvc2008
SET _ROOT=
```

- 使用 MinGW 来编译，设置与上面相似。不同处： MinGW 安装路径加到 path 变量中，而不是调用 vcvarsall.bat 。
Note: Setups for MinGW are similar; they differ only in that the bin folder of the installation should be added to the path instead of calling the Windows SDK setup script. For MinGW, please make sure that no sh.exe can be found in the path, as it affects mingw32-make.

- 如果使用到其他三方库，将其相关路径回到环境变量中。
Settings required by the additional libraries (see Qt for Windows Requirements) should also go this file below the call to the Windows SDK setup script.

- configure 配置参数
https://doc.qt.io/archives/qt-5.6/configure-options.html

- 默认是源码目录内编译，可设置 -prefix 选项指定安装目录。
The default behavior of configure is to create an in-source build of Qt 5. If you want to install Qt 5 to a separate location, you need to specify the command line option -prefix <location>. 

- -developer-build 选项构建开发者使用包。
Alternatively, the command line option -developer-build creates an in-source build for developer usage.

- 选择使用 MinGW 来编译。
mingw32-make

- 使用 nmake distclean 清空构建内容。（build directory 构建目录）
Note: If you later need to reconfigure and rebuild Qt from the same location, ensure that all traces of the previous configuration are removed by entering the build directory and typing nmake distclean before running configure again.

# QT 解压包下的 README 文件

- 系统要求
System requirements
    - Perl 5.8 or later
    - Python 2.7 or later
    - C++ compiler supporting the C++98 standard

- 其他的特殊要求，参考
     For other platform specific requirements,
     please see section "Setting up your machine" on:
     http://wiki.qt.io/Get_The_Source

- Windows 平台，打开命令行，检测如下工具是否安装:
     Open a Windows SDK (7.0, 7.1 or later) command prompt. Ensure that the
     following tools can be found in the path:
     * Perl version 5.12 or later   [http://www.activestate.com/activeperl/]
     * Python version 2.7 or later  [http://www.activestate.com/activepython/]
     * Ruby version 1.9.3 or later  [http://rubyinstaller.org/]
     
- 可简单使用的方法。
  + PERL
    - perl -h
    - perl -v
  + PYTHON
    - python -？
    - pyhton -V
    - python --version
  + GIT
    - git --help
    - git --version


- 仅构建部分模块及其依赖模块。
 It is possible to build selected modules with their dependencies by doing
 a `make module-<foo>'.  For example, to build only qtdeclarative,
 and the modules it depends on:

   ./configure -prefix $PWD/qtbase <license>
   make -j4 module-qtdeclarative

- 从 git 构建。

- 构建文档。

# Qt5.7.0配置选项（configure options）
https://blog.csdn.net/caoshangpa/article/details/53706801
linux 平台

- 其实际是翻译于官方文档 [Qt Configure Options](https://doc.qt.io/archives/qt-5.6/configure-options.html)

configure是一个命令行工具，用于配置Qt编译到指定平台。
configure必须运行于Qt源码根目录。
当运行configure时，编译源码使用的是所选工具链中的make工具。

- 源码目录、编译目录和安装目录
源码目录就是包含源码的目录。
编译目录是包含Makefiles文件、object文件和其他中间文件的目录。
安装目录是二进制文件和库文件安装的目录。

- 当编译目录和源码目录不一样时，称为影子编译（shadow build）
方法就是新建一个目录，然后cd到该目录中运行configure。
此时，configure时生成的Makefiles文件，以及编译时生成的中间文件都会拷贝到编译目录。

- 通过影子编译，可以同时进行多个不同配置选项的编译过程，互不影响。

- -prefix 指定安装目录
默认的安装目录和平台相关，但是在configure时，可以通过-prefix选项指定安装目录，比如./configure -prefix /opt/Qt-5.7。
make install指令时，编译完成的bin、lib或者其他子目录就会拷贝到/opt/Qt-5.7目录中。

- 排除Qt模块
使用configure的-skip选项可以排除Qt模块，一般情况下模块名就是源码目录中对应的子目录名。

- 有些子目录会包含多个模块，比如说qtconnectivity目录就包含了Qt NFC模块和Qt Bluetooth模块，排除这两个模块需要将-skip qtconnectivity作为配置参数，如下所示。
./configure -skip qtconnectivity

- 包含或排除特性
-feature-<feature> 和 -no-feature-<feature>选项用于包含和排除特性。

- 可用的<feature>都被罗列在tbase/src/corelib/global/qfeatures.txt文件中。
要禁用accessibility特性，可用使用-no-feature-accessibility选项，如下所示。
./configure -no-feature-accessibility

- 第三方库 
Qt源码中包含了一些第三方库，如果想使用Qt自带的第三方库，可用通过-qt配置；如果想使用系统中的第三方库，可用通过-system配置。

- 禁用第三方库，用-no替换-qt就行。
./configure -no-zlib -qt-libjpeg -qt-libpng -system-xcb

- 编译选项。-platform选项指定了目标平台和编译时使用的编译器
./configure -platform linux-g++-32

- Qt支持的平台和编译器都在qtbase/mkspecs目录中。

- 对于Windows系统，可以用MinGW或者Visual Studio工具链。
configure.bat -platform win32-g++

- 交叉编译选项。 -xplatform：指定目标平台，可用的xplatform与platform类似，也在qtbase/mkspecs目录中。

- Windows中使用OpenGL选项
在Windows中，Qt可以配置使用系统的OpenGL或者自带的ANGLE。

- 默认情况下，Qt会配置使用ANGLE，ANGLE依赖于DirectX SDK。ANGLE使得依赖于OpenGL的Qt应用程序可以在没有安装OpenGL的机器上运行。

# Qt5.8 在windows下静态编译
https://blog.csdn.net/zhaoxd200808501/article/details/79368841
安装编译涉及到的工具，并验证。
在 QT Creator 的命令行中执行编译。
跳过了部分模块。
如果编译过之后发现有问题需要在没有编译过的源码基础上编译，在编译过的源码上编译出来有问题（我编译的时候没有重新用没有编译过的源码导致花了好多时间）。
将编译的版本配置到 QT Creator 构建套件中。


# 进行编译操作。

- 源码目录 D:\temp\qt
- 创建影子编译目录 D:\temp\qt_wnd
- 先使用windows编译工具，如上先创建 D:\temp\qt5vars.cmd 及快捷链接。
- 使用快捷链接(即 D:\temp\qt5vars.cmd)创建命令窗口。
- cd D:\temp\qt_wnd
- d:
- nmake distclean
  + 执行报错无效。
    * NMAKE : fatal error U1073: 不知道如何生成“distclean”
- D:\temp\qt\configure
  + D:\temp\qt\configure.bat 未指定其他参数。
  + 要求回答是否商业版？使用 -opensource 参数，自动回答为开源版本。
    * Which edition of Qt do you want to use ? 
  + 是否同意GPL协议？使用 -confirm-license 参数，自动回答同意。
    * Do you accept the terms of the license? 
  + 检测到未安装 DirectX SDK ，无法支持 ANGLE 。需要指定 -opengl desktop 使用 Open GL 。
    * WARNING: The DirectX SDK could not be detected:
    * ANGLE is no longer supported for this compiler.
    * Disabling the ANGLE backend.
    * WARNING: Using OpenGL ES 2.0 without ANGLE.
    * Specify -opengl desktop to use Open GL.
    * The build will most likely fail.
  + 编译目录下生成有 Makefile 文件，缓存文件 .qmake.super，及 qtbase 目录。
- nmake confclean
  + 执行报错无效。
- nmake distclean
  + 进行一系列删除操作，耗时较长。
- 删除清空 D:\temp\qt_wnd 下所有内容。
- D:\temp\qt\configure -debug -nomake examples -confirm-license -opensource
  + 仍然提示，检测到未安装 DirectX SDK ，无法支持 ANGLE 。


- D:\temp\qt\configure -debug -nomake examples -confirm-license -opensource -opengl desktop






















