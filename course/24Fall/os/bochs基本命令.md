 

本文将介绍一下[哈工大](https://so.csdn.net/so/search?q=%E5%93%88%E5%B7%A5%E5%A4%A7&spm=1001.2101.3001.7020)李治军老师《操作系统》课程在完成 [Lab](https://so.csdn.net/so/search?q=Lab&spm=1001.2101.3001.7020) 时所使用到的 Bochs 调试工具的使用方法。这是一款汇编级调试工具，打开调试模式非常简单，只需在终端下输入如下指令：

#### 1、_bochs 调试基本指令大全_

| **功能**            | **指令**       | **举例**                 |
| ----------------- | ------------ | ---------------------- |
| 在某物理地址设置断点        | b addr       | b 0 x 90000            |
| 运行到断点位置           | c            | c                      |
| 单步运行（遇到函数则进入）     | s            | s                      |
| 单步运行（遇到函数则跳过）     | n            | n                      |
| 继续运行上调指令          | 回车           | 回车                     |
| 显示当前所有断点信息        | info break   | info break             |
| 显示所有使用的寄存器值       | r            | r                      |
| 显示段寄存器值           | sreg         | sreg                   |
| 显示控制寄存器值          | creg         | creg                   |
| 显示 CPU 状态信息       | info cpu     | info cpu               |
| 显示浮点寄存器值          | fp           | fp                     |
| 退出调试模式            | q            | q                      |
| 查看堆栈              | print-stack  | print-stack            |
| 每执行一条指令就打印 CPU 信息 | trace-reg    | trace-reg on           |
| 查看内存物理地址内容        | xp /nuf addr | xp /40 bx 0 x 9013 e   |
| 查看线性地址内容          | x /nuf addr  | x /40 bx 0 x 13 e      |
| 反汇编一段内存           | u start end  | u 0 x 30400 0 x 3040 D |
| 反汇编执行的每一条指令       | trace-on     | trace-on               |
| 查看 bochs 基本命令     | help         | help                   |
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20241119222450.png)
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20241119222459.png)

#### 2、使用方法

（1）进入调试模式

```shell
cd oslab      // 进入 oslab 文件夹下
./dbg-asm     // 启动 bochs 调试模式
```

出现如下界面，即表示成功进入 boch 调试模式。

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/964ea7285b41d6bb7ad5396406847876.png)

（2）调试方法

在 0 x 7 e 00 处打上断点（即 setup 的启动位置），并运行到断点处，出现如下界面。此时 bootsect. s 已经运行至导入 setup. s 处，但 setup. s 还未运行。

```shell
b 0x7e00       // 在 0x7e00 处加载断点
c              // 运行到断点为止
```

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/55c2b973501a630216ab5fb2eac04f40.png)

> 需要注意的是：终端上显示的代码是下一行将要执行的，是还未执行的代码。

此外，我们还可以通过单步运行来一行一行运行代码，或者查看寄存器信息。

```shell
n              // 单步运行
回车            // 继续上次的命令
r              // 查看常用寄存器信息
sreg           // 查看段寄存器信息
q              // 退出 debug
```

显示段寄存器信息：

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/90f84655e9085d332c7bda2fd2ea43d0.png)

至此，关于李治军老师的[操作系统](https://so.csdn.net/so/search?q=%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F&spm=1001.2101.3001.7020)课程 bochs 使用方法已介绍完毕，更加具体的使用方法可以参考 Bochs 使用手册 [Bochs User Manual (sourceforge.io)](https://bochs.sourceforge.io/doc/docbook/user/index.html)。

本文转自 <https://blog.csdn.net/weixin_53159274/article/details/137796343>，如有侵权，请联系删除。