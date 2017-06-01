title: 常用的命令
author: bigcong
tags:
  - ''
  - 命令
categories:
  - 命令
date: 2017-05-17 16:17:00
---



##  系统命令



### Mac查看端口占用
```
lsof -i tcp:8080

```

### 给予某个用户权限某个用户权限
```
 chown -R jenkins:jenkins /data/app/jar/
```
###   安装ZSH

``` bash
    apt-get install zsh
    sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```



### 启用root

``` bash
    sudo passwd root
    vim /etc/ssh/sshd_config
    把这行修改为“PermitRootLogin yes
```
### ssh 无密码登录

``` bash
    ssh-keygen -t rsa 
    vim .ssh/authorized_keys
    chmod 600 .ssh/authorized_keys
    chmod 700 -R .ssh 
```
### 给予某个用户权限某个用户权限
```
 chown -R jenkins:jenkins /data/app/jar/
```

### curl 模拟提交文件
```
curl -F "file=@/Users/cong/Downloads/1.jpg" http://localhost:8081/upload/test
```

## 运维命令


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

### 备份数据库脚本
```
#!/bin/sh 
date=` date +%F`
echo $date
 mysqldump -h 172.0.0.1  -uroot -pcc cc  > /data/app/sql/cc-$date.sql
```

### redis常用配置
```
  daemonize yes  后台启动
  bind 0.0.0.0  绑定IP
  dir /var/lib/redis  修改数据文件存储位置

```


## 树莓派
### Mac 下将img 烧录到 内存卡中

``` bash
       sudo dd if=2016-03-18-raspbian-jessie-lite.img of=/dev/rdisk2 bs=32m
```


### 更换树莓派源

``` bash
   vim /etc/apt/sources.list
   注释官方源之后，加入下面这些
   deb http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ wheezy main contrib non-free rpi 
   deb-src http://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ wheezy main contrib non-free rpi 
   deb http://mirrors.aliyun.com/raspbian/raspbian/ wheezy main non-free contrib
   deb-src http://mirrors.aliyun.com/raspbian/raspbian/ wheezy main non-free contrib
```
## git 命令

### git 回退某个版本


有时候我们会要会退某一个版本,我们首先要找到我们要回退的版本号

```
 git log
 
```

然后我们找到要回退的版本号的，将本地分支reset需要回退的分支版本

```bash
git reset --hard   a0dd99cd7a00ac95d3e0a54d4b0a1a51db41d498

```

这时候我们如果git push，那么会一定会出现错误，所以需要用加上-f

```bash
git push -f

```
### git 查看远程分支
```
git branch -a
```
### git 拉取远程分支并创建本地分支
```
git checkout -b develop  remotes/origin/develop


```


