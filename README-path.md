### 什么是环境变量
+ bash shell用一个叫做环境变量的特性来存储有关shell会话和工作环境的信息，这项特性允许你在内存中存储数据，以便程序或shell中运行的脚本能够轻松访问他们，这是存储持久数据的简单方法；
#### 全局环境变量
+ 全局环境变量对于shell会话和所有生成的子shell都是可见的；局部变量只对创建他们的shell可见； Linux系统在你开始bash会话时就设置了一些全局环境变量，系统环境变量基本上都是全大写字母，以区别普通用户的环境变量，你的登录方式会影响到所设置的环境变量；查看所有的全局环境变量可以使用：`env`、`printenv`；要显示个别环境变量的值可以使用printenv命令，但是不能使用env命令：`printenv 变量名` 如：`printenv HOME`；也可以使用echo显示变量的值：使用echo引用某个环境变量时，需要在变量前加一个美元符号$ 如：`echo $HOME($HOME 可以当做命令行参数 如 ls $HOME)`；
#### 局部环境变量
+ 局部变量只对创建他们的shell可见；显示某个特定进程的所有的环境变量（包括局部变量、全局变量、用户定义变量）：`set`；
### 设置PATH环境变量
+ 当你在shell命令行输入一个外部命令，shell必须搜索系统来找到对应的程序，PATH环境变量定义了用于进行命令和程序的查找的目录，如果命令或程序的位置没有包含在PATH中，如果不使用绝对目录的话，shell是没有办法找到的；应用程序放置可执行文件的目录常常不在PATH环境变量所包含的目录中，解决的办法是保证PATH环境变量包含了所有存放应用程序的目录；`echo $PATH`  就能查看；在PATH中添加路径：`PATH=$PATH:/HOME/DIR` 将/HOME/DIR添加在PATH中，添加完成就可以在虚拟目录结构中的任何位置执行程序；`PATH=$PATH:.  `将当前目录添加到PATH中；对PATH变量的修改只能持续到退出或重启系统，这种效果并不会一直持续；如果希望子shell也能找到你的程序的位置，一定要记住把修改后的PATH环境变量导出；
### 设置用户定义变量
#### 设置局部用户定义变量
+ 通过等号给环境变量赋值，值可以是数字和字符串，如果环境变量的值包含空格，必须使用双引号括起来（注：变量名、等号、变量值之间没有空格）：`my_variable=“hello world”（使用echo $my_variable就可以显示出来，现在使用该环境变量的值可以通过 $my_variable引用即可）`；用户定义的局部变量请使用小写，避免重新定义系统环境变量而带来的麻烦；设置局部变量之后，就能在该shell进程中使用它了，但是生成了一个另外的shell，他在子shell中不可用。如果在子进程中设置局部变量，一旦该子进程退出，该局部变量就不可用了；
#### 设置全局环境变量
+ 在设置全局环境变量的进程创建的子进程中，该变量可用；

|创建全局环境变量的步骤|
|------|
|先创建局部环境变量，然后将该局部环境变量导出到全局环境中|
|```my_variable=hello```|
|```export my_variable```|
+ 修改子shell中的全局环境变量并不会影响到父shell中该变量的值；尽管子shell重新定义并导出了变量my_variable，但父shell中的my_varibale变量依然保持原来的值；
### 删除环境变量
+ 使用`unset`命令(引用环境变量时不要使用$)：`unset my_variable （只删除本进程的环境变量，对其父进程不会影响；删除父进程的环境变量会影响子shell）`；如果要用到变量，使用`$`，如果要操作变量，就不使用$，这条规则的一个例外就是使用printenv显示某个变量的值；
### 默认的shell环境变量

