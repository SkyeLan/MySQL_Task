项目一：查找重复的电子邮箱（难度：简单） 

创建 email表，并插入如下三行数据 

| Id | Email   |
|----|---------|
| 1  | [a@b.com] |
| 2  | [c@d.com]|
| 3  | [a@b.com]|

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





项目二：查找大国（难度：简单） 
创建如下 World 表

| name            | continent  | area       | population   | gdp           |
|-----------------|------------|-----------|--------------|--------------|
| Afghanistan     | Asia       | 652230     | 25500100     | 20343000      |
| Albania         | Europe     | 28748      | 2831741      | 12960000      |
| Algeria         | Africa     | 2381741    | 37100000     | 188681000     |
| Andorra         | Europe     | 468        | 78115        | 3712000       |
| Angola          | Africa     | 1246700    | 20609294     | 100990000     |

如果一个国家的面积超过300万平方公里，或者(人口超过2500万并且gdp超过2000万)，那么这个国家就是大国家。 
编写一个SQL查询，输出表中所有大国家的名称、人口和面积。 



查询语句：
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
