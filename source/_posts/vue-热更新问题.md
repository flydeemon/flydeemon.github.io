---
title: vue-热更新问题
date: 2017-09-05 20:12:18
tags:
categories: vue
---

最近调试 vue 项目遇到一个热更新的问题

```
HMR] Update check failed: Error: Manifest request to 
/0ca55ad0f6c9c867e01c.hot-update.json timed out. 
at XMLHttpRequest.request.onreadystatechange 
(http://localhost:8080/app.js:39:22)
```

这个问题是 webpack 更新版本导致的
webpack-dev-middleware: ^1.12.0 此模板没有Webpack 3的官方支持
所以要返回 "webpack-dev-middleware": "~1.11.0"

并且注释

```
+// compiler.plugin('compilation', function (compilation) {
 +//   compilation.plugin('html-webpack-plugin-after-emit', function (data, cb) {
 +//     hotMiddleware.publish({ action: 'reload' })
 +//     cb()
 +//   })
```