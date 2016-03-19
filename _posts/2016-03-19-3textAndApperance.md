---
layout: post
title: knockoutjs三  text和apperance的绑定
---
#knockoutjs三  text和apperance的绑定

 由于换了工作，要熟悉新的工作环境，所以没有什么时间做自己的事情，今天开始重新开始继续下面的文章，争取尽早写完
 

	中间有一部分computed绑定没有写入文章，那是比较高级的用法，开发基本用不到，我在github中有例子，大家想了解
	可以自己去看看。
首先是visible绑定：
``` 	<li class="list-group-item-danger">
            <div data-bind="visible: shouldShowMessage">
                你能看到
            </div>
        </li>
        
        
        self.shouldShowMessage = ko.observable(true);
        self.shouldShowMessage1 = ko.observable(false);
        self.shouldShowMessage2 = ko.observable(0);
        self.shouldShowMessage3 = ko.observable(undefined);
        self.shouldShowMessage4 = ko.observable(null);
        self.shouldShowMessage5 = ko.observable("");
```
visible后面的值是类false的值那么该元素就不会显示，比如false，0，undefined，null，“”都是类false的值
相反，是类true的值就会显示该元素。visible后面的不仅仅可以是一个observable的值，也可以是一个function，但是记得返回值，不然返回的是undefined，永远不会显示;
```

 <li class="list-group-item-danger">
            <div data-bind="visible: shouldShowMessage5()">
                你能看到5
            </div>
        </li>
        self.shouldShowMessage5 = function(){
        	//return 1;
        };
```
方法绑定要加（），不然showShowMessage5返回的是一个function对象，永远是true。


第二个是text绑定，text就是绑定一个值，
```
   <!--绑定会覆盖你节点中的值-->
    <p class="text-muted text-warning">这是第<span data-bind="text:index">1</span>个例子</p>
    <!--该处绑定的是一个对象，那么就会调用他的toString方法，返回一个字符串，进行绑定-->
```
切记绑定会覆盖你节点中的值，你要是想加入一点别的字段，可以在js中处理
```
model.index("6")//就像jQuery中的赋值一样改变这个值。


```
其他还有些简单的用法可以看我的例子，
第三介绍属性绑定;
```

<!--html绑定，需要确保是安全的html，而不是别人插入你数据库的，防止脚本注入攻击-->
    <div data-bind="html: details"></div>
    <!--css绑定-->
    <!--可以添加几个class，当后面条件满足时就起作用-->
    <!--不符合JavaScript命名规范的css变量名需要加上''，不然会失效-->
    <p data-bind="css: {'text-danger text-center':price()>50 }">价格高于50就显示红色</p>
    <a class="btn btn-danger" id="upPrice">提高价格</a>
    <a class="btn btn-danger" id="downPrice">降低价格</a>
    <!--style绑定-->
    <p data-bind="style:{color:price() >50?'red ':'black',textDecoration: 'line-through' }">价格高于50就显示红色</p>
    <!--attr绑定-->
    <a data-bind="attr:{'id':attr().id,'title':attr().title,'href':attr().href}">属性绑定,点击可直通百度</a>
    
  ```
  属性绑定最重要的是要记住不符合JavaScript命名规范的css变量名需要加上''，不然会失效，比如background-color就需要加‘’，不然会绑定失败。
  
  
  这次的东西很简单，很抱歉很久没有更新，新的一年希望大家进步不断，工作顺利！！！
  代码托管在https://github.com/lushunming/knockoutJSDemo.git可以直接克隆。

