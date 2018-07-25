### 功能脚本
#### 批量修改文件内容
```
sed -i 's/123/333/g' *.txt
```

### 当Ubuntu系统上adb显示不到手机，并且lsusb不能显示设备的问题
+ 使用`dmesg |grep -iE "mediatek|"`命令查看操作系统内核log，可以看到如下：
![image](https://github.com/ningbaoqi/Linux/blob/master/gif/pic-1.jpg) 
+ 然后使用 `sudo service udev restart`重启服务；接着使用`lsusb`即可查看到手机设备：
![image](https://github.com/ningbaoqi/Linux/blob/master/gif/pic-2.jpg) 
+ 根据上面的的显示数据后，需要修改`/etc/udev/rules.d/51-android.rules`文件，配置该设备：
![image](https://github.com/ningbaoqi/Linux/blob/master/gif/pic-3.jpg) 
+ 但是目前使用`adb devices`无法显示到设备，需要按如下修改：
![image](https://github.com/ningbaoqi/Linux/blob/master/gif/pic-4.jpg) 
+ 然后使用`sudo service udev restart`重启驱动服务；使用`adb kill-sever`干掉adb服务；使用`adb start-server`重新启动adb服务；使用`adb devices`即可显示手机设备：
![image](https://github.com/ningbaoqi/Linux/blob/master/gif/pic-5.jpg) 
