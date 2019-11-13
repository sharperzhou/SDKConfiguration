## 前言
多数软件开发工具都可以在跨平台下运行，通常这类软件为了兼容不同平台，都是通过类似配置文件或环境变量设置就能运行起来。虽然此教程是在Windows系统下写的，但也可以为在类Unix系统下软件配置作参考，因其原理基本类似。
本教程涉及的软件开发工具在官方网站一般都提供压缩包下载，虽然有些以安装包的形式下载，但其安装后的文件仍然可以拷贝到其他电脑上使用。

## 基础知识
+ 关于环境变量
> 1. 一般都设置 **系统变量** ，不要去设置用户变量。  
> 2. 最主要设置的地方是 **PATH** 变量，配置时需要追加项目，以半角分号分隔不同项目。  
> 3. 有些工具的配置需要新建环境变量值，如```JAVA_HOME```。  

+ 关于添加右键菜单项
> 1. 右键菜单项分为三种情况，分别为 **选中文件 (```\HKEY_CLASSES_ROOT\*\shell```)** 、 **选中文件夹 (```\HKEY_CLASSES_ROOT\Directory\shell```)** 和 **在文件夹内 (```\HKEY_CLASSES_ROOT\Directory\Background\shell```)** 弹菜单。
> 2. 通常是在 **shell** 项下新建一个所需要的项，再在该项下新建一个 **command** 项。
> 3. 涉及路径的项目，最好都加上引号，以免路径中存在空格而无法识别。


### CMake
* 下载地址：https://cmake.org/download/
* 解压位置，如 D:\SDK\CMake
* 环境变量  
    ```
    PATH=%PATH%;D:\SDK\CMake\bin
    ```

### git
* 下载地址：https://git-scm.com/downloads
* 解压位置，如 D:\SDK\Git
* 环境变量  
    ```
    PATH=%PATH%;D:\SDK\Git\cmd
    ```
* 右键菜单   
    ```
    [HKEY_CLASSES_ROOT\Directory\Background\shell\gitbash]
    @="Git Bash Here"
    "Icon"="D:\\SDK\\Git\\git-bash.exe"

    [HKEY_CLASSES_ROOT\Directory\Background\shell\gitbash\command]
    @="\"D:\\SDK\\Git\\git-bash.exe\" \"--cd=%v.\""
    ```
    > 注意：路径中有空格必须用引号，command中命令和参数都需要引号，command的参数是```"--cd=%v."```

### Java
* 下载地址：https://www.oracle.com/technetwork/java/javase/downloads/index.html
    > 注意：官网提供的JDK是安装包，但可以将安装包的内容拷贝到其他计算机使用。
* 解压位置，如 D:\SDK\Java\jdk1.8.0_191
* 环境变量
    ```
    JAVA_HOME=D:\SDK\Java\jdk1.8.0_191
    PATH=%PATH%;%JAVA_HOME%\bin
    ```
    > 注意：目前主流版本的JDK不需要设置CLASSPATH这一环境变量。

### MinGW
* 下载地址：https://sourceforge.net/projects/mingw-w64/files/
    > 32位系统建议下载 **i686-posix-dwarf** ，64位系统建议下载 **x86_64-posix-seh**
* 解压位置，如 D:\SDK\MinGW\x86_64-posix-seh-8.1.0
* 环境变量
    ```
    PATH=%PATH%;D:\SDK\MinGW\x86_64-posix-seh-8.1.0\bin
    ```

### nodejs
* 下载地址：https://nodejs.org/en/download/
* 解压位置，如 D:\SDK\node
* 环境变量
    ```
    PATH=%PATH%;D:\SDK\node;D:\SDK\node\npm_modules
    ```
* 配置npm
    ```
    $ npm config set prefix "D:\SDK\node\npm_modules"
    $ npm config set cache "D:\SDK\node\npm_cache"
    $ npm config set registry https://registry.npm.taobao.org
    ```

### nsis
* 下载地址：https://sourceforge.net/projects/nsis/files/
* 解压位置，如 D:\SDK\nsis
* 环境变量
    ```
    PATH=%PATH%;D:\SDK\nsis
    ```

### Python
* 下载地址：https://www.python.org/downloads/windows/
* 解压位置，如 D:\SDK\Python\Python37
* 环境变量
    ```
    PATH=%PATH%;D:\SDK\Python\Python37;D:\SDK\Python\Python37\Scripts
    ```
* 更新pip
    ```
    $ python -m pip install --upgrade pip
    ```
* 设置国内镜像
    ```
    $ pip config set global.index-url "https://pypi.tuna.tsinghua.edu.cn/simple"
    ```

