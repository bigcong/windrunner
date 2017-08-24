title: supervisor配置文件
author: bigcong
tags:
  - 配置文件
categories:
  - linux
date: 2017-08-24 16:53:00
---
```
[program:jakiro]
command=java -jar  -XX:MetaspaceSize=256m -XX:MaxMetaspaceSize=512m  -Xms256M -Xmx256M build/libs/jakiro-0.0.1-SNAPSHOT.war  --server.port=8094
autorstart=true
directory=/Users/cong/.jenkins/workspace/jakiro
stdout_logfile=/usr/local/etc/supervisor.d/logs/jakiro.log
environment = HOME="/root", USER="root"

```