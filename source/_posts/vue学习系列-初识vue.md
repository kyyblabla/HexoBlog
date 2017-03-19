---
title: vue学习系列-初识vue
tag:
  - vue
categories:
  - 前端
date: 2017-03-19 20:32:27
---

几个月前还沉浸在AngularJS的强大之中，最近才猛然发现vue已经火热到不行。赶紧学习一下。

<!-- more -->

## 写在前面

几个月前还沉浸在AngularJS的强大之中，最近才猛然发现vue已经火热到不行。赶紧学习一下。

目前版本为2.x，相对于1.x有一定的改变。1.x使用较为广泛一些，能查的资料多一些，还是从1.x开始啃吧。另外值得一说的是，vue-router作为与单页应用息息相关的一个模块，2.x也是相对于1.x有着所谓的“破坏性”升级，即不能向下兼容。当时没注意，还是踩了一个深深的坑，所以在此**建议**无论是vue还是vue-router都从从1.x开始搞起，摸清1.x的套路再往2.x升级也不迟，至少不至于拿着2.x问题去找1.x的答案。

## vue-cli 安装
vue似乎生来伴随着webpack，官方也提供 `vue-cli`用于构建vue项目骨架， 安装方法如下：
```shell
npm install vue-cli -g
```
使用`vue -V`可以查看当前版本：
```shell
vue -V
2.3.1
```
可以看到当前版本为2.3.1，则默认构建2.x版本的vue项目骨架。

## 初始化项目骨架

使用一下命令极客初始化：

```
vue init webpack vue-test
```
但是前面说过，默认会构建2.x版本，于是构建1.x版本的命令如下：
```
vue init webpack#1.0 vue-test
```
之后的项目初始化`README.md`已经写得很清楚了，可以参照步骤去做。

## 一些必要的构建配置

项目根目录下build文件包含项目构建相关的配置与脚本，一般情况下不需要改动太多东西，安装默认配置即可。有一些必要的东西，比如JQuery的全局配置,可以再webpack.base.conf.js的plugins属性下加入：
```  
new webpack.ProvidePlugin({      
$: 'jquery',
'jQuery': 'jquery' })  
}
```
如果需要根据不用环境的参数（如测试环境与生产环境的API地址）可以再对环境的webpack config文件的plugins加入：

```
new webpack.DefinePlugin({  
'process.env': config.dev.env,  
ENV: config.dev.env //这里可以配置任何根据环境变化的参数
}
)
```

## 结语

很简单的一个开始，vue虽然学的时间不长，但也是从AngularJS这种重量级项目下转过来的，vue的很多地方都可以`无师自通`，当然遇到的坑也在所难免，会在以后一一道来，另外学习vue的过程中还结合了另外一套ui框架[semantic-ui](http://www.semantic-ui.cn/)，即语义化ui，相较于bootstrap，有一些吸引人的地方当然也是bootstrap用的有点烦了^_^，想尝尝鲜。

