title: mysql注意点
tags:
  - mysql
categories: []
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


