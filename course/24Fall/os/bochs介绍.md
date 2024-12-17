 

**目录**

[一、前言：](#t0)

[bochs当前信息](#t1)

[二、Bochs简介](#t2)

[1、什么是Bochs](#t3)

[2、Bochs能在哪些机器上运行](#t4)

[3、Bochs模拟器适合哪些人使用](#t5)

[三、准备使用Bochs](#t6)

[1、下载Bochs的源代码](#t7)        

[2、解压并观察源代码](#t8)

[3、配置Bochs](#t9)

[平台相关的配置](#t10)

[Bochs使用的图形库](#t11)

[Bochs通用配置](#t12)

[CPU与内存配置](#t13)

[对设备的模拟支持](#t14)

[总结configure](#t15)

[make前的准备](#t16)

[4、make构建之后](#t17)

[1、bin目录](#1%E3%80%81bin%E7%9B%AE%E5%BD%95)

[①bochs是模拟器本身](#%E2%91%A0bochs%E6%98%AF%E6%A8%A1%E6%8B%9F%E5%99%A8%E6%9C%AC%E8%BA%AB)

[②bximage是一个磁盘工具](#%E2%91%A1bximage%E6%98%AF%E4%B8%80%E4%B8%AA%E7%A3%81%E7%9B%98%E5%B7%A5%E5%85%B7)

[③bxhub是一个网络工具](#%E2%91%A2bxhub%E6%98%AF%E4%B8%80%E4%B8%AA%E7%BD%91%E7%BB%9C%E5%B7%A5%E5%85%B7)

[2、lib目录](#2%E3%80%81lib%E7%9B%AE%E5%BD%95)

[3、share](#3%E3%80%81share)

[让你的Bochs跑起来：](#t18)

[四、编写Bochs的配置文件](#t19)

[1、ROM image](#t20)

[2、配置内存](#t21)

[3、调试选项](#t22)

[4、控制可选插件](#t23)

[5、设置启动方式和磁盘](#t24)

[1、设置软盘](#t25)

[2、设置硬盘](#t26)

[6、设置pci](#t27)

[7、设置VGA信息](#t28)

[8、设置键盘与鼠标](#t29)

[9、设置clock时钟](#t30)

[10、日志信息](#t31)

[11、调试信息](#t32)

[调试信息输出位置](#t33)

[12、CPU信息设置](#t34)

[①cpu的各个参数：](#t35)

[②cpuid的各个参数](#t36)

[五、Bochs调试内核](#t37)

[1、执行控制命令](#t38)

[①执行到底](#t39)

[②单步执行](#t40)

[③打个断点](#t41)

[④查看信息](#t42)

[1、查看寄存器的值](#1%E3%80%81%E6%9F%A5%E7%9C%8B%E5%AF%84%E5%AD%98%E5%99%A8%E7%9A%84%E5%80%BC)

[2、查看内存里的数据](#2%E3%80%81%E6%9F%A5%E7%9C%8B%E5%86%85%E5%AD%98%E9%87%8C%E7%9A%84%E6%95%B0%E6%8D%AE)

[3、反汇编](#3%E3%80%81%E5%8F%8D%E6%B1%87%E7%BC%96)

[4、多核CPU](#4%E3%80%81%E5%A4%9A%E6%A0%B8CPU)

[⑤通用设置指令](#t43)

[⑥其他指令](#t44)

[六、Bochs已实现的功能和未来的计划](#t45)

* * *

一、前言：
-----

_**相信很多人都有使用模拟器的需求，因为并不是所有的场景都能用虚拟机代劳，如果你需要对程序精心的调试，实时查看内存与寄存器信息、研究指令集的工作原理，那么模拟器就是一种非常重要的工具。常见的模拟器有很多，最出名的就是 Qemu, 它既可以作为模拟器又可以作为虚拟机使用，并且对大多数 CPU 指令集架构提供支持，且有多种工作模式，支持 kvm 加速、gdb 调试等等功能，可以说对于操作系统内核开发、嵌入式开发、指令集设计等都有着非常重要的作用。但是我今天不讲 Qemu 而是另一个开源的 x 86 模拟器 --- bochs（读音同:box  \[bɒks\]）. 对于内核开发者来说，这也是一个非常重要的工具，它可以提供比 Qemu+gdb 更加精细、精准的调试，可以查看更多的信息，对于内核开发初学者来说是一个强悍的工具，更重要的是它是开源的，并且现在还在更新。我相信许多学习内核开发的新手都是先使用 bochs 进行模拟和调试，然后再转向 Qemu 等其他模拟器，Bochs 作为这么一个基础仿真软件，初学者用起来如果比较困惑的话可能对后续的内核开发不利。同时, 如果大家也把 Bochs 作为内核开发使用的模拟器，大家最好在正式学习之前把基础的 Linux 命令给学会，这样未来的学习将会事半功倍**_。大家如果觉得本文章还是有那么一点点帮助的话，可以把它推荐给其他内核学习者，毕竟简化环境的搭建对于初学者而言还是非常重要的。这篇文章也许比较长，但是和官方文档比起来已经很精简、很浓缩了，对于内核开发者而言，看几千页的手册也只是家常便饭，请大家耐心看完吧。

### [bochs](https://so.csdn.net/so/search?q=bochs&spm=1001.2101.3001.7020) 当前信息

[bochs 官网](https://bochs.sourceforge.io/ "bochs 官网")

[bochs 官方文档](https://bochs.sourceforge.io/doc/docbook/user/index.html "bochs 官方文档")

[bochs 下载地址](https://sourceforge.net/projects/bochs/files/bochs/ "bochs 下载地址")

[bochs 百度百科](https://baike.baidu.com/item/bochs/586473?fr=ge_ala "bochs 百度百科")

  
[bochs GitHub 开源地址](https://github.com/bochs-emu/Bochs "bochs GitHub 开源地址")  
 

令人高兴的是 Bochs [模拟器](https://so.csdn.net/so/search?q=%E6%A8%A1%E6%8B%9F%E5%99%A8&spm=1001.2101.3001.7020)现在已经全面转向 GItHub 进行开发了，并且仓库几乎是日日更新，如果大家觉得出现了 bug 或者需要提一些建议的话可以直接发一个 issue, 如果是做虚拟化方向的话可以参考 bochs 或者给它提交 pr。

bochs 作为一个[开源](https://edu.csdn.net/cloud/pm_summit?utm_source=blogglc)工具，它本身是可以使用 GNU/linux 自带的包管理器安装的，但直接使用包管理器安装的 bochs 并不具备调试功能，如果想使用 bochs 来调试自己的内核，请务必下载它的源代码并自己配置和编译。

![](https://i-blog.csdnimg.cn/blog_migrate/fde1284897135cce60e85d393d948720.png)

至于为什么我会想起来写 bochs 的文档，那正是因为 bochs 在今年 (2024) 三月份发布了其最新版本 bochs-2.8，我就想开源开发者这么努力、坚持不懈做出更好、更先进、支持更多 CPU 和指令集的模拟器，那么我是不是也该为社区做一点什么呢？bochs 的英文文档可以说是已经非常详细了，但是它的中文文档好像就比较少，只有一些自己配置 bochs 的资料，对于全面使用 bochs 模拟器来调试内核来说还是不太够用，那么希望大家看了这篇文章就可以配置出适合自己的 bochs 模拟器，并用它来调试和学习 x 86 架构和操作系统内核。

![](https://i-blog.csdnimg.cn/blog_migrate/535a9a28ada852b084a56f5734cc898c.png)

最新版新增了几块现代 CPU, 有了这些新 CPU, 就可以在模拟器里为自己的内核开发出更多的基础功能，大家不要着急，我会在后面的章节告诉大家怎么把这些 CPU 给使用起来，让自己的操作系统内核跑在如图所示的先进的 CPU 上面。不过我听说 Bochs 的开发者是 Intel 的员工，不知道是不是因为这个原因，新版本的 Bochs 只是新增了多块 Intel CPU 的支持，对于 AMD 则没有新增，并且根据我的亲自尝试，模拟的 AMD 的 CPU 这块 CPU 甚至还不支持 x 2 APIC, 这对于开发一个现代内核来说非常不方便，如果大家想基于 AMD 芯片调试内核，那么我还是推荐大家使用 Qemu+gdb。

既然我的标题里都写了这是中文文档，那么我肯定会教大家怎么使用到 Bochs 来调试自己的内核。祝大家**内核**学习顺利吧。

* * *

二、Bochs 简介
---------

### 1、什么是 Bochs

        Bochs是一个完整模拟Intel x86指令集的计算机程序。它包括对Intel x86CPU、常见IO设备和自定义BIOS的仿真，除了IntelCPU之外还有AMD处理器的支持。Bochs拥有标准PC外设的设备模型：鼠标、键盘、VGA卡/显示器、磁盘、定时器芯片、网卡等。

Bochs 最早由 Kevin Lawton 大佬于 1994 年开始编写，2000 年 3 月，Bochs 以 LGPL 协议开源出来。

它一开始使用 svn 集中式版本管理工具，现在已经改成了 Git 分布式版本管理来管理项目。

>   LGPL 协议：
>   This library is free software; you can redistribute it and/or
>   modify it under the terms of the GNU Lesser General Public
>   License as published by the Free Software Foundation; either
>   version 2 of the License, or (at your option) any later version.
> 
>   This library is distributed in the hope that it will be useful,
>   but WITHOUT ANY WARRANTY; without even the implied warranty of
>   MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
>   Lesser General Public License for more details.
> 
>   You should have received a copy of the GNU Lesser General Public
>   License along with this library; if not, write to the Free Software
>   Foundation, Inc., 51 Franklin St, Fifth Floor, Boston, MA  02110-1301 USA

### 2、Bochs 能在哪些机器上运行

        Bochs使用C++编程语言编写，由于C++具有跨平台性，因此Bochs可以在x86,PPC,Alpha,Sun,MIPS等指令集的CPU上面运行。Bochs是一个单纯的模拟器、它不是虚拟机，它的指令集的实现并不依赖于宿主机本身拥有的指令集，也就是不使用VMX等虚拟化指令集的支持。Bochs支持x86的高度仿真，也就是可以把它当成一台物理机器，拥有自己的BIOS。

![](https://i-blog.csdnimg.cn/blog_migrate/83fc6ca50d0d2cd37d55ed49871630be.png)bochs 实际上提供了源码包、exe 文件和 rpm 包，其中最重要的就是源代码。有了源代码，Bochs 可以拿来跑在很多机器上，只是可能需要自己去编译和构建。

### 3、Bochs 模拟器适合哪些人使用

  实际上 Bochs 完全可以拿来当成一个“虚拟机”，比如在没有 Windows 生态的机器上跑 Windows 操作系统。不过我是站在内核开发者的角度来看，更多把 Bochs 作为一个能够模拟真实 PC 环境的仿真工具。实际上 Bochs 在为 indows、Linux、MacOS 都可以跑，由于我没有其中一些设备，因此我就在 GNU/Linux 上面使用 Bochs 作为例子。

三、准备使用 Bochs
-----------

![](https://i-blog.csdnimg.cn/blog_migrate/540b1b887d078b8bc261048766f61663.png)

可以使用包管理器安装，但是包管理器安装的 Bochs 不具备调试功能。

* * *

#### 

### 1、下载 Bochs 的源代码        

  Bochs 模拟器有很多版本，从最开始的 1.0 版本到现在最新的 2.8 版本，大家需要选择一个合适的版本，不同版本有不同的特点，使用的配置文件的语法也不尽相同，如果大家知道自己需要哪一个版本就最好，如果大家不知道该选择哪一个版本那么我推荐大家使用 Bochs-2.8 也就是最新的版本，我也是按照这个版本的文档写成的中文文档。新旧版本的 Bochs 的配置文件语法会有不同（而官方文档里的是最新的语法），所以推荐大家大胆使用最新版本即可。本文是我对 Bochs 英文文档的个人理解，里面也许会有错误，请大家还是以官方文档为主，如果大家认为我有什么地方写的不对，可以在评论区指正一下。

点进 Bochs 2.8 这个目录，可以看到提供了很多不同的包，那么我们这里选择下载源码包，名称中带有 src 的就是源码包。. zip 源码包带有 msvc 字样，应该是给 Windows 用的。我主要在 Linux 上写内核，因此会选择 bochs-2.8. tar. gz.

* * *

### 2、解压并观察源代码

```bash
tar -xvf bochs-2.8.tar.gz
```

解压后会在 tar 包所在目录产生一个新目录 bochs-2.8

![](https://i-blog.csdnimg.cn/blog_migrate/314acd49f66358dad3ba5619a40e9092.png)

我们不要急着就开始配置和编译，而是要先观察。

<table border="1" cellpadding="1" cellspacing="1" style="width: 500px; user-select: auto;"><tbody style="user-select: auto;"><tr style="user-select: auto;"><td style="user-select: auto;">文件/目录</td><td style="user-select: auto;">作用</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">configure</td><td style="user-select: auto;">非常重要的 shell 脚本，配置的时候执行它</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">Makefile. in</td><td style="user-select: auto;">根据 configure 脚本的配置生成最终的 Makefile 文件</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">install-sh</td><td style="user-select: auto;">用于在安装过程中复制文件</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">main. cc</td><td style="user-select: auto;">Bochs 的主程序入口点</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">bios 目录</td><td style="user-select: auto;">包含 Bochs 使用的 BIOS 文件</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">gui 目录</td><td style="user-select: auto;">Bochs 支持图形界面调试 (不过我更喜欢字符界面调试)</td></tr></tbody></table>

我们在最终执行 make install 之前实际上要稍微修改一些文件才能编译通过，否则可能会出现错误，因此需要简单了解一下目录里面的构成。

### 3、配置 Bochs

  这一步可以说是最重要的，我们怎么配置 Bochs, 那么最终构建出来的 Bochs 就会具有什么样的能力；或者说关闭一些配置，那么 Bochs 就会失去什么样的能力。  
我们在执行 make install 之前执行./configure，但不是直接这么执行就好，而是要自己配置。

比如./configure --with-x 11 .... 等一系列配置

#### 平台相关的配置

<table border="1" cellpadding="1" cellspacing="1" style="width: 500px; user-select: auto;"><tbody style="user-select: auto;"><tr style="user-select: auto;"><td style="user-select: auto;">Platform</td><td style="user-select: auto;">GUI</td><td style="user-select: auto;">说明</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">Win 32/MinGW</td><td style="user-select: auto;">--with-win 32</td><td style="user-select: auto;">Windows 平台带上这个参数</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">MacOS/Darwin</td><td style="user-select: auto;">--with-carbon</td><td style="user-select: auto;">Mac 平台带上这个参数</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">MacOS 9</td><td style="user-select: auto;">--with-macos</td><td style="user-select: auto;">这应该比较老了</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">AmigaOS</td><td style="user-select: auto;">--with-amigaos</td><td style="user-select: auto;">我不了解这个系统</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">带有 x 显示服务器的 Linux</td><td style="user-select: auto;">--with-x 11</td><td style="user-select: auto;">Linux 上用这个参数</td></tr></tbody></table>

虽然说是需要带有 x 显示服务器的 Linux 用--with-x 11，但实际上只要是 Linux 就用这个参数就好了，Bochs 是可以跑在 Xwayland 上面的。

#### Bochs 使用的[图形库](https://so.csdn.net/so/search?q=%E5%9B%BE%E5%BD%A2%E5%BA%93&spm=1001.2101.3001.7020)

由于 Bochs 是跑在操作系统上的，因此需要调用图形库才能使用。

<table border="1" cellpadding="1" cellspacing="1" style="width: 500px; user-select: auto;"><tbody style="user-select: auto;"><tr style="user-select: auto;"><td style="user-select: auto;">显示库选项</td><td style="user-select: auto;">作用</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--with-x 11</td><td style="user-select: auto;">Linux 上用这个</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--with-win 32</td><td style="user-select: auto;">Win 32 原生 GUI</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--with-carbon</td><td style="user-select: auto;">使用 Carbon GUI</td></tr><tr style="user-select: auto;"><td style="user-select: auto;"><code style="user-select: auto;" onclick="mdcp.copyCode(event)">--with-sdl</code></td><td style="user-select: auto;">启用对 SDL 1.2. x GUI 接口的支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;"><code style="user-select: auto;" onclick="mdcp.copyCode(event)">--with-sdl 2</code></td><td style="user-select: auto;">启用对 SDL 2. x GUI 接口的支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;"><code style="user-select: auto;" onclick="mdcp.copyCode(event)">--with-term</code></td><td style="user-select: auto;">需要 curses 库</td></tr><tr style="user-select: auto;"><td style="user-select: auto;"><code style="user-select: auto;" onclick="mdcp.copyCode(event)">--with-wx</code></td><td style="user-select: auto;">启用对 wxWidgets 配置和显示接口的支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;"><code style="user-select: auto;" onclick="mdcp.copyCode(event)">--with-nogui</code></td><td style="user-select: auto;">你不关心视频输出/单纯调试</td></tr><tr style="user-select: auto;"><td style="user-select: auto;"><code style="user-select: auto;" onclick="mdcp.copyCode(event)">--with-all-libs</code></td><td style="user-select: auto;">自动检测系统上安装的库 (我没试过)</td></tr></tbody></table>

我启动了三个选项

\--with-x 11 --with-wx --with-sdl 2  
大家可以参考我的做法

#### Bochs 通用配置

这会是一个大的表格，如果大家没有耐心看了，那么可以直接参考我的做法

<table border="1" cellpadding="1" cellspacing="1" style="width: 500px; user-select: auto;"><tbody style="user-select: auto;"><tr style="user-select: auto;"><td style="user-select: auto;">通用选项</td><td style="user-select: auto;">默认情况</td><td style="user-select: auto;">说明</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-plugins</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用插件支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-debugger</td><td style="user-select: auto;">关</td><td style="user-select: auto;">Bochs 内置调试器，默认关闭因此使用包管理器安装的 Bochs 不带调试功能</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-debugger-gui</td><td style="user-select: auto;">开 (如果 debugger 开)</td><td style="user-select: auto;">有图形界面的调试器</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-readline</td><td style="user-select: auto;">-</td><td style="user-select: auto;">提供命令行编辑和历史记录功能</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-gdb-stub</td><td style="user-select: auto;">关</td><td style="user-select: auto;">使用 gdb 调试, 它与--enable-debugger 不兼容，并且 gdb 调试和 smp 也不兼容</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-docbook</td><td style="user-select: auto;">-</td><td style="user-select: auto;">如果系统安装了<code style="user-select: auto;" onclick="mdcp.copyCode(event)">docbook 2 html 则默认开启</code></td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-instrumentation=<code style="user-select: auto;" onclick="mdcp.copyCode(event)">directory</code></td><td style="user-select: auto;">关</td><td style="user-select: auto;">仪器支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-xpm</td><td style="user-select: auto;">开</td><td style="user-select: auto;">XMP</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-show-ips</td><td style="user-select: auto;">开</td><td style="user-select: auto;">启用测量 IPS（每秒指令数）的日志记录功能</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-logging</td><td style="user-select: auto;">开</td><td style="user-select: auto;">运行时记录日志</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-cpp</td><td style="user-select: auto;">关</td><td style="user-select: auto;">将所有. cc 文件重命名为. cpp</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-idle-hack</td><td style="user-select: auto;">关</td><td style="user-select: auto;">保持 Bochs 响应性 (Bochs 不占用过量的系统资源)</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-assert-checks</td><td style="user-select: auto;">-</td><td style="user-select: auto;">BX_ASSERT 事件在断言失败时会导致 panic</td></tr></tbody></table>

我的做法：除了--enable-docbook, 全开

#### CPU 与内存配置

<table border="1" cellpadding="1" cellspacing="1" style="width: 500px; user-select: auto;"><tbody style="user-select: auto;"><tr style="user-select: auto;"><td style="user-select: auto;">配置参数</td><td style="user-select: auto;">默认情况</td><td style="user-select: auto;">说明</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-cpu-level={<code style="user-select: auto;" onclick="mdcp.copyCode(event)">3,4,5,6</code>}</td><td style="user-select: auto;">6</td><td style="user-select: auto;">386/486/586/686 及以上（你选 6 就好）</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-smp</td><td style="user-select: auto;">关</td><td style="user-select: auto;">对称多处理器支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-fpu</td><td style="user-select: auto;">开</td><td style="user-select: auto;">浮点运算单元</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-3 dnow</td><td style="user-select: auto;">关</td><td style="user-select: auto;">AMD 的指令集</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-vmx</td><td style="user-select: auto;">关</td><td style="user-select: auto;">支持 Intel 虚拟化扩展（VMX）</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-svm</td><td style="user-select: auto;">关</td><td style="user-select: auto;">支持 AMD SVM（安全虚拟机）扩展模拟</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-avx</td><td style="user-select: auto;">关</td><td style="user-select: auto;">支持 AVX 指令集</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-x 86-debugger</td><td style="user-select: auto;">关</td><td style="user-select: auto;">支持 x 86 调试器</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-monitor-mwait</td><td style="user-select: auto;">关</td><td style="user-select: auto;">支持 MONITOR/MWAIT 指令</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-alignment-check</td><td style="user-select: auto;">-</td><td style="user-select: auto;">如果 CPU 级别大于 4 则开启 (支持 CPU 中的对齐检查和 #AC异常 )</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-configurable-msrs</td><td style="user-select: auto;">关</td><td style="user-select: auto;">支持用户配置模拟的 MSR</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-long-phy-address</td><td style="user-select: auto;">关</td><td style="user-select: auto;">支持大于 32 位的客户物理地址</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-a 20-pin</td><td style="user-select: auto;">开</td><td style="user-select: auto;">支持 A 20 引脚</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-large-ramfile</td><td style="user-select: auto;">开</td><td style="user-select: auto;">支持大于主机支持的客户内存</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-repeat-speedups</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用对重复 I/O 和内存复制加速的支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-fast-function-calls</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用对快速函数调用的支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-handlers-chaining</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用对处理程序链优化的支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-all-optimizations</td><td style="user-select: auto;">关</td><td style="user-select: auto;">开启所有开发者认为安全使用的速度优化选项：<code style="user-select: auto;" onclick="mdcp.copyCode(event)">--enable-repeat-speedups</code>、<code style="user-select: auto;" onclick="mdcp.copyCode(event)">--enable-fast-function-calls</code>、<code style="user-select: auto;" onclick="mdcp.copyCode(event)">--enable-handlers-chaining</code></td></tr></tbody></table>

我的做法：全部打开

#### 对设备的模拟支持

<table border="1" cellpadding="1" cellspacing="1" style="width: 500px; user-select: auto;"><tbody style="user-select: auto;"><tr style="user-select: auto;"><td style="user-select: auto;">配置选项</td><td style="user-select: auto;">默认情况</td><td style="user-select: auto;">说明</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-cdrom</td><td style="user-select: auto;">开</td><td style="user-select: auto;">启用对真实 CD-ROM/DVD 驱动器的使用</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-sb 16</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用 Sound Blaster 模拟, 可用的低级声音接口会自动检测。</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-es 1370</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用 ES 1370 声音模拟</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-gameport</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用标准 PC 游戏端口</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-ne 2000</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用 NE 2000 网络卡支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-pnic</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用 PCI 伪 NIC（网络卡）支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-e 1000</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用 Intel (R) 82540 EM 千兆以太网适配器支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-clgd 54 xx</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用 Cirrus Logic GD 54 xx（CL-GD 5430 ISA 或 CL-GD 5446 PCI）视频卡支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-voodoo</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用实验性的 3 dfx Voodoo Graphics 模拟。Voodoo 1 已知可以工作，Voodoo 2 支持尚未完成，但几乎可用</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-iodebug</td><td style="user-select: auto;">跟随 debugger</td><td style="user-select: auto;">Dave Poirier 编写了一个使用 I/O 端口的实验性调试器接口，使得在客户操作系统中运行的软件可以访问调试器的功能</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-pci</td><td style="user-select: auto;">开</td><td style="user-select: auto;">启用有限的 i 440 FX / i 430 FX / i 440 BX PCI 支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-pcidev</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用 PCI 主机设备映射支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-usb</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用 i 440 FX / i 440 BX PCI USB 支持（UHCI）</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-usb-ohci</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用 USB OHCI 支持, 提供带有 2 端口根集线器的主控制器</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-usb-ehci</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用 USB EHCI 支持, 提供带有 6 端口根集线器的主控制器</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-usb-xhci</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用 USB xHCI 支持, 提供带有 4 端口根集线器的主控制器</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">--enable-raw-serial</td><td style="user-select: auto;">关</td><td style="user-select: auto;">启用对串行端口模拟的支持，以访问宿主的串行端口</td></tr></tbody></table>

我的做法：--enable-voodoo --enable-iodebug 可以打开

其他配置你可以根据自己的情况自行配置，比如你想写 USB 驱动，那么就可以打开--enable-usb 等

#### 总结 configure

相比大家对官方文档里的这些配置参数有了一定的了解，可以看到，参数真的非常的多，如果大家不知道哪些是自己必备的，那么你可以尽可能多的选择一些参数，编译出来你不使用也是可以的。但是如果你参数加少了，那么你就得重新编译了，这样得不偿失。

这里我提供我自己的 configre

```bash
./configure --with-x11 --with-wx --with-sdl2 --enable-plugins --enable-debugger --enable-debugger-gui --enable-readline --enable-xpm --enable-show-ips --enable-logging --enable-assert-checks --enable-cpp --enable-idle-hack --enable-cpu-level=6 --enable-smp --enable-fpu --enable-3dnow --enable-x86-64 --enable-vmx --enable-svm --enable-avx --enable-x86-debugger --enable-monitor-mwait --enable-alignment-check --enable-configurable-msrs --enable-long-phy-address --enable-a20-pin --enable-large-ramfile --enable-repeat-speedups --enable-fast-function-calls --enable-handlers-chaining --enable-all-optimizations --enable-cdrom --enable-sb16 --enable-es1370 --enable-gameport --enable-ne2000 --enable-pnic --enable-e1000 --enable-clgd54xx --enable-voodoo --enable-iodebug --enable-pci --enable-pcidev --enable-usb --enable-usb-ohci --enable-usb-ehci --enable-usb-xhci --enable-raw-serial --enable-vmx=2  --prefix=/home/april_zhao/bochs
```

大家可以看到我还添加了一个参数--prefix=directory

这个参数就是给 Bochs 安一个家，否则会放置到默认的 FHS 位置，由于我在调试内核的时候可能会使用不同版本和编译参数的 Bochs, 因此我不会去使用系统全局的 Bochs 而是我项目本地的 Bochs, 因此放置到一个我自己创建的目录里。

当然这只是我的一个建议，因为这么做的话你可以把 bochs 附加到你的项目里, 假如你需要多台设备同时用于开发的话就不需要每个设备各自编译一次，你 git clone 的时候就会把 bochs 环境自动带到的新设备然后直接 make bochs 就可以调试你的内核。

**你可以不参考我的做法，可以为你的每台设备都各自构建一个 bochs，当然如果你嫌麻烦的话我已经打包好了带有调试功能的 bochs 的 rpm 包，你下载我的 rpm 包然后使用包管理器安装就可以了。**

[带有调试功能的 Bochs 的 rpm 包 ![icon-default.png?t=N7T8](https://i-blog.csdnimg.cn/blog_migrate/003a2ce7eb50c2e24a8c624c260c5930.png)https://github.com/hehellooedas/ToyOS/releases/download/Kernel/bochs\_debug-2.8-1.x86\_64.rpm](https://github.com/hehellooedas/ToyOS/releases/download/Kernel/bochs_debug-2.8-1.x86_64.rpm "带有调试功能的 Bochs 的 rpm 包")

如果你使用了我打包的 rpm 包，请保护这个包的版本，不要让它升级或降级，这样会被官方提供的、没有调试功能的 Bochs 给覆盖掉，你需要保护这个包的版本。

```bash
sudo dnf versionlock add bochs
```

 如果你不使用 rpm 系 Linux 可以看看我下面打的两个包：

[带有调试功能的 Bochs 的 deb 包 ![icon-default.png?t=N7T8](https://i-blog.csdnimg.cn/blog_migrate/003a2ce7eb50c2e24a8c624c260c5930.png)https://github.com/hehellooedas/ToyOS/releases/download/Kernel/bochs\_2.8-2\_amd64.deb](https://github.com/hehellooedas/ToyOS/releases/download/Kernel/bochs_2.8-2_amd64.deb "带有调试功能的 Bochs 的 deb 包")[带有调试功能的 Bochs 的 tgz 包 ![icon-default.png?t=N7T8](https://i-blog.csdnimg.cn/blog_migrate/003a2ce7eb50c2e24a8c624c260c5930.png)https://github.com/hehellooedas/ToyOS/releases/download/Kernel/bochs-2.8.tgz](https://github.com/hehellooedas/ToyOS/releases/download/Kernel/bochs-2.8.tgz "带有调试功能的 Bochs 的 tgz 包")

如果大家以上的尝试都失败了也没有关系，我给大家把 bochs 打包进了 docker, 大家可以通过 docker 来运行 bochs. 这里我就把代码放在这里，就不发布构建好的镜像，大家下载我的压缩包然后自己构建这样更好，代码是开源的，也无需担心有什么病毒。

[bochs\_debug\_docker. tar. xz ![icon-default.png?t=N7T8](https://i-blog.csdnimg.cn/blog_migrate/003a2ce7eb50c2e24a8c624c260c5930.png)https://github.com/hehellooedas/ToyOS/releases/download/Kernel/bochs\_debug\_docker.tar.xz](https://github.com/hehellooedas/ToyOS/releases/download/Kernel/bochs_debug_docker.tar.xz "bochs_debug_docker. tar. xz") 大家先安装好 docker 或者 podman, 然后下载这个. tar. xz，下载好之后解压缩。

```cobol
tar -xvf bochs_debug_docker. tar. xzcd dockerfiledocker build -t bochs_debug_docker . #然后耐心等待一段时间 docker run -it --rm -e DISPLAY=$DISPLAY -v /tmp/.X11-unix:/tmp/.X11-unix bochs_debug_docker bash
```

运行之后会进入 docker 环境

```cobol
dnf install python3-dnf-plugin-versionlockdnf versionlock add bochs
```

在这个环境里，大家就可以直接运行 bochs -f /path/bochsrc

由于这是在容器里，很多操作也许是无法进行的，大家可以在宿主机里编译好自己的内核，然后移动到 docker 里运行.

```bash
docker cp /path/kernel containerid:/root
```

同时，如果你启动 bochs 提示 panic, 也不要慌，可能是一些音频设备无法访问物理机的设备文件，大家可以使用 alwayscont 跳过这些 panic，毕竟你如果想写音频驱动的话，大概率已经有能力使用更高级的 Qemu 了，也一般也不用再用 bochs 来调试.

> sdl 12-compat-1.2.68-2. fc 40. x 86\_64  
> qemu-ui-sdl-8.2.2-2. fc 41. x 86\_64  
> qemu-audio-sdl-8.2.2-2. fc 41. x 86\_64  
>  
> 
> 这是 sdl 音频相关的包，大家也可以在 docker 容器里面安装它

**这里最重要的一点我在前面的表格里已经提到了：--enable-gdb-stub 这个参数和--enable-debugger 是不能共存的，也就是你要么使用 bochs 自带的调试工具，要么使用 gdb 远程调试，不可兼得。并且 gdb 调试是不能够开启 smp 的，也就是--enable-gdb-stub 和--enable-smp 不能共存。**

**如果大家想体验两种调试风格，那就只能编译两次，也就是编译出两个 Bochs, 然后可以都放进项目里，bochs\_debug 和 bochs\_gdb\_debug.**

因此我在这里推荐，尽量使用 bochs 自带的调试工具吧，除非你的内核不需要开启 smp 或者你不需要多核处理器的支持。

做好这一些配置之后，大家千万不要忙着直接就 make install，因为这么多很有可能会出错的。

#### make 前的准备

```bash
cp misc/bximage.cpp misc/bximage.cccp iodev/hdimage/hdimage.cpp iodev/hdimage/hdimage.cccp iodev/hdimage/vmware3.cpp iodev/hdimage/vmware3.cccp iodev/hdimage/vmware4.cpp iodev/hdimage/vmware4.cccp iodev/hdimage/vpc.cpp iodev/hdimage/vpc.cccp iodev/hdimage/vbox.cpp iodev/hdimage/vbox.cccp misc/bxhub.cpp misc/bxhub.cccp iodev/network/netutil.cpp iodev/network/netutil.cc
```

在我的配置中，我就需要做一些 cp 操作，修改一些 c++程序的文件名，否则会导致报错，大家可以跟着这么做，然后再执行 make install ，假如这么做了之后还是报错了，那么大家有可能需要更多的 cp 操作，同样是把. cpp 文件替换成. cc 文件就好。在编译过程中还会出现各种各样的错误，它们很有可能是因为你的系统缺少了某些库或者包，这就需要大家根据报错日志自行安装这些缺少的库，使用包管理器安装就好了。安装好之后再执行 make install，如果还是提示同样的错误，那么你可以重新执行./configure 然后再 make install.

![](https://i-blog.csdnimg.cn/blog_migrate/eab3005f41a6786535b38d23ede70db2.png)

make install 执行成功之后，在你的--prefix 指定的目录里会出现三个新目录: bin lib share

* * *

### 4、make 构建之后

##### 1、bin 目录

这是 Bochs 最关键的目录，它里面保存了几个重要二进制命令：bochs (模拟器本身)、bxhub（虚拟网络环境）、bximage（创建虚拟磁盘）。

##### ①bochs 是模拟器本身

这个我会在后面讲到该怎么使用。

##### ②bximage 是一个磁盘工具

这个工具非常有用，你就把它当作是一个交互的命令行就好，直接执行 bximage. 然后根据它的提问进行回答，以创建你的虚拟磁盘。

> ❯ bximage  
> \========================================================================  
>                                bximage  
>  Disk Image Creation / Conversion / Resize and Commit Tool for Bochs  
>                                  $Id$  
> \========================================================================  
>   
> 1\. Create new floppy or hard disk image   #创建磁盘  
> 2\. Convert hard disk image to other format (mode)   # 切换磁盘格式  
> 3\. Resize hard disk image   # 修改磁盘尺寸  
>   
> 4\. Commit 'undoable' redolog to base image  
> 5\. Disk image info  
>   
> 0\. Quit  
>   
> Please choose one \[0\] 1  
>   
> Create image  
>   
> Do you want to create a floppy disk image or a hard disk image?  #
> 
> 创建硬盘还是软盘  
> Please type hd or fd. \[hd\]    
>   
> What kind of image should I create?  
> Please type flat, sparse, growing, vpc or vmware 4. \[flat\]    
>   
> Choose the size of hard disk sectors.  
> Please type 512, 1024 or 4096. \[512\]    
>   
> Enter the hard disk size in megabytes, between 10 and 8257535  
> \[10\] 512 M  
>   
> What should be the name of the image?  
> \[c.img\] hard. disk  
>   
> Creating hard disk image 'hard. disk' with CHS=1040/16/63 (sector size = 512)  
>   
> The following line should appear in your bochsrc:  
>  ata 0-master: type=disk, path="hard. disk", mode=flat  
> ❯ ls  
> 公共模板视频图片文档下载音乐桌面  bochs\_rpm  coding  hard. disk  test. c  wpsoffice  
> ❯ file hard. disk  
> hard. disk: data  
> ❯ ll -h hard. disk  
> \-rw-r-----. 1 april\_zhao april\_zhao 512 M  3 月 27 日 16:18 hard. disk  
>  

回答的问题和磁盘分区的时候类似。

这里面的英文也不难，相信大家都能够看得懂。

这里面比较难分别的可能是虚拟磁盘的格式，我这里给大家说一说：

*   Flat 扁平格式：是一种预分配的磁盘格式，磁盘的容量在创建的时候就被分配和固定给下来。性能更好，不会动态分配磁盘空间。如果你需要的虚拟磁盘大小不大，就几十 MB, 调试内核和做磁盘驱动、文件系统使用，就可以拿 Flat 格式作为启动磁盘。如果你不知道该怎么选择磁盘格式，那就选这个。
*   Sparse 稀疏格式：是动态增长的虚拟磁盘，在创建的时候体积很小，不断写入数据后体积会增大。
*   Growing：和 Sparse 类似。
*   vpc：和 Microsoft Virtual PC 兼容。
*   vmware 4：和 vmware 虚拟机兼容。

##### ③bxhub 是一个网络工具

[bxhub 文档](https://bochs.sourceforge.io/doc/docbook/user/using-socket.html "bxhub 文档")

它支持互连两个 Bochs 会话，话使用名为“bxhub”的外部程序通过 UDP 在同一台机器上运行。也就是 bxhub 可以连接多个 Bochs 模拟出来的系统进行 UDP 网络连接。

```cobol
❯ bxhubRX port #1 in use: 40001RX port #2 in use: 40003Host MAC address: b0:c4:20:00:00:0fFTP / TFTP support and network boot disabledPress CTRL+C to quit bxhub
```

想进行网络连接当然是需要网络适配器的，这是计算机网络物理层的要求，因此你需要在你的 bochsrc 里进行配置，让 Bochs 给你模拟一块网卡：

```cobol
ne2k: mac=52:54:00:12:34:56, ethmod=socket, ethdev=mymachine:40000, script=""ne2k: mac=52:54:00:12:34:56, ethmod=socket, ethdev=40000, script=""
```

如果你和我一样，直接在你的主机系统里敲这个命令行 bxhub. 那么会使用默认情况：

*   UDP 端口 40000
*   默认进行两个 Bochs 会话进行连接
*   服务器端的 MAC 地址：b 0:c4:20:00:00:0f
*   禁用 FTP/TFTP

如果你不使用默认的情况，你需要添加一些参数：

*   \-ports=\[2--6\]           虚拟以太网端口的数量
*   base=                   - 基本 UDP 端口
*   \-mac=                     主机的 MAC 地址
*   tftp=                        使用指定目录作为 root，以获取 FTP 支持
*   \-bootfile=                DHCP 的网络引导文件
*   \-log=                       设置日志级别 (1,2,3) 默认是 1
*   \-logfile=                  将日志输出发送到指定文件
*   \--help                      显示帮助信息

> “vnet”服务器现在还使用 TFTP 目录作为 root 提供被动 FTP 支持。 FTP 服务器名称为 vnet-ftp。对于只读访问，必须将用户名设置为匿名并使用任意密码。该模式支持浏览目录子树和下载文件。对于读/写访问，必须将用户设置为 bochs，密码为 bochs。这支持上传、重命名和删除文件、创建和删除目录。

##### 2、lib 目录

![](https://i-blog.csdnimg.cn/blog_migrate/616a43be5b189706d866716b422db39f.png)

这个目录下的文件是 Bochs 模拟器的插件库，它们是 Bochs 运行时可以按需加载的共享库（. so 文件）。这些插件提供了对各种设备的模拟支持，包括声音设备、网络接口卡、USB 控制器、图形适配器等。大家知道这个目录的作用就行，我们后续不太需要去配置和管理这个目录下的文件（没事不要去动它，Bochs 模拟器会自己选择需要的运行库的）。

里面的文件大致作用如下表：

<table border="1" cellpadding="1" cellspacing="1" style="width: 500px; user-select: auto;"><caption style="user-select: auto;">设备模拟插件</caption><tbody style="user-select: auto;"><tr style="user-select: auto;"><td style="user-select: auto;">文件名</td><td style="user-select: auto;">作用</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">libbx_ne 2 k. so</td><td style="user-select: auto;">提供对 NE 2000 网卡的模拟</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">libbx_sb 16. so</td><td style="user-select: auto;">提供对 Sound Blaster 16 声音卡的模拟</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">libbx_e 1000. so</td><td style="user-select: auto;">提供对 Intel E 1000 网卡的模拟</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">libbx_vga. so</td><td style="user-select: auto;">提供对 VGA 图形适配器的模拟</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">libbx_usb*. so</td><td style="user-select: auto;">提供对 USB 控制器标准的模拟</td></tr></tbody></table>

<table border="1" cellpadding="1" cellspacing="1" style="width: 500px; user-select: auto;"><caption style="user-select: auto;">网络模拟插件</caption><tbody style="user-select: auto;"><tr style="user-select: auto;"><td style="user-select: auto;">文件名</td><td style="user-select: auto;">作用</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">libbx_eth_slirp. so</td><td style="user-select: auto;">通过用户模式网络堆栈（如 slirp）提供网络连接</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">libbx_eth_socket. so</td><td style="user-select: auto;">通过套接字提供网络连接</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">libbx_eth_tuntap. so</td><td style="user-select: auto;">通过 TUN/TAP 设备提供网络连接</td></tr></tbody></table>

<table border="1" cellpadding="1" cellspacing="1" style="width: 500px; user-select: auto;"><caption style="user-select: auto;">图形界面插件</caption><tbody style="user-select: auto;"><tr style="user-select: auto;"><td style="user-select: auto;">文件名</td><td style="user-select: auto;">作用</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">libbx_sdl 2_gui. so</td><td style="user-select: auto;">提供基于 SDL 2. x 的图形用户界面</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">libbx_x_gui. so</td><td style="user-select: auto;">提供基于 X Window 系统的图形用户界面</td></tr></tbody></table>

##### 3、share

1.  BIOS-bochs-latest：BIOS 模拟软件
2.  VGABIOS-lgpl-latest-cirrus：VGA 模拟软件

大家主要需要了解的就是以上两个文件，我会在后面再提到他俩。在 share 目录中还有两个子目录，分别是 doc 和 man, 这两个目录原本是要依照 FHS 放置到/usr 里头的。当你执行 man bochs 命令的时候会把内容显示出来，作为帮助文档，那么既然我们使用--prefix 参数把 Bochs 放置到自己的目录里而不是依照 FHS 标准放置的话，就不能使用 man 命令去查看帮助文档了，大家可以手动翻阅这两个目录里的文档。

* * *

### 让你的 Bochs 跑起来：

  想让 Bochs 跑起来其实非常简单，我们只需要使用 bochs/bin/bochs 这个命令，直接运行它，那么 bochs 就跑起来了，但是 Bochs 这时候会非常疑惑，它不知道自己该跑什么程序，因此我们要通过一个配置文件来告知 Bochs 模拟器让它以何种方式模拟。

```bash
bochs -f bochsrc
```

使用-f 选项指定 Bochs 要使用的配置文件，这个 bochsrc 就是配置文件的文件名，当然本质上是配置文件的位置。bochsrc 是我取的名字，你不一定要让这个配置文件叫这个名字，实际上叫什么名字都可以。总之使用-f 选项指定配置文件的位置。

如果你是使用的自己编译的 Bochs, 或者你改变了 Bochs 目录的位置, 那么在启动的时候是需要**配置环境变量**的：

```cobol
export BXSHARE = xxxx/bochs/lib/bochs/share/bochsexport LTDL_LIBRARY_PATH = xxxx/bochs/lib/bochs/plugins
```

是如图所示的这两个环境变量，你可以把它写入到~/. zshrc 或 ~/. bashrc 或 /etc/bashrc, 这些地方。那么当你的 shell 启动的时候就会引入这两个环境变量。

如果你不想直接执行 bochs 脚本这么麻烦，而是自己写了一个 Makefile 脚本，那么你可以在 Makefile 脚本里添加环境变量，不需要添加到 bashrc 了

```cobol
BXSHARE = bochs/lib/bochs/share/bochsexport LTDL_LIBRARY_PATH = bochs/lib/bochs/plugins
```

好了，当你看到这里的时候你已经配置并安装好了 Bochs, 并且已经知道怎么启动它，但这仅仅是一个开始，重头戏其实在后面。

* * *

四、编写 Bochs 的配置文件
--------------

编写配置文件可以说是这篇博客里最麻烦的过程，有很多各参数需要配置和调试，我在观看官方的英文文档的时候也是非常头疼，不过麻烦的部分我尽可能帮大家给解决掉，请大家耐心听我一一道来。

我会由浅入深的开始讲，方便读者随时知道自己当前进行设置的目的是什么。

### 1、ROM image

我先填一个前面埋的坑，就是那两个重要文件。

```cobol
#设置ROM和VGA模拟romimage:file="bochs/share/bochs/BIOS-bochs-latest"vgaromimage:file="bochs/share/bochs/VGABIOS-lgpl-latest"  #Bochs自带的VGA文件设定的VBE显示地址为 0xe0000000 ，你启动VBE后可以往这里头写入数据以显示像素
```

bochsrc 里需要指定这两个文件的位置，如果你的 bochs 是跟随项目的，那就如上述代码这么写就好；

如果你想要使用默认 FHS 的 Bochs

```cobol
romimage:file="/usr/share/bochs/BIOS-bochs-latest"vgaromimage:file="/usr/share/bochs/VGABIOS-lgpl-latest"  #你可以添加参数进去romimage :file="/usr/share/bochs/BIOS-bochs-latest", options=fastboot #使用这个参数可以让BIOS跳过启动菜单 ，那么启动就可以快一点
```

那就要这样写。总之就是要明确两个重要文件的位置。如果你找不到你的这两个文件在什么地方，你可以使用 find 命令去查找:

```matlab
sudo find / -name "*BIOS-bochs-latest*"
```

![](https://i-blog.csdnimg.cn/blog_migrate/eb2dfd10d8831fd7855b724deb76cd17.png)我安装了不止一个版本的 Bochs.

对于新手而言，只要知道这两个文件就足够了。如果你还需要更多的配置，还得看官方文档。

[ROM images](https://bochs.sourceforge.io/doc/docbook/user/rom-images.html "ROM images")

* * *

### 2、配置内存

我想从简单到难的顺序写，内存对于大家来说肯定是非常不陌生的。

```cobol
megs: 128  #设定内存大小为128MBmegs : 2048 #最大支持的内存大小为2048MB
```

这样就设置了 Bochs 模拟出来的计算机环境的内存是 128 MB 大小。Bochs 模拟器支持的最大内存为 2048 MB 也就是 2 GB 。你可以填入的最小的数是 1, 也就是 1 MB 大小的内存，毕竟 8086 CPU 的地址总线是 20 位，最大的寻址空间就是 1 MB. 其实在官方文档里，megs 参数还有其他用法，不过我个人觉得按照上面的样子这么写就可以了，也不用做过多的考虑，我相信内核开发者的计算机内存大小一般也不会低于 1 GB 了，如果你的内存实在不足，bochs 将会提示:std:: bad\_alloc 这样的字样（充满了 C++命名空间的气息）。官方文档虽然写的非常详细，但是也没有必要全部都考虑进去，能够达到自己的目的就好。

* * *

### 3、调试选项

调试选项就是你设置 bochs 以什么方式来调试，是字符界面调试还是图形界面调试，bochs 产生的界面使用哪一个图像库来绘制这样。

```cobol
#使用命令行进行调试config_interface :textconfigdisplay_library: x  #使用图形界面进行调试config_interface :textconfigdisplay_library: x, options="gui_debug"
```

以上是我的选项，我建议读者按照我这么设置就挺好了，不过也可以根据自己的需要进行调试设置。

config\_interface 可选参数: textconfig  /   wx   /   win 32 config

```cobol
使用示例：  display_library: x  display_library: sdl 2, options=fullscreen  display_library: options=cmdmode    "cmdmode"     - 按 F 7 后调用标题栏按钮处理程序（sdl、sdl 2、win 32、x）  "fullscreen"  - 以全屏模式启动（sdl、sdl 2）  "gui_debug"   - 使用 GTK 调试器 GUI (sdl, x) / Win 32 调试器 GUI (sdl, sdl 2, win 32)  "hideIPS"     - 禁用状态栏中的 IPS 输出（rfb、sdl、sdl 2、term、vncsrv、win 32、wx、x）  "nokeyrepeat" - 关闭主机键盘重复（sdl、sdl 2、win 32、x）  "no_gui_console" - 使用系统控制台而不是内置 GUI 控制台（rfb、sdl、sdl 2、vncsrv、x）  "timeout"     - 等待客户端（rfb、vncsrv）的时间（以秒为单位）
```

* * *

### 4、控制可选插件

```cobol
plugin_ctrl: unmapped=0, e 1000=1 # unload 'unmapped' and load 'e 1000'
```

就是控制哪些插件是开启的，哪些插件是关闭的，为 1 是开启，为 0 是关闭。

> 默认情况下将加载这些插件（如果存在）：'biosdev'， 'extfpuirq'， 'Gameport'、'iodebug'、'Parallel'、'Serial'、'Speaker' 和 'Unmapped'。

提示：有些插件可能需要调用系统的 API, 如果你缺少某写包或者未开放某些端口，bochs 是会报错的，因此如果你的 bochs 启动的时候出现了 panic, 你可以关掉某些插件。

```cobol
#设置插件plugin_ctrl :unmapped=1, biosdev=1, speaker=1, extfpuirq=1, parallel=1, serial=1, iodebug=1
```

这是我的插件设置。

* * *

### 5、设置启动方式和磁盘

```csharp
  boot: floppy  #从软盘启动  boot: cdrom, disk    #先从cd启动 ，如果不行再从硬盘启动  boot: network, disk  #先从网络启动 ，如果不行再去硬盘启动  boot: cdrom, floppy, disk    #先cd启动 ，不行就去软盘找，再不行就去硬盘找
```

不用写 4 个 boot 上去，写一个 boot 就好，表明从哪个存储设备启动，并设置启动顺序，你最多可以写三个设备进去。

磁盘设置可以说是整个 bochsrc 配置文件里面最重要的设置了，如果你在启动 bochs 的时候提示，没有找到可启动的设备，或者没有启动项，那么大概率是磁盘设置错误。就是说 Bochs 不知道该怎么从你的磁盘加载 MBR 进行启动。

* * *

#### 1、设置软盘

```cobol
floppy_bootsig_check:disabled=0 floppya:type=1_44,1_44="./tools/boot. img", status=inserted, write_protected=0 #3 .5 英寸高密度软盘
```

虽然现在来看软盘早已淘汰，不过有时候可以用来研究软盘。

floppy\_bootsig\_check: disabled=1

这将禁用启动软盘上的 0 xaa 55 签名检查。默认情况下检查是启用的。

正常情况下, 启动从软盘时会检查 BOOT 扇区的末尾是否有标准的 0 xaa 55 签名。但是有些非标准的软盘可能缺少这个签名。通过设置 disabled=1 可以禁用这个检查, 从而允许来自没有签名的软盘的启动。

默认情况下,检查是启用的 (disabled=0)。只有在需要兼容某些非标准启动软盘的情况下, 才需要设置为 disabled=1 禁用检查。

软盘比较在意尺寸和大小，大家在创建的时候就应该自己的软盘是什么规格的软盘

支持以下软盘介质类型: 2\_88,1\_44,1\_2,720 k, 360 k, 320 k, 180 k, 160 k, 以及"image"让 Bochs 能自动检测软盘介质类型 (只对图像有效, 不适用于原始软盘驱动器)。在这种情况下, 尺寸必须匹配支持的类型之一。

* * *

#### 2、设置硬盘

```cobol
实例：ata 0: enabled=1, ioaddr 1=0 x 1 f 0, ioaddr 2=0 x 3 f 0, irq=14 ata 1: enabled=1, ioaddr 1=0 x 170, ioaddr 2=0 x 370, irq=15 ata 2: enabled=1, ioaddr 1=0 x 1 e 8, ioaddr 2=0 x 3 e 0, irq=11 ata 3: enabled=1, ioaddr 1=0 x 168, ioaddr 2=0 x 360, irq=9
```

这些选项支持最大 4 个 ata 通道。每个通道的双 io 地址和中断必须指定。默认下 ata 0 和 ata 1 处于启用状态, 具有上述值。

irq 指定模拟的 ATA 控制器对应的中断线路，也就是磁盘通过 ATA 给你发送中断消息时候的中断号，比如 irq=14, 则你应该设定 0 x 2 e 中断跳转到对应的磁盘处理函数，因为前 0 x 20 个中断被 Intel 保留了，因此从 0 x 20 开始计算普通中断号。

这里请注意一下，虽然官方文档里已经提供了 4 个 ATA 通道的 irq 值，但是经过我的尝试，这个值是有可能与别的设备的中断号有冲突，如果大家遇到了冲突的现象可以尝试更换一个中断号。还有就是在设置 ATA 通道连接的 master 和 slave 磁盘的时候，如果你 ioaddr 1 对应 master、ioaddr 2 对应 slave 失败了，你可以尝试交换了一下这二者，把原本连接到 master 的磁盘连接到 slave 磁盘。

ioaddr 为 IO 端口的起始，如 ioaddr=0 x 1 f 0

```cobol
/*  磁盘 0  */ #define PORT_DISK 0_DATA         0 x 1 f 0  //数据端口 #define PORT_DISK 0_ERROR        0 x 1 f 1  //错误状态 #define PORT_DISK 0_SECTOR_CNT   0 x 1 f 2  //要操作的扇区数 #define PORT_DISK 0_SECTOR_LOW   0 x 1 f 3  //扇区号/LBA (7:0) #define PORT_DISK 0_SECTOR_MID   0 x 1 f 4  //柱面号 (7:0)/LBA (15:8) #define PORT_DISK 0_SECTOR_HIGH  0 x 1 f 5  //柱面号 (15:8)/LBA (23:16) #define PORT_DISK 0_DEVICE       0 x 1 f 6  //设备工作方式 #define PORT_DISK 0_CMD          0 x 1 f 7  //控制命令端口 #define PORT_DISK 0_STATUS       0 x 3 f 6  //状态/控制寄存器   /*  磁盘 1  */ #define PORT_DISK 1_DATA         0 x 170 #define PORT_DISK 1_ERROR        0 x 171 #define PORT_DISK 1_SECTOR_CNT   0 x 172  #define PORT_DISK 1_SECTOR_LOW   0 x 173 #define PORT_DISK 1_SECTOR_MID   0 x 174 #define PORT_DISK 1_SECTOR_HIGH  0 x 175 #define PORT_DISK 1_DEVICE       0 x 176     #define PORT_DISK 1_CMD          0 x 177 #define PORT_DISK 1_STATUS       0x376
```

通过上面的端口可以分别对 ATA 0 通道的 master 磁盘和 slave 磁盘进行操作。其他三个 ATA 通道也是类似的做法。**每个 ATA 通道可以连接两块磁盘，因此你需要为每个 ATA 选项提供 ioaddr 1 和 ioaddr 2, 表示该硬盘对应的 I/O 端口号的初始地址。**

```cobol
ata 0-master: type=disk, path=10 M. img, mode=flat, cylinders=306, heads=4, spt=17, translation=noneata 1-master: type=disk, path=2 GB. cow, mode=vmware 3, cylinders=5242, heads=16, spt=50, translation=echsata 1-slave: type=disk, path=3 GB. img, mode=sparse, cylinders=6541, heads=16, spt=63, translation=autoata 2-master: type=disk, path=7 GB. img, mode=undoable, cylinders=14563, heads=16, spt=63, translation=lbaata 2-slave: type=cdrom, path=iso. sample, status=inserted
```

<table border="1" cellpadding="1" cellspacing="1" style="width: 500px; user-select: auto;"><caption style="user-select: auto;">ATA 设备的选项</caption><tbody style="user-select: auto;"><tr style="user-select: auto;"><td style="user-select: auto;">选项</td><td style="user-select: auto;">含义</td><td style="user-select: auto;">有效值</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">type</td><td style="user-select: auto;">当前磁盘的类型</td><td style="user-select: auto;">disk/cdrom</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">path</td><td style="user-select: auto;">指定磁盘的位置</td><td style="user-select: auto;">相对位置或绝对位置</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">mode</td><td style="user-select: auto;">虚拟磁盘的模式</td><td style="user-select: auto;">flat | concat | dll | sparse | vmware 3 | vmware 4 | undoable | growing | volatile | vpc | vbox | vvfat</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">cylinders</td><td style="user-select: auto;">柱面数</td><td style="user-select: auto;"></td></tr><tr style="user-select: auto;"><td style="user-select: auto;">heads</td><td style="user-select: auto;">磁头数</td><td style="user-select: auto;"></td></tr><tr style="user-select: auto;"><td style="user-select: auto;">spt</td><td style="user-select: auto;">扇区数</td><td style="user-select: auto;"></td></tr><tr style="user-select: auto;"><td style="user-select: auto;">status</td><td style="user-select: auto;">当前状态（仅对 cdrom 有效）</td><td style="user-select: auto;">inserted | ejected]</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">biosdetect</td><td style="user-select: auto;">没啥用不用看</td><td style="user-select: auto;">auto | cmos | none</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">translation</td><td style="user-select: auto;">磁盘转换方案</td><td style="user-select: auto;">none | lba | large | rechs | auto</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">model</td><td style="user-select: auto;">识别 ATA，命令返回的字符串</td><td style="user-select: auto;">字符串</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">journal</td><td style="user-select: auto;">我也不知道这是做什么的</td><td style="user-select: auto;">没用过这个参数</td></tr></tbody></table>

1.  对 bximage 创建的磁盘镜像文件, 如果 CHS 设置为 0/0/0, Bochs 会根据 heads=16 和 spt=63 自动计算柱面值。
    
2.  对其他磁盘镜像或模式, 柱面、磁头和扇区数必须手动指定。镜像文件实际大小必须等于 C_H_S\*512 字节。
    
3.  如果使用其他项目产生的平扁磁盘镜像, 文件尾可能包含附加信息, 导致校验失败。这时候可以选择"继续"跳过 Panic。
    
4.  磁盘转换方案用于老式 INT 13 BIOS 功能和 DOS 等旧系统:
    
    none: 不转换, 支持 528 MB 以下盘
    
    large: 标准位移算法, 支持 4.2 GB 以下盘
    
    rechs: 改进的 echs 算法, 假设 15 个磁头, 支持 7.9 GB 以下盘
    
    lba: 标准 LBA 辅助算法, 支持 8.4 GB 以下盘
    
    auto: 自动选择最佳方案
    

简而言之:

*   对 bximage 镜像, 可以自动检测柱面值
*   对其他镜像需要手动指定 CHS 值
*   文件大小必须匹配 CHS 格式
*   转换方案为老旧系统提供向下兼容

> 现代计算机和计算机标准的发展速度真是太快了，为了方便和可调式，没有必要再使用麻烦的 CHS 方案去寻找扇区了，直接使用 LBA 方案，这样不用考虑太多的硬件和硬件的兼容性的问题。就算要使用 CHS 方式来寻找扇区，那么尽量使用 bochs 的官方工具 bximage 来产生虚拟磁盘，这样可以免于自己设定磁盘的 CHS 信息，当 bochs 启动的时候会初始化 IDE 硬盘，你可以在日志里查看你设定的磁盘的 CHS 信息。

![](https://i-blog.csdnimg.cn/blog_migrate/e53be3f2da93a25d52f4c3dce96196ea.png)

如图所示，这表明，我的 ata 0 的主盘和 ata 1 的从盘分别连接着一块磁盘。

同一块磁盘是不能连上两个接口的，当你的 ata 的 path 选项里第一次出现这块磁盘的时候，它会被 bochs 给锁定，如果你在另一个 path 里写上同一个文件的路径，那么这样会在 bochs 启动的时候被阻止。

### 6、设置 pci

```cobol
  pci: enabled=1, chipset=i 440 fx # 如果编译时打开了 pci 支持，那么这个选项是默认的  pci: enabled=1, chipset=i 440 fx, slot 1=pcivga, slot 2=ne 2 k, advopts=noacpi  pci: enabled=1, chipset=i 440 bx, slot 5=voodoo, slot 1=e 1000
```

chipset

当前支持 i 430 FX、i 440 FX 和 i 440 BX (有限) 芯片组, 默认为 i 440 FX。

slotX

可以指定连接到 PCI 插槽的设备。最多 5 个插槽。对于 PCI/ISA 混合设备, 如果要模拟 PCI 模式,要指定插槽 (cirrus、ne 2 k、pcivga)。支持为 PCI 只设备指定插槽,但如果不指定会自动分配 (e 1000、es 1370、pcidev 等)。每个插槽类型只能使用一次。对于 i 440 BX, 插槽 5 是 AGP 槽。目前只有'voodoo'可以连接到 AGP 槽。

advopts

使用高级 PCI 选项可以控制芯片组的行为。以逗号分隔多个选项。默认的“Bochs i 440 FX”启用 ACPI 和 HPET, 但原始 i 440 FX 不支持。"noacpi"和"nohpet"可以禁用它们。"noagp"禁用 i 440 BX 不完整的 AGP 子系统。

> 这里我想大家也不用考虑太多，按照 Bochs 模拟器默认的配置就好了

### 7、设置 VGA 信息

```cobol
vga:extension=cirrus, extension=vbe, update_freq=60, realtime=1, ddc=file: monitor. bin
```

这是官方文档里写的配置。其中我们需要注意到的是 update\_freq 这个参数，它代表了你的 VGA 屏幕的刷新率。VGA 更新频率指定每秒显示更新的次数。 VGA 更新定时器默认使用实时引擎，值为 10（有效范围：1 到 75）。该参数可以在运行时更改。特殊值 0 支持使用模拟图形设备的帧速率。我设置为 60 HZ, 这意味着 1/60 秒钟 Bochs 会把显示缓冲区里的数据映射到屏幕上。

> “realtime”选项指定 VGA 更新定时器的操作模式。如果设置为 1，则 VGA 计时器基于实时，否则基于 ips 设置。如果主机速度较慢（低 ips、update\_freq）并且客户机适当地使用 HLT，则将其设置为 0 且“clock:sync=none”可能会在客户机空闲时提高客户机 GUI 的响应能力。默认值为 1。
> 
> 参数“ddc”定义返回显示器 EDID 数据的 DDC 仿真的行为。默认情况下，使用“Bochs Screen”的“内置”值。其他选择是“禁用”（无 DDC 仿真）和“文件”（从用冒号分隔的文件/路径名读取监视器 EDID）。

### 8、设置键盘与鼠标

```cobol
  keyboard: type=mf, serial_delay=150, paste_delay=100000  keyboard: keymap=gui/keymaps/x 11-pc-de. map  keyboard: user_shortcut=ctrl-alt-del
```

type - 指定键盘类型 (xt/at/mf), 默认 mf

> *   xt 键盘:
> 
> 是最早期 IBM PC 推出的键盘类型, 1982 年诞生。
> 
> 采用最简单的电气规格, 没有 LED 指示灯, 功能键较少。
> 
> *   at 键盘:
> 
> 是 IBM AT 机型于 1984 年推出的升级型键盘。
> 
> 加入了打字机样式的结构, 增加了 PageUp/Down, Home, End 等功能键。
> 
> 引入了面向插针式连接设计。
> 
> *   mf 键盘:
> 
> 是微软在 1990 年推出兼容 PC 标准的键盘设计。
> 
> 增加了方向键集成入数字键盘区, Esc 键变大, Del 键独立出来。
> 
> 变成我们现在熟悉的 104 键标准布局。

serial\_delay -键盘到控制器的串行延迟, 单位微秒

paste\_delay - 粘贴字符到控制器的尝试频率, 给 guests 的时间应对输入流, 默认 0.1 秒

keymap - 重新映射本地键盘到 US 标准键盘布局

user\_shortcut - 指定用户按钮对应的快捷键组合, 最多 3 个按键名用'-'连接

支持的按键包括 Alt/Ctrl/Del 等 modifier, 数字功能键, 方向键等。

```cobol
  mouse: enabled=1  mouse: type=imps 2, enabled=1  mouse: type=serial, enabled=1  mouse: enabled=0, toggle=ctrl+f 10
```

type - 鼠标类型, 默认 ps 2, 也支持 imps 2 (滚动 ps 2 鼠标)、serial 串口鼠标等

enabled - 是否创建鼠标事件, 0 为关闭。但硬件模拟不受影响。

toggle - 运行时切换鼠标 capturing 方法, 默认 ctrl+鼠标中键, 也可以换成 ctrl+F 10 等组合键。

mouse 类型可以模拟不同接口的鼠标。enabled 控制用户交互, 切勿默认开启。

toggle 设置运行时方便切换鼠标状态的组合键, 如 dosbox 的 ctrl+F 10。

![](https://i-blog.csdnimg.cn/blog_migrate/9f6b1ea5133303a0a3ce0356ea221f16.png)

如图所示，红色框框里的这个按钮就是鼠标进入键，当你点击这个按钮之后，你的鼠标就被 Bochs 给捕获了，也就是你不能再操控你的主机电脑了。那么该怎么让 Bochs 把鼠标还给我们呢。

toggle 这个参数就是设置了一套按键组合，当你使用了这个组合按键，那么鼠标就会还给主机系统。

```cobol
mouse: type=ps 2, enabled=1, toggle=ctrl+mbutton
```

默认是**鼠标中键**，如果大家不小心点进去了，但又拿不回来的话，你可以使用 Ctrl + Alt + t 打开一个终端，那么这时候鼠标会短暂的还给你，然后你快速点击终端，再用 kill 关闭 Bochs.

```cobol
pkill -9 bochs
```

不过这是一个笨方法，是在实在没办法的情况下才使用的，现在大家知道了，这个返还鼠标的组合键是可以自己设置的。

### 9、设置 clock 时钟

```cobol
Syntax:  clock: sync=[none|slowdown|realtime|both], time 0=[timeValue|local|utc] Examples:  clock: sync=none,     time 0=local       # Now (localtime)  clock: sync=slowdown, time 0=315529200   # Tue Jan  1 00:00:00 1980  clock: sync=none,     time 0="Mon Jan  1 00:00:00 1990" # 631148400  clock: sync=realtime, time 0=938581955   # Wed Sep 29 07:12:35 1999  clock: sync=realtime, time 0="Sat Jan  1 00:00:00 2000" # 946681200  clock: sync=none,     time 0=1           # Now (localtime)  clock: sync=none,     time 0=utc         # Now (utc/gmt) 默认的配置 sync=none, rtc_sync=0, time 0=local
```

sync 控制与主机时间的同步程度, time 0 设置引导时间, 可以指定**绝对时间戳**或**相对主机的本地/UTC 时间**。slowdown (牺牲性能保持可重复)、realtime (牺牲可重复性实时同步)

> 这个时钟一般来说就保持默认配置就好，即把你的宿主机操作系统的时间同步到 Bochs 的虚拟机的硬件 RTC 里，除非说你需要设定虚拟时间，否则没必要修改。

### 10、日志信息

```perl
示例: logprefix: %t-%e-@%i-%dlogprefix: %i%e%d
```

这设置日志行前缀格式字符串。可以使用以下特殊标签:

%t : 11 位十进制定时器计数  
%i : 8 位十六进制当前 CPU 指令指针 (SMP 模式下忽略)  
%e : 1 个字符事件类型 (i/d/p/e)  
%d : 5 个字符设备名称 (在\[\]中)

默认:%t%e%d

logprefix 允许定制日志行前缀的格式, 包括时间戳、cpu 寄存器、事件类型和设备名等信息。

通过组合特殊标签可以生成结构化的前缀, 方便分类和查询日志。

### 11、调试信息

```cobol
示例: debug: action=ignore, pci=reportinfo: action=reporterror: action=reportpanic: action=ask
```

Bochs 会产生四类事件:

*   debug: 用于调试, 会产生大量消息
*   info: 有意义但不常见的事件
*   error: 不应该出现但不影响模拟的条件
*   panic: 模拟无法继续运行

这四行分别设置每类事件的响应动作:

*   fatal: 终止模拟
*   ask: 询问用户下一步
*   warn: 显示对话框并继续
*   report: 输出到控制台
*   ignore: 忽略

#### 

#### 调试信息输出位置

        你可以把 Bochs 生成的调试信息导出到文件然后慢慢观察。

```typescript
示例: debugger_log: debugger. outdebugger_log: /dev/null (Unix only) debugger_log: -
```

需要指定保存的位置。如果你不需要把调试信息保存到文件里可以把调试信息输出到/dev/null 这个“黑洞”设备里，或者干脆不生成。

类似这样的小配置还有很多，这里我不想一一列举，我就放一个我的配置在这里供大家参考，如果大家有需要，我再一一说明。

```cobol
print_timestamps: enabled=0 debugger_log: -magic_break: enabled=0 port_e 9_hack: enabled=0 private_colormap: enabled=0 clock: sync=none, time 0=local, rtc_sync=0# no cmosimage# no loaderlog: -logprefix: %t%e%ddebug: action=ignoreinfo: action=reporterror: action=reportpanic: action=ask
```

* * *

### 12、CPU 信息设置

这也是整个 bochsrc 的核心配置，通过这个配置能决定 bochs 将模拟哪一块 CPU, 支持哪些指令集，能够提供什么样的性能，这些都是可以自己配置的。为了让大家比较形象地看到参数的配置方式，我这里先放上我的配置过程供大家参考，随后我会解析每一个配置参数应该怎么填写。

Intel CPU 配置如下：

```cobol
cpu: count=1:4:2, ips=5000000, quantum=16, model=tigerlake, reset_on_triple_fault=1, cpuid_limit_winnt=0, ignore_bad_msrs=1, mwait_is_nop=0, msrs="msrs. def" cpuid: x 86_64=1, level=6, mmx=1, sep=1, aes=1, movbe=1, xsave=1, apic=x 2 apic, sha=1, adx=1, xsaveopt=1, avx_f 16 c=1, avx_fma=1, bmi=bmi 2,1 g_pages=1, pcid=1, fsgsbase=1, smep=1, smap=1, mwait=1, vmx=1, svm=1 cpuid: family=6, model=0 x 1 a, stepping=5, vendor_string="GenuineIntel", brand_string="11 th Gen Intel (R) Core (TM) i 5-1135 G 7 (TigerLake)"
```

AMD CPU 配置如下：

```cobol
cpu: count=1:1:1, ips=4000000, quantum=16, model=ryzen, reset_on_triple_fault=1, cpuid_limit_winnt=0, ignore_bad_msrs=1, mwait_is_nop=0, msrs="msrs. def" cpuid: x 86_64=1, level=6, mmx=1, sep=1,  aes=1, movbe=1, xsave=1, apic=x 2 apic, sha=1, adx=1, xsaveopt=1, avx_f 16 c=1, avx_fma=1, bmi=bmi 2,1 g_pages=1, pcid=1, fsgsbase=1, smep=1, smap=1, mwait=1, vmx=1 cpuid: family=6, model=0 x 1 a, stepping=5, vendor_string="AuthenticAMD", brand_string="AMD Ryzen 7 1700"
```

大家可能觉得这里比较复杂，前面的配置只需要一个或者两个参数就配置好了，而这里却有十余个地方可以配置，如果大家觉得太麻烦，可以直接用我的配置。大家在调试内核的时候不一定非得只用一个 bochsrc, 像我的话是 Intel CPU 和 AMD CPU 各自写了一份 bochsrc, 那么在调试的时候就可以用来观察 Intel 和 AMD CPU 的不同之处。在这里，**我们需要做的就是配置好 cpu 和 cpuid 这两个参数.**

cpu 配置的是 CPU 的具体能力，性能如何？什么样的工作限制？用什么模型？

cpuid 就是配置 CPU 的信息，属于哪一个家族？支持哪些指令集？CPU 名字是什么？这里的 cpuid 其实就是我们熟知的 cpuid, 你使用 x 86 的指令 cpuid 查出来的信息就是在这里设置的；你使用 CPU-Z 之类的软件去查看 CPU 的时候就会显示这些信息。

![](https://i-blog.csdnimg.cn/blog_migrate/af0297b9534a12771121cba519351a4b.png)

![](https://i-blog.csdnimg.cn/blog_migrate/f928dd9613ed2a4a4a9579bd7e2f1c8c.png)

由于我在 Linux, 我就使用开源的**[CPU-X](https://github.com/TheTumultuousUnicornOfDarkness/CPU-X "CPU-X")**替代一下 CPU-Z。大家可以对比一下，其中的 stepping 参数就是这里的步进，vendor\_string 就是型号。这样我们让这二者对比起来，大家现在应该明白这两个参数的重要作用了。虽然 Bochs 能够模拟的 CPU 数量并不算特别多，但是可选参数是真的多，我相信也足够大家使用了，如果大家震惊于 Bochs 模拟器对 x 86 架构 CPU 仿真的认真和精准，大家不妨可以给 Bochs 项目点个 star, 甚至提交 pr, 让 Bochs 项目可以发扬光大, 只是 Bochs 对 AMD CPU 的仿真就不是那么先进，有 AMD 公司的大牛可以试着帮助其对 AMD CPU 的仿真。

| 架构名 | CPU 型号 | CPU 等级 |
| --- | --- | --- |
| bx\_generic | Default Bochs CPU configured with [CPUID](https://bochs.sourceforge.io/doc/docbook/user/bochsrc.html#BOCHSOPT-CPUID "CPUID") option | cpu level 5 |
| pentium | Intel Pentium (P 54 C) | cpu level 5 |
| pentium\_mmx | Intel Pentium MMX | cpu level 5 |
| amd\_k 6\_2\_chomper | AMD-K 6 (tm) 3 D processor (Chomper) | cpu level 5 |
| p 2\_klamath | Intel Pentium II (Klamath) | cpu level 6 |
| p 3\_katmai | Intel Pentium III (Katmai) | cpu level 6 |
| p 4\_willamette | Intel (R) Pentium (R) 4 (Willamette) | cpu level 6 |
| core\_duo\_t 2400\_yonah | Intel (R) Core (TM) Duo CPU T 2400 (Yonah) | cpu level 6 |
| atom\_n 270 | Intel (R) Atom (TM) CPU N 270 | cpu level 6 |
| p 4\_prescott\_celeron\_336 | Intel (R) Celeron (R) 336 (Prescott) | cpu level 6, x 86-64 |
| athlon 64\_clawhammer | AMD Athlon (tm) 64 Processor 2800+ (Clawhammer) | cpu level 6, x 86-64 |
| athlon 64\_venice | AMD Athlon (tm) 64 Processor 3000+ (Venice) | cpu level 6, x 86-64 |
| turion 64\_tyler | AMD Turion (tm) 64 X 2 Mobile TL-60 (Tyler) | cpu level 6, x 86-64 |
| phenom\_8650\_toliman | AMD Phenom X 3 8650 (Toliman) | cpu level 6, x 86-64 |
| core 2\_penryn\_t 9600 | Intel Mobile Core 2 Duo T 9600 (Penryn) | cpu level 6, x 86-64 |
| corei 5\_lynnfield\_750 | Intel (R) Core (TM) i 5 750 (Lynnfield) | cpu level 6, x 86-64 |
| corei 5\_arrandale\_m 520 | Intel (R) Core (TM) i 5 M 520 (Arrandale) | cpu level 6, x 86-64 |
| corei 7\_sandy\_bridge\_2600 k | Intel (R) Core (TM) i 7-2600 K (Sandy Bridge) | cpu level 6, x 86-64, avx |
| zambezi | AMD FX (tm)-4100 Quad-Core Processor (Zambezi) | cpu level 6, x 86-64, avx |
| trinity\_apu | AMD A 8-5600 K APU (Trinity) | cpu level 6, x 86-64, avx |
| ryzen | AMD Ryzen 7 1700 | cpu level 6, x 86-64, avx |
| corei 7\_ivy\_bridge\_3770 k | Intel (R) Core (TM) i 7-3770 K CPU (Ivy Bridge) | cpu level 6, x 86-64, avx |
| corei 7\_haswell\_4770 | Intel (R) Core (TM) i 7-4770 CPU (Haswell) | cpu level 6, x 86-64, avx |
| broadwell\_ult | Intel (R) Processor 5 Y 70 CPU (Broadwell) | cpu level 6, x 86-64, avx |
| corei 7\_skylake\_x | Intel (R) Core (TM) i 7-7800 X CPU (Skylake) | cpu level 6, x 86-64, avx |
| corei 3\_cnl | Intel (R) Core (TM) i 3-8121 U CPU (Cannonlake) | cpu level 6, x 86-64, avx |
| corei 7\_icelake\_u | QuadCore Intel Core i 7-1065 G 7 (IceLake) | cpu level 6, x 86-64, avx |
| tigerlake | 11 th Gen Intel (R) Core (TM) i 5-1135 G 7 (TigerLake) | cpu level 6, x 86-64, avx |

大家不要着急，你先看一看我上面放的表，这也是官方文档里的表，这张表非常重要。

*   bx\_generic 是 Bochs 的默认 CPU 定义, 根据 CPUID 指令参数进行配置。
    
*   pentium, pentium\_mmx 等是 Intel 各个年代的桌面 CPU, 如 Pentium, Pentium MMX 等。
    
*   amd\_k 6\_2\_chomper 是 AMD K 6 系列 CPU。
    
*   p 2\_klamath 是 Intel Pentium II 系列。
    
*   p 3\_katmai 是 Intel Pentium III 系列。
    
*   p 4\_willamette 是 Intel Pentium 4 系列中的 Willamette 核心。
    
*   core\_duo\_t 2400\_yonah 是 Intel Core Duo 移动 CPU。
    
*   atom\_n 270 是 Intel Atom 系列低功耗 CPU。
    
*   athlon 64\_clawhammer 等是 AMD 第一代 Opteron 和 Athlon 64 系列 CPU。
    
*   turion 64\_tyler 是 AMD Turion 64 移动 CPU。
    
*   phenom\_8650\_toliman 是 AMD Phenom 系列 CPU。
    
*   core 2\_penryn\_t 9600 是 Intel Core 2 Duo 笔记本 CPU。
    
*   corei 5/i 7 系列代表 Intel 各代酷睿 CPU, 从 Lynnfield 到现代的 Tiger Lake 都有支持。
    
*   zambezi 是 AMD FX 四核 CPU。
    
*   trinity\_apu 是 AMD 时代第一代整合 GPU 的 CPU。
    
*   ryzen 代表 AMD 现代 Ryzen 家族 CPU。
    

#### ①cpu 的各个参数：

count 指的是处理器的拓扑结构，它是以: 符号分隔，这是 SMP 体系结构里的重要概念。

其中1:4:2 的含义是当前计算机系统有 1 块 CPU, 每块 CPU 拥有 4 个物理核心，每个物理核心拥有两个逻辑线程。总而言之就是，当前计算机 CPU 是 4 核心 8 线程。请注意，Bochs 对 CPU 的配置自由度还是比较高的，虽然现实里你模拟的这块 CPU 是 4 核心 8 线程，但实际上这个 count 参数你可以自己设置，比如你设置成 1:1:1 那么它就会变成单核 CPU, 不管你后面 cpuid 里写的是哪一块 CPU。相信大家也猜到了，这么 count 的数量不可能可以设置成无限大，它实际上受限于对 APIC 的仿真能力。大家可以尝试一下它最多模拟多少逻辑核心。这里稍微注意一下，由于 bochs 对 AMD CPU 仿真能力还没跟上时代，如果大家想做 SMP 的实验请使用 Intel 的 CPU. 这个参数里面总的逻辑线程数量越大，初始化的时间就越长，请大家按照需求来考虑。

ips 指的是每秒钟能够处理的指令的数量，这个参数非常能够反映 CPU 的性能，下面一个参考表格。

| Bochs | Speed | Machine/Compiler | Typical IPS |
| --- | --- | --- | --- |
| 2.4.6 | 3.4 Ghz | Intel Core i 7 2600 with Win 7 x 64/g++ 4.5.2 | 85 to 95 MIPS |
| 2.3.7 | 3.2 Ghz | Intel Core 2 Q 9770 with WinXP/g++ 3.4 | 50 to 55 MIPS |
| 2.3.7 | 2.6 Ghz | Intel Core 2 Duo with WinXP/g++ 3.4 | 38 to 43 MIPS |
| 2.2.6 | 2.6 Ghz | Intel Core 2 Duo with WinXP/g++ 3.4 | 21 to 25 MIPS |
| 2.2.6 | 2.1 Ghz | Athlon XP with Linux 2.6/g++ 3.4 | 12 to 15 MIPS |

你可以根据你的需要来调整仿真的 CPU 的性能，数量越大，仿真的 CPU 性能越强，大家自行考虑。

quantum 指的是在将控制权返回到另一个 cpu 之前允许处理器执行的最大指令量。

*   当 Bochs 在 SMP 模式下运行时, 它会轮流地让每个 CPU 执行一小段代码, 然后切换到下一个 CPU 上执行。这个一个 CPU 执行的最多指令数量就叫做"quantum"。
    
*   小的 quantum 值意味着 CPU 间切换的频率更高, 每一个 CPU 得到运行的时间 slice 更短。大的 quantum 值则相反, 每个 CPU 可以连续运行更长时间。
    
*   调整这个 quantum 参数可以控制 Bochs 模拟的多个 CPU 的时间片轮转频率, 如何平衡它们的负载和响应时间。
    
*   太小的 quantum 可能会造成过多的上下文切换开销, 太大的 quantum 则可能导致某个 CPU 独占超长时间不让其他 CPU 执行。
    

如果大家不知道这是什么意思，请按照我的设置来做。

model 这个参数我相信大家应该不陌生，它其实就是我上面那个表格里的 CPU 架构，你选择了哪一块 CPU, 那么就把那块 CPU 对应的 CPU 架构的值复制粘贴到这里来。比如我选择了 11 th Gen Intel (R) Core (TM) i 5-1135 G 7 (TigerLake) 这一块 CPU, 那么我就应该设置 model 值为 tigerlake.

reset\_on\_triple\_fault

这个参数的含义是当发生三重错误时，Bochs 的行为，你设置为 1 就好。意味着当发生三重错误时，Bochs 会重启，物理机也会是这样。所以当你的内核无缘无故重启的时候，你就要看看是否发生了三重错误，三重错误意味着遇到了一些离了个大谱的问题，不重启不行了。

cpuid\_limit\_winnt

这个参数固定设置为 0 就好了，完全就是为了兼容旧的 WIndowsNT.

> *   Windows NT 在引导过程中, 仅能支持 CPUID 功能号 ≤ 2 的处理器。更高号的 CPUID 信息它无法识别和使用。
>     
> *   但是现实中的 CPU 的 CPUID 功能号往往大于 2。如果直接使用复杂的真 CPU 特性, Windows NT 就可能无法正常启动。
>     
> *   所以通过设置 cpuid\_limit\_winnt=1, Bochs 会限制模拟 CPU 的最大 CPUID 功能号为 2。
>     
> *   这可以起到“欺骗”Windows NT, 让它以为 CPU 仅支持较低功能, 从而顺利完成安装和引导
>     

ignore\_bad\_msrs

MSR 寄存器为 x 86 架构中非常重要的一系列用于控制 CPU 运行、功能开关、调试、跟踪程序执行、监测 CPU 性能等方面的寄存器。但是如果你访问到不识别的 MSR 地址，原本应该是会出发 GP 通用保护异常的，而 Bochs 为了兼容更多的 CPU, 并不模拟所有的 MSR 寄存器。因此这个参数的含义就是忽略错误的 MSR 寄存器访问，就是说就算你读写了一个不存在的 MSR 地址，也不会出发 GP 异常。ignore 就是忽略的意思。

mwait\_is\_nop

mwait 是一种机制，就是让 CPU 在低功耗下运行，物理机当然可以这么做，但是 Bochs 想实现这种机制，难度实在太大。因此这个选项的含义就是把你的 mwait 指令给替换成 nop 指令，nop 指令执行起来很简单。你可以关闭这个转换机制。

msrs

MSR 是模型专有寄存器, 不同 CPU 型号的 MSR 种类和属性各不相同。

Bochs 内置仅支持部分常见 MSR, 无法覆盖所有真实 CPU 的 MSR。因此需要你来指定模拟文件的位置。你可以按照我的写法写。

```php
##                   ----------------------------------#                      Bochs CPU MSRs configuration#                   ----------------------------------## LEGEND:# ------##    MSR ADDRESS - MSR address in hex (supplied in ECX register for RDMSR/WRMSR)#    MSR TYPE    - MSR type, see below##    The following fields have any meaning for MSRs with no type only:##    RESET_HI    - reset value of the MSR (bits 63:32)#    RESET_LO    - reset value of the MSR (bits 31:00)##    NOTE: the value of the MSR doesn't change on INIT (software reset).##    RSRVD_HI    - mask of reserved bits (bits 63:32)#    RSRVD_LO    - mask of reserved bits (bits 31:00)##    NOTE: #GP fault will be generated when trying to modify any of MSR#          reserved bits.##    IGNRD_HI    - mask of ignored bits (bits 63:32)#    IGNRD_LO    - mask of ignored bits (bits 31:00)##    NOTE: Ignored bits will keep their reset value, all writes to these #          bits are ignored.## MSR TYPES:# ---------##    0 - No type.#    1 - MSR contains linear address, #        #GP if writing non-canonical address in 64-bit mode.#    2 - MSR contains physical address,#        #GP if writing a value which exceeds emulated physical address size.#  # ADDRESS  TYPE   RESET_HI   RESET_LO    RSRVD_HI   RSRVD_LO   IGNRD_HI   IGNRD_LO# ---------------------------------------------------------------------------------   0 x 02 c     0    00000000   00000000    00000000   00000000   00000000   00000000
```

有兴趣的了解一下就好，大多数人不需要看懂这些文件。

#### ②cpuid 的各个参数

level 是模拟的 CPU 级别，你选好要仿真的 CPU 之后直接查表，是 5 就设置为 5, 是 6 就设置为 6

mmx=1 则打开了 mmx 指令集。MMX 主要用于通过硬件加速支持整数 SIMD 操作。

sep=1 则打开了 SEP 指令集的支持，这是 sysenter 和 sysexit，我相信写过内核的对这两条指令应该不陌生，它们能快速地在内核态与用户态之间进行切换，快速系统调用。

aes=1 则打开了 AES 指令集的支持，这是加密、解密相关的指令集。

相信经过我上面的这几个例子，大家已经知道这几个参数该怎么写了，开启就=1, 关闭就=0. 我们现在要弄懂的就是每个指令集提供的功能是什么。我帮大家做了一个表格。

<table border="1" cellpadding="1" cellspacing="1" style="width: 500px; user-select: auto;"><tbody style="user-select: auto;"><tr style="user-select: auto;"><td style="user-select: auto;">指令集/可选参数名</td><td style="user-select: auto;">描述</td><td style="user-select: auto;">使用条件</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">mmx</td><td style="user-select: auto;">多媒体扩展指令集</td><td style="user-select: auto;">BX_CPU_LEVEL&gt;=5</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">apic</td><td style="user-select: auto;">高级可编程中断控制器</td><td style="user-select: auto;">BX_CPU_LEVEL&gt;=5</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">sep</td><td style="user-select: auto;">快速系统调用与返回</td><td style="user-select: auto;">BX_CPU_LEVEL&gt;=6</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">simd</td><td style="user-select: auto;">单指令多数据流指令集支持 (SSE SSE 2 SSE 3 SSSE 3 SSE 4_1 等)</td><td style="user-select: auto;">&gt;=6</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">sse 4 a</td><td style="user-select: auto;">AMD sse 4_a 支持</td><td style="user-select: auto;">&gt;=6</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">misaligned_sse</td><td style="user-select: auto;">AMD 错位 SSE 模式支持</td><td style="user-select: auto;">&gt;=6</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">aes</td><td style="user-select: auto;">aes 指令集支持</td><td style="user-select: auto;">&gt;=6</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">sha</td><td style="user-select: auto;">sha 指令集支持</td><td style="user-select: auto;">&gt;=6</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">movbe</td><td style="user-select: auto;">～</td><td style="user-select: auto;">&gt;=6</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">adx</td><td style="user-select: auto;">ADCX/ADOX 支持</td><td style="user-select: auto;">&gt;=6</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">xsave</td><td style="user-select: auto;">XSAVE 拓展支持</td><td style="user-select: auto;">&gt;=6</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">xsaveopt</td><td style="user-select: auto;">XSAVEOPT 指令支持</td><td style="user-select: auto;">&gt;=6</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">avx_f 16 c</td><td style="user-select: auto;">AVX float 16 转换指令支持</td><td style="user-select: auto;">编译时启用--enable-avx</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">avx_fma</td><td style="user-select: auto;">AVX 融合乘加 (FMA) 指令支持</td><td style="user-select: auto;">编译时启用--enable-avx</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">bmi</td><td style="user-select: auto;">BMI 1/BMI 2 指令支持</td><td style="user-select: auto;">编译时启用--enable-avx</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">fma 4</td><td style="user-select: auto;">AND 四操作数 FMA 指令支持</td><td style="user-select: auto;">编译时启用--enable-avx</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">xop</td><td style="user-select: auto;">AMD XOP 指令支持</td><td style="user-select: auto;">编译时启用--enable-avx</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">tbm</td><td style="user-select: auto;">AMD TBM 指令支持</td><td style="user-select: auto;">编译时启用--enable-avx</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">x 86_64</td><td style="user-select: auto;">启用长模式支持</td><td style="user-select: auto;">需要 x 86-64 支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">1 g_pages</td><td style="user-select: auto;">启用 1 GB 大小页面支持</td><td style="user-select: auto;">需要 x 86-64 支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">pcid</td><td style="user-select: auto;">启用进程上下文标识符 OCID 支持</td><td style="user-select: auto;">需要 x 86-64 支持</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">smep</td><td style="user-select: auto;">启用监督式执行保护支持</td><td style="user-select: auto;">&gt;=6</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">smap</td><td style="user-select: auto;">启用监督式预防支持</td><td style="user-select: auto;">&gt;=6</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">mwait</td><td style="user-select: auto;">选择 monitor/mwait 指令支持</td><td style="user-select: auto;">编译时启用--enable-monitor-mwait</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">vmx</td><td style="user-select: auto;">选择 VMX 扩展模拟支持</td><td style="user-select: auto;">编译时启用--enable-vmx</td></tr><tr style="user-select: auto;"><td style="user-select: auto;">svm</td><td style="user-select: auto;">选择 AMD SVM 安全虚拟机扩展支持</td><td style="user-select: auto;">编译时启用--enable-svm</td></tr></tbody></table>

*   Family: 表示 CPU 家族, 如 Intel Sandy Bridge 为 6 等
*   Model: 表示 CPU 型号, 不同产品会有不同 model 值
*   Stepping: 表示片上细化版本
*   stepping 字段表示 CPU 的微型号, 数字越大表示芯片做工水平越高

这几个参数就是你在 bochs 启动之后使用 cpuid 指令查出来的信息，就是在这里设置的。你可以封装这些从 cpuid 查出来的信息，写成类似 CPU-Z 的带有图形界面的程序。

vendor\_string 这是 CPU 的厂商标识符

已知的制造商以及其 ID 如下：

*   `"AMDisbetter!"` – [AMD](https://zh.wikipedia.org/wiki/%E8%B6%85%E5%A8%81%E5%8D%8A%E5%AF%BC%E4%BD%93 "AMD") K 5 的早期工程样品
*   `"AuthenticAMD"` – [AMD](https://zh.wikipedia.org/wiki/%E8%B6%85%E5%A8%81%E5%8D%8A%E5%AF%BC%E4%BD%93 "AMD")
*   `"CentaurHauls"` – IDT/半人马座（Centaur）/[兆芯](https://zh.wikipedia.org/wiki/%E5%85%86%E8%8A%AF "兆芯")
*   `"CyrixInstead"` – [Cyrix](https://zh.wikipedia.org/wiki/Cyrix "Cyrix")/[意法半导体](https://zh.wikipedia.org/wiki/%E6%84%8F%E6%B3%95%E5%8D%8A%E5%B0%8E%E9%AB%94 "意法半导体")/[IBM](https://zh.wikipedia.org/wiki/IBM "IBM")
*   `"GenuineIntel"` – [英特尔](https://zh.wikipedia.org/wiki/%E8%8B%B1%E7%89%B9%E5%B0%94 "英特尔")
*   `"TransmetaCPU"` – [全美达](https://zh.wikipedia.org/wiki/%E5%85%A8%E7%BE%8E%E9%81%94 "全美达")
*   `"GenuineTMx 86"` – [全美达](https://zh.wikipedia.org/wiki/%E5%85%A8%E7%BE%8E%E9%81%94 "全美达")
*   `"Geode by NSC"` – [国家半导体](https://zh.wikipedia.org/wiki/%E5%9C%8B%E5%AE%B6%E5%8D%8A%E5%B0%8E%E9%AB%94 "国家半导体")
*   `"NexGenDriven"` – [NexGen](https://zh.wikipedia.org/wiki/NexGen "NexGen")
*   `"RiseRiseRise"` – Rise
*   `"SiS SiS SiS "` – [硅统](https://zh.wikipedia.org/wiki/%E7%9F%BD%E7%B5%B1%E7%A7%91%E6%8A%80 "硅统")
*   `"UMC UMC UMC "` – [联华电子](https://zh.wikipedia.org/wiki/%E8%81%AF%E8%8F%AF%E9%9B%BB%E5%AD%90 "联华电子")（台联电）
*   `"VIA VIA VIA "` – [威盛](https://zh.wikipedia.org/wiki/%E5%A8%81%E7%9B%9B%E9%9B%BB%E5%AD%90 "威盛")
*   `"Vortex 86 SoC"` – DM&P Vortex 86
*   `"  Shanghai  "` – [兆芯](https://zh.wikipedia.org/wiki/%E5%85%86%E8%8A%AF "兆芯")
*   `"HygonGenuine"` – 海光
*   `"Genuine  RDC"` – RDC
*   `"E 2 K MACHINE"` – MCST Elbrus

我在这里放了这么多个厂商，并不是都能放进 bochs 里，总之要模拟哪个厂商的 CPU, 这个字符串就填写哪一个就好了。

brand\_string 这也是一个字符串，是 CPU 的型号或者说是名字，取值只能是前面表格里的。

相信大家看到这里已经跃跃欲试了，想自己写 CPU 的配置文件出来，那么我在这里举几个例子，大家看了之后就一切都清楚了。

配置文件 1 及其效果：

```cobol
cpu: count=1:4:2, ips=10000000, quantum=16, model=tigerlake, reset_on_triple_fault=1, cpuid_limit_winnt=0, ignore_bad_msrs=1, mwait_is_nop=0, msrs="msrs. def" cpuid: x 86_64=1, level=6, mmx=1, sep=1, aes=1, movbe=1, xsave=1, apic=x 2 apic, sha=1, adx=1, xsaveopt=1, avx_f 16 c=1, avx_fma=1, bmi=bmi 2,1 g_pages=1, pcid=1, fsgsbase=1, smep=1, smap=1, mwait=1, vmx=1, svm=1 cpuid: family=6, model=0 x 1 a, stepping=5, vendor_string="GenuineIntel", brand_string="11 th Gen Intel (R) Core (TM) i 5-1135 G 7 (TigerLake)"
```

![](https://i-blog.csdnimg.cn/blog_migrate/d7a438cfe328b1632a6dfd7b1f5e0cd7.png)

上面的 Bochs 图就是我使用 CPUID 这条汇编指令查看到了 CPU 信息。

配置文件 2 及其效果：

```cobol
cpu: count=1:1:1, ips=4000000, quantum=16, model=ryzen, reset_on_triple_fault=1, cpuid_limit_winnt=0, ignore_bad_msrs=1, mwait_is_nop=0, msrs="msrs. def" cpuid: x 86_64=1, level=6, mmx=1, sep=1,  aes=1, movbe=1, xsave=1, apic=x 2 apic, sha=1, movbe=1, adx=1, xsaveopt=1, avx_f 16 c=1, avx_fma=1, bmi=bmi 2,1 g_pages=1, pcid=1, fsgsbase=1, smep=1, smap=1, mwait=1, vmx=1 cpuid: family=6, model=0 x 1 a, stepping=5, vendor_string="AuthenticAMD", brand_string="AMD Ryzen 7 1700"
```

![](https://i-blog.csdnimg.cn/blog_migrate/a25c9069bf991cc7753751cba987f5e3.png)

大家看见了，我修改了配置文件之后，CPUID 查看到的信息也会跟着改变。

配置文件 3 及其效果：

```cobol
cpu: count=1:4:2, ips=10000000, quantum=16, model=corei 7_skylake_x, reset_on_triple_fault=1, cpuid_limit_winnt=0, ignore_bad_msrs=1, mwait_is_nop=0, msrs="msrs. def" cpuid: x 86_64=1, level=6, mmx=1, sep=1, aes=1, movbe=1, xsave=1, apic=x 2 apic, sha=1, adx=1, xsaveopt=1, avx_f 16 c=1, avx_fma=1, bmi=bmi 2,1 g_pages=1, pcid=1, fsgsbase=1, smep=1, smap=1, mwait=1, vmx=1, svm=1 cpuid: family=6, model=0 x 1 a, stepping=5, vendor_string="GenuineIntel", brand_string="Intel (R) Core (TM) i 7-7800 X CPU (Skylake)"
```

![](https://i-blog.csdnimg.cn/blog_migrate/b5dc67fdd202695f31b4716fdda53b7e.png)

相信大家已经总结出规律了：如果你想换另外一块 CPU 进行模拟仿真，那么你只需要对照我前面给你的那张表格，修改 model, ventor\_string，brand\_string 即可。

cpuid 这个参数还是非常重要的，它代表了你要模拟仿真的 CPU 具备哪些指令集的支持，你在做内核编程的时候在使用较为先进的指令之前也需要对它进行判断，只有你的 CPU 支持该指令集，你才可以使用这条指令，否则的话 CPU 就会报 #UD异常 。这里我需要提醒一下，Bochs 的 I/O APIC 和 HPET 这两个设备是默认打开的，大家在使用 Bochs 模拟这两个设备的时候不需要去 ACPI 找它们的地址也不需要去主板上的芯片找，直接跳过开启阶段，直接使用就好。大家在设置指令集支持情况的时候，除非你说你就是在要没有硬件指令集支持的情况下做软件支持，否则的话你就尽可能打开更多的指令集，这样会更加贴近你的 pc 机器的实际情况，因为现代 x 86 计算机支持的指令集已经是非常多了。

* * *

相信大家看到这里，已经对 bochsrc 配置有了一定的了解。我上面讲述的配置并不完善，还有一些其他的配置，希望大家能够看英文的官方文档。如果你是一个初学者，可以照着我的描述写自己的配置。

```cobol
megs: 2048  #设置插件plugin_ctrl :unmapped=1, biosdev=1, speaker=1, extfpuirq=1, parallel=1, serial=1, iodebug=1 #bochs调试选项config_interface :textconfigdisplay_library: x  #设置ROM和VGA模拟romimage :file="/usr/share/bochs/BIOS-bochs-latest"vgaromimage:file="/usr/share/bochs/VGABIOS-lgpl-latest"  #设置软盘启动 #boot : floppy #floppy_bootsig_check :disabled=0 #floppya :type=1_44,1_44="./tools/boot. img", status=inserted, write_protected=0 #3 .5 英寸高密度软盘  #设置硬盘启动boot : diskata 0:enabled=1, ioaddr 1=0 x 1 f 0, ioaddr 2=0 x 3 f 0, irq=14 ata 0-master:type=disk, path="./tools/boot. img", mode="flat", translation=lba  #主盘ata0-slave :type=none   ata 1:enabled=1, ioaddr 1=0 x 170, ioaddr 2=0 x 370, irq=15 ata 1-master:type=noneata 1-slave:type=disk, path="./tools/hd 60 M. img", mode="flat", translation=lba  ata 2:enabled=0 ata 3:enabled=0 pci:enabled=1, chipset=i 440 fxvga:extension=cirrus, extension=vbe, update_freq=60, realtime=1   cpu: count=1:4:2, ips=10000000, quantum=16, model=tigerlake, reset_on_triple_fault=1, cpuid_limit_winnt=0, ignore_bad_msrs=1, mwait_is_nop=0, msrs="msrs. def" cpuid: x 86_64=1, level=6, mmx=1, sep=1, aes=1, movbe=1, xsave=1, apic=x 2 apic, sha=1, adx=1, xsaveopt=1, avx_f 16 c=1, avx_fma=1, bmi=bmi 2,1 g_pages=1, pcid=1, fsgsbase=1, smep=1, smap=1, mwait=1, vmx=1, svm=1 cpuid: family=6, model=0 x 1 a, stepping=5, vendor_string="GenuineIntel", brand_string="11 th Gen Intel (R) Core (TM) i 5-1135 G 7 (TigerLake)"  print_timestamps: enabled=0 debugger_log: -magic_break: enabled=0 port_e 9_hack: enabled=0 private_colormap: enabled=0 clock: sync=none, time 0=local, rtc_sync=0# no cmosimage# no loaderlog: -logprefix: %t%e%ddebug: action=ignoreinfo: action=reporterror: action=reportpanic: action=ask  keyboard: type=mf, serial_delay=250, paste_delay=100000, user_shortcut=nonekeyboard: user_shortcut=ctrl-alt-del mouse: type=ps 2, enabled=1, toggle=ctrl+mbutton  speaker: enabled=1, mode=soundsb 16:midimode=2, midifile=output. mid, wavemode=3, wavefile=output. wav, dmatimer=900000 sound: waveoutdrv=sdl, waveindrv=alsa,, waveout=dunmy parport 1: enabled=1, file=noneparport 2: enabled=0 com 1: enabled=1, mode=nullcom 2: enabled=0 com 3: enabled=0 com 4: enabled=0 clock:sync=none, rtc_sync=0, time 0=localvoodoo:enable=1, model=voodoo 1 #gdbstub : enabled=1, port=1234, text_base=0, data_base=0, bss_base=0 #该配置在使用gdb调试的时候使用 , port=1234 指明 gdb 调试的端口号 #你在另一个终端执行gdb命令 ，然后执行 target remote : 1234 就可以连接到 bochs #如果你使用bochs自带的调试器 ，就不能在配置里出现gdbstub的配置（二者是水火不容）
```

我这里给出我的完整的配置，大家可以在它的基础上修修改改，符合自己的实际情况就好。

其中还有一个参数叫 voodoo，这是 Bochs 模拟器支持的 Voodoo 图形卡的仿真。Voodoo 图形卡是 3 dfx 公司在 90 年代推出的一系列著名的视频卡，主要用于加速 3 D 计算机图形的渲染。按照 Bochs 官方文档的说法，Bochs 提供了几种型号的图形卡的仿真支持：

1.  Voodoo 1
2.  Voodoo 2
3.  Banshee
4.  Voodoo 3

我在配置文件里写的是 Voodoo 1, 因为它已经完整的支持了，实际上你可以改成 Voodoo 2, 文档里说这个模型的支持已经基本完成，可以是用了。其他两张卡还在建设中。你可以认为：Bochs 模拟器提供的 VBE 显示缓冲区的地址为 0 xe 0000000 这个地方，Bochs 会把这个区域里的数据映射到“显卡”的显存里，你只需要往这个地方写入数据，就会在屏幕上相应的位置显示像素点。

* * *

五、Bochs 调试内核
-----------

在编写好配置文件后，就可以执行 bochs -f /bochsrc 来启动 bochs, 当然你可以把这一步写近 Makefile 或者 Shell 脚本里。

我就介绍一下命令行调试内核的方法，Bochs 本身是可以用图形界面调试的，只是我用不习惯 gui, 还是命令行原汁原味好一点。我会在这个章节演示一下我调试内核的场景。

请注意：如果你想调试内核，那么你在执行./configure 的时候必须开启 Bochs 内置的调试器！

 ./configure --enable-debugger

![](https://i-blog.csdnimg.cn/blog_migrate/563423078f5ef998e34ed6a5e4160437.png)

如果 Bochs 运行正常的话会进入这样一个界面。

对于我们来说，直接使用 6 开始调试就可以了。如果你不想调试，你可以使用 7 退出 bochs.

![](https://i-blog.csdnimg.cn/blog_migrate/98c9551ebcbd2763f9f435b5385f7e06.png)

这就是 Bochs 刚开启时候的界面。左上角是 Bochs 的 logo, 右上角有一个 x 按钮，你点击它是不能够关闭 Bochs 的，因为你是在终端里打开，你想关闭 Bochs 就只能在终端里与 Bochs 进行交互的时候，使用 q 命令才能正常关闭 Bochs, 除此之外，你还可以使用我下面将要介绍的 Power 按钮关闭 Bochs.

第二行有一些列的按钮，我挨个介绍他们的作用：

1.  软盘按钮：切换软盘介质的状态 (inserted/ejected) 有两个软盘按钮，左边那个控制 floopya, 右边那个控制 floopyb；
2.  CD-ROM 按钮：切换第一个 CD-ROM 驱动器的介质状态；
3.  鼠标按钮：是否捕获主机系统的鼠标（这个我之前着重讲过了）；
4.  用户按钮（USER）：向客户操作系统（模拟器里运行的系统）发送预定义的键盘快捷键；
5.  复制按钮（Copy）：将文本模式屏幕上的文本导出到你的剪贴板；
6.  粘贴按钮（Paste）：将你的主机系统剪贴板里的东西作为模拟按键输入到虚拟机里
7.  快照按钮（Snapshot）：保存 Bochs 屏幕的快照，就是截图的意思；
8.  配置按钮（CONFIG）：停止模拟并启动运行时配置
9.  重置按钮（Reset）：触发模拟的硬件重置
10.  挂起按钮（Suspend）：将当前模拟状态保存到磁盘，稍后可以使用 bochs -r 命令恢复
11.  电源按钮（Power）：停止模拟并退出 Bochs

大家不用专门去记忆这些按钮是干嘛的，它上面写着英文，理解一下就好。

我这里着重再讲一下这个配置按钮，就是一个锤子一个扳手、下面写着 CONFIG 的那个按钮，你在 Bochs 正在运行的时候点击这个按钮，就会进入如图所示的界面。

![](https://i-blog.csdnimg.cn/blog_migrate/621d110d6101c7c1d48d723e17865765.png)

你可以在这个界面里更改软盘或 CD-ROM 的镜像或设备、调整日志选项、USB 选项等。

![](https://i-blog.csdnimg.cn/blog_migrate/465e25a18719dfcf40116f4adcf3ca93.png)

大家可以看到，Bochs 提示了一些“reset”的初始化信息，并且默认使用的 CPU 核心是 CPU 0 (Switching to CPU 0)，可以通过命令去设置查看当前选择的 CPU 信息，这个我以后再说。

因为我现在开启了 4 核心 8 线程，因此可以看到 8 条一模一样的信息：

```cobol
(0) [0 x 0000 fffffff 0] f 000: fff 0 (unk. ctxt): jmpf 0 xf 000: e 05 b          ; ea 5 be 000 f 0
```

这是刚启动时候的 CPU 地址，此时 BIOS 还没有开始执行自检的代码，也就是开机的时候，执行地址位于 0 xffff 0 这个地方（CS=0 xf 000, IP=fff 0），相信大家学过 8086 汇编语言的都知道这个。

它执行的第一行代码就是 jmpf 0 xf 000: e 05 b ,这个地方位于主板上的 ROM 映射到内存的区域，跳过去之后执行一些 BIOS 自检代码。自检完成之后最终会跳到 0 x 7 c 00 这个 MBR 地址，也就是你设置的磁盘的 0 磁头 0 柱面 1 扇区这个地方，ROM 里的代码会自动把磁盘上的该扇区放置到 0 x 7 c 00 - 0 x 7 dff (共 512 字节）。

### 1、执行控制命令

这也是 Bochs 中最常用的命令，Bochs 模拟器刚开启的时候是一条你的代码也没有执行的，甚至连你的 MBR 都还没有加载到内存中呢！  
 

#### ①执行到底

c

cont

continue

短的是简写，方便调试

意思就是 Bochs 一直往后面执行，像真的 CPU 一样，不停地执行机器码，直到遇到**断点**(实际上我们的调试就是基于这个，让 ip 在执行到错误的指令或者访问到错误的数据之前停下来，然后反汇编查看是否有什么错误)，或者遇到悬停指令（jmp $ / jmp .），它才会停下来。如果遇到重大错误（不可能恢复的那种），Bochs 会直接重启，然后会和你执行 c 命令之前一样的状态，等待着你的控制和调试。

这里我推荐大家记忆的时候记全名，然后实际调试的时候，用缩写。

#### ②单步执行

s \[count\]

step \[count\]

执行 count 条指令，这个 count 默认为 1.

注意这个\[\]是表示可选参数的意思，你调试的时候不要写\[\]上去。

s \[cpu\] \[count\]

step \[cpu\] \[count\]

这个单步调试还可以指定 CPU, 当你开启 SMP 以后，那么你就有多个 CPU 执行单元，你可以选择其中一个执行单元执行 count 条指令

s all \[count\]

s all \[count\]

你当前的所有 CPU 执行单元同时执行 count 条指令

两个重要快捷键：

Ctrl+C : 停止执行，控制权交还给用户。

Ctrl+D：在停止执行的状态退出 Bochs, 相当于 q、quit、exit 命令，它们的作用是一样的，都是正常退出 Bochs，如果你是以不正常的方法退出 Bochs, 则会留下一些 lock 文件保护你的硬盘映像什么的。

#### ③打个断点

打断点可以说是整个调试过程里面，最重要的一部分了，

pbreak addr

pb addr

break addr

b addr

上面这四条指令的含义是一样的，就是在物理地址 addr 这块地方设置一个断点，这里的 p 的含义就是 physical，我们通常来说使用这条指令就足够了。这里注意一下，因为内存地址我们常用 16 进制来表示，所以你在写这个 addr 的时候假如你是 16 进制，请你加上 0 x 开头，否则就是 10 进制的地址了。如果你要用 8 进制作为地址那也可以，使用 0 开头。

>         hexidecimal:    0 xcdef 0123
>         decimal:        123456789
>         octal:          01234567

此外，由于 x 86 架构的分段特性，如果仅使用物理地址来指明你要打的断点的内存地址的话，也许是不太方便的，那么 Bochs 模拟器非常贴心的给出了一些其他适配与 Intel 分段机制的打断点的方法。

vbreak reg:offset

vb reg:offset

想必大家也看出来这么做的意图了，reg 指定断点所在位置的的段地址，offset 指定偏移量，如果你在实模式下调试的话，这么做会方便很多。不过我测试下来，b 指令好像也能接收这样的参数。

查看断点：

info break

![](https://i-blog.csdnimg.cn/blog_migrate/53affa4524a6a1527a98069861c076ae.png)

我打的断点会全部被记录下来，并且默认是开启状态，这个是否开启你也可以进行设置。

```typescript
  bpe    n                    开启断点  bpd    n                    关闭断点  delete n                    删除断点  del    n                    缩写  d      n                    更简单的缩写
```

![](https://i-blog.csdnimg.cn/blog_migrate/f60ed1c73d7dfbd343165c7ce9ef9c7c.png)

除了虚拟地址和物理地址之外，还有一种线性地址打断点的方式，这个不太常用啊，我这里就不说了。

以上是代码执行到的断点，也就是只有你的 cs: ip 执行到了这个地址才会中断，假如没有执行到，那么这个断点其实就是白费的，不起作用的。

* * *

下面是数据访问的断点，或者更确切来说是**监视点**

```perl
watch read addrwatch r    addr
```

就是在 addr 这个内存地址处插入一个监视点，当有代码去访问、去读这块内存地址的时候，会中断它的操作。

那么也有写监视点

```perl
watch write addrwatch w     addr
```

![](https://i-blog.csdnimg.cn/blog_migrate/de9a9086ad37936190314bd77ed65cb4.png)

![](https://i-blog.csdnimg.cn/blog_migrate/6c94df7ee672fe3f3562b302e2eb9dc9.png)

大家可以看到，当我读写入数据到这块内存地址的时候，果然中断了。

```undefined
watch     查看当前所有已设置的监视点 unwatch   取消所有监视点 unwatch addr 取消执行地址的监视点
```

```kotlin
watch stop    当监视点被访问的时候中断掉 watch continue  当监视点被访问的时候继续模拟，什么也不做
```

#### ④查看信息

当你已经在断点处中断的时候，你需要查看当前的实时信息，从而进行调试。这里的信息可以是寄存器的值、内存里的数据、代码段里的代码（当前这是反汇编得出来的）。

##### 1、查看寄存器的值

Bochs 真的可以查看好多好多信息啊，大家可以则其所需，挑选你需要查看的寄存器查看。在多核心开启的情况下是有多组寄存器的。

| 命令                     | 功能描述                           |
| ---------------------- | ------------------------------ |
| `r/reg/regs/registers` | 列出 CPU 的整数寄存器及其当前值。            |
| `fp /fpu`              | 列出所有浮点处理单元寄存器的内容。              |
| `mmx`                  | 列出所有 MMX 寄存器的内容。               |
| `sse/xmm`              | 列出所有流式 SIMD 扩展（SSE）寄存器的内容。     |
| `ymm/zmm`              | 列出所有高级向量扩展（AVX）寄存器的内容。         |
| `amx/tile n`           | 显示 AMX 技术状态和 TILE 寄存器的内容。      |
| `sreg`                 | 列出所有段寄存器（如 CS, DS 等）及其内容。      |
| `dreg`                 | 列出所有调试寄存器（如 DR 0, DR 1 等）及其内容。 |
| `creg`                 | 列出所有控制寄存器（如 CR 0, CR 3 等）及其内容。 |

这里面对重要的应该就是 r 和 sreg, 查看通用寄存器信息和段寄存器信息。

比如 creg 指令，在查看缺页中断的时候你就可以用来查看 cr 2 寄存器的值

| 命令 | 功能描述 |
| --- | --- |
| `info cpu` | 列出所有 CPU 寄存器及其内容。 |
| `info eflags` | 显示解码后的 EFLAGS 寄存器内容。 |
| `info break` | 显示当前断点的状态信息。 |
| `info tab` | 显示页表地址转换信息。 |
| `info idt` | 显示中断描述符表（IDT）的内容。 |
| `info gdt` | 显示全局描述符表（GDT）的内容。 |
| `info ldt` | 显示局部描述符表（LDT）的内容。 |
| `info device` | 显示指定设备的状态。 |

以上是一些 info 类的指令，它用来查看特殊寄存器的信息。从这里我们不难看出，Bochs 对于 x 86 体系结构相关的信息查看是更加全面和底层的，Bochs 的开发者对于 x 86 体系结构是非常熟悉了解的，所以对于手写内核的人来说，Bochs 是一个更加适合**入门**的工具，对 x 86 体系结构的学习更加好。但是它的缺点就是当你用 c 语言写内核的时候，它无法像 gdb 那样使用 gcc -g 添加的额外调试信息来帮助调试 c 代码。所以**当你已经熟悉 x 86 体系结构的时候，当你已经脱离 MBR 和 loader 进入 kernel 的时候，你不妨就可以替换成 Qemu+gdb**, 这样调试 c 代码会更加方便。否则的话你只能在 c 语言写的内核里自己构建更加强大的调试和日志功能，使得你在代码出问题的时候方便查探到是哪一个内存地址、哪一条机器指令导致的出错。

Bochs 除了能查看寄存器的信息，甚至还可以修改某些寄存器的值。注意：你只能用来修改通用寄存器和 ip 寄存器，其他寄存器的值你不能修改。

```cobol
set eax = 2+2/2 set esi = 2*eax+ebx
```

注意寄存器名称之后需要有一个空格来分隔，你可以直接写一个立即数上去，也可以使用别的寄存器的值参与计算

```cobol
<bochs:1> rCPU 0:rax: 00000000_00000000 rbx: 00000000_00000000 rcx: 00000000_00000000 rdx: 00000000_00000000 rsp: 00000000_00000000 rbp: 00000000_00000000 rsi: 00000000_00000000 rdi: 00000000_00000000 r 8 : 00000000_00000000 r 9 : 00000000_00000000 r 10: 00000000_00000000 r 11: 00000000_00000000 r 12: 00000000_00000000 r 13: 00000000_00000000 r 14: 00000000_00000000 r 15: 00000000_00000000 rip: 00000000_0000 fff 0 eflags: 0 x 00000002: id vip vif ac vm rf nt IOPL=0 of df if tf sf zf af pf cf<bochs:2> set eax = 0 x 1234<bochs:3> set ebx = 0 xabcd<bochs:4> set ecx = eax+ebx<bochs:5> rCPU 0:rax: 00000000_00001234 rbx: 00000000_0000 abcdrcx: 00000000_0000 be 01 rdx: 00000000_00000000 rsp: 00000000_00000000 rbp: 00000000_00000000 rsi: 00000000_00000000 rdi: 00000000_00000000 r 8 : 00000000_00000000 r 9 : 00000000_00000000 r 10: 00000000_00000000 r 11: 00000000_00000000 r 12: 00000000_00000000 r 13: 00000000_00000000 r 14: 00000000_00000000 r 15: 00000000_00000000 rip: 00000000_0000 fff 0 eflags: 0 x 00000002: id vip vif ac vm rf nt IOPL=0 of df if tf sf zf af pf cf<bochs:6> 
```

怎么样, 是不是非常有意思？可以在 Bochs 的调试窗口修改寄存器的值。当然，你也可以修改 rip 的值，但是修改之前你要小心，要是 rip 指向了你不知道的地址，那么出错是很正常的，你可以在内存的某个固定的地方写入一个调试函数，然后一旦出现什么错误，你就可以在 Bochs 里修改 rip 是它进入这个函数里，然后打印你需要的信息。

##### 2、查看内存里的数据

```bash
xp /nuf addr    查看内存物理地址内容 x /nuf addr     查看内存线性地址内容
```

 其中的 nuf 指的是：

*   **n（数量）**：指定要显示的单位数量。
*   **u（单位大小）**：
    *   `b`：字节
    *   `h`：半字（2 字节）
    *   `w`：字（4 字节）
    *   `g`：巨字（8 字节）
*   **f（格式）**：
    *   `x`：十六进制
    *   `d`：十进制
    *   `u`：无符号十进制
    *   `o`：八进制
    *   `t`：二进制

比如我想看看我的 MBR 的二进制数据

```cobol
xp /256 hx 0 x 7 c 00
```

![](https://i-blog.csdnimg.cn/blog_migrate/b21f24fb6170064b7715ff1121081a65.png)

那么我就可以查看物理地址从 0 x 7 c 00 开始 256 个半字（总共 512 B），以 16 进制的形式打印。

通常来说，我们只需要查看内存里的内容已经能够满足需求了，但是 Bochs 还有更多的操作。

```cobol
setpmem 0 x 7 dfe 2 0 x 55 aa
```

使用 setpmem 指令可以修改内存里的值，比如说我这里要修改 0 x 7 dfe 这个内存地址的 2 B, 交换 0 x 55 和 0 xaa 的顺序。

![](https://i-blog.csdnimg.cn/blog_migrate/1fdd5b8c3764c0a231cd576966996069.png)

内存地址里的值修改成功! 我尝试了一下，在交换了 0 x 55 和 0 xaa 的顺序之后代码还是正常运行的，看来检测 OBR 是否为 OBR 的过程是在加载 MBR 的过程中做的，也就是 BIOS 自己的代码。

转储指定内存地址的数据到文件

```cobol
writemem "mbr. bin" 0 x 7 c 00 512
```

这就是把 0 x 7 c 00 这个内存地址开始 512 字节的部分存储到指定的文件里，这里我设置成了 mbr. bin，请注意文件名一定要用双引号。

![](https://i-blog.csdnimg.cn/blog_migrate/7dbb788090f4a5c4f29b9d559eccd4ca.png)

这确实是我写的 mbr

```csharp
loadmem "filename" addr
```

把文件里的数据加载到 addr 指定的内存里。**有了这个工具，你就可以暂时不从文件系统里读出你的 loader 和 kernel 而是直接写入到内存里，然后用 jmp 指令跳过去。**

```undefined
deref addr deep
```

进行多层解引用操作。例如，`deref rax 3` 表示解引用寄存器 `rax` 三次。

```cobol
 crc  addr 1  addr 2 
```

`crc addr 1 addr 2`：计算从 `addr 1` 到 `addr 2` 的物理内存范围内的 CRC 32 校验值。

上面这两条指令是在是不常用到，大家了解一下就好了。

##### 3、反汇编

在正式介绍反汇编之前，有两条指令需要大家知道一下

```vbnet
trace ontrace off
```

trace 是追踪的意思，当你每执行一条指令之后都会被记录下来，在关闭的情况下，你使用 c 执行到底的话，它是不会记录反汇编的结果的。

```vbnet
trace-mem ontrace-men off
```

在内存追踪模式开启的情况下，程序对内存的每一次访问都会被记录和显示，包括读取和写入操作。这对于分析程序如何与内存交互、诊断内存访问错误非常有帮助。

在你的程序加载和运行之前，你可以进行静态的反汇编，即使用 objdump 等工具进行反汇编。我相信每一位内核开发者这个工具都是不陌生的，我这里再强调一下 --- objdump 确实不可或缺。

一下是 objdump 命令的参数

| 选项 | 长格式 | 描述 |
| --- | --- | --- |
| `-a` | `--archive-headers` | 显示归档文件的头信息。 |
| `-b` | `--target=bfdname` | 指定目标文件的二进制格式。 |
| `-C` | `--demangle[=style]` | 解析低级别符号名称到用户级别名称。 |
| `-d` | `--disassemble` | 只反汇编可能包含指令的段。 |
| `-D` | `--disassemble-all` | 反汇编所有非空非 BSS 段。（重要） |
| `-f` | `--file-headers` | 显示文件的头部信息。 |
| `-g` | `--debugging` | 显示调试信息。 |
| `-h` | `--section-headers` 或 `--headers` | 显示节头信息。 |
| `-i` | `--info` | 显示所有支持的架构和对象格式列表。 |
| `-l` | `--line-numbers` | 在反汇编输出中显示源代码行号。 |
| `-S` | `--source` | 显示源代码。 |
| `-t` | `--syms` | 显示符号表。 |
| `-x` | `--all-headers` | 显示所有头信息，包括符号表和重定位条目。 |
| `-M` | `--disassembler-options` | 为反汇编器指定目标特定的信息。 |

* * *

下面我开始介绍 Bochs 自带调试器的反汇编功能：

u start end

反汇编一段内存，从 start 开始到 end 结束。

```cobol
<bochs:2> u 0 x 100000 0 x 1000200000000000100000: (                    ): mov ax, 0 x 0010            ; 66 b 810000000000000100004: (                    ): mov ds, ax                ; 8 ed 80000000000100006: (                    ): mov es, ax                ; 8 ec 00000000000100008: (                    ): mov fs, ax                ; 8 ee 0000000000010000 a: (                    ): mov ss, ax                ; 8 ed 0000000000010000 c: (                    ): mov esp, 0 x 00007 e 00       ; bc 007 e 00000000000000100011: (                    ): lgdt ds:[rip+96176]       ; 0 f 0115 b 07701000000000000100018: (                    ): lidt ds:[rip+100275]      ; 0 f 011 db 3870100000000000010001 f: (                    ): mov ax, 0 x 0010            ; 66 b 81000
```

能够在 Bochs 的调试器界面看到自己写的汇编代码，是不是很感动，很开心？

反汇编更多的时候是用在调试的时候，当你出错的时候你去探测出错的代码的位置，然后反汇编这段地址，看是否是某一条指令的错误或者是反汇编的结果和你的代码的结果不一样。因为 gcc 编译器可能会指令重排列，它不会严格按照你指示的顺序进行汇编，而是会有自己的优化。

x 86 架构的指令是非定长指令，也就是每一条指令的机器码的长度不是固定的，这和 risc-v 等定长指令指令集全然不同，risc-v 指令集你可以通过机器码反推出对应的汇编指令，但是 x 86 平台你想这么做的话，难度可不是一般的大。因此在 x 86 架构上调试，**程序员是相当相当依赖于反汇编器**的，可以说你会不会 x 86 架构，就看你反汇编调试的能力是否足够强。

##### 4、多核 CPU

Bochs 模拟器是支持硬件的 SMP 功能的，就看你怎么设置了。多核技术就是把多个 CPU 核心塞进一个 CPU 里面，而超线程技术是每个处理器核心能够集成两个逻辑处理单元（通常来说是两个）。

实际上每个逻辑核心都有一套自己的寄存器，所以 Bochs 它不是只能查看一套寄存器的值，而是每一套寄存器的值都能够查看、能够设置。

```bash
set $cpu=n
```

我们使用这样一条指令来设置你当前选择的那个核心，CPU 从 0 开始索引。

> <bochs:2> r  
> CPU 0:  
> rax: 00000000\_00000000  
> rbx: 00000000\_00000000  
> rcx: 00000000\_00000022  
> rdx: 00000000\_00000001  
> rsp: ffff 8000\_0013 fff 8  
> rbp: ffff 8000\_0013 fff 8  
> rsi: 00000000\_0000000 a  
> rdi: 00000000\_00000010  
> r 8 : 00000000\_0000 ff 00  
> r 9 : 00000000\_00000000  
> r 10: ffff 8000\_00104 f 53  
> r 11: 00000000\_00080000  
> r 12: 00000000\_00000000  
> r 13: 00000000\_00000000  
> r 14: 00000000\_00000000  
> r 15: 00000000\_00000000  
> rip: ffff 8000\_00104022  
> eflags: 0 x 00000246: id vip vif ac vm rf nt IOPL=0 of df IF tf sf ZF af PF cf  
> <bochs:3> set $cpu=1  
> Switching to CPU 1  
> <bochs:4> r  
> CPU 1:  
> rax: 00000000\_00000001  
> rbx: 00000000\_00000000  
> rcx: ffff 8000\_001250 e 0  
> rdx: ffffffff\_ffffffff  
> rsp: ffff 8000\_0160 fec 8  
> rbp: ffff 8000\_0160 fff 8  
> rsi: ffff 8000\_00142500  
> rdi: ffff 8000\_00000000  
> r 8 : 00000000\_00080000  
> r 9 : 00000000\_00000000  
> r 10: 00000000\_00000000  
> r 11: 00000000\_00000000  
> r 12: 00000000\_00000000  
> r 13: 00000000\_00000000  
> r 14: 00000000\_00000000  
> r 15: 00000000\_00000000  
> rip: ffff 8000\_00113 b 1 f  
> eflags: 0 x 00000293: id vip vif ac vm rf nt IOPL=0 of df IF tf SF zf AF pf CF

在多核调试的过程中，其实本质和单核调试差不多，就是你在查看寄存器信息之前需要找到对应的 CPU 核心，而不是直接一个 r 指令，那样只能查看到 CPU 0 的信息。

#### ⑤通用设置指令

这些指令不是在你调试的时候用的，而是在你正式开始调试前，你要告诉 Bochs，你想要什么样的体验。

| 命令 | 功能描述 |
| --- | --- |
| **show** | 显示当前的 `show` 模式设置，即当前启用了哪些符号信息显示。 |
| **show mode** | 切换处理器模式切换事件的显示。启用后，每当处理器切换模式时，Bochs 将显示相关信息。 |
| **show int** | 切换中断事件的显示。启用后，每当发生中断时，Bochs 将显示相关信息。 |
| **show call** | 切换调用指令事件的显示。启用后，每当执行调用指令时，Bochs 将显示相关信息。 |
| **show ret** | 切换从中断返回指令（iret）事件的显示。启用后，每当执行 iret 指令时，Bochs 将显示相关信息。 |
| **show off** | 关闭所有符号信息的显示。此命令将禁用上述所有事件的显示。 |
| **show dbg-all** | 打开所有符号信息显示标志。此命令启用所有类型事件（模式、中断、调用、返回）的显示。 |
| **show dbg-none** | 关闭所有符号信息显示标志。此命令禁用所有类型事件的显示。 |

show int 的结果

![](https://i-blog.csdnimg.cn/blog_migrate/8daa81be75cf489231875007d17b7edf.png)

也就是每一次产生中断的时候都会输出日志，告诉程序员你的 CPU 现在产生中断了，我的内核这里不断地产生时钟中断，每触发一次，就会告诉我一下。这样的做法相当于是触发器-回调函数了，每次触发就会执行对应的函数打印日志。Bochs 还具备可定制化的检测和回调，这里我只是说明一下可以这么做，具体怎么做请查看官方文档。

#### ⑥其他指令

| 命令 | 功能描述 |
| --- | --- |
| **ptime** | 打印自模拟开始以来的当前时间（时钟滴答数）。 |
| **sb delta** | 在未来插入一个以 "delta" 指令为时间间隔的时间断点（"delta" 是一个跟随 "L" 的 64 位整数，例如 1000 L）。 |
| **sba time** | 在指定的 "time" 处插入一个时间断点（"time" 是一个跟随 "L" 的 64 位整数，例如 1000 L）。 |
| **print-stack \[num words\]** | 打印栈顶的数个 16 位字，"num words" 默认为 16。仅在受保护模式下且栈段的基地址为零时可靠工作。 |
| **print-string addr** | 从一个线性地址打印一个以 null 结束的字符串。 |
| **bt \[num\_entries\]** | 打印回溯跟踪。 |
| **source file** | 使调试器执行一个脚本文件。 |
| **addlyt file** | 每次执行停止时，使调试器执行一个脚本文件。 |

六、Bochs 已实现的功能和未来的计划
-------------------

这一部分其实已经不是 Bochs 模拟器的使用教程了，不过既然官方文档讲述了这些内容，我这里就就放一些链接在这里，大家感兴趣的可以去了解一下。

[Bochs 已实现的功能与描述](https://bochs.sourceforge.io/doc/docbook/user/features.html#AEN80 "Bochs 已实现的功能与描述")

[Bochs 支持的平台](https://bochs.sourceforge.io/doc/docbook/user/supported-platforms.html#AEN232 "Bochs 支持的平台")

[Bochs 模拟出来的 BIOS](https://bochs.sourceforge.io/doc/docbook/user/bios-tips.html#AEN4867 "Bochs 模拟出来的 BIOS")

[Bochs 开发者手册](https://bochs.sourceforge.io/doc/docbook/development/index.html "Bochs 开发者手册")

本文转自 <https://blog.csdn.net/qq_61653333/article/details/136962598>，如有侵权，请联系删除。