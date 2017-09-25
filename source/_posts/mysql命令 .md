title: mysql命令
tags:
  - 命令
categories:
  - mysql
author: ''
date: 2017-08-24 16:48:00
---

---
## mysql 查看表占用

```
 select table_name,data_length from information_schema.tables;
```

### 查看慢查询
```
show full processlist; 
```

###  开启远端权限
```
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'IDENTIFIED BY '' WITH GRANT OPTION; 

```

###     定时备份sql，那么可在/etc/crontab配置文件中加入下面代码行：
```
30 1 * * * root mysqldump -u root -pPASSWORD --all-databases | gzip > /mnt/disk2/database_`date '+%m-%d-%Y'`.sql.gz

```
## mysql命令


### mysql将结果导出文件
```
mysql -h 172.1.0.1  -uroot -pcc  --default-character-set=utf8 jeeplus_schema -e "select count(*),uname,phone from user group by uname  having count(*)>1;" > /tmp/repeat.txt
```
### mysql 关联表一起更新
```
UPDATE user_points p,
 (
	SELECT
		uuid,
		sum(number) outnumber
	FROM
		user_itl_consume
	GROUP BY
		uuid
) outcome,
 (
	SELECT
		uuid,
		sum(number) innumber
	FROM
		user_itl_income
	GROUP BY
		uuid
) income
SET p.point = (
	income.innumber - outcome.outnumber
)
WHERE
	p.uuid = income.uuid
AND p.uuid = outcome.uuid
AND income.innumber - outcome.outnumber != p.point;

```


