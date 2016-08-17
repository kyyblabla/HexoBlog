---
title: Hexo构建Github博客
date: 2016-03-04 09:16:54
tags:
- hexo
- nodejs
- 博客
categories: 
- nodejs

---
是一款简洁好用的博客工具， 通过Mardown文件生成静态文件构成的站点，可以让开发者发布博客时更关注博客本身。通过简单的配置，Hexo可将静态博客站点部署到Github上。例如本博客就是全部由Hexo生成并部署到Github上的。

<!-- more -->
## Hexo ##
[Hexo](http://hexo.io "heo")是一款简洁好用的博客工具，通过Mardown文件生成静态文件构成的站点，可以让开发者发布博客时更关注博客本身。通过简单的配置，Hexo可将静态博客站点部署到Github上。例如本博客就是全部由Hexo生成并部署到Github上的。

## Github博客 ##
Github提供免费的博客空间，开通博客很简单，就是创建一个名称如下形式的代码仓库：
用户名.github.io
如:kyyblabla.github.io。往改仓库下提交静态文件即可作为博客内容。

## Hexo部署到Github ##
将博客仓库地址配置到Hexo的配置文件_config.yml下：

```xml
deploy:
  type: git
  repository: git@github.com:kyyblabla/kyyblabla.github.io.git
  branch: master
```

添加用来部署到Git的插件：
```
npm install hexo-deployer-git --save
```

在Github上配置自己的公钥后，通过命令即可部署到github：
```
hexo d
```



