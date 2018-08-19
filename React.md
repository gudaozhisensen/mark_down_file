#react


```
//react head
<head>
    <script src="../build/react.js"></script>
    <script src="../build/react-dom.js"></script>
    <script src="../build/browser.min.js"></script>
  </head>
```

`<script>` 标签的 `type `属性为` text/babel`

凡是使用 `JSX` 的地方，都要加上 `type="text/babel"`



####state和props
1. `state`是组件自己管理数据，控制自己的状态，可变；
2. `props`是外部传入的数据参数，不可变；
3. 没有`state`的叫做无状态组件，有`state`的叫做有状态组件；
4. 多用`props`，少用`state`。也就是多写无状态组件。

***
需要定义`state`来更新和修改数据。而子组件只能通过`props`来传递数据。
在子组件中；我们可以使用 `this.props.name` 来获取父组件的`state`值；
在父组件中使用`state`;并通过子组件上使用`this.props`将其传递到子组件上；
在`render`函数中；我们设置`name`和`site`来获取父组件传递过来的数据；
`props`相当于组件的数据流；它总是会从父组件向下传递至所有的子组件；

***
1：组件间的状态传递；
（props） `props`从父组件到子组建的数据传递
2:组件的内部状态；
(state)  `state`只能定义在组件内部；定义组件的自己的状态，`React`中的数据流是单向的；只会从父组件传递到子组件；属于`props`；


每个`component`里基本由二个部分组成：
```	
组件类本体
	…
	 render 的方法返回一个嵌套结构的视图
	render（）{
	….
	Return(
	<div></div>
	….
	);
	}

```

####`constructor`和`super()`
输入的数据通过 `this.props `传入 `render() `方法。
如果你用到了`constructor`就必须写`super()`,是用来初始化this的，可以绑定事件到`this`上;
`super(props)`的目的：在`constructor`中可以使用`this.props`
如果你在`constructor`中要使用`this.props`,就必须给super加参数：`super(props)`；
（无论有没有`constructor`，在`render`中`this.props`都是可以使用的，这是`React`自动附带的；）
如果没用到`constructor`,是可以不写的

