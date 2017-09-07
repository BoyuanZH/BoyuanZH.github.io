---
layout:     post
title:      "SQL tricks"
date:       2017-09-01
author:     "BoyuanZH"
header-img: "img/post-bg-building.jpg"
tags:
    - SQL
    - Study Notes
---

### Session Variable

> [569. Median Employee Salary](https://leetcode.com/problems/median-employee-salary/description/)
> 

The execution order inside the sql server of `order by` statement is interesting, following two approach both work to create the ranking per company.

```
SELECT 
        e.Id,
            e.Salary,
            e.Company,
            IF(@prev = e.Company, @Rank:=@Rank + 1, @Rank:=1) AS rank,
            @prev:=e.Company
    FROM
        (SELECT * FROM Employee ORDER BY Company, Salary DESC) e, (SELECT @Rank:=0, @prev:=0) AS temp
```


```
SELECT 
        e.Id,
            e.Salary,
            e.Company,
            IF(@prev = e.Company, @Rank:=@Rank + 1, @Rank:=1) AS rank,
            @prev:=e.Company
    FROM
        Employee e, (SELECT @Rank:=0, @prev:=0) AS temp
    ORDER BY e.Company , e.Salary , e.Id
```

This may imply the way sql server handling `@variable` is different from normal database columns.

