---
title: ctfhub_web_http_1
date: 2024-07-17 13:35:55
tags: 
- ctfhub
- web
categories: ctfhub
---

## 自定义请求头

### 题解1
> 使用python的request库，发送一个自定义的请求
``` python
import requests

def CTFHub(url, headers=None, params=None, data=None):
    """
    发送自定义HTTP请求方法 'CTFHUB' 到指定的URL，并返回响应。

    :param url: 请求的URL
    :param headers: 自定义HTTP头（默认是None）
    :param params: URL参数（默认是None）
    :param data: 请求体数据（默认是None）
    :return: 响应对象
    """
    method = 'CTFHUB'

    try:
        # 使用 requests.request 方法伪造自定义的请求方法
        response = requests.request(method, url, headers=headers, params=params, data=data)

        # 检查响应状态码
        if response.status_code == 200:
            print("Request was successful!")
        else:
            print(f"Request failed with status code: {response.status_code}")

        return response

    except requests.exceptions.RequestException as e:
        print(f"An error occurred: {e}")
        return None

# 示例用法
url = 'http://challenge-b8e57159e7124466.sandbox.ctfhub.com:10800/index.php'

# 发送自定义的CTFHUB请求
response = CTFHub(url)
if response:
    print(response.text)

```
#### 获得Flag

``` html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8"/>
    <title>CTFHub HTTP Method</title>
</head>
<body>

good job! ctfhub{72412434616ed2edddca4786}

</body>
</html>
```

### 题解2
> 使用curl命令
- 参考[https://cnblogs.com/duhuo/p/5695256.html](https://cnblogs.com/duhuo/p/5695256.html)

``` shell
curl -v -X CTFHUB http://challenge-b8e57159e7124466.sandbox.ctfhub.com:10800/index.php
```