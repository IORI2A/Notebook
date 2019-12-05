```
MySQL驱动插件(*qsqlmysql*) 与 MySQL驱动(*libmysql*) 是两个不同的东西。

```

MySQL 官网
https://www.mysql.com/
下载速度相当慢。
mysql-installer-community-8.0.18.0.msi
mysql-installer-web-community-8.0.18.0.msi

Qt连接MySQL
https://blog.csdn.net/cgzhello1/article/details/8619276
Qt4.8.4 + MySQL 5.1 + windows ，描述自己编译QMYSQL数据库插件，并简单调测验证。
QT4 一般情况下，只带了qsqlite4和qodbc两种驱动，不能直接使用mysql数据库。需要自己编译其他数据库驱动。
C:\MySQL\lib\opt\libmysql.lib
libqsqlmysqld4.a和qsqlmysqld4.dll
C:\MySQL\bin\libmySQL.dll

QT连接MySQL
https://www.cnblogs.com/zhaotian/p/5790068.html
Qt 5 + MYSQL 5.7 + linux ，描述需要MYSQL的动态链接库，并简单调测验证。
QT 提示只有 QMYSQL driver not loaded
Qt 访问 MySQL 需要 2 个动态链接库文件，一个是 Qt 自己的 MySQL 驱动插件，另一个是 MySQL 提供的动态链接库，缺一不可。
在程序里指定要访问的数据库为 MySQL，Qt 会自动的加载 MySQL 驱动插件，其实现依赖于MySQL 的动态链接库访问 MySQL。
Qt 5 的 SDK 默认提供了编译好的 MySQL 驱动插件，位于 plugins/sqldrivers ，可以直接使用。
Qt 4 需要我们自己编译 MySQL 的驱动插件。
opt/..../libmysqlclient.18.dylib
libmysqlclient.20.dylib

Qt+MySQL编程
https://blog.csdn.net/qq_29176963/article/details/82776559
Qt5.5.0 + MySQL5.7.17.0 + windows ，描述连接数据库、增删改查操作，及Qt+MySQL发布。
../MySQL/MySQL Server 5.7/lib/libmysql.dll
../MySQL/MySQL Server 5.7/lib/libmysql.lib

Windows 下实现 Qt 连接 MySQL
https://www.jianshu.com/p/df8d020c832f
Qt 5.9.0 + MySQL + windows ，描述需要QT的QMYSQL数据库插件 和 MYSQL的动态链接库，及重新编译QMYSQL数据库插件，并简单调测验证。
MySQL 提供的 libmysql.dll 和 libmysqld.dll 
Qt 自带已编译好的 qsqlmysql.dll 和 qsqlmysqld.dll 。**Qt安装目录\5.9\mingw53_32\plugins\sqldrivers\ **
安装 MySQL 可以去官网下载安装包，不过我不太喜欢这样做，因为现在 MySQL 的安装组件太多太杂，很多东西都是不必要。推荐去一些开源镜像站上下载对应版本，比如说 Tuna、USTC。

Ubuntu,QT5连接MySQL
https://www.cnblogs.com/HuangWj/p/5132887.html
QT5.5 +  MySQL + Ubuntu ，描述 libqsqlmysql 与 libmysqlclient 版本不匹配时可重新编译匹配。
libqsqlmysql.so ， plugin/sqldrivers
libqsqlmysql.so 依赖的 libmysqlclient*** 是低版本，自己编译 libqsqlmysql.so 。 

QT连接mysql（解决QT5.12无mysql驱动）
https://blog.csdn.net/u013894391/article/details/95097583
QT5.12.3 +  mysql8.0 + windows ，描述自带获取libqmysql，仅需从MYSQL获取 libmysql 。
自带MYSQL驱动，不用重新编译生成libqmysql库。
libmysql.dll 。
使用windeployqt.exe 复制依赖项时无法复制libmysql.dll。需要手动。

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'AM**6688';

在QT中使用MySQL数据库
https://blog.csdn.net/yunzhifeiti/article/details/72709140
QT5.4.2 +  mysql + windows ，描述重新编译qsqlmysql匹配MYSQL版本。
QT安装目录中的plugins/sqldrivers文件夹下是否存在 qsqlmysql.dll 文件
有时候即使有Mysql的驱动，仍然报错，说明QT中自带的Mysql的驱动不依赖，需要自己重新编译。
下载安装 MYSQL 。 https://dev.mysql.com/downloads/connector/c/ （ https://dev.mysql.com/downloads/c-api/ C API (libmysqlclient) ）

查询Windows下的dll/exe所依赖的文件
https://blog.csdn.net/jaryguo/article/details/52759961
VC的 dumpbin 工具。

d:\Program Files (x86)\Microsoft Visual Studio 9.0\VC>dumpbin /DEPENDENTS D:\Qt\Qt5.8.0\5.8\mingw53_32\bin\qsqlmysql.dll
Microsoft (R) COFF/PE Dumper Version 9.00.30729.01
Copyright (C) Microsoft Corporation.  All rights reserved.


Dump of file D:\Qt\Qt5.8.0\5.8\mingw53_32\bin\qsqlmysql.dll

File Type: DLL

  Image has the following dependencies:

    libgcc_s_dw2-1.dll
    KERNEL32.dll
    msvcrt.dll
    libstdc++-6.dll
    Qt5Core.dll
    Qt5Sql.dll
    libmysql.dll

Qt5.4以上版本使用MySQL数据库(避免各种坑)
https://blog.csdn.net/pp634077956/article/details/51093554
5.4以上版本已经装好了MySQL驱动插件。
安装Qt一定要勾选源码，后续可能涉及到编译源码。
安装MySQL的时候不要用默认安装的路径,那个里面有空格(比如/program files/…),Qt好像不能识别。
最好使用.zip的MySQL进行安装,用命令行配置安装也比较简单。
5.7.11以上版本的MySQL如果是MIS版本的,好像没有让你自己选择安装路径的选项。所以最好还是.zip格式的。

Qt5.8 下链接 Mysql 错误以及解决方法
https://www.cnblogs.com/hbrw/p/6753849.html
64 位 Qt 要用 64 位的 Mysql 驱动，32 位的 Qt 要用 32 位的Mysql 驱动
把 /Mysql/lib 下的 libmysql.dll 拷贝到 /Qt/mingw53_32/bin 下
mysql 8.0 加密方式变了，你可以重装选择旧的加密方式


**安装32位的 MYSQL 5.7.x(最大) ，获取32位的libmysql**
 
**再次安装 mysql-installer-community-8.0.18.0.msi ，在 MYSQL SHELL 中执行**
命令行连接到数据库服务器(MySQL server -> session)
\connect root:AM**6688@localhost:3306

使用哪个数据库(schema,对应其实就是数据库名)
\use <schema>
使用sys数据库。(schema = sys)
\use sys

切换到执行SQL语句。
\sql





QT5.12.0使用mysql8.0
https://blog.csdn.net/lwd512768098/article/details/89294518

