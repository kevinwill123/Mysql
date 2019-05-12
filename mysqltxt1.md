## Mysql学习任务1
#### mysql软件安装及数据库基础

- 安装软件及服务器设置：使用的是brew安装的
- 下载了navicat premium的破解版，并与上面的mysql数据库进行了连接和操作，测试可行
- 数据库的基础概念
 - 数据库的定义：保存有组织的数据的容器（通常是一个文件或一组文件）
 - 关系型数据库：依据关系模型来创建的数据库。其中关系模型就是“一对一，一对多，多对多”等关系模型，关系模型就是指二维表格模型，因此一个关系型数据库就是由二维表及其之间的联系组成的一个数据组织。与之相对的就是非关系型数据库，菲关系型模型有但是不限于列模型（存储的数据是一列一列的，便于索引），键值对模型（如字面含义），文档类模型（类似于键值对模型）等。
 - 二维表：在关系模型中，数据结构表示为一个二维表，一个关系就是一个二维表（但是不是任意一个二维表都能表示一个关系），二维表名就是关系名。表中的第一行通常称为属性名。
 - 行：表中的一个记录。
 - 列：表中的一个字段，所有的表都是由一个或者多个列组成的。
 - 主键：一列（或者一组列），其值能够唯一标志表中的每一行。
 - 外键：表的外键是另一个表的主键，外键可以有重复的，可以是空值。是用来与其他表建立联系用的，一个表可以有多个外键。

#### Mysql基础-1

- 导入示例数据库成功

```
>mysql -u root -p
>CREATE DATABASE IF NOT EXISTS yiibaidb DEFAULT CHARSET utf8 COLLATE utf8_general_ci;
>use yiibaidb;
>source 这里我们直接拖动文件在此就可以自动添加文件路径

>show databases;
>show tables;
>desc <tablename>;
```
- SQL：structured query language 模块化的查询语言，sql是一种专门用来与数据库沟通的语言。
- mysql：数据库管理的软件。
- 查询语句：SELECT FROM
 - 去重语句：SELECT DISTINCT ... FROM <TABLENAME>
 - 前N个语句：SELECT * FROM <TABLENAME> LIMIT m,n 从第m条记录到第n条记录
 - CASE...END：sql里面的if条件语句，一般的使用 CASE WHEN CONDITION1 THEN RESULT1 WHEN CONDITION2 THEN RESULT2 ELSE RESULT3 END 上面的句子就是：if 当con1条件满足的时候 返回res1，当con2满足的时候，返回res2，else 否则返回 res3. END来结束这段if语句。
- 筛选语句 WHERE
 - 运算符：加 + 减 - 乘 * 除 / 商 DIV 取余 MOD
 - 通配符：在where语句中结合like使用 _ : 匹配任意一个字符，% ：匹配0~n个字符 n大于等于1；select * from <tablename> where ... like '____c'; select * from <tablename> where ... like 'a%'
 - 操作符：and or not xor
- 分组语句 GROUP BY
 - 聚集函数：AVG() 求平均值；COUNT() 统计行的数量；MAX() 求最大值；MIN() 求最小值；SUM() 求累加和； 默认情况下 忽略列值为null的行，不参与计算
 - HAVING子句：通常与GROUP BY子句一起使用,HAVING+过滤条件，（1）having是在分组之后对数据尽心过滤，where在分组之前对数据进行过滤（2）having后面可以使用聚合函数，where后面不可以使用聚合函数
- 排序语言 ORDER BY
 - 正序：asc
 - 逆序：desc
 - order by age desc, id asc 按照年龄降序排序，如果年龄相等，则按照编号进行升序排序
- 函数
 - 时间函数：ADDDATE(d,n),ADDTIME(t,n),CURDATE(),CURRENT_DATE(),CURRENT_TIME(),CURRENT_TIMESTAMP(),CURTIME(),DATE(),DATEDIFF(d1,d2),DATE_ADD(d,INTERVAL exprtype),DATE_FORMAT(d,f)...
 - 数值函数：ABS(X)...
 - 字符串函数：CHAR_LENGTH(S),CONCAT(S1,S2,...,SN),LOWER(S),UPPER(S)...
- SQL注释：# 单行注释， -- 单行注释， /* ... */ 多行注释

#### 作业
1.项目1

```
create table email (
Id int not null primary key;
Email varchar(255)
);
insert into email value('1','a@b,com');
insert into email value('2','c@d,com');
insert into email value('3','a@b,com');

select Email from email group by Email;
```

2.项目2

```
create table World (
name varchar(50) not null;
continent varchar(50) not null;
area int not null;
population int not null;
gdp int not null
);

INSERT INTO World
  VALUES('Afghanistan','Asia',652230,25500100,20343000);
INSERT INTO World 
  VALUES('Albania','Europe',28748,2831741,12960000);
INSERT INTO World 
  VALUES('Algeria','Africa',2381741,37100000,188681000);
INSERT INTO World
  VALUES('Andorra','Europe',468,78115,3712000);
INSERT INTO World
  VALUES('Angola','Africa',1246700,20609294,100990000);
  
select name, population, area from World where area > 3000000 or population > 25000000 and gdp > 20000000;
```  
 
