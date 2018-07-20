### 软件程序管理
+ Ubuntu Linux发行版本采用的是`/etc/init.d`目录，将开机时启动或停止某个应用的脚本放在这个目录下；
#### 硬件设备管理
+ Linux为系统上的每个设备都创建了一种称为设备节点的特殊文件，与设备的所有通信都通过设备节点完成，每个设备节点都有唯一的数值对供Linux内核识别它，数值对包括一个主设备号和一个次设备号，类似的设备被划分到同样的主设备号下，次设备号用于标识主设备组下的某个特定设备；
### Ubuntu快捷方式

|Ubuntu快捷方式|功能|
|------|------|
|`Ctrl/Shift+鼠标点击文件`|实现多选文件|
|`Shift+delete`|永久删除文件|
|`Ctrl+s`|保存文件|
|`Ctrl+h`|显示隐藏文件|
|`Ctrl+f`|在文件中查找|
|`Ctrl+L` |在文件夹中输入网址|
|`F3`|显示两个文件夹|
|`F2`|重命名|

### 安装linux系统
+ 将系统放到U盘中，开机按F2进入BIOS模式，然后选择启动盘，就会有机械提示操作即可；
### 通过图形化终端仿真访问CLI（经常使用的这个）

|快捷方式|功能|
|------|------|
|Ctrl+Alt+T|快速打开图形化终端|
|Shift+Ctrl+N|启动新的终端，但是必须在原本有终端的情况下，并且该终端获取到焦点|
|Shift+Ctrl+T|在原有终端中启动一个标签页，在该终端获取焦点时有效|
|Shift+Ctrl+W|关闭当前获取焦点的标签页|
|Shift+Ctrl+Q|关闭当前终端|
|Shift+Ctrl+C|将所选的文本复制到GNOME的剪切板中|
|Shift+Ctrl+V|将GNOME剪切板中的文本粘贴到会话中|
|F11|打开/关闭终端窗口全桌面显示模式|
|Ctrl+-|逐步减小窗口显示字号|
|Ctrl+0|恢复默认字号|
|Shift+Ctrl+F|打开find窗口，提供待搜索文本的搜索选项|
|Ctrl+PageDown|使下一个标签页成为活动标签|
|Ctrl+PageUp|使上一个标签页成为活动标签|
|Shift+Ctrl+PageUp|使当前标签页移动到前一个标签页的前面|
|Shift+Ctrl+PageDown|使当前标签页移动到下一个标签页的后面|
|Ctrl+L|清屏终端|

### 通过Linux控制台终端访问CLI（虚拟控制台）
#### 进入虚拟控制台
+ `Ctrl+alt+F1~Ctrl+alt+F6`；其中F几就表示虚拟控制台几，在打开的虚拟控制台中有tty2的字样表示虚拟控制台2；虚拟控制台中不能运行任何图形化程序；
#### 登录虚拟控制台
+ 在进入虚拟控制台需要登录，输入用户名和密码；
#### 退出虚拟控制台
+ Ctrl+alt+F7；
#### 设置虚拟控制台

|设置虚拟控制台的背景色和文本颜色|
|------|
|setterm -inversescreen on 打开了inversescreen特性使用on，背景色为白色、文本颜色为黑色|
|setterm -inversescreen off 关闭了inversescreen特性使用off，背景色为黑色，文本颜色为白色|
|setterm -background white 设置背景色为白色（颜色可选：black、red、green、yellow、blue、magenta、cyan、white）|
|setterm -foreground black 设置文本颜色为黑色（颜色可选：black、red、green、yellow、blue、magenta、cyan、white）|

#### 用于设置前景色和背景色的setterm选项

|选项|参数|描述|
|------|------|------|
|-background|black、red、green、yellow、blue、magenta、cyan、white|将虚拟控制台背景色改为指定颜色|
|-foreground|black、red、green、yellow、blue、magenta、cyan、white|将虚拟控制台的前景颜色改为指定颜色|
|-inversescreen|on或off|交换背景色和前景色|
|-reset|无|将虚拟控制台外观恢复到默认设置并清屏|
|-store|无|将虚拟控制台的前景颜色和背景颜色设置为-reset选项显示的颜色但是不清屏|

### shell的类型
+ 用户ningbaoqi使用GUN bash shell作为自己的默认shell程序；可以查看：`cat /etc/passwd`；bash shell程序位于/bin目录下的bash，该文件是可执行程序；默认的交互shell会在用户登录某个虚拟控制台终端或在GUI中运行终端仿真器时启动；可以使用`./可执行文件`来启动可执行文件，并且可以使用exit命令来退出bash shell；

### shell的父子关系
+ 执行shell的可执行文件就可以创建新的shell，这个新启动的shell被称为子shell，启动这个shell的shell就是父shell；在生成子shell进程时，只有部分父shell进程的环境被复制到子shell环境中；子shell可以从父shell中创建，也可以从另一个子shell中创建；

|bash shell程序可使用命令行参数修改shell启动方式|描述|
|------|------|
|`-c string`|从string中读取命令并进行处理|
|`-i`|启动一个能接受用户输入的交互shell|
|`-l`|以登录shell的形式启动|
|`-r`|启动一个受限shell 用户会被限制在默认目录中|
|`-s`|从标准输入中读取命令|

#### 进程列表
+ 可以将多个命令一起输入，用；做分割就形成了命令列表；命令列表要成为进程列表，这些命令就需要包含在（）内：如：`（pwd；ls；cd /etc；pwd；cd；pwd；ls）`这样在执行进程列表的时候将会生成一个子shell来执行对应的命令；要想知道是不是生成了子shell，需要借助环境变量的命令 ：`echo $BASH_SUBSHELL `如果返回0表示没有生成子shell，如果返回大于0的数说明存在子shell；如：`（pwd；ls；cd /etc；pwd；cd；pwd；ls；echo $BASH_SUBSHELL）`；
#### 探索后台模式
+ `sleep 10 `将会使终端睡眠10秒（但是现在是在前台）；要想置于后台模式：`sleep 10&`（需要在命令后面加&符号，将会创建子shell执行）；显示后台作业信息：jobs  显示当前运行在后台模式中的所有用户的进程；后台模式非常方便，可以让我们在CLI中创建出有实用价值的子shell；
#### 协程
+ 协程可以同时做两件事，它在后台生成一个子shell，并在这个子shell中执行命令；进行协程处理，要使用 coproc 命令：`coproc sleep 10`；生成子shell的成本不低，而且速度慢，创建嵌套的shell更是火上浇油；