|环境变量|描述|
|------|------|
|CDPATH|  冒号分割的目录列表，作为cd命令的搜索路径|
|HOME  | 当前用户的主目录|
|IFS  | shell用来将文本字符串分割成字段的一系列字符|
|MAIL   |当前用户收件箱的文件名（bash shell会检查这个文件，看看有没有新邮件）|
|OPTARG | getopts 命令处理的最后一个选项参数值|
|MAILPATH  |冒号分隔的当前用户收件箱的文件名列表（bash shell会检查列表中的每个文件，看看有没有新邮件）|
|OPTIND  | getopts命令处理的最后一个选项参数的索引号|
|PATH   |shell 查找命令的目录列表，由冒号分隔|
|PS2   |shell命令行界面的次提示符|
|PS1   |shell命令行界面的主提示符|
|BASH | 当前shell实例的全路径名|
|BASH_ALIASES | 含有当前已设置别名的关联数组|
|BASH_ARCV|  含有传入子函数或shell脚本的参数的数组变量|
|BASH_ARGC  |含有传入子函数或shell脚本的参数总数的数组变量|
|BASH_CMDS | 关联数组，包含shell执行过的命令的所在位置|
|BASH_VERSINFO | 含有当前运行的bash shell的主版本号和次版本号的数组变量|
|BASH_SOURCE | 含有当前正在执行的shell函数所在源文件名的数组变量|
|BASH_SUBSHELL  |当前子shell环境的嵌套等级 初始值为0|
|BASH_COMMAND|  shell正在执行的命令或马上就执行的命令|
|BASH_REMATCH|  只读数组，在使用正则表达式的比较运算符=~进行肯定匹配时，包含了匹配到的模式和子模式|
|BASH_LINENO|  含有当前执行的shell函数的源代码行号的数组变量|
|BASH_ENV | 设置了的话，每个bash脚本会在运行前先尝试运行该变量定义的启动文件|
|BASH_EXECUTION_STRING | 使用bash -c选项传递过来的命令|
|BASH_VERSION  |当前运行的bash shell的版本号|
|COMP_POINT  |当前光标位置相对于当前命令起始的索引|
|BASHOPTS |当前启动的bash shell选项列表|
|COMP_LINE  |当前命令行|
|COMP_CWORD | COMP_WORDS变量的索引值，后者含有当前光标的位置|
|BASHPID|  当前bash进程的PID|
|COLUMNS  |当前bash shell实例所用终端的宽度|
|COMPREPLY | 含有由shell函数生成的可能填充代码的数组变量|
|DIRSTACK|  含有目录栈当前内容的数组变量|
|COPROC|  占用未命名的协进程的I/O文件描述符的数组变量|
|COPM_KEY  |用来调用shell函数补全功能的最后一个键|
|COMP_TYPE  |一个整数值，表示所尝试的补全类型，用以完成shell函数补全|
|COMP_WORDBREAKS  |ReadLine库中用于单词补全的词分隔字符|
|COMP_WORDS  |含有当前命令行所有单词的数组变量|
|EMACS  |设置为 t 时，表明emacs shell缓冲区正在工作，而行编辑功能被禁用|
|ENV | 如果设置了该环境变量，在bash shell脚本运行之前会先执行已定义的启动文件|
|EUID|  当前用户的有效用户ID|
|FCEDIT | 供fc命令使用的默认编辑器|
|FIGNORE | 在进行文件名补全时可以忽略后缀名列表，有冒号分隔|
|FUNCNAME | 当前执行的shell函数的名称|
|FUNCNEST  |当设置成非零值时，表示所允许的最大函数嵌套级别数 一旦超出，当前命令即被终止|
|GLOBIGNORE  |冒号分隔的模式列表，定义了在运行文件名扩展时可以忽略的一组文件名|
|HISTFILE |保存shell历史记录列表的文件名，默认为.bash_history|
|GROUPS|  含有当前用户属组列表的数组变量|
|HISTCMD  |当前命令在历史记录中的编号|
|histchars  |控制历史记录扩展，最多可有3个字符|
|HISTCONTROL|  控制哪些命令留在历史记录列表中|
|HISTTIMEFORMAT | 如果设置了切非空，就用做格式化字符串，以显示bash历史中每条命令的时间戳|
|HISTIGNORE|  以冒号分隔的模式列表，用来决定历史文件中哪些命令会被忽略|
|HISTFILESIZE | 最多在历史文件中存多少行|
|HOSTTYPE|  当前运行bash shell的机器|
|HISTSIZE|  最多在历史文件中存多少条命令|
|HOSTNAME | 当前主机的名称|
|HOSHFILE|  shell在补全主机名时读取的文件名称|
|INPUTRC | readline初始化文件名 默认为.inputrc|
|IGNOREEOF | shell在退出前必须收到连续的EOF字符的数量|
|LC_ALL|  定义了一个语言环境类别能够覆盖LANG变量|
|LANG | shell的语言环境类别|
|LC_COLLATE|  设置对字符串排序时用的排序规则|
|LC_CTYPE | 决定如何解释出现在文件名扩展和模式匹配中的字符|
|LC_MESSAGES | 在解释前面带有$的双引号字符串时，该环境变量决定了所采样的语言环境设置|
|LINES|  定义了终端上可见的行号|
|LINENO  |设置执行的脚本的行号|
|LC_NUMERIC | 决定着格式化数字时采用的语言环境设置|
|MAPFILE|  一个数组变量，当mapfile命令未指定数组变量作为参数时，他存储了mapfile所读入的文本|
|MAILCHECK | shell 查看新邮件的频率默认为60|
|MACHTYPE | 用CPU-公司-系统格式定义的系统类型|
|OLDPWD | shell之前的工作目录|
|OPTERR | 设置为1时，bash shell会显示getopts命令产生的错误|
|PIPESTATUS | 含有前台进程的退出状态列表的数组变量|
|OSTYPE  |定义了shell所在的操作系统|
|POSIXLY_CORRECT|  设置了的话，bash以POSIX模式启动|
|PROMPT_COMMAND  |设置了的话，在命令行主提示符显示之前会执行这条命令|
|PPID | bash shell父进程的PID|
|PROMPT_DIRTRIM | 用来定义当启动了\w或\W提示符字符串转义时显示的尾部目录名的数量|
|PS3| select命令的提示符|
|SHELL | bash shell 的全路径名|
|REPLY | read命令的默认变量|
|SECONDS | 自从shell启动到现在的秒数|
|READLIE_LINE|  使用bind -x命令时，存储readline缓冲区的内容|
|READLINE_POINT|  当使用bind -x命令时，表示readline缓冲区内容插入点的当前位置|
|PS4 | 如果使用了bash的-x选项，在命令行之前显示的提示信息|
|RANDOM  |返回一个0~32767的随机数|
|PWD | 当前工作目录|
|TIMEFORMAT|  指定shell的时间显示格式|
|TMOUT | select和read命令在没输入的情况下等待多久，以秒为单位，默认值为0，表示无限长|
|SHELLOPTS | 已启动bash shell选项列表，列表项之间以冒号分隔|
|SHLVL  |shell的层级，每次启动一个新的shell该值增加1|
|TMPDIR | 目录名，保存bash shell创建的临时文件|
|UID  |当前用户的真实用户ID|
+ 不是所有的默认环境变量都会在运行set命令时列出，就算列出了，也未必必须有值；
### 定位系统环境变量
+ 当登入Linux系统启动bash shell时，默认情况下bash会在几个文件中查找命令，这些文件叫做启动文件或环境文件，bash检查的启动文件取决你启动bash shell的方式；

