### 从源码安装

|从源码安装的步骤|
|------|
|`tar -zxvf 软件包（解压软件包）`：解压后的命令可以看见README或AAAREADME文件，这个文件非常重要，包含了软件安装所需要的操作|
|`make`命令会编译源码，然后连接器会为这个包创建最终的可执行文件|
|`make install `进行安装|

### 基于Debian的系统（发行版有Ubuntu）
+ `dpkg`命令是基于Debain系统PMS工具的核心，包含在这个PMS中的其他工具；dpkg包含的工具：`apt-get`、`apt-cache`、`aptitude`；命令行下使用`aptitude`命令有助于避免常见的软件安装问题；
#### 用aptitude管理软件包（在ubuntu 上没有）
+ 如果使用的Linux发行版中已经安装了aptitude，只需要在shell中输入aptitude即可；快速查看指定包的信息：`aptitude show package_name`；无法通过aptitude看到的一个细节是所有跟某个特定软件包相关的所有的文件列表，要得到这个列表，就必须用dpkg命令：`dpkg -L package_name`；同样可以进行反向操作，查找某个指定文件属于哪个软件包：`dpkg --search absolute_file_name`；注意：在使用的时候必须用绝对文件路径；
#### 用aptitude安装软件包
+ 要确定准备安装的软件包的名称如：`aptitude search package_name` 如 `aptitude search wine`；在显示的包列表中，每个包之前都会有一个`p`或`i`，其中含义如表；

|符号|含义|
|------|------|
|`i`|表示这个包现在已经安装到了你的系统上|
|`p`|表示这个包可用，但是没有安装|
|`v`|表示这个包可用，但是没有安装|
|`p` |表示软件包删除了并且配置文件也删除了|
|`c`|表示这个包已经删除但配置文件尚未从系统中清除|

+ 在系统上用aptitude从软件仓库中安装软件包非常简单：`aptitude install package_name`；

#### 用aptitude更新软件

|命令|说明|
|------|------|
|`aptitude safe-upgrade`|safe-upgrade选项会将所有已安装的包更新到软件仓库中的最新版本，更有利于系统稳定|
|`aptitude full-upgrade`|不会检查包与包之间的依赖关系|
|`aptitude dist-upgrade`|不会检查包与包之间的依赖关系|

#### 用aptitude卸载软件
+ 要想只删除软件包而不删除数据和配置文件，可以使用aptitude的remove选项，要删除软件包和相关的数据和配置文件可以使用purge选项：`sudo aptitude purge wine`；要看软件包是否已删除，可以利用aptitude的search选项，如果在软件包名称的前面看到一个C，意味着软件已删除，但配置文件尚未从系统中清除，如果前面的是个p的话，说明配置文件也已删除；

#### aptitude仓库
+ `aptitude`默认的软件仓库位置是安装Linux发行版时设置的，具体位置存储在文件`/etc/apt/sources.list`中；aptitude只会从这些仓库中下载文件，在搜索软件进行安装或更新时，aptitude同样只会检查这些库，如果想加入一些额外的库可以修改这个文件，但是要确保安全；

|/etc/apt/sources.list文件说明|
|------|
|deb (or deb-src) address distribution_name package_type_list|
|deb或deb-src说明软件包的类型，deb说明这是一个已编译程序源，deb-src说明这是源代码的源|
|address 是软件仓库的web地址|
|distribution_name 这个特定软件仓库的发行版版本的名称|
|package_type_list 条目可以不止一个词，它表明仓库里面有什么类型的包，如（main 、restricted、universe、partner）|

#### dpkg
+ 安装.deb文件：`sudo dpkg -i xxx.deb`；

