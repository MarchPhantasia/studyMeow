---
title: ctfhub-web-302jumpto
date: 2024-07-17 13:52:53
tags: 
- ctfhub
- web
categories: ctfhub
---

## 302跳转是什么
根据题目提示为HTTP临时重定向

**简单记录一下HTTP临时重定向是什么**

>HTTP重定向：服务器无法处理浏览器发送过来的请求（request），服务器告诉浏览器跳转到可以处理请求的url上。（浏览器会自动访问该URL地址，以至于用户无法分辨是否重定向了。） 
重定向的返回码3XX说明。Location响应首部包含了内容的新地址或是优选地址的URL。

状态码
- 301：在请求的URL已被移除时使用。响应的Location首部中应该包含资源现在所处的URL。 
- 302：与301状态码类似，但是，客户端应该使用Location首部给出的URL来零食定位资源，将来的请求仍然使用老的URL。

官方的比较简洁的说明：

- 301 redirect: 301 代表永久性转移(Permanently Moved)
- 302 redirect: 302 代表暂时性转移(Temporarily Moved )
尽量使用301跳转！301和302状态码都表示重定向，就是说浏览器在拿到服务器返回的这个状态码后会自动跳转到一个新的URL地址，这个地址可以从响应的Location首部中获取（用户看到的效果就是他输入的地址A瞬间变成了另一个地址B）——这是它们的共同点。他们的不同在于。301表示旧地址A的资源已经被永久地移除了（这个资源不可访问了），搜索引擎在抓取新内容的同时也将旧的网址交换为重定向之后的网址；302表示旧地址A的资源还在（仍然可以访问），这个重定向只是临时地从旧地址A跳转到地址B，搜索引擎会抓取新的内容而保存旧的网址。

HTTP中的重定向和请求转发的区别
转发是服务器行为，重定向是客户端行为。为什么这样说呢，这就要看两个动作的工作流程：

> 转发过程：客户浏览器发送http请求——》web服务器接受此请求——》调用内部的一个方法在容器内部完成请求处理和转发动作——》将目标资源发送给客户；

在这里，转发的路径必须是同一个web容器下的url，其不能转向到其他的web路径上去，中间传递的是自己的容器内的request。在客户浏览器路径栏显示的仍然是其第一次访问的路径，也就是说客户是感觉不到服务器做了转发的。转发行为是浏览器只做了一次访问请求。

重定向过程：客户浏览器发送http请求——》web服务器接受后发送302状态码响应及对应新的location给客户浏览器——》客户浏览器发现是302响应，则自动再发送一个新的http请求，请求url是新的location地址——》服务器根据此请求寻找资源并发送给客户。

在这里location可以重定向到任意URL，既然是浏览器重新发出了请求，则就没有什么request传递的概念了。在客户浏览器路径栏显示的是其重定向的路径，客户可以观察到地址的变化的。重定向行为是浏览器做了至少两次的访问请求的。

重定向，其实是两次request

> 第一次，客户端request   A,服务器响应，并response回来，告诉浏览器，你应该去B。这个时候IE可以看到地址变了，而且历史的回退按钮也亮了。重定向可以访问自己web应用以外的资源。在重定向的过程中，传输的信息会被丢失。
### 题解

能够看见有两个302的转发请求
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240717140551.png)

我不知道为什么啊，放到burpsuite的repeater发请求（往index.php发请求）就能拿到，我的curl命令似乎有些问题（curl命令在wsl下好用了。
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240717142541.png)


![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240717142642.png)