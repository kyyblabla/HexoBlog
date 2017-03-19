---
title: vue学习系列-vue结合Semantic-UI
date: 2017-03-19 20:30:57
tag:
  - vue
  - Semantic-UI
categories:
  - 前端
---
优秀的前端界面框架，语义化的标签更容易理解与记忆，不过相比于bootstap，组件还是少了一些。但可以在个人项目用来尝尝鲜，因为它足够漂亮和简约。

<!-- more -->

## 新鲜的Semantic-UI
优秀的前端界面框架，语义化的标签更容易理解与记忆，不过相比于bootstap，组件还是少了一些。但可以在个人项目用来尝尝鲜，因为它足够漂亮和简约。

## 与vue的结合
###  安装&编译
安装方法如下：
```
npm install semantic-ui --save
```

安装过程中会有一些选项提示，按照默认选择回车即可，这里不会将它安装到`node_modules`中，事实有些配置还是需要我们修改的，比如它就默认引用了来至于google的字体样式，这个显然是需要修改的，将修改后的代码打包后才能在项目中引用的。默认情况下，vue项目结构如下:

- build
- config
- dist
- src
- semantic
 - dist
 - src

Semantic-UI 使用gulp构建，确保本地全局安装过gulp，构建如下：
```
cd semantic
gulp build
```
编译好的文件存放在semantic/dist目录下，包括js、css等

### 引用

可以先对semantic目录配置别名:
```
resolve: {  
alias: {    
'src': path.resolve(__dirname, '../src'),    
'assets': path.resolve(__dirname, '../src/assets'),    
'components': path.resolve(__dirname, '../src/components'),    
'semantic': path.resolve(__dirname, '../semantic')
 }
},
```
在js与css中引用：
```
<script>
import  'semantic/dist/semantic'
</script>

<style lang="less">  
@import "~semantic/dist/semantic.min.css"; 
</style>
<scrip>
```

### 使用实例

Semantic-UI依赖于jQuery来调动组件。需要在ready函数中进行组件初始化。以下是一个下拉列表的示例。

```
<template>
<select id="s1" v-model="semeModel" class="ui dropdown"> 
 <option value="-1">defult</option> 
 <option value="1">value1</option>
</select>
</template>
<script>
export default{
  data{
     someModel:1
  }, 
  ready:function(){
     $('#s1').dropdown()     
    //这里 someModel 的值不会渲染到界面中，需要手动设置，这是一个很坑爹的地方，正在寻求解决方案。。。
    this.$nextTick(function () {  
         $('#s1').dropdown('set selected', this.someModel) 
    )}
}
</script>
```
在github上，Semantic-UI的vue组建貌似并不多（angular+bootstrap却是非常非常多），所以很多东西需要在使用过程中手动造车轮，比如轮播图、分页组件。本人自己造的勉强能用，还不敢拿出来献丑，准备磨炼一段在贡献出来。



