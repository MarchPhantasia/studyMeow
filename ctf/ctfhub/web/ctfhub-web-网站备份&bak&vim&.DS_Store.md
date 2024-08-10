
### 常见的网站备份文件名和后缀。
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240717163036.png)

www.zip 下面有一个文件，但是文件是空的，但是这个文件名可以在网站中索引到

![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240717171542.png)



### 网站的.bak 后缀文件
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240717172118.png)

### vim 相关
[ctf-web-信息收集](https://blog.csdn.net/m0_74317362/article/details/131962105)

**备份文件是隐藏文件，文件名前面还有一个点，是 .index.php.swp**
所以实际上是.index.php.swp


### DS_Store相关
吧唧url后面加.DS_Store 可以下载一个文件，目前看来vscode直接打开出现问题，通过cat命令可以获得
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240717215635.png)

- c9d9a3e11e37e8841cf599e4a714238c.txt
- 在吧唧的url后面加这个就会发现了，好了。flag就有了