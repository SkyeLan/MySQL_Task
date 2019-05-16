# 【任务二】

## 2.1 MySQL 基础 （二）- 表操作
### 学习内容
1. MySQL表数据类型
2. 用SQL语句创建表
	语句解释     设定列类型 、大小、约束     设定主键 
3. 用SQL语句向表中添加数据
    语句解释     多种添加方式（指定列名；不指定列名） 
4. 用SQL语句删除表
   语句解释     DELETE     DROP     TRUNCATE     不同方式的区别 
5. 用SQL语句修改表
   修改列名     修改表中数据     删除行     删除列     新建列     新建行
   



### 作业

#### 项目三：超过5名学生的课（难度：简单）

创建如下所示的courses 表 ，有: student (学生) 和 class (课程)。

| student | class      |
|---------|------------|
| A       | Math       |
| B       | English    |
| C       | Math       |
| D       | Biology    |
| E       | Math       |
| F       | Computer   |
| G       | Math       |
| H       | Math       |
| I       | Math       |
| A       | Math       |

建表：

```mysql
create table courses (
	student char(1) not null,
	class char(10) not null
);
```

插入数据：

```mysql
insert into courses values("A", "Math");
insert into courses values("B", "English");
insert into courses values("C", "Math");
insert into courses values("D", "Biology");
insert into courses values("E", "Math");
insert into courses values("F", "Computer");
insert into courses values("G", "Math");
insert into courses values("H", "Math");
insert into courses values("I", "Math");
insert into courses values("A", "Math");
```

编写一个 SQL 查询，列出所有超过或等于5名学生的课。

Note：学生在每个课中不应被重复计算。

```mysql
select class from courses group by class having(count(*)>=5);
```
输出:

| class   |
|---------|
| Math    |



#### 项目四：交换工资（难度：简单）

创建一个 salary 表，如下所示，有 m=男性 和 f=女性 的值 。

|id	|name	|sex	|salary|
|-----|-----------|-----------|----------|
|1 	|A   	|m   |	2500  |
|2 |	B   |	f   |	1500   |
|3 	|C   |	m   |	5500   |
|4 |	D   |	f   	|500   |


建表：

```mysql
create table salary(
	id int not null,
	name char(5) not null,
	sex char(1) not null,
	salary long
);
```

插入数据：

```mysql
insert into salary values(1,"A","m",2500);
insert into salary values(2,"B","f",1500);
insert into salary values(3,"C","m",5500);
insert into salary values(4,"D","f",500);
```



交换所有的 f 和 m 值。要求使用一个更新查询，并且没有中间临时表。

```mysql
UPDATE salary AS s1 JOIN salary AS s2 
ON (s1.sex = "m" AND s2.sex = "f")
SET s1.sex = s2.sex, s2.sex = s1.sex;
```
输出:

|id	|name	|sex|	salary|
|------|-----------|--------|--------------|
|1 	|A   |	f  |	2500   |
|2 	|B   |	m   |	1500   |
|3 |	C   |	f   |	5500   |
|4 |	D   |	m   |	500   |





## 2.2 MySQL 基础 （三）- 表联结
### 学习内容
1. MySQL别名
2. INNER JOIN
3. LEFT JOIN
4. CROSS JOIN
5. 自连接
6. UNION



### 作业

#### 项目五：组合两张表 （难度：简单）

在数据库中创建表1和表2，并各插入三行数据

表1: Person

| 列名 | 类型 |
|-------------|---------|
| PersonId | int |
| FirstName | varchar |
| LastName | varchar |

PersonId 是上表主键

表2: Address

| 列名 | 类型 |
|------------|---------|
| AddressId | int |
| PersonId | int |
| City | varchar |
| State | varchar |

AddressId 是上表主键


建表：

```mysql
create table Person(
	PersonId  int PRIMARY key,
	FirstName  varchar(10),
	LastName  varchar(10)
);

create table Address(
	AddressId  int PRIMARY key,
	PersonId int,
	City  varchar(20),
	State  varchar(20)
);
```

插入数据：

```mysql
INSERT into Person VALUES
(1,"san","zhang"),
(2,"si","li"),
(3,"wu","wang");

INSERT into Address VALUES
(1,2,"nanjing","jiangsu"),
(2,1,"suzhou","jiangsu"),
(3,4,"shanghai","shanghai");
```



编写一个 SQL 查询，满足条件：无论 person 是否有地址信息，都需要基于上述两表提供 person 的以下信息：FirstName, LastName, City, State

```mysql
select FirstName, LastName, City, State
from Person LEFT JOIN Address
on Person.PersonId = Address.PersonId;
```
输出:

|FirstName	|LastName	|City|	State|
|------|-----------|--------|--------------|
|si 	|li   |	nanjing |	jiangsu |
|san 	|zhang   |	suzhou |	jiangsu |
|wu |	wang |	   |	   |



#### 项目六：删除重复的邮箱（难度：简单）

编写一个 SQL 查询，来删除 email 表中所有重复的电子邮箱，重复的邮箱里只保留 **Id **最小的那个。

| Id | Email |
|----|---------|
| 1 | a@b.com |
| 2 | c@d.com |
| 3 | a@b.com |

Id 是这个表的主键。


建表：

```mysql
create table email(
	id int primary key,
	email char(50)
);
```

插入数据：

```mysql
insert into email VALUES
(1,"a@b.com"),
(2,"c@d.com"),
(3,"a@b.com");
```



删除 email 表中所有重复的电子邮箱，重复的邮箱里只保留 **Id **最小的那个。

```mysql
delete from email where id not in(
SELECT temp.id FROM(
select MIN(id) AS id from email group by Email
)temp); 

select * from email;
```
输出:

| Id | Email |
|----|------------------|
| 1 | a@b.com |
| 2 | c@d.com |