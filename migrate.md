# 数据分割总结
##### 第一步:明确要做什么
##### 第二步：理清思路
##### 第三部：最后代码实现，而且做好笔记难免会遗忘！
想让数据库掌握的更好:我个人觉得，没有什么好说的就是多练，让自己的逻辑思维变得更强
要在理解的基础上去消化它，不然写了也白写!

对于分割的方法：方法有多种
##### 1、可以多表关联查询
##### 2、使用union语句
##### 区别：
##### 就是关联查询代码复杂，不容易理解！
##### 使用union代码会简化，但效率会低！

```这是分步创建城市表lagou_city 
select count(*)   cityName  from s_provinces;
create table  lagou_city as 
select d.id,p.cityName as province ,c.cityname as city ,d.cityName as district  from 
(select * from s_provinces where depth=3)d
join s_provinces c on d.parentId =c.id and c.depth=2
join s_provinces p on c.parentId =p.id and p.depth=1;

```

```
--查询有 null的数据
insert into lagou_city 
select c.id, p.cityName as province, c.cityName as city, null as district from (select * from s_provinces where depth=2) c
join s_provinces p on c.parentId = p.id and p.depth = 1;

```


```
##这是分割的公司表
create table lagou_company as
select distinct  
t.company_id as cid,
t.company_short_name as short_name,
t.company_full_name as full_name, 
t.financestage as financestage
from lagou_position t;
```
