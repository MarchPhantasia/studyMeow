# scrcpy 投屏

- 工具
	- https://github.com/Genymobile/scrcpy
- 键盘控制
	- https://www.wuzao.com/Genymobile/scrcpy/doc/keyboard.md#uhid
	- https://www.wuzao.com/Genymobile/scrcpy/doc/keyboard.md
- 问题解决 tcpip
	- https://www.cnblogs.com/an-shiguang/p/17840668.html

## 部分 bat 文件

``` shell
.\scrcpy.exe -e --keyboard=uhid --stay-awake

.\scrcpy.exe -d --keyboard=uhid --stay-awake
```

## adb 端口重启

``` shell
adb tcpip 5555
> restarting in TCP mode port: 5555

adb connect 手机ipv4地址:5555
> connected to 192.168.5.126:5555

# 在进行正常的tcpip连接即可

```
