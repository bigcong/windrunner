title: "\_树莓派一些总结"
tags:
  - 教程
categories:
  - 总结
date: 2017-04-14 17:13:00
---


## 总结

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

