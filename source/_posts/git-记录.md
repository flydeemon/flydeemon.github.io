---
title: git 记录
date: 2018-03-07 14:45:01
tags: git
categories: git
---

# Git 服务器安装

```
yum install git -y
useradd git
passwd git

cd /var
mkdir www
chown -R git:git /var/www
chmod 774 /var/www
cd www
git init --bare demo.git
```

### 禁用 git 用户 shell 登录

```
vim /etc/passwd

git:x:1000:1000::/home/git:/usr/bin/git-shell
```

### 公钥

```
cd /home/git
mkdir .ssh
chown -R git:git .ssh
touch .ssh/authorized_keys

// 加入公钥
vim .ssh/authorized_keys

chmod 700 .ssh
chmod 600 .ssh/authorized_keys
```

### 自动同步到站点目录

```
cd /var/www/demo.git/hooks
vim post-receive
chown git:git post-receive
chmod +x post-receive
```

post-receive 文件

```
#!/bin/bash
git --work-tree=/var/www chckout -f
```


### git 客户端

```
git clone git@host:/var/www/demo.git

git add .
git commit -m ""
git push
```