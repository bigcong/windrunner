title: "\_总结"
tags:
  - 教程
categories:
  - 总结
date: 2017-05-04 10:02:00
---


## 总结

### tensorflow的基本类型

``` bash
       Variable  计算图谱中的变量
       Constant  常量
       Placeholder  预先的变量，类似于占位符，暂时变量？
```
### 常用命令
 ```
   hexo d -g     hexo 编译发布
 ```
### gradle 仓库加速
  ```
    maven{url'http://maven.aliyun.com/nexus/content/groups/public'}  
  ```
### 连接redis远程服务器
  ```
   redis-cli -h 123.57.220.83 -p 6379 auth iGn7mIJZYW2rdzJqT
  ```
### pptp VPN 创建连接
  ```
sudo pptpsetup --create pptpd  --server x.x.x.x  --username 11111  --password  00000  --encrypt --start   
  
  ```
### 保留两位小数四舍五入
　  ```
double   f   =   111231.5585;  
BigDecimal   b   =   new   BigDecimal(f);  
double   f1   =   b.setScale(2,   BigDecimal.ROUND_HALF_UP).doubleValue();  
```

### java 8 分区

```
  Map<Boolean, List<CaCustomerCard>> collect = caCustomerCards.stream().collect(Collectors.partitioningBy(t -> t.getId() == cardId));

```

