# 安装
<!-- toc -->


## Introduction(简介)
有很多种方法可以在不同平台上安装并运行Tomcat。相关主要内容在文档`RUNNING.txt`中。如果本文内容未能解答您的问题，欢迎阅读该txt文档。

## Windows
在Windows上安装Tomcat通过Windows安装工具即可轻松完成。此安装工具的界面及功能与其他有安装向导的安装工具非常类似，仅有几处地方需要我们留心一下：

* **作为一个服务安装(Installation as a service)**: 无论你选择了什么配置，Tomcat都会被当做一个Windows服务来安装。在组件页面勾选『自动启动』选项，Tomcat将随Windows的开机时同时启动。出于安全方面的因素考虑，Tomcat服务会以一个权限更小的单独用户来运行。（具体请参见Windows服务管理工具及相关文档）
* **Java安装路径（Java location）**:Tomcat安装包会提供一个默认的JRE用于运行Tomcat服务。该安装包会依据注册表中的信息来确定所使用的Java7或者是更新版本的JRE的路径，其中也包括JDK中含带的JRE。在64位的系统中，安装包会优先寻找64位的JRE，只有当64位的JRE无法找到时，才会考虑定位32位的JRE。安装时并不强制要求使用默认的JRE配置。任何已安装的Java7或更新版本的JRE（32位或64位）都可被使用。
* **托盘图标（Tray icon）**：当Tomcat作为一个服务运行时，系统托盘栏中并不会展示任何相关图标。注意：当在安装结束时选择运行Tomcat，此时却会展示一个托盘图标。
* 关于如何管理Tomcat Windows服务的相关内容，请参阅文档[Windows Service HOW-TO][1]

该安装包会创建一个用于启动和配置Tomcat的快捷方式。需要注意的是，Tomcat Administrator 应用只有在Tomcat运行时才可使用。

## Unix后台进程
Tomcat可通过commons-daemon项目中的jsvc工具以后台进程的方式运行。编译jsvc需要用到的的源代码tar包已经囊括在Tomcat的的二进制文件中。构建jsvc需要一个符合ANSI标准的C编译器（比如GCC），GNU Autoconf和一个JDK。

在执行构建脚本之前，需要设置好指向JDK根路径的名为JAVA_HOME的环境变量。或者，在执行./configure脚本的时候通过`--with-java`参数设置指定的JDK路径。比如像这样：`./configure --with-java=/usr/java`

此处我们假设使用了GNU TAR压缩工具，以及`CATALINA_HOME`是一个指向Tomcat安装根路径的环境变量。通过以下命令，应当可以在`$CATALINA_HOME/bin`文件夹下产生编译好的jsvc的目标二进制文件。

```bash
cd $CATALINA_HOME/bin
tar xvfz commons-daemon-native.tar.gz
cd commons-daemon-1.0.x-native-src/unix
./configure
make
cp jsvc ../..
cd ../..
```

以下命令可以让Tomcat以后台进程的方式运行。

```bash
CATALINA_BASE=$CATALINA_HOME
cd $CATALINA_HOME
./bin/jsvc \
    -classpath $CATALINA_HOME/bin/bootstrap.jar:$CATALINA_HOME/bin/tomcat-juli.jar \
    -outfile $CATALINA_BASE/logs/catalina.out \
    -errfile $CATALINA_BASE/logs/catalina.err \
    -Dcatalina.home=$CATALINA_HOME \
    -Dcatalina.base=$CATALINA_BASE \
    -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager \
    -Djava.util.logging.config.file=$CATALINA_BASE/conf/logging.properties \
    org.apache.catalina.startup.Bootstrap
```

如果你的Java虚拟机默认是以服务器模式运行而不是客户端模式的话，你还会需要设置参数`-jvm server`。这一问题在Mac OSX系统中就有遇到过。

jsvc还有一些其他有用的参数，比如说`-user`参数将会在后台进程初始化完成后切换至指定的另一个用户下。这样做的好处是，Tomcat可以以一个普通用户的身份运行却拥有占用特殊的端口。需要注意的一点是，如果你想以`root`角色启动Tomcat，你则需要禁用`org.apache.catalina.security.SecurityListener`检查，以免在启动时阻止你以`root`角色启动。

`jsvc --help`命令会显式完整的jsvc使用信息。特别是`-debug`参数在运行调试jsvc中相当有用。

文件`$CATALINA_HOME/bin/daemon.sh`可作为系统启动自动化脚本`/etc/init.d`中使用jsvc自动启动Tomcat的模板脚本。

注意，我们此处说的这种启动Tomcat后台进程的方法，需要在你的运行环境的classpath中含有`Commons-Daemon`的JAR包文件。`Commons-Daemon`包一般情况下存在于`bootstrap.jar`的manifest文件的Class-Path路径下，但是如果你在运行时遇到`ClassNotFoundException`异常或者是`NoClassDefFoundError`异常，则需要在运行时通过`-cp`参数手动指定`Commons-Daemon`的路径。



[1]:http://tomcat.apache.org/tomcat-8.0-doc/windows-service-howto.html
