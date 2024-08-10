---
title: ctfhub-web-http基础认证
date: 2024-07-17 14:49:27
tags: 
- ctfhub
- web
catogories: ctfhub
---
## 介绍
[http基础认证介绍](https://zh.wikipedia.org/wiki/HTTP%E5%9F%BA%E6%9C%AC%E8%AE%A4%E8%AF%81)
## 题解

> 题目已经给了密码表

- 本题爆破解决

在使用intruder获得密码的payloads之后，拦下来一个请求连接

- payloads 使用密码表
- payload rule 添加prefix `admin:`
- payload rule 添加encode `base64`
- 不需要使用urlEncode

打，发现一个响应码为200的就好