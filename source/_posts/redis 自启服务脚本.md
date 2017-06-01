title: redis自启服务脚本
tags:
  - redis
  - 运维
categories:
  - 命令
date: 2017-06-01 11:17:00
---

---
### 启动脚本

```
# chkconfig:   2345 90 10

# description:  Redis is a persistent key-value database

###########################
PATH=/usr/local/bin:/sbin:/usr/bin:/bin
   
REDISPORT=6379
EXEC=/data/lib/redis-3.2.8/src/redis-server
REDIS_CLI=/data/lib/redis-3.2.8/src/redis-cli
   
PIDFILE=/var/run/redis_6379.pid
CONF="/data/lib/redis-3.2.8/redis.conf"
   
case "$1" in
    start)
        if [ -f $PIDFILE ]
        then
                echo "$PIDFILE exists, process is already running or crashed"
        else
                echo "Starting Redis server..."
                $EXEC $CONF
        fi
        if [ "$?"="0" ] 
        then
              echo "Redis is running..."
        fi
        ;;
    stop)
        if [ ! -f $PIDFILE ]
        then
                echo "$PIDFILE does not exist, process is not running"
        else
                PID=$(cat $PIDFILE)
                echo "Stopping ..."
                $REDIS_CLI -p $REDISPORT SHUTDOWN
                while [ -x ${PIDFILE} ]
               do
                    echo "Waiting for Redis to shutdown ..."
                    sleep 1
                done
                echo "Redis stopped"
        fi
        ;;
   restart|force-reload)
        ${0} stop
        ${0} start
        ;;
  *)
    echo "Usage: /etc/init.d/redis {start|stop|restart|force-reload}" >&2
        exit 1
esac
##############################
```

### 设置权限
```
 chmod +x redis
 chkconfig --add redis
 chkconfig redis on
 chkconfig --level 3 redis on
```


