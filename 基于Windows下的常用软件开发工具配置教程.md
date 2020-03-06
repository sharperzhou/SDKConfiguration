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
    ```r
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
    ```js
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
    ```r
    $ python -m pip install --upgrade pip
    ```
* 设置国内镜像
    ```r
    $ pip config set global.index-url "https://pypi.tuna.tsinghua.edu.cn/simple"
    ```

### Qt
* 官方下载地址：http://download.qt.io/official_releases/qt/ 
* 国内镜像地址：https://mirrors.tuna.tsinghua.edu.cn/qt/official_releases/qt/ 
* 解压位置，如 D:\SDK\Qt\5.9.7
* 环境变量
    ```
    QTDIR=D:\SDK\Qt\5.9.7
    QT_PLUGIN_PATH=%QTDIR%\plugins
    PATH=%PATH%;%QTDIR%\bin
    ```
    > 注意：windows下必须设置plugin目录，否则编译后程序无法启动
    > 如果使用QtCreator，因QtCreator中也存在plugin，可能与Qt中的plugin存在冲突，因此在QT_PLUGIN_PATH环境变量中还需要添加QtCreator的plugin目录，两者用分号分隔环境变量值

### VSCode
* 下载地址：https://code.visualstudio.com/#alt-downloads
* 解压位置：D:\SDK\VSCode
* 在任意文件显示右键菜单项
    ```r
    [HKEY_CLASSES_ROOT\*\shell\VSCode]
    @="用 VSCode 打开"
    "icon"="D:\\SDK\\VSCode\\Code.exe,0"

    [HKEY_CLASSES_ROOT\*\shell\VSCode\command]
    @="D:\\SDK\\VSCode\\Code.exe \"%1\""
    ```

* 在任意文件夹显示右键菜单项
    ```r
    [HKEY_CLASSES_ROOT\Directory\shell\VSCode]
    @="用 VSCode 打开"
    "icon"="D:\\SDK\\VSCode\\Code.exe,0"

    [HKEY_CLASSES_ROOT\Directory\shell\VSCode\command]
    @="D:\\SDK\\VSCode\\Code.exe \"%1\""
    ```

* 在文件夹内按shift显示右键菜单
    ```r
    [HKEY_CLASSES_ROOT\Directory\Background\shell\VSCode]
    @="用 VSCode 打开"
    "icon"="D:\\SDK\\VSCode\\Code.exe,0"
    "Extended"=""
    "NoWorkingDirectory"=""

    [HKEY_CLASSES_ROOT\Directory\Background\shell\VSCode\command]
    @="D:\\SDK\\VSCode\\Code.exe \"%v\""
    ```

> 注意命令参数的区别，在文件或文件夹上显示右键菜单的命令参数为 ```%1``` ，在文件夹内显示的命令参数为 ```%v```  
> 在文件夹内按shift键显示右键菜单需要设置名称为 **Extended** 和 **NoWorkingDirectory** 的数值项，如果直接右键显示则无需设置这两项

### vim
* 下载地址：https://github.com/vim/vim-win32-installer/releases
* 解压位置：D:\SDK\vim
* 环境变量
    ```
    PATH=%PATH%;D:\SDK\vim
    ```
> 经过以上配置，可以初步使用vim，在命令行中输入vim或gvim就可以进行编辑。更高级的用法需要配置vimrc文件及插件。

* 配置vimrc文件，使vim拥有语法高亮、出现行号及tab按空格缩进等功能
  1. 打开powershell，输入如下命令
        ```bash
        $ vim ~/.vimrc
        ```
  2. 进入vim窗口，按键盘 `i` 进入 **编辑模式** ，此时可输入内容，按如下进行输入
        ```vim
        set number
        syntax on
        set tabstop=4
        set shiftwidth=4
        set expandtab
        ```
  3. 按键盘 `Esc` 退出 **编辑模式** ，再按键盘 `:` ，此时可在窗口左下角输入命令，输入 `wq` 会保存编辑并退出vim，返回powershell窗口

* 安装插件管理器，推荐使用vim-plug插件
  1. 打开powershell，输入如下命令在用户目录下新建目录
        ```bash
        $  mkdir -p ~/vimfiles/autoload
        ```
  2. 再次输入如下命令，下载 `plug.vim` 文件并放到 `autoload` 文件夹下
        ```bash
        $uri = 'https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim'
        (New-Object Net.WebClient).DownloadFile(
            $uri,
            $ExecutionContext.SessionState.Path.GetUnresolvedProviderPathFromPSPath(
                "~\vimfiles\autoload\plug.vim"
            )
        )
        ```
        > 该步骤操作完全可以在浏览器中输入地址：https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim ，手动下载该文件并放到对应的文件夹即可。
  3. 配置vimrc文件，添加一个示例插件，用vim打开vimrc文件，在上一步骤中配置的.vimrc文件中附加如下内容
        ```vim
        " 指定插件存放的位置
        call plug#begin('~/vimfiles/plugged')

        " 所有插件必须plug#begin()和plug#end()所标记的区域内
        " 每个插件以Plug命令开始，每行一个
        " Plug后跟插件地址，每个地址使用单引号包裹

        " 如下安装一个C++语法高亮插件
        Plug 'octol/vim-cpp-enhanced-highlight'

        call plug#end()
        ```
        > 推荐一个vim插件网站：https://vimawesome.com/ ，搜索想要的插件，网站会给出vim-plug类型的安装地址，拷贝至vimrc文件中对应的plug#begin()和plug#end()所标记的区域内

  4. 保存vimrc文件，退出vim并重新加载vimrc文件，依次按 `Esc`，`:` 切换到vim的命令模式，然后输入 `PlugInstall` 安装实例插件，完成后可输入 `PlugStatus` 查看插件的状态。vim-plug的插件仓库为：https://github.com/junegunn/vim-plug ，在此可查看命令的说明及使用。



### MySQL
* 国内镜像地址：https://mirrors.tuna.tsinghua.edu.cn/mysql/downloads/
* 解压位置，如 D:\SDK\MySQL
* 环境变量
    ```
    PATH=%PATH%;D:\SDK\MySQL\bin
    ```
* 配置过程
  1. 在 **解压位置** 下新建 **my.ini** 文件，假定数据存储在 **data** 文件夹，设置如下配置
        ```ini
        [mysql]
        default-character-set=utf8
        [mysqld]
        port=3306
        basedir="D:/SDK/MySQL"
        datadir="D:/SDK/MySQL/data"
        max_connections=200
        character-set-server=utf8
        default-storage-engine=INNODB
        ```
  2. 以 **管理员身份** 打开命令行工具，输入如下命令生成不带密码的root用户
        ```
        $ mysqld --initialize-insecure
        ```
        > 如果需要重新初始化，必须先清空data文件夹
  3. 接着在命令行工具中 **安装** 并 **启动** 服务
        ```
        $ mysqld -install
        $ net start mysql
        ```
        > 注意，停止及卸载服务命令为  
        >    ```
        >    $ net stop mysql
        >    $ mysqld -remove
        >    ```
  4. 接着，无密码进入MySQL
        ```
        $ mysql -u root
        ```
  5. 登录后，为root账户设置密码，并开启远程登录
        ```sql
        use mysql; -- 切换至mysql数据库
        update user set authentication_string=password('新密码') where user='root';  -- 修改新密码
        update user set host='%' where user='root';  -- 授予远程访问权限
        flush privileges;  -- 刷新数据库
        exit; -- 退出数据库
        ```
  6. 退出数据库后，通过ip地址和密码登录，并指定登录端口号
        ```
        $ mysql -h 192.168.x.x -u root -p -P 3306
        ```
