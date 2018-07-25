#### 一、sudo：获取root权限

|命令|说明|
|------|------|
|`sudo su`|切换到root用户|

#### 二、tree：树状显示目录结构

|命令|说明|
|------|------|
|`tree`|遍历当前文件夹下的树状结构|

#### 三、find：查找

|命令|功能|
|------|------|
|`find ./ -name *fingerprint_sensor_location*`|查看文件按照文件名过滤|
|`find . -name "*.log" 或者 find . -type f -name "*.log"`|查看当前文件夹下以.log为后缀的文件名|
|`find .\|xargs grep -ri "IBM" -l或find .\|xargs grep - -color=auto "IBM"`|查看当前文件夹下所有含有“IBM”字符串的文件名|
|`find /opt/soft/test/ -perm 777`|查看/opt/soft/test/文件夹下权限为777的文件|

#### 四、exit：退出

|命令|说明|
|------|------|
|`exit`|退出shell|

#### 五、cd：切换目录

|命令|说明|
|------|------|
|`cd -`|切换到刚才的目录|

#### 六、执行可执行文件

|命令|说明|
|------|------|
|`./可执行文件名`|执行当前文件夹的可执行文件|

#### 七、网络相关

|命令|说明|
|------|------|
|`netstat`|显示所有socket：`netstat -a` ；查看1234端口连接：`netstat \|grep "1234"`|
|`ping`| 查看与指定IP或者网址是不是可以连通（指定次数，如测试5次）：`ping IP地址/网址 -c 5 `；查看与指定IP或者网址是不是可以连通（一直检测）：`ping IP地址/网址`|