|启动bash shell的方式|
|------|
|登录时作为默认登录shell|
|作为非登录shell的交互式shell|
|作为运行脚本的非交互shell|

#### 登录shell

+ 当你登录Linux时，bash shell会作为登录shell启动，登录shell会在5个不同的启动文件里读取命令；

|五个启动文件|说明|
|------|------|
|`/etc/profile`|是系统上默认的bash shell的主启动文件，系统上的用户登录时都会执行这个启动文件，只要登录了Linux系统，bash shell就会执行该文件中的命令；该文件执行了/etc/bash.bashrc文件，该文件中包含了系统环境变量，在脚本中有for循环，用来迭代`/etc/profile.d`目录下的所有文件|
|`$HOME/.bash_profile`|$HOME目录下的启动文件(针对用户，可以做定制)；提供用户专属的启动文件来定义该用户所用到的环境变量，大部分Linux发行版本只有其中的一到两种文件，每个用户都可以编辑这些文件并添加自己的环境变量，这些环境变量会在每次启动bash shell会话时生效|
|`$HOME/.bashrc`|$HOME目录下的启动文件(针对用户，可以做定制)；提供用户专属的启动文件来定义该用户所用到的环境变量，大部分Linux发行版本只有其中的一到两种文件，每个用户都可以编辑这些文件并添加自己的环境变量，这些环境变量会在每次启动bash shell会话时生效|
|`$HOME/.bash_login`|$HOME目录下的启动文件(针对用户，可以做定制)；提供用户专属的启动文件来定义该用户所用到的环境变量，大部分Linux发行版本只有其中的一到两种文件，每个用户都可以编辑这些文件并添加自己的环境变量，这些环境变量会在每次启动bash shell会话时生效|
|`$HOME/.profile`|$HOME目录下的启动文件(针对用户，可以做定制)；提供用户专属的启动文件来定义该用户所用到的环境变量，大部分Linux发行版本只有其中的一到两种文件，每个用户都可以编辑这些文件并添加自己的环境变量，这些环境变量会在每次启动bash shell会话时生效|
+ bash shell会按照下列顺序，运行第一个被找到的文件，余下的则被忽略；

|启动文件|
|------|
|`$HOME/.bash_profile`|
|`$HOME/.bash_login`|
|`$HOME/.profile`|

+ 注意：这个列表中并没有`$HOME/.bashrc`文件，这是因为该文件通常通过其他文件运行的；

#### 交互式shell进程
+ 如果你的bash shell 不是登录系统时启动的（比如在命令行中敲下bash时启动的），那么你启动的shell叫做交互式shell，交互式shell不会像登录shell一样运行，但可以输入命令；如果bash是作为交互式shell启动的，它不会访问/etc/profile文件，只是检查用户HOME目录中的.bashrc文件；.bashrc文件有两个作用：查看/etc目录下通用的bashrc文件；为用户提供一个定制自己的命令别名和私有脚本函数的地方；
#### 非交互式shell
+ 系统执行shell脚本时用的就是这种shell，它没有命令行提示符（脚本能以不同的方式执行，只有其中的某一些方式能够启动子shell）；当启动非交互式shell进程时，他会检查这个BASH_ENV环境变量来查看要执行的启动文件，如果有指定，shell就执行该文件里的命令，这个BASH_ENV在默认情况下并未设置；
#### 环境变量持久化
+ 对于全局环境变量来说，可以更倾向于将新的或修改过的变量设置放在/etc/profile中，但是这不是个好主意，如果你升级了所用的发行版，这个文件也会跟着更新，那你所定制过的环境变量设置就没有了，最好在/etc/profile.d目录中创建一个以.sh结尾的文件，把所有新的或修改过的全局环境变量放置在这个文件中；大多数发行版本中，存储个人用户永久性bash  shell变量的地方是`$HOME/.BASHRC`文件，但如果设置了BASH_ENV变量，那么记住，除非它指向的是$HOME/.BASHRC文件，否则你应该将非交互式shell的用户变量放在别的地方；
