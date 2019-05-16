1.MySQL表数据类型

所允许的数据的类型，每个表列都有相应的数据类型，它限制（或允许）该列中存储的数据。

- 字符串数据类型
存储字符串，如名字、地址、电话号码、邮政编码等。有两种基本的字符串类型，分别为定长字符串和变长字符串。
定长字符串：CHARACTER(n) 固定长度为n
变长字符串：VARCHAR(n) 或CHARACTER VARYING(n) 最大长度为n
- 数值数据类型
FLOAT(p)：近似数值，尾数精度 p。一个采用以 10 为基数的指数计数法的浮点数。该类型的 size 参数由一个指定最小精度的单一数字组成。
FLOAT：近似数值，尾数精度 16。
INTEGER：整数值（没有小数点）。精度 10。
SMALLINT：整数值（没有小数点）。精度 5。
INTEGER(p)：	整数值（没有小数点）。精度 p。
BOOLEAN：存储 TRUE 或 FALSE 值。
BINARY(n)：	二进制串。固定长度 n。
BIT：单个二进制位数，或者为0或者为1，主要用于开/关标志。
- 日期和时间数据类型
DATE：日期值。
DATETIME（或TIMESTAMP）：日期时间值。
SMALLDATETIME：日期时间值，精确到分（无秒或者毫秒）。
TIME：时间值。
- 二进制数据类型

2.用SQL语句创建表

```
CREATE TABLE table_name
(
column_name1 data_type(size),
column_name2 data_type(size),
column_name3 data_type(size),
....
);
```
例子：
```
CREATE TABLE Persons
(
PersonID int,
LastName varchar(255),
FirstName varchar(255),
Address varchar(255),
City varchar(255)
);
```
语句解释     
列数据表达：列名+数据类型（长度大小）

带约束的写法：
```
CREATE TABLE table_name
(
column_name1 data_type(size) constraint_name,
column_name2 data_type(size) constraint_name,
column_name3 data_type(size) constraint_name,
....
);
```
NOT NULL：指示某列不能存储NULL值
UNIQUE：保证某列的每行必须有唯一的值
FOREIGN KEY：保证一个表中的数据匹配另一个表中的值得参照完整性
CHECK：保证列中的值符合指定的条件
DEFAULT：规定没有给列赋值时的默认值
PRIMARY KEY：NOT NULL和UNIQUE的结合。确保某列（或两个列多个列的结合）有唯一标识，有助于更容易更快速地找到表中的一个特定的记录

设定主键：PRIMARY KEY
 
3. 用SQL语句向表中添加数据

语句解释     
多种添加方式（指定列名；不指定列名） 
指定列名：
```
INSERT INTO table_name (column1,column2,column3,...)
VALUES (value1,value2,value3,...);
```
不指定列名：
```
INSERT INTO table_name
VALUES (value1,value2,value3,...);
```
是否指定列名就像关键字传参和位置传参的区别一样。

4. 用SQL语句删除表

语句解释     
DELETE：用于删除表中的记录

删除表中的行：
```
DELETE FROM table_name
WHERE some_column=some_value;
```     
删除所有的数据：
```
DELETE FROM table_name;
或
DELETE * FROM table_name;
```
DROP ： 删除索引、表和数据库
DROP INDEX-删除表中的索引
```
ALTER TABLE table_name DROP INDEX index_name
```  
DROP TABLE：删除表
```
DROP TABLE table_name
```
DROP DATABSE：删除数据库
```
DROP DATABASE database_name
```
 TRUNCATE：删除表内的数据，但是不删除数据表本身
```
TRUNCATE TABLE table_name
```     
不同方式的区别：
```
如果我们要删除掉整个表或者数据或者整个索引（列）需要用DROP
删除行就用DELETE，可以删除表中所有的数据，但是表结构属性和索引不会变化
TURNCATE和不带where的delete是一样的，不过速度更快
```

 5. 用SQL语句修改表

修改列名：     

修改表中数据：
```
UPDATE table_name
SET column1=value1,column2=value2,...
WHERE some_column=some_value;
```
其含义为在table_name表，WHERE所在的行将对应的column的值进行修改。如果没有添加WHERE，那么就是将所有行的column的值都进行修改

删除行
```
DELETE FROM table_name
WHERE some_column=some_value;
```         
删除列
```
ALTER TABLE table_name DROP COLUMN column_name
```     
新建列
```
ALTER TABLE table_name
ADD column_name datatype     
```
新建行
```
INSERT INTO table_name
VALUES (value1,value2,value3,...);
或
INSERT INTO table_name (column1,column2,column3,...)
VALUES (value1,value2,value3,...);
```

