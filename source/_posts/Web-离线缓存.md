---
title: Web 离线缓存
date: 2017-04-20 19:43:59
tags:
categories: Web
---

# 一、H5之前如何实现存储

## 1.关于存储

  * cache
  * 磁盘文件
  * 数据库
  * 内存

## 2.H5之前

### cookies

  * http请求头上会带着
  * 大小4K（每个域名）
  * 主Domain污染

### UserData

  * 只有IE支持(5.0 -- 9.0)
  * XML文件
  * 64K

### 目标

  * 解决4K大小问题
  * 解决请求头常带存储信息的问题
  * 解决关系型存储的问题
  * 跨浏览器

# 二、H5常见的存储方式

## 1.localstorage && sessionstorage

  * 存储形式：key --> value
  * 过期：永久存储，永不失效，除非手动删除
  * 大小：官方文档是每个域名5M

### 常用API

  * getItem(key)
  * setItem(key, value)
  * removeItem(key)
  * key(index)
  * clear()

### 区别

  * localstorage 是全局的
  * sessionstorage 是会话级别，当关闭标签会消失
  * 都可以存数组、json、图片、脚本、样式文件

### 注意事项

  * 使用前要判断浏览器是否支持（用window.localstorage和localstorage和.set()看是否报错)
  * 写数据时，需要异常处理，避免超出容量抛错
  * 避免把敏感的信息存入 localstorage
  * key 的唯一性
  * IOS 无痕浏览会停止存储

### 使用限制

  * 存储更新策略，过期控制
  * 子域名之间不能共享存储数据（借助 postMessage 跨域）
  * 超出存储大小之后如何存储（LRU，FIFO算法）
  * server 端如何取到 (get,post请求)

### 使用场景

  * 利用本地数据，减少网络传输
  * 弱网络环境下，高延迟，低带宽，尽量把数据本地化

## 2.IndexedDB && Web SQL

  * 一种能在浏览器中持久地存储结构化数据的数据库，并且为 Web应用提供了丰富的查询能力
  * Web SQL：W3C已经不再支持

### 存储结构

IndexedDB 是安于命分配独立空间，一个独立域名下可以创建多个数据库，每个数据库可以创建多个对象存储空间（表），一个对象存储空间可以存储多个对象数据

### 功能

  * 增删改查
  * 事务
  * 游标
  * 索引

## 3.application cache

### 什么是离线缓存（offline application）

它可以让 Web应用在离线的情况下继续使用，通过 manifest 文件知名需要缓存的资源

### 检测是否在线

navigator.onLine

### 如何引用

  * 在 HTML 页面中应用 manifest 文件 `<html manifest="sample.appcache">`
  * 在 apche 服务器中 conf 目录下 mime.type 文件添加  text/cache-manifest 标识

### 如何更新

  * 如何有修改资源文件，必须通过修改 manifest 文件来刷新被缓存的文件列表

### 优势

  * 完全离线
  * 资源被缓存，加载更快
  * 减低 server 负载

### 缺陷

  * 含有 manifest 属性的当前请求页无论如何都会被缓存
  * 更新需要建立在 manifest 文件的更新，文件更新后是需要在此刷新（需要2此刷新才能获取新资源）
  * 更新是全局性的，无法单独更新某个文件（无法单点更新）
  * 对于链接的参数变化是敏感的，任何一个参数的修改都会被（master）重新缓存（重复缓存含参页面） index.html 和 index.html?renew=1 会被认为是不同的文件，分别缓存

### 使用场景

  * 单地址的页面
  * 对实时性要求不高的业务
  * 离线 webapp