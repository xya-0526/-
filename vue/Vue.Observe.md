# vue.observable

`Vue.observable` 是 Vue.js 2.6+ 中引入的一个方法，它允许你将一个普通的 JavaScript 对象转换成响应式对象。也就是说，当对象的属性发生变化时，相关的视图（例如组件）会自动更新。

使用场景 

全局状态管理

 用来代理vuex 或事件总线 一些简单操作

简单的数据共享

如果只是需要在几个组件间共享简单的状态，`Vue.observable` 是一个不错的选择

vue3  是通过 ref reactive 创建响应式

原理：

```js
Vue.observable(obj)
      ↓
observe(obj)
      ↓
new Observer(obj)
      ↓
遍历 obj 所有属性 → defineReactive → defineProperty(get/set)
      ↓
读取属性 → 收集依赖（Dep.depend）
修改属性 → 通知更新（Dep.notify → Watcher.update → 组件重渲染）
```



