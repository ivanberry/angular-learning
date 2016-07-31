# *Angular*能干吗

*Angular*能强化我们标准化HTML文档，以下我们通过直接书写静态文档和*Angular*来强化实现HTMl，理解*Angular*起到的部分作用。从中，我们一步步能看出我们是如何将静态文件*Angular*化的。

```html
<ul>
  <li>
    <span>Nexus S</span>
    <p>
      Fast just got faster with Nexus S.
    </p>
  </li>
  <li>
    <span>Motorola XOOM™ with Wi-Fi</span>
    <p>
      The Next, Next Generation tablet.
    </p>
  </li>
</ul>
```

以上一个列表，很简单的结构，我们看看如何实现*Angular*化。

软件架构有多种模式，a采用的是*MVC*模式，通过解耦模型，视图和控制器达到*分治*和*复用*的目的。

## 视图与模板

*Angular*中，视图是通过绑定*model*的HTMl模板*template*，这就意味着，一旦我们的*model*有变动，视图层就会有对应更新:

```html
<html ng-app="phonecatApp">
<head>
  <script src="bower_components/angular/angular.js"></script>
  <script src="app.js"></script>
</head>
<body ng-controller="PhoneListController">
  <ul>
    <li ng-repeat="phone in phones">
      <span>{{phone.name}}</span>
      <p>{{phone.snippet}}</p>
    </li>
  </ul>
</body>
</html>
```

`ngRepeat` directive 和两个a表达式：

- *ng-repeat = "phone in phones"*: 属性就是一个循环输出，repeator告诉a，我们需要循环输出一个列表，其中变量数组为phones,自定义变量phone后，模板中就用它来代替，这和*Thinkphp*中的`volist`很是相似，还是比较容易理解的。

- *{{}}*: 模板取值语言

`ngController` directive，通过它我们添加了一个*PhoneListController*到*body*标签：

- *PhoneListController*接管整个区域,并暗示我们区域内的数据绑定跟我们这个控制器密切联系。

`ng-app="phonecatApp"` directive是我们的模块名，这个模块下右包含我们的控制器*PhoneListController*。

## 模型与控制器

```javascript
// Define the `phonecatApp` module
var phonecatApp = angular.module('phonecatApp',[]);

// Define the `PhoneListController` controller on the `phonecatApp` module
phonecatApp.controller('PhoneListController', function PhoneListController($scope) {
  $scope.phones = [
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
});
```

数据模型是一个简单的数组，它在控制器中实例化，控制器是一个传入*$scope*参数的构建函数。我们定义了控制器，并将它注册到了*phonecatApp*模块。尽管到现在为止，控制器并没有干啥，但是它却是非常重要的角色，它提供了我们数据的上下文，并允许建立模型与视图件的数据绑定：

- *PhoneListController*控制器使得*phone*数据绑定到了*$scope*上，并注入到了我们控制器中，这个作用域继承于根作用域的，这个作用域在绑定了对应控制器的标签区域都是可访问的。

## 作用域

作用域是JS中的一个基础知识，同样在*Angular*中也是关键的一部分，它是联系视图模板，模型和控制器的*胶水*, 通过作用域*Angular*可以保持模型和视图的分离，它们之间不能之间访问，但是通过作用域作为媒体却是能够实现同步的绑定。

![angular中的作用域](https://docs.angularjs.org/img/tutorial/tutorial_02.png)







