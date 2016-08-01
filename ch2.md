# 组件化

上一章节我们学到了通过控制器和视图模板讲静态HTMl页面转变成了动态视图，这是*SPA*应用中非常常见的，替代服务端生成静态文件输出为客户端接管，并实现动态交互，即时更新模型中数据的变化，这一般是由用户交互产生的变化。模板（视图中包含数据绑定和展示逻辑），控制器则是为视图模板提供行为和逻辑的上下文环境。

以上论述，我们应该还有更大的改进部分：

1. 如果我们需要复用视图呢？
2. 联系控制器和视图的作用域并没有独立出来。

## 复用组件

模板+控制器是一种常用的软件开发模式，*Angular*更是提供了简单有效的组合二者，使得成为可复用单元，并有独立的入口，称之为组件。另外，*Angular*还为每一个组件实例创建了独立的作用域，这意味着应用其他部分不会对我们的组件有原型继承等风险。关于组件化是一个很大的话题，不是简简单单就能概述清楚，需要深入的学习。

通过*Angular* module的*component*方法，我们能创建组件。需要我们提供的是组件名字和组件定义对象(简称CDO)，我们依然按照之前的命名规则，组件(属于*directive*)采用驼峰命名，而HTML文档的索引则采用*kebab-case*命名。

最简单CDO可以只包括模板和控制器(其实对于更加简单的应用，连控制器都可以不用，*Angular*会创建一个默认的控制器)，让我们来看个简单的例子：

```javascript
angular
    .module('myApp')
    .component('greetUser', {
        template: 'Hello, {{$ctrl.user}}',
        controller: function GreetUserController() {
            this.user = 'world';
        }
    });
```

上面的例子很简单，它在*myApp*模块下有个名为*greetUse*组件，并拥有模板和控制器，当我们在HTML文档中实例化组件时：

```html
<greet-user></greet-user>
```

*Angular*通过组件的模板，将它拓展为DOM树，但是这里有个新东西*$ctrl*，它是什么呢？

有不同的利用使得我们不要直接对作用域进行操作，我们应该通过控制器实例操作它，比如为控制器添加属性和方法等等(控制器中的this)，而不是直接操作作用域。从模板中，我们可以通过*$ctrl*来访问控制器，之后会有更多的例子可以观察到。

## 组件使用

我们利用新学习的技能来实践下组件化：

*app/index.html*:

```html
<html ng-app="phonecatApp">
<head>
    <script src="angular.js"></script>
    <script src="app.js"></script>
    <script src="phone-list.component.js"></script>
</head>
<body>
    // use a custom component to render a list of phones
    <phone-list></phone-list>
</body>
</html>
```

*app/app.js*:

```js
// define the *phonecatApp* module
angular.module('phonecatApp', []);
```

*app/phone-list.component.js*:

```js
// 组件`phoneList`注册，包括它关联的控制器和视图模板
angular
    .module('phonecatApp')
    .component('phoneList', {
        template:
            '<ul>' +
                '<li ng-repeat="phone in $ctrl.phones">' +
                    '<span>{{phone.name}}</span>' +
                    '<p>{{phone.snippet}}</p>' +
                '</li>' +
            '</ul>',
        controller: function phoneListController() {
            this.phones = [
                {
                name: 'Nexus S',
                snippet: 'Fast just got faster with Nexus S.'
                }, {
                name: 'Motorola XOOM™ with Wi-Fi',
                snippet: 'The Next, Next Generation tablet.'
                }, {
                name: 'MOTOROLA XOOM™',
                snippet: 'The Next, Next Generation tablet.'
                }
            ];
        }
    });

```

看看我们都应用了什么新知识：

1. 手机列表能够复用了，只要在页面任何地方利用`<phone-list></phone-list`实例化就好。
2. 我们主要视图页面更加清晰，通过它我们就能知道页面会展示一个*手机列表*的视图。
3. 组件跟外部环境是相对独立的，我们不用担心会破坏什么。
4. 组件测试也变得简单

![组件实例1](https://docs.angularjs.org/img/tutorial/tutorial_03.png)

图中，我们能可视化观察到很多知识点：作用域初始化，作用域继承，模块组件之间的关系以及*directive ngRepeat*的应用。结合图形，对*Angular*理解能更加深入。



