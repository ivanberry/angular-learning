# 开篇

通过AngularJS的官方教程一步一步学习，这一章节主要是环境和资源的管理，没有从本质上接触库

```html
<!doctyle html>
<html lang='en' ng-app>
    <head>
        <meta charset='utf-8' >
        <title>My HTML File</title>
        <link rel='depsss'>
    </head>
    <body>
    <p> Nothing {{'yet' + '!'}}</p>
    </body>
</html>
```

上面是第0章中的HTML文件，跟我们普通项目没有什么差别，不过唯一一点是在HTML元素上多了要给`ng-app`属性，对*Angular*有了解的同学应该对这个*ng-*前缀有点认识，对于一个工程，有这么个前缀，就意味着这是一个*Angular*工程了。再往下看，我们的段落元素标签中，有一个看起来很奇怪的东西，其实对模板语言有了解的话，这和*大胡子*等模板语言无差。

`ng-app`是*Angular*中的一个*directive*称为*ngApp*(这里对于自定义属性是采用的*kebab-case*,而对应a中为*camelCase*命名)，这个属性的标签区域被认为是整个应用区域的*根元素*，这在之后作用域等等都是有很大关联的。


理所当然，我们需要引入*a.js*,引入后，它会注册一个回调函数，当我们的HTMl文档下载完成后就会触发，这一点跟*jquery*有点像，理解起来不难，而回掉触发的结果是*a*寻找*ngApp*,一旦，它就将建立一个与*a*对应的关系，这个区域内，*a*就接管。

`ng-app`被找到后，就会有个初始化的过程：

1. 依赖注入
2. 根作用域创建,建立应用上下文
3. a功能开始：视图，绑定等等

之后，就是交互了，一些事件可能会触发，而引起*model*的变化，当此类事件发生时，a就会作为对应的反应，更新对应的视图。

![简单流程](https://docs.angularjs.org/img/tutorial/tutorial_00.png)






