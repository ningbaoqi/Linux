### 功能脚本
#### 批量修改文件内容
```
sed -i 's/123/333/g' *.txt
```

### 当Ubuntu系统上adb显示不到手机，并且lsusb不能显示设备的问题
+ 使用`dmesg |grep -iE "mediatek|"`命令查看操作系统内核log，可以看到如下：
![image](https://github.com/ningbaoqi/Linux/blob/master/gif/pic-1.jpg) 
