---
title: dirsearch常用命令
date: 2024-07-17 15:05:32
tags:
  - ctf
categories: ctf
---

# dirsearch 常用命令

dirsearch 命令
---

## 指定网址

```
python dirsearch.py -u http://xxxx
```

## 指定网站语言

```
python dirsearch.py -u http://xxxx -e php
```

## 指定字典

```
python dirsearch.py -u http://xxxx -w
```

## 递归目录（子级也会被搜索）

```
python dirsearch.py -u http://xxxx -r
```

## 使用随机 UA

```
python dirsearch.py -u http://xxxx --random-agents 
```
