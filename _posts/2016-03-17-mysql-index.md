---
layout: post
title:  "mysql索引"
date:   2016-03-16 14:25:30
categories: php
excerpt: mysql索引用法
---

* content
{:toc}

## 前置索引
ALTER TABLE wx_union ADD KEY(openid(10));

## mysql key_len
* 索引字段的附加信息：可以分为变长和定长数据类型讨论，当索引字段为定长数据类型，比如char，int，datetime，需要有是否为空的标记，这个标记需要占用1个字节；对于变长数据类型，比如：varchar，除了是否为空的标记外，还需要有长度信息，需要占用2个字节；

* 同时还需要考虑表所使用的字符集，不同的字符集，gbk编码的为一个字符2个字节，utf8编码的一个字符3个字节;
(备注：当字段定义为非空的时候，是否为空的标记将不占用字节)

如：`user`表为utf-8.索引字段 `uid` 为int(10)，不允许为空 则key_len = 4 （int是占4个字符）
如：`user`表为utf-8.索引字段 `age` 为int(10)，允许为空 则key_len = 4 + 1 （int是占4个字符）
如：`user`表为utf-8.索引字段 `user_name` 为varchar(50)，允许为空 则key_len = 50 * 3 + 2 + 1 = 153
如：`user`表为gbk.  索引字段 `user_name` 为varchar(50)，不允许为空  则key_len = 50 * 2 + 2 = 102


* varchar(255) 和varchar(256)
MySQL的varchar索引只支持不超过768个字节 或者 768/2=384个双字节 或者 768/3=256个三字节的字段
而 GBK是双字节的，UTF-8是三字节的,所以一般我们设置为varchar(255).这样就可以用到索引

* char 和varchar 的区别
char是一种固定长度的类型，varchar则是一种可变长度的类型，它们的区别是：

char(M)类型的数据列里，每个值都占用M个字节，如果某个长度小于M，MySQL就会在它的右边用空格字符补足．（在检索操作中那些填补出来的空格字符将被去掉）在varchar(M)类型的数据列里，每个值只占用刚好够用的字节再加上一个用来记录其长度的字节（即总长度为L+1字节）．