```
项目3：
CREATE TABLE courses (
student VARCHAR(10) NOT NULL,
class VARCHAR(20) NOT NULL,
)
INSERT INTO courses(student,class)
VALUES('A','MATH');
INSERT INTO courses(student,class)
VALUES('B','ENGLISH');
INSERT INTO courses(student,class)
VALUES('C','MATH');
INSERT INTO courses(student,class)
VALUES('D','BIOLOGY');
INSERT INTO courses(student,class)
VALUES('E','MATH');
INSERT INTO courses(student,class)
VALUES('F','COMPUTER');
INSERT INTO courses(student,class)
VALUES('G','MATH');
INSERT INTO courses(student,class)
VALUES('I','MATH');

SELECT class FROM courses GROUP BY HAVING COUNT(class) >= 5;
```
项目4：

```
CREATE TABLE salary (
id INT NOT NULL PRIMARY KEY,
name VARCHAR(255) NOT NULL,
sex VARCHAR(255) NOT NULL,
salary INT(20) NOT NULL
)

INSERT INTO salary VALUES('1','A','m','2500');
INSERT INTO salary VALUES('2','B','f','1500');
INSERT INTO salary VALUES('3','C','m','5500');
INSERT INTO salary VALUES('4','D','f','500');

UPDATE salary 
  SET sex = CASE 
                                WHEN sex = 'm' THEN 'f' ELSE 'm'
                     END;
```

Mysql - 表联结

MySQL别名:

```
列的sql别名语法：
SELECT column_name AS alias_name
FROM table_name;

行的sql别名语法：
SELECT column_name(s)
FROM table_name AS alias_name;
```

INNER JOIN：只有符合两个表格都存在的属性的时候这个表格才能被联结

```
SELECT column_name(s)
FROM table1
INNER JOIN table2
ON table1.column_name=table2.column_name;
或
SELECT column_name(s)
FROM table1
JOIN table2
ON table1.column_name=table2.column_name;
```

LEFT JOIN：按照左边的表格属性进行联结，除了INNER JOIN之外的部分会出现在联结后的表格中，不过是数值均为NULL

```
SELECT column_name(s)
FROM table1
LEFT JOIN table2
ON table1.column_name=table2.column_name;
或
SELECT column_name(s)
FROM table1
LEFT OUTER JOIN table2
ON table1.column_name=table2.column_name;
```

CROSS JOIN：不管条件 直接相连

```
SELECT column_list
FROM A
CROSS JOIN B;
或
SELECT 
    column_list
FROM
    A,
    B;
```

自连接：一个表与自身进行连接，称为自连接

```
SELECT
    column1,
    column2,
    column3,
        ...
FROM
    table1 A
INNER JOIN table1 B ON B.column1 = A.column2;

在这里A和B是table表的别名，其实是同一样式的表
```

UNION
warning:UNION 内部的每个 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每个 SELECT 语句中的列的顺序必须相同。

```
SELECT column_name(s) FROM table1
UNION
SELECT column_name(s) FROM table2;
```
```
UNION ALL:
SELECT column_name(s) FROM table1
UNION ALL
SELECT column_name(s) FROM table2;
```
以上几种方式的区别和联系：
1.INNER LEFT RIGHT FULL + JOIN 其实都是两张表在联结时候的一种判断或者限定条件，INNER JOIN意思就是限定为两者都有的序列，这有两者符合条件下的行可以进行融合。LEFT JOIN就是以左侧的表的对应属性为主，但是左侧表可以在与右侧表进行结合的时候就缺少了右侧表的被选中的其他属性的对应值，在这种情况下，其对应值为NULL进行显示，而不会直接像INNER一样剔除掉。RIGHT JOIN其实就是left的右侧版本。FULL JOIN就是left和right的融合版本。
2.UNION JOIN就是提取了表之间同属性下的所有值，并且结合在了一起，但是结果是一种集合方式。
3.自连接 自连接就是自己和自己连接，自连接可行的情况就是两个不同的属性有一个共同的属性，这一点我理解有点像自己的外键。

项目五

```
CREATE TABLE Person (
PersonID int(10) PRIMARY KEY,
FirstName varchar(255) NOT NULL,
LastName varchar(255) NOT NULL
);
INSERT INTO Person
VALUES('1','xiaoming','huang');
INSERT INTO Person
VALUES('2','ying','yang');
INSERT INTO Person
VALUES('3','kai','zhao');

CREATE TABLE Address (
AddressId int(10) PRIMARY KEY,
PersonId int(10) NOT NULL,
City varchar(255) NOT NULL,
State varchar(255) NOT NULL
);
INSERT INTO Address
VALUES('024','1','shenyang','liaoning');
INSERT INTO Address
VALUES('0411','2','dalian','liaoning');
INSERT INTO Address
VALUES('0412','3','anshan','liaoning');

SELECT FirstName,LastName,City,State From Person
LEFT JOIN Address ON Person.PersonId=Address.PersonId;
```

项目六

```
CREATE TABLE email (
Id int(5) NOT NULL PRIMARY KEY,
Email varchar(255) NOT NULL
);

INSERT INTO email
VALUES('1','a@b.com');
INSERT INTO email
VALUES('2','c@d.com');
INSERT INTO email
VALUES('3','a@b.com');

DELETE P2 FROM email AS P1, email AS P2
WHERE  P1.Email = P2.Email AND P1.Id < P2.Id;
```