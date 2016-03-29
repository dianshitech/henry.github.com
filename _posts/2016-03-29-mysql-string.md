---
layout: post
title:  mysql string的一些用法
date:   2016-03-29
categories: mysql
excerpt: mysql索引用法
---

* content
{:toc}

## 前置索引
SELECT *,instr(',1,10,2,4,12,7,',concat(',',id,',')) as c FROM `im_tag_info` WHERE id in (1,10,2,4,12,7) order by c asc

## INSTR(字段名, 字符串)

这个函数返回字符串在某一个字段的内容中的位置, 没有找到字符串返回0，否则返回位置（从0开始）

## CONCAT(str1,str2,…)

返回结果为连接参数产生的字符串。如有任何一个参数为NULL ，则返回值为 NULL。


## CONCAT_WS(separator,str1,str2,...)

CONCAT_WS() 代表 CONCAT With Separator ，是CONCAT()

的特殊形式。第一个参数是其它参数的分隔符。分隔符的位置放在要连接的两个字符串之间。分隔符可以是一个字符串，也可以是其它参数。

select concat_ws(',','11','22','33');

## LTRIM(str)

mysql> SELECT LTRIM(' barbar');

mysql> SELECT TRIM(LEADING '，' FROM '，，barxxx'); //删除指定首字符 如'，

-> 'barxxx'
mysql> SELECT TRIM(BOTH '，' FROM '，，bar，，，'); //删除指定首尾字符

-> 'bar'
mysql> SELECT TRIM(TRAILING '，' FROM 'barxxyz，，');

-> 'barxxyz'