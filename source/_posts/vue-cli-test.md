---
title: vue-cli 测试报错
date: 2017-08-25 16:37:40
tags: 
categories: vue
---
# 关于 vue-cli e2e 和 unit 测试报错的问题

1.` npm run e2e ` 报错

* 发现 ` Error retrieving a new session from the selenium server ` 的错误


* 解决办法: 更新 chromedriver, selenium-server


` npm install --save-dev chromedriver selenium-server `


***

2.` npm run unit ` 报错

* 发现类似这样的错误

``` 
	WARN [plugin]: Error during loading "karma-phantomjs-launcher" plugin:
		Path must be a string. Received null
	...

	WARN [launcher]: Can not load "PhantomJS", it is not registered!
		Perhaps you are missing some plugin?
```

* 解决办法: 安装 phantomjs-prebuilt


` npm install --save-dev phantomjs-prebuilt `