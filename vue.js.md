#vue.js

####安装vue.js步骤

先安装`node.js`
在命令行中键入 `npm -v`

####查看版本
####升级 npm
`cnpm install npm -g`

安装vue脚手架
`cnpm install vue-cli -g`

新建项目
`vue init webpack my-project`

安装router
`cnpm install vue-router --save`
安装项目依赖
`cd my-project`
`npm install`
启动项目
`npm run dev`

####new一个vue对象时可以设置属性

`data`：儲存數據
`methods`：写方法function的地方
`watch`：监听
`computed`:计算属性
`computed`相当于属性的一个实时计算，如果实时计算里关联了对象，那么当对象的某个值改变的时候，同事会出发实时计算。


数据渲染：`{{}}`  `v-text:`  `v-html`
控制模块隐藏：`v-if`  `v-show`

循环：`v-for`
事件绑定：`v-on`  缩略@
属性绑定：`v-bind` 缩略：
进行数据双向绑定:`v-model`

####由于 JavaScript 的限制，Vue 不能检测以下变动的数组：
1. 当你利用索引直接设置一个项时，例如：`vm.items[indexOfItem] = newValue`
可用这个方法解决：
`Vue.set(example1.items, indexOfItem, newValue)`

2. 当你修改数组的长度时，例如：`vm.items.length = newLength`
可用这个方法解决：
`example1.items.splice(newLength)`

####`V-model`的3个修饰符
`V-model.lazy`=  惰性更新，移出输入框时才更新
`V-model.trim`=    消除空格
`V-model.number`=    转化成成数字

`V-model`能用到`input textarea select`


`Class` 与 `style` 绑定技巧[^1]
```
<div：class="{'active' : isactive , 'danger' : hasError}"></div>
```
[^1]:`active`是类名   isactive 是条件
<br/>
* *
---
###vue中的各个文件
`main.js`是我们的入口js文件，主要作用是初始化vue实例并使用需要的插件。

`App.vue`是我们的主组件，所有页面都是在`App.vue`下进行切换的。

`Vue2.0`全家桶(`vue+vue-router+vuex+axios+es6+sass`)
* *
---
<br/>

子组件向父组件传递用`events`
子组件向外发布事件
父组件监听
![](https://i.imgur.com/8CknfHu.png)
父组件向子组件传递用`props`
父组件向内传递属性


* *
---
<br/>
用了`Export default`
才能`import`输出的内容
`import xxx form './components/xxx'`

同步事件：`mutations`
异步事件：`actions`
你可以通过 `store.state` 来获取状态对象，以及通过 `store.commit` 方法触发状态变更：

你不能直接改变 `store` 中的状态。改变` store` 中的状态的唯一途径就是显式地提交 (commit) `mutation`。


###路由的创建

```
import VueRouter from 'vue-router'
//引入component
import goods from './components/goods/goods'
import ratings from './components/ratings/ratings'
import seller from './components/seller/seller'

Vue.use(VueRouter)

const routes = [
  /*路由重定向*/
  { path: '/', redirect: 'goods' },
  // 路由定向
  { name: goods, path: '/goods', component: goods },
  { name: ratings, path: '/ratings', component: ratings },
  { name: seller, path: '/seller', component: seller }


];
// 接着创建路由实例
const router = new VueRouter({
  // ES6缩写语法，相当于routes:routes
  routes,
  linkActiveClass:'active'
});

/* eslint-disable no-new */
// 有这条规则new Vue就不用赋值给变量
new Vue({
  el: '#app',
  router,
  template: '<App/>',
  components: { App }
});
```