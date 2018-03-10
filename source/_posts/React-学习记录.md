---
title: React 学习记录
date: 2017-04-20 15:23:34
tags:
categories: react
---
# 一、环境搭建

1.使用 git 管理仓库

	git init

2.使用 npm 管理项目

	npm init

3.使用 react 库编写

	npm install --save-dev react react-dom

4.使用 ES2015 语法

	npm install --save-dev babel-core babel-loader babelify babel-preset-es2015 babel-preset-react

5.使用 webpack 构建模块

	npm install -g webpack webpack-dev-server
	npm install --save-dev webpack webpack-dev-server

6.启动项目

	webpack 编译文件，需要在浏览器打开本地 index.html
	webpack-dev-server --content-base --inline --hot 实时编译，浏览器地址 http://localhsot:8080

# 二、React 笔记

1.组件中定义 this.xxx 时要在 super() 后定义

2.render 中的 this 指向当前类的实例

3.render 中的 this.props[xxx] 的值指向在组件类被调用的地方所赋的值

4.当在 render 中需要遍历时，Array.prototype.map() 需要为 html 元素设置唯一 key。可以使用 React.Children.map() 遍历组件中的子元素

5.组件类的类名首字母必须是大写，组件类只能包含一个顶层标签

6.JSX 语法中，标签中的 class 和 for 属性分别写成 className 和 htmlFor，否则会报错

7.在组件中的监听器需要都需要进行绑定 this.handle = this.handle.bind(this) 否则监听器中的 this 将指向 null

8.需要获取真实的标签节点需要 this.refs.xxx 并在组件中定义该属性 `<div ref="xxx"></div>`

9.在 ES6 中不需要重写 getInitialState() 直接在构造器中定义 this.state = xxx

10.区分 this.props 和 this.state，this.props 是一旦定义就不会发生改变；this.state 是与用户交互的状态，随时会改变