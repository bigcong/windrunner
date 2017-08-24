title: mysql注意点
tags:
  - mysql总结
  - ''
categories:
  - mysql
date: 2017-07-14 12:15:00
---

---
### pt-query-digest
可以慢查询将查询报告保存到数据库中，以及追踪负载随着时间的变化


### 剖析单条查询
```
set profiling=1;
show profiles;
show profile for query 1;
show status;
show global status;
```

### DATETIME 和TIMESAMP 的区别
dateTime和timesamp列可以存储相同类型的数据：时间日期，精确到秒，然而timestamp只试用datetime一半的存储空间，并且会根据时区的变化，具有特殊更新能力，timestamp允许的范围比较小。


### DECIMAL

因为CPU不支持DECIMAL的直接计算。对于DECIMAL列，可以指定小数点前后所允许的最大位数，这也会消耗更多的空间消耗。高版本的mysql会将DECIMAL打包存在一个二进制的字符串中，一种9个字节，小数点后用4个字节，小数点前用4个字节，小数点占一个字节。高版本mysql自身实现了高精度计算。相对而言，cpu直接支持浮点型计算，运行时间更快

### VARCHAR 和CHAR
#### VARCHAR
1. 用于存储可变字符串，是最常见的字符串数据类型，比定长类型更节省空间。当时如果mysql表使用ROW_FORMT=FIXED创建的话，每一行都会使用定长存储，这会浪费空间
2. varchar需要使用1或2个额外字节记录字符串的长度，如果列的最大长度小于255，则使用1个字节，否则就需要2个字节
3. 如果update操作是，使行变得比原来更长，这就是导致了需要做额外的工作，InnoDB则需要分裂页来使行可以放在页内。
4. varchar适合：字符串的最大长度比平均长度大很多，列的跟新很少，所以碎片不是问题。

#### CHAR
char类型是定长的,适合存储很短的字符串，或者所有的都接近同一个长度。例如，char非常适合存储Md5值
定长的char类型不容易产生碎片，对于非常短的列，char比varchar在存储空间上也更有效率。char(1)只需要一个字节，而varchar(1)却需要两个字节，因为还有一个记录长度的额外字节

#### BLOB和TEXT类型
BlOB类型存储的是二进制数据，没有排序规则或者字符集，而TEXT类型有字符集和排序规则
它只对每一个列的最前max_sort_length， 字节而不是整个字符串做排序。
不能将BLOB和TEXT列全部长度进行索引，也不能使用这些索引消除排序

####  使用枚举(ENUM)代替字符串类型
实际存储为整数，而不是字符串

```
select e+0 form eum_test;

```















