## [H5页面监听Android物理返回键](https://juejin.im/post/5c0915795188250b064f4fa0)

##### history 属性
```js
history.length

history.state
```
##### history 方法
```js
history.back()

history.forward()

history.go()
```
##### HTML5 新API
history.pushState(state, title, url); 添加一条历史记录，不刷新页面
history.replaceState(state, title, url); 替换一条历史记录，不刷新页面
##### 事件
popState事件：历史记录发生变化时触发，调用history.pushState()或history.replaceState()不会触发此事件
```js
window.addEventListener('popstate', handlePopstate);
```
hashchange事件：页面hash值发生改变时触发
```js
window.addEventListener('hashchange', handleHashChange);
```


## [几种常见的Vue组件间的传参方式](https://juejin.im/post/5c112ae6f265da61682b3c7b)

##### VueX

优点

解决了多层组件之间繁琐的事件传播。
解决了多组件依赖统同一状态的问题。
单向数据流
为Vue量身定做，学习成本不高


缺点

不能做数据持久化，刷新页面就要重制，要做数据持久化可以考虑使用localstorage。
增加额外的代码体积，简单的业务场景不建议使用。

##### EventBus
优点

解决了多层组件之间繁琐的事件传播。
使用原理十分简单，代码量少。


缺点

由于是都使用一个Vue实例，所以容易出现重复触发的情景，例如：

多人开发时，A、B两个人定义了同一个事件名。
两个页面都定义了同一个事件名，并且没有用$off销毁（常出现在路由切换时）。
在for出来的组件里注册。


项目一大用这种方式管理事件会十分混乱，这时候建议用vuex。

##### props和\$emit/$on
优点

使用最为简单，也是父子组件传递最常见的方法。
Vue为给props提供了类型检查支持。
$emit不会修改到别的组件的同名事件，因为他只能触发父级的事件，这里和event-bus不同

缺点

单一组件层级一深需要逐层传递，会有很多不必要的代码量。
不能解决了多组件依赖统同一状态的问题。

##### provide/inject
优点

不用像props一层层传递，可以跨层级传递。


缺点

用这种方式传递的属性是非响应式的，所以尽可能来传递一些静态属性。
引用官网的话是它将你的应用以目前的组件组织方式耦合了起来，使重构变得更加困难。，我对这句话的理解是用了provide/inject你就要遵循它的组件组织方式，在项目的重构时如果要破坏这个组织方式会有额外的开发成本，其实event-bus也有这个问题。

##### slot
优点
可以在父组件里自定义插入到子组件里的内容，虽然其他属性也可以，但是我觉得slot更倾向于自定义的条件是来自于父容器中。
复用性好,适合做组件开发。

缺点
和props一样不支持跨层级传递。
##### \$parent/$children
优点

可以拿到父子组件实例，从而拥有实例里的所有属性。


缺点

用这种方法写出来的组件十分难维护，因为你并不知道数据的来源是哪里，有悖于单向数据流的原则
this.$children拿到的是一个数组，你并不能很准确的找到你要找的子组件的位置，尤其是子组件多的时候。
