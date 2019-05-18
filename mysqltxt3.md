#### 数据导入导出

- 将之前创建的任意一张MySQL表导出,且是CSV格式
使用SELECT ... INTO OUTFILE 语句导出数据
导出到txt：

```
mysql> SELECT * FROM runoob_tbl 
    -> INTO OUTFILE '/tmp/runoob.txt';
```
导出csv：

```
mysql> SELECT * FROM passwd INTO OUTFILE '/tmp/runoob.txt'
    -> FIELDS TERMINATED BY ',' ENCLOSED BY '"'
    -> LINES TERMINATED BY '\r\n';
```
- 再将CSV表导入数据库

	1.mysql命令导入：
```
mysql -u用户名    -p密码    <  要导入的数据库数据(runoob.sql)
```
	2.source命令导入：

```
mysql> create database abc;      # 创建数据库

mysql> use abc;                  # 使用已创建的数据库 

mysql> set names utf8;           # 设置编码

mysql> source /home/abc/abc.sql  # 导入备份数据库
```
	3.使用LOAD DATA导入数据

```
mysql> LOAD DATA LOCAL INFILE 'dump.txt' INTO TABLE mytbl;
```

```
mysql> LOAD DATA LOCAL INFILE 'dump.txt' INTO TABLE mytbl
  -> FIELDS TERMINATED BY ':'
  -> LINES TERMINATED BY '\r\n';
```


项目七：

```
mysql> CREATE TABLE Empolyee (
    -> Id int not null primary key,
    -> Name varchar(255) not null,
    -> Salary int not null,
    -> DepartmentId int not null);

mysql> INSERT INTO Employee VALUES
    -> ('1','joe','70000','1'),
    -> ('2','henry','80000','2'),
    -> ('3','sam','60000','2'),
    -> ('4','max','90000','1');
    
mysql> create table Department (
    -> DepartmentId int not null primary key,
    -> Name varchar(255) not null
    -> );
    
mysql> insert into Department values 
    -> ('1','IT'),
    -> ('2','Sales');

create table tmp as (select Department.Name AS Department,Employee.Name,Salary from Employee                                                            partmentId);

delete p2 from tmp as p1, tmp as p2 where p1.Department = p2.Department AND p1.Salary > p2.Salary;

mysql> select * from tmp;
+------------+-------+--------+
| Department | Name  | Salary |
+------------+-------+--------+
| IT         | max   |  90000 |
| Sales      | henry |  80000 |
+------------+-------+--------+
2 rows in set (0.00 sec)
```

项目八：

```
CREATE TABLE seat(id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,student VARCHAR(100) NOT NULL);

mysql> INSERT INTO seat VALUES(
    -> '1','ABBOT'),
    -> ('2','DORIS'),
    -> ('3','EMERSON'),
    -> ('4','GREEN'),
    -> ('5','JEAMES');

SELECT * FROM (
SELECT id-1 AS id,student FROM seat WHERE id%2=0

UNION

SELECT id+1 AS id,student FROM seat WHERE id%2=1 AND (id+1)<=(SELECT COUNT(*) FROM seat)

UNION

SELECT id AS id,student FROM seat WHERE id%2=1 AND (id+1)>(SELECT count(*) FROM seat) ) AS c1

ORDER BY id ASC;

+----+---------+
| id | student |
+----+---------+
|  1 | DORIS   |
|  2 | ABBOT   |
|  3 | GREEN   |
|  4 | EMERSON |
|  5 | JEAMES  |
+----+---------+
5 rows in set (0.00 sec)
```

项目九：

```
mysql> CREATE TABLE score(
    -> id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    -> Score FLOAT NOT NULL);
Query OK, 0 rows affected (0.01 sec)

mysql> INSERT INTO score VALUES ('1','3.50'), ('2','3.65'), ('3','4.00'), ('4','3.85'), ('5','4.00'), ('6','3.65');

mysql> SELECT * FROM score;
+----+-------+
| id | Score |
+----+-------+
|  1 |   3.5 |
|  2 |  3.65 |
|  3 |     4 |
|  4 |  3.85 |
|  5 |     4 |
|  6 |  3.65 |
+----+-------+
6 rows in set (0.00 sec)

SELECT Score,id FROM score ORDER BY Score DESC;

mysql> SELECT Score,id FROM score ORDER BY Score DESC;
+-------+----+
| Score | id |
+-------+----+
|     4 |  3 |
|     4 |  5 |
|  3.85 |  4 |
|  3.65 |  2 |
|  3.65 |  6 |
|   3.5 |  1 |
+-------+----+
6 rows in set (0.00 sec)

SELECT DISTINCT Score From (SELECT Score,id FROM score ORDER BY Score DESC);

SELECT Score,(SELECT COUNT(DISTINCT Score) FROM score WHERE Score>=s.Score) AS Rank

FROM score AS s
ORDER BY Score DESC;


select * from (
select 
    score,
    (select count(distinct score) from score as s2 where s2.score >= s1.score) AS _Rank 
from score as s1) S
order by score DESC;

+-------+-------+
| score | _Rank |
+-------+-------+
|  4.00 |     1 |
|  4.00 |     1 |
|  3.85 |     2 |
|  3.65 |     3 |
|  3.65 |     3 |
|  3.50 |     4 |
+-------+-------+
6 rows in set (0.00 sec)
```



