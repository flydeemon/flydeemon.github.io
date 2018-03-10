---
title: vue-cli eslint 问题
date: 2017-08-16 11:21:13
tags:
categories: vue
---
# 关于 vue-cli 带给我们的困扰

vue-cli 自带的 eslint 配置的代码风格和我们平时使用的风格不一样

主要是两个：

* 缩进是两个空格
* 在函数的括号前面必须有一个空格

这样就会带给我们一些编码上的困扰，接下来我们来看如何解决它！

## 解决方法

1.修改该文件 `.eslintrc.js`, 加入代码修改缩进为4个空格和修改函数的括号前面不需带空格

![pic](pm1.png)

2.确保 `src` 下的文件缩进风格是 4 个 space (我的编辑器是 sublime)

![pic](pm2.png)

## 如果我不想使用 eslint 怎么办？

直接注释图下的代码， `build/webpack.base.conf.js` 路径下

![pic](pm3.png)
