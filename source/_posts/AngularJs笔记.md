---
title: AngularJs 笔记
tags:
  - angularjs
  - javascript
  - xx
categories:
  - ds

---
### 指令directive
指令`directive`的作用就是实现标签的语义化，扩展标签的功能与属性
如下定义了一个标签指令`hahaha`：
```javascript
app.directive('hahaha', function() {
			var d = {
				restrict: "E",
				replace: true, //替换掉原来的标签名称为模板内是我标签名
				transclude: true, //保存标签内容
				template: "<div><p>哈哈</p><div ng-transclude></div></div>", // div ng-transclude 表示用div标签包含原来的内容
			};
			return d;
		});
```
`template`属性用来输出替换原有标签`hahaha`,html定义为：
```xml
<hahaha>
    <span>文字1</span>
    <span>文字2</span>
</hahaha>
```
输出后的html内容为：
```xml
<div><p>哈哈</p>
	<div ng-transclude="">
    	<span class="ng-scope">文字1</span>
    	<span class="ng-scope">文字2</span>
	</div>
</div>
```

### 监控视图内容变化
对于某些动态页面，模型值改变引起视图改变，如本博客在后台编辑过程中，可实时预览内容显示效果。需要在视图渲染完毕后调用highlight方法进行代着色。
定义指令`onFinishRenderPost`：
```javascript
app.directive('onFinishRenderPost', function($timeout) {
	return {
		restrict: 'A',
		link: function($scope, $el, $attrs) {
			$scope.$watch(
				function() {
					return $el[0].innerText; //el表示当前监控的元素，可监控文本内容变化
				},
				function(newValue, oldValue) {
					if (newValue !== oldValue) {
						//数据改变,说明内容加载完毕
						//highlightCodeUtil.hlight(""); //这里进行代码高亮操作
					}
				}
			);
		}
	};
});
```
使用指令：
```xml
<div class="post-context" on-finish-render-post ng-bind-html="post.context|to_html">
</div>
```

### 模型值输出为html
通过`ng-bind-html`标签可以将模型内容作为html输出,直接使用`<div ng-bind-html="html">`会报错：

> Error: [$sce:unsafe] Attempting to use an unsafe value in a safe context.

这里需要使用`$sce.trustAsHtml(text)`将模型值进行转化
可通过定义过滤器避免报错：
```javascript
app.filter('to_html', ['$sce',
	function($sce) {
		return function(text) {
			return $sce.trustAsHtml(text);
		}
	}
]);
```
```xml
<div ng-bind-html="html|to_html">
</div>
```
也可定义函数：
```javascript
$scope.toHtml = function(html) {
	return $sce.trustAsHtml(html);
}
```
```xml
<div ng-bind-html="toHtml(html)">
</div>
```

### iframe路径控制
使用`ng-src`加载路径，不可直接使用原始路径，需通过`$sce.trustAsResourceUrl`转化原始路径：
```javascript
$scope.trustSrc = function(url) {
    return $sce.trustAsResourceUrl(url);
}
```
在iframe中使用转换函数
```xml
<iframe ng-src="{{trustSrc(url)}}" width="300" height="200">
</iframe>
```