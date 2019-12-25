# [Xamarin.Android](https://docs.microsoft.com/en-us/xamarin/android/)

## [Get Started with Xamarin.Android](https://docs.microsoft.com/en-us/xamarin/android/get-started/)

### [Setup and Installation](https://docs.microsoft.com/en-us/xamarin/android/get-started/installation/)

#### [Windows Installation](https://docs.microsoft.com/en-us/xamarin/android/get-started/installation/windows)

- Windows 平台上为集成开发工具 Visual Studio 安装 Xamarin.Android
  + Xamarin 已经集成到 Visual Studio 中，可直接使用 Visual Studio 安装器(Visual Studio installer)。
  + [Installing Xamarin on Windows](https://docs.microsoft.com/en-us/xamarin/get-started/installation/windows)
  + 安装 Xamarin ，其子集组件 Xamarin.xxx （如 Xamarin.Android ）都将被安装。

- 配置 Xamarin.Android
  + Java Development Kit (JDK)  （使用 JDK 8）
  + Android SDK
  + Android NDK （安装无？？？）
  + 开发环境（安装路径），安装时有默认，安装后可变更。 Tools > Options > Xamarin > Android Settings 。

#### [Setting up the Android SDK for Xamarin.Android](https://docs.microsoft.com/en-us/xamarin/android/get-started/installation/android-sdk?tabs=windows)
- 运行 Xamarin Android SDK Manager 的一些要求：
  + Visual Studio 2017 version 15.7 or later is required.
  + Visual Studio Tools for Xamarin version 4.10.0 or later （伴随“Mobile development with .NET 工作负载”一同安装）。
  + Java Development Kit （伴随“Mobile development with .NET 工作负载”一同安装）。 （JDK 8）

- Xamarin Android SDK Manager 随着“Mobile development with .NET 工作负载”的安装一同安装。 

- Android SDK 管理器(Android SDK Manager)
  + 下载、安装 Android SDK 工具、平台和组件。(Android SDK tools, platforms, and other components)
  + Android API 等级(Android API level)
  + Tools > Android > Android SDK Manager
  + 默认是 Google Android SDK Manager 。（可安装最高版本为 25.2.3 的 Android SDK 工具包。）
  + 用于下载安装各种等级、版本的 Android SDK 工具包，其中包含各种组件。主要包括 Platforms 和 Tools 。
    - 各个版本的 Android 平台。
      + Android API level
    - 工具有
      + Android Emulator
      + low-level debugger (LLDB)
      + NDK
      + HAXM 加速
      + Google Play 库
    - 存储库选择
      + 默认情况下，Android SDK 管理器从由 Microsoft 托管的存储库下载平台组件和工具。 
      + 可以将 SDK 管理器切换为使用 Google 的存储库。 （使用 Google 存储库不受支持，因此不建议将其用于日常开发。）
  + Xamarin Android SDK 管理器插件(Xamarin Android SDK Manager plugin)。（可安装更高版本的 Android SDK 工具包）（可从 Visual Studio Marketplace 获取）
  + Google 的独立 SDK 管理器已在 Android SDK 工具包 25.2.3 版本中弃用。

#### [Android Emulator Setup](https://docs.microsoft.com/en-us/xamarin/android/get-started/installation/android-emulator/)
- 安卓模拟器(Android Emulator)  （Android 仿真器）
  + 用于调测运行程序。
  + 在计算机上模拟 Android 设备包括以下部分：
    - Google Android Emulator 。
      + [QEMU](https://www.qemu.org/) 通用性开源的机器仿真和模拟项目。
    - 仿真器映像 (An Emulator Image)
    - Android 虚拟设备 (AVD) (Android Virtual Device)
  + 针对 x86 体系结构进行优化的特殊仿真器映像。
  + 使用以下两项虚拟化技术之一可显著提高性能：
    - Microsoft Hyper-V 
    - Intel 硬件加速执行管理器 (HAXM) (Intel's Hardware Accelerated Execution Manager)

- 仿真出各种虚拟设备(virtual device)。

- 硬件加速设置。
  + 如果不启用硬件加速，模拟器可能会运行很慢。
  + x86 虚拟设备映像与虚拟化功能结合使用，可以极大地提高 Android Emulator 的性能。
  + 两种加速方式：
    - 使用 HYPER-V 加速。（Microsoft 的 Hyper-V 和 Windows 虚拟机监控程序平台） (Windows Hypervisor Platform)(WHPX)
      + 检查：cmd > systeminfo
      + Windows Features （启用或关闭 Windows 功能）
        - Hyper-V 
          + Hyper-V not on windows features
            - If Hyper-V is not shown in the Windows Features dialog then I assume you're using Windows 10 Home Edition. You need to upgrade to one of the more business orientated versions of Windows, Hyper-V is not available separately. https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/
        - Windows Hypervisor Platform （ Windows 虚拟机监控程序平台）
      + 安装仿真器包(Android Emulator package) 27.2.7 及以上
        - Tools > Android > Android SDK Manager > Tools
    - 使用 HAXM 加速。（Intel 硬件加速执行管理器） (Intel's Hardware Accelerated Execution Manager)(HAXM)
      + 检查：cmd > sc query intelhaxm
      + 安装包下载 [Intel Hardware Accelerated Execution Manager](https://github.com/intel/haxm)
  
- Android Device Manager  (Xamarin Android Device Manager) 
  + 创建和自定义虚拟设备(virtual devices)。
  + 自定义虚拟设备的配置文件属性(profile properties)。
  + 仿真模拟不现配置的硬件设备。
  + 注意一些运行要求。
  + Tools > Android > Android Device Manager
  + 选择一个设备，点击 Start 按钮启动运行。
  + 编辑 Android 虚拟设备的配置文件属性。  

#### [Set Up Device for Development](https://docs.microsoft.com/en-us/xamarin/android/get-started/installation/set-up-device-for-development)

- 设置 Android 设备，并连接到电脑，调测运行 app 程序。
  + 开启设备的调试(Debugging)模式。
    - Android 版本不同，可能设置上稍有差异。
  + 安装 USB 驱动。
  + 通过 USB 或者 WiFi 将设备连接到电脑。

### [Hello, Android](https://docs.microsoft.com/en-us/xamarin/android/get-started/hello-android/)

#### [Hello, Android: Quickstart](https://docs.microsoft.com/en-us/xamarin/android/get-started/hello-android/hello-android-quickstart?pivots=windows)

- 源码下载。[Xamarin.Android - Phoneword](https://docs.microsoft.com/en-us/samples/xamarin/monodroid-samples/phoneword/).

- Windows 系统要求。
  + Windows 10.
  + Visual Studio 2019 or Visual Studio 2017 (version 15.8 or later): Community, Professional, or Enterprise.
  
- 如果使用模拟器(Android emulator)，最好开启硬件加速(hardware acceleration)。

- 创建工程。
  + File > New > Project 
  + Android 模板。
  + 工程命名为 Phoneword 。
  + 空白工程(Blank App)。

- Android Designer 中可直接打开 .axml 和 .xml 文件。

- Resources folder > layout folder > activity_main.axml （最新版本可能是 content_main.axml ）
  + 程序的界面布局文件。

- Toolbox
  + Text (Large)
  + Plain Text (EditText)
  + Button 
  + TextView 
  
- Properties pane （属性面板）
  + Id 属性 @+id/PhoneNumberText ？？？

- 增加新文件。
  + Phoneword 工程 > 右键 > Add > New Item... 
  + Visual C# > Code > Code File
  + 文件命名为 PhoneTranslator.cs
  
- 编写代码。
  + 功能代码。 （业务代码？逻辑？）

- 连接用户界面 (Wire up the user interface)
  + 插入支持代码(backing code)。
  + MainActivity 类。 （自动生成，但可手动修改完善）
  + OnCreate 方法。
  + 加载界面。
  + 实现响应按钮点击事件。
  
- 构建代码。
  + Build > Rebuild Solution
  + 有关构建时出错的一引些解决建议。
  
- 设置 app 名称。
  + values folder > strings.xml > app name
  + Phone Word
  
- 在模拟器或者真实设备中运行 app 。
  + 参看其他链接。
  + 可参考上方 "Set Up Device for Development" 。
  + 设置运行的目标设备。
    - 问题：不支持的设备
      + 不能使用设备 Xiaomi HM NOTE 1S (Android 4.4 - API 19)， 因为设备API级别低于清单文件中定义的最低 Android 版本。
      + 处理方式：
        - 对比安装时选择的 Android 8.1 - Oreo 
          + Android SDK Platform 27
          + Google APIs Intel x86 Atom System Image
        - 选择安装 Android 4.4 - Kit Kat
          + Android SDK Platform 19
          + Google APIs Intel x86 Atom System Image
        - 变更工程项目属性。
          + 应用程序：使用 Android 版本编译：（目标框架），更改为 Android 4.4 (Kit Kat) 。 （原： Android 8.1 (Oreo) ）
          + Android 清单： 最低 Android 版本：，更改为 Android 4.4 (API 级别 19 - Kit Kat)。 （原： Android 5.0 (API 级别 21 - Lollipop) ）
        - **搜索： Mono.AndroidTools.InstallFailedException: Failure [INSTALL_FAILED_USER_RESTRICTED]**
          + [deploy fail Error: Mono.AndroidTools.InstallFailedException: Failure [INSTALL_FAILED_UPDATE_INCOMPATIBLE]](https://stackoverflow.com/questions/40541529/deploy-fail-error-mono-androidtools-installfailedexception-failure-install-fa)
        - **搜索： Failure INSTALL_FAILED_USER_RESTRICTED**
          + [Failure [INSTALL_FAILED_USER_RESTRICTED: Install canceled by user]](https://blog.csdn.net/hpp_1225/article/details/82491235)
          + [解决小米手机USB安装apk时AS报错：INSTALL_FAILED_USER_RESTRICTED](https://www.jianshu.com/p/368e161285cd)

#### [Hello, Android: Deep Dive](https://docs.microsoft.com/en-us/xamarin/android/get-started/hello-android/hello-android-deepdive?pivots=windows)

- 理解 Android 程序是如何工作的。
  + 根据示例程序来详解。
  
- 解析 Xamarin.Android 程序结构。
  + Anatomy （解剖）
  + 解决方案、工程 目录组织结构。
    - Properties （属性）
      + AndroidManifest.xml 描述 Xamarin.Android 程序的一些基本要求(requirements)
        - name
        - version number
        - permissions
      + AssemblyInfo.cs .NET无文件(.NET assembly metadata file)。包含程序的一些基本信息。
    - References （引用） 包含构建、运行程序需要使用的组件(assemblies)
      + .NET assemblies
        - System
        - System.Core
        - System.Xml
      + Xamarin's assembly
        - Mono.Android
    - Assets （资产） 包含运行时需要使用的文件。这些文件可通过生成的 Assets 类来访问。详情参见[Using Android Assets](https://docs.microsoft.com/en-us/xamarin/android/app-fundamentals/resources-in-android/android-assets?tabs=windows)
      + fonts
      + local data
      + text
    - Resources （资源） 包含程序使用到的资源。这些资源可通过生成的 Resource 类来访问。详情参见[Android Resources](https://docs.microsoft.com/en-us/xamarin/android/app-fundamentals/resources-in-android/?tabs=windows)
      + strings
      + images
      + layouts
      + AboutResources.txt 是对 Resources 的简明指南描述。
  + Resources 详解。
    - drawable 包含可绘制资源
      + images
      + bitmaps
    - mipmap 包含适用于不同启动器图标密度的可绘制文件。？？？
    - layout 包含 Android 界面布局设计文件 (.axml)
      + 模板默认创建的布局文件 activity_main.axml
    - values 包含存储数据值 XML 文件。
      + strings
      + integers
      + colors
      + 模板默认创建 Strings.xml 来存储字符串值(string) 
    - Resource.designer.cs 也即 Resource 类，包含各个资源的 ID 。是由 Xamarin.Android 工具自动生成。
      + 不要手动编辑， Xamarin.Android 会自动重写覆盖更改。

- app 基础知识和体系结构基础知识
  + Android 应用程序不具有单一入口点；即，没有类似 main 的代码行，来被操作系统调用，从而启动该程序。
  + 当 Android 实例化应用程序的一个类时，会启动该应用程序，此时 Android 将整个应用程序的进程加载到内存中。
  + 这种特性比较有用。增加程序复杂性。


AXML stands for Android XML
Android Designer

## [Deployment and Testing](https://docs.microsoft.com/en-us/xamarin/android/deploy-test/)

### [Debugging](https://docs.microsoft.com/en-us/xamarin/android/deploy-test/debugging/)

#### [Debugging on the Android Emulator](https://docs.microsoft.com/en-us/xamarin/android/deploy-test/debugging/debug-on-emulator?tabs=windows)

### [Preparing an Application for Release](https://docs.microsoft.com/en-us/xamarin/android/deploy-test/release-prep/?tabs=windows)

- 设置应用程序图标。
  + Properties > Android Manifest > Application icon
    - @drawable/icon
      +Resources/drawable/icon.png
  + Properties\AssemblyInfo.cs
    - [assembly: Application(Icon = "@drawable/icon")]
    - the namespace of the Application attribute is Android.App
    
- 设置应用程序版本号。
  + 版本号(Version Number)
    - 一个数值。
    - 安卓或者应用程序内部使用。
    - 应当不让用户看到。
    - AndroidManifest.xml
      + android:versionCode
  + 版本名称(Version Name)
    - 一个字符串。
    - 非内部使用。
    - 展示给用户看的。
    - AndroidManifest.xml
      + android:versionName
  + 版本号与版本名称无联性。
  + Properties > Android Manifest
    + Version Number
    - Version Name
    
- 收缩APK (Android application package)
  + 使用 Xamarin.Android 连接器(Xamarin.Android linker)优化管理代码级(C#)。
    - 配置： Properties > Android Options > Linking
  + 使用 ProGuard 在 Java 字节码级优化 APK 。
    - 仅在发布版本下才可设置。
    - 对 Xamarin.Android 程序没有影响 ？？？






