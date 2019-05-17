# 【任务一】
## 1.1 MySQL 软件安装及数据库基础
### 学习内容 
1. 软件安装及服务器设置。    
	
	教程 http://www.runoob.com/mysql/mysql-install.html
	
2. 使用图形界面软件 Navicat

3. 数据库基础知识    

   数据库定义、关系型数据库、二维表、行、列、主键、 外键

4. MySQL数据库管理系统
    数据库、数据表、视图、存储过程




## 1.2 MySQL 基础 （一）- 查询语句
### 学习内容
1. SQL是什么？MySQL是什么？

2. 查询语句 SELECT FROM 
  语句解释     去重语句     前N个语句     CASE...END判断语句 

3. 筛选语句 WHERE 
  语句解释     运算符/通配符/操作符 

4. 分组语句 GROUP BY
  聚集函数     语句解释     HAVING子句 

5. 排序语句 ORDER BY 
  语句解释     正序、逆序 

6. 函数
  时间函数     数值函数     字符串函数 

7. SQL注释

8. SQL代码规范
  [SQL编程格式的优化建议](https://zhuanlan.zhihu.com/p/27466166)

  [SQL Style Guide](https://www.sqlstyle.guide/)



### 作业

#### 项目一：查找重复的电子邮箱（难度：简单） 

创建 email表，并插入如下三行数据 

| Id | Email   |
|----|---------|
| 1  | [a@b.com] |
| 2  | [c@d.com]|
| 3  | [a@b.com]|

创建表：
```mysql
CREATE TABLE email (
ID INT NOT NULL PRIMARY KEY,
Email VARCHAR(255)
);
```

插入数据：
```mysql
INSERT INTO email VALUES('1','a@b.com');
INSERT INTO email VALUES('2','c@d.com');
INSERT INTO email VALUES('3','a@b.com');
```



编写一个 SQL 查询，查找 Email 表中所有重复的电子邮箱。 


查询语句：
```mysql
select name, population, area 
from world 
where area > 3000000 or (population>25000000 and gdp>20000000);
```
输出: 

| Email   |
|---------|
| [a@b.com]|



#### 项目二：查找大国（难度：简单） 

创建如下 World 表

| name            | continent  | area       | population   | gdp           |
|-----------------|------------|-----------|--------------|--------------|
| Afghanistan     | Asia       | 652230     | 25500100     | 20343000      |
| Albania         | Europe     | 28748      | 2831741      | 12960000      |
| Algeria         | Africa     | 2381741    | 37100000     | 188681000     |
| Andorra         | Europe     | 468        | 78115        | 3712000       |
| Angola          | Africa     | 1246700    | 20609294     | 100990000     |

创建表
```mysql
CREATE TABLE World (
    name VARCHAR(50) NOT NULL,
    continent VARCHAR(50) NOT NULL,
    area INT NOT NULL,
    population INT NOT NULL,
    gdp INT NOT NULL
);
```

插入数据
```mysql
INSERT INTO World VALUES('Afghanistan','Asia',652230,25500100,20343000);
INSERT INTO World VALUES('Albania','Europe',28748,2831741,12960000);
INSERT INTO World VALUES('Algeria','Africa',2381741,37100000,188681000);
INSERT INTO World VALUES('Andorra','Europe',468,78115,3712000);
INSERT INTO World VALUES('Angola','Africa',1246700,20609294,100990000);
```



如果一个国家的面积超过300万平方公里，或者(人口超过2500万并且gdp超过2000万)，那么这个国家就是大国家。 
编写一个SQL查询，输出表中所有大国家的名称、人口和面积。 

```mysql
select name, population, area 
from world 
where area > 3000000 or (population>25000000 and gdp>20000000);
```
输出: 

| name        | population | area   |
| ----------- | ---------- | ------ |
| Afghanistan | 25500100   | 652230 |
|Algeria	|37100000	|2381741|
