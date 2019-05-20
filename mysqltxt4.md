项目10：

```
CREATE TABLE Trips (
Id INT NOT NULL PRIMARY KEY,
Client_Id INT NOT NULL,
Driver_Id INT NOT NULL,
City_Id INT NOT NULL,
Status enum('completed','cancelled_by_driver','cancelled_by_client'),
Request_at DATE NOT NULL);


INSERT INTO Trips VALUES
(1,1,10,1,'completed',20131001),
(2,2,11,1,'cancelled_by_driver',20131001),
(3,3,12,6,'completed',20131001),
(4,4,13,6,'cancelled_by_client',20131001),
(5,1,10,1,'completed',20131002),
(6,2,11,6,'completed',20131002),
(7,3,12,6,'completed',20131002),
(8,2,12,12,'completed',20131003),
(9,3,10,12,'completed',20131003),
(10,4,13,12,'cancelled_by_driver',20131003);

mysql> select * from Trips;
+----+-----------+-----------+---------+---------------------+------------+
| Id | Client_Id | Driver_Id | City_Id | Status              | Request_at |
+----+-----------+-----------+---------+---------------------+------------+
|  1 |         1 |        10 |       1 | completed           | 2013-10-01 |
|  2 |         2 |        11 |       1 | cancelled_by_driver | 2013-10-01 |
|  3 |         3 |        12 |       6 | completed           | 2013-10-01 |
|  4 |         4 |        13 |       6 | cancelled_by_client | 2013-10-01 |
|  5 |         1 |        10 |       1 | completed           | 2013-10-02 |
|  6 |         2 |        11 |       6 | completed           | 2013-10-02 |
|  7 |         3 |        12 |       6 | completed           | 2013-10-02 |
|  8 |         2 |        12 |      12 | completed           | 2013-10-03 |
|  9 |         3 |        10 |      12 | completed           | 2013-10-03 |
| 10 |         4 |        13 |      12 | cancelled_by_driver | 2013-10-03 |
+----+-----------+-----------+---------+---------------------+------------+
10 rows in set (0.00 sec)



CREATE TABLE Users (
Users_Id INT NOT NULL PRIMARY KEY,
Banned VARCHAR(20) NOT NULL,
Role enum('client','driver','partner')
);

INSERT INTO Users VALUES
(1,'No','client'),
(2,'Yes','client'),
(3,'No','client'),
(4,'No','client'),
(10,'No','driver'),
(11,'No','driver'),
(12,'No','driver'),
(13,'No','driver');

mysql> select * from Users;
+----------+--------+--------+
| Users_Id | Banned | Role   |
+----------+--------+--------+
|        1 | No     | client |
|        2 | Yes    | client |
|        3 | No     | client |
|        4 | No     | client |
|       10 | No     | driver |
|       11 | No     | driver |
|       12 | No     | driver |
|       13 | No     | driver |
+----------+--------+--------+
8 rows in set (0.00 sec)
```
| 1 | No | client | | 2 | Yes | client | | 3 | No | client | | 4 | No | client | | 10 | No | driver | | 11 | No | driver | | 12 | No | driver | | 13 | No | driver |

| 1 | 1 | 10 | 1 | completed |2013-10-01| | 2 | 2 | 11 | 1 | cancelled_by_driver|2013-10-01| | 3 | 3 | 12 | 6 | completed |2013-10-01| | 4 | 4 | 13 | 6 | cancelled_by_client|2013-10-01| | 5 | 1 | 10 | 1 | completed |2013-10-02| | 6 | 2 | 11 | 6 | completed |2013-10-02| | 7 | 3 | 12 | 6 | completed |2013-10-02| | 8 | 2 | 12 | 12 | completed |2013-10-03| | 9 | 3 | 10 | 12 | completed |2013-10-03| | 10 | 4 | 13 | 12 | cancelled_by_driver|2013-10-03| 

项目11：

```
mysql> select * from Employee;
+----+-------+--------+--------------+
| Id | Name  | Salary | DepartmentId |
+----+-------+--------+--------------+
|  1 | joe   |  70000 |            1 |
|  2 | henry |  80000 |            2 |
|  3 | sam   |  60000 |            2 |
|  4 | max   |  90000 |            1 |
|  5 | janet |  69000 |            1 |
|  6 | randy |  85000 |            1 |
+----+-------+--------+--------------+
6 rows in set (0.00 sec)


mysql> select * from Department;
+--------------+-------+
| DepartmentId | Name  |
+--------------+-------+
|            1 | IT    |
|            2 | Sales |
+--------------+-------+
2 rows in set (0.00 sec)

SELECT t2.Name AS Department,t1.Name AS employee,t1.Salary AS Salary FROM Employee AS t1,Department AS t2 WHERE t1.DepartmentId=t2.DepartmentId;

+------------+----------+--------+
| Department | employee | Salary |
+------------+----------+--------+
| IT         | joe      |  70000 |
| Sales      | henry    |  80000 |
| Sales      | sam      |  60000 |
| IT         | max      |  90000 |
| IT         | janet    |  69000 |
| IT         | randy    |  85000 |
+------------+----------+--------+
6 rows in set (0.00 sec)


SELECT t2.Name AS Department,t1.Name AS employee,t1.Salary AS Salary FROM Employee AS t1,Department AS t2 WHERE t1.DepartmentId=t2.DepartmentId ORDER BY Salary DESC;

+------------+----------+--------+
| Department | employee | Salary |
+------------+----------+--------+
| IT         | max      |  90000 |
| IT         | randy    |  85000 |
| Sales      | henry    |  80000 |
| IT         | joe      |  70000 |
| IT         | janet    |  69000 |
| Sales      | sam      |  60000 |
+------------+----------+--------+
6 rows in set (0.00 sec)

SELECT Department,employee,Salary FROM(
SELECT Department,employee,Salary FROM (SELECT t2.Name AS Department,t1.Name AS employee,t1.Salary AS Salary FROM Employee AS t1,Department AS t2 WHERE t1.DepartmentId=t2.DepartmentId ORDER BY Salary DESC) tmp WHERE tmp.Department='IT' ORDER BY Salary DESC LIMIT 3) AS C1
UNION
SELECT Department,employee,Salary FROM (
SELECT Department,employee,Salary FROM (SELECT t2.Name AS Department,t1.Name AS employee,t1.Salary AS Salary FROM Employee AS t1,Department AS t2 WHERE t1.DepartmentId=t2.DepartmentId ORDER BY Salary DESC) tmp WHERE tmp.Department='Sales' ORDER BY Salary DESC LIMIT 3) AS C2;

```

项目12：

```
+----+-------+
| id | score |
+----+-------+
|  1 |  3.50 |
|  2 |  3.65 |
|  3 |  4.00 |
|  4 |  3.85 |
|  5 |  4.00 |
|  6 |  3.65 |
+----+-------+
6 rows in set (0.00 sec)

select * from (
select 
    score,
    (select count(score) from score as s2 where s2.score > s1.score)+1 AS 'Rank' 
from score as s1) S
order by score DESC;

+-------+------+
| score | Rank |
+-------+------+
|  4.00 |    1 |
|  4.00 |    1 |
|  3.85 |    3 |
|  3.65 |    4 |
|  3.65 |    4 |
|  3.50 |    6 |
+-------+------+
6 rows in set (0.00 sec)
```





