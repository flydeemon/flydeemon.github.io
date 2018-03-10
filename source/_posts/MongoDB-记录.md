---
title: MongoDB 记录
date: 2017-08-31 21:25:13
tags:
categories: MongoDB
---
# mongoDB 记录

1.开启你的 mongodb 服务

```
mongod -dbpath "D:\Program Files\MongoDB\data\db" 数据库路径
-logpath "D:\Program Files\MongoDB\data\log\MongoDB.log" log的路径 
-logappend 追加文件
-serviceName "MongoDB" 服务名
-auth 是否需要用户验证
-install 安装服务
```

2.连接 mongodb

```
shell> mongo  默认链接本地数据库

shell> mongo://user:pwd@host:port/db 连接远程数据库
```

3.mongoose.model 默认会帮你的集合名加复数形式(s)，所以你必须正确让 mongoose 认识你指定的集合名

` new Schama({}, {collection: '你的集合名'}) `

or

` schema.set('collection', 'actor') `


# CentOS7 下安装 Mongodb 3.6.3

```
// 1.下载解压
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-3.6.3.tgz
tar-zxvf zxvf mongodb-linux-x86_64-3.6.3.tgz

// 2.移动到 /usr/local/下
rm -f mongodb-linux-x86_64-3.6.3.tgz
mv mongodb-linux-x86_64-3.6.3 /usr/local/mongodb
cd /usr/local/mongodb

// 3.建立数据库存储路径和配置文件
mkdir data
mkdir data/db
mkdir data/logs
vim mongod.conf

```

设置环境变量
```
vim /etc/profile
# mongodb
export MONGODB_HOME=/usr/local/mongodb
export PATH=$MONGODB_HOME/bin:$PATH
```

配置文件
```
	dbpath=/usr/local/mongodb/data/db
	logpath=/usr/local/mongodb/data/logs/mongodb.log #这个要指定文件
	fork=true
	logappend=true #日志追加
	port=27017
	# auth=true 先注释掉
```

设置为服务必须在linux的/etc/init.d/下建立一个mongod的初始化启动文件
```
cd /etc/init.d/
touch mongod
chmod +x mongod
vim mongod

// 添加服务
chkconfig --add mongod
chkconfig mongod on
service mongod start
```

启动文件
```
#!/bin/bash  
#chkconfig: 2345 80 90  
#description: mongodb  
start() {  
	/usr/local/mongodb/bin/mongod -f /usr/local/mongodb/mongod.conf  
}  
  
stop() {  
    /usr/local/mongodb/bin/mongod -f /usr/local/mongodb/mongod.conf --shutdown  
}  
case "$1" in  
  start)  
 start  
 ;;  
  
stop)  
 stop  
 ;;  
  
restart)  
 stop  
 start  
 ;;  
  *)  
 echo  
$"Usage: $0 {start|stop|restart}"  
 exit 1  
esac
```


# Mongodb 登录授权

```
use admin
db.createUser({user:"master",pwd:"master",roles:[{"role":"userAdminAnyDatabase","db":"admin"}]})

// 退出 mongo 停止 mongod 服务
// 修改 mongod.conf 使用 bind_ip=0.0.0.0 auth=true
// 重启 mongod 服务

use admin
db.auth('master','master') 
use test
db.createUser({user:"demo",pwd:"demo",roles:[{"role":"readWrite","db":"test"}]})
db.auth('demo', 'demo')
```

最后是远程连接

```
mongo host:port/db -u user -p pwd
```