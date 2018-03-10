---
title: Node 记录
date: 2017-08-31 21:30:28
tags: Node
categories: Node
---
当你定义的CSS中有position属性值为absolute、relative或fixed，
用z-index此取值方可生效。


# CentOS7 安装 node.js 8.9.4

```
wget http://nodejs.org/dist/v8.9.4/node-v8.9.4-linux-x64.tar.gz  
tar zxvf node-v8.9.4-linux-x64.tar.gz
mv node-v8.9.4-linux-x64 /usr/local/
mv /usr/local/node-v8.9.4-linux-x64/ /usr/local/node

vim /etc/profile
# nodejs
export NODE_HOME=/usr/local/node
export PATH=$NODE_HOME/bin:$PATH
```