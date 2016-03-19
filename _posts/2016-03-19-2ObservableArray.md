---
layout: post
title: knockoutjs二   observableArray的使用
---
#knockoutjs二   observableArray的使用

 上次忘记讲了，viewmodel可以有好几仲形式。
1. ``` var viewModel={}``` 这样写对应的绑定为	```ko.applyBindings(viewModel);```
2. ```function ViewModel(){}```这样写的把绑定方式是 ``` var viewMode=new ViewModel(); ko.applyBindings(viewModel);```

obervableArray的用法如下：

```
<div data-bind="foreach:{data:myObservableArray, as :'item'} ">
			<div data-bind="text:item"></div>
		</div>
		<script>
			function Model() {
				var self = this;
				self.myObservableArray = ko.observableArray('');
				self.myObservableArray.push('Some value');
				self.myObservableArray.push('Some ');
			}
			var model = new Model();
			ko.applyBindings(model);
		</script>```
```

在使用时我们在model的内部可以使用this.myObservableArray 来获取这个操作进行操作，在model的外部则可以使用model.myObservableArray来获取这个方法进行操作。其实model.myObservableArray这是一个方法，所以其实dom中绑定是可以这样```<div data-bind="foreach:{data:myObservableArray(), as :'item'} ">```
如下图

![这里写图片描述](http://img.blog.csdn.net/20151230192620973)
这证明了他是一个方法。
而我用console给他添加了一个元素。
![这里写图片描述](http://img.blog.csdn.net/20151230192639729)
就立即在view中显示了。如下：
![改变后的值](http://img.blog.csdn.net/20151230192537253)
这次的例子中用到了foreach绑定，先不介绍，只要把它当做一个循环就可以了。
可以在obervableArray中初始化数据的，不一定要push进去

```
	var anotherObservableArray = ko.observableArray([
    { name: "Bungle", type: "Bear" },
    { name: "George", type: "Hippo" },
    { name: "Zippy", type: "Unknown" }
]);
```
可以用操作数组的方式操作它,比如：
```
	model.myObservableArray.push("1");
					alert('The length of the array is ' + model.myObservableArray().length);
					alert('The first element is ' + model.myObservableArray()[0]);
					model.myObservableArray.splice(0, 1);
					alert('The length of the array is ' + model.myObservableArray().length);
					alert('The first element is ' + model.myObservableArray()[0]);
```
官网说model.myObservableArray.push("1");这个方法比这样调用原生js 的myObservableArray().push('1')的array的潜在push要好，但是我发现调用myObservableArray().push('1')这个方法调用后view不会改变，也即是说根本没有通知到view进行改变（不知道是不是一个bug）。
 - knockoutjs给出了对于observableArray的这些操作：pop, push, shift, unshift, reverse, sort, splice。就个原生js中数组的操作一样。
 - knockoutjs还增加了一些有用的方法如：remove and removeAll，
 - remove（）中传入一个方法如：remove( function (item) { return item.age < 18; } ) 就是去除所有item的age小于18的，并返回一个剩余元素的数组。
  -removeAll( ['Chad', 132, undefined] )：就是去除所有传入的数组中的元素，并返回一个包含剩余元素的数组。
代码托管在https://github.com/lushunming/knockoutJSDemo.git可以直接克隆。
