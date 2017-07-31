## mysql 查看表占用

```
 select table_name,data_length from information_schema.tables;
```

### 查看慢查询
```
show full processlist; 
```