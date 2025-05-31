# 动态给vue的data添加一个新的属性时会发生什么？怎样解决？

## 出现的问题

页面不会立即响应数据

## 出现的原因

vue2 中 数据响应式 是通过 object.defineProperty 当数据行初始化时 会通过object.defineProperty 进行代理  

而 后添加的数据属性没有进行代理配置 ，因此不会引起页面法师变化

## 解决

若想实现数据与视图同步更新，可采取下面三种解决方案：

- Vue.set()
- Object.assign()
- $forcecUpdated()

1.通过Vue.se()将 新添加的属性 经行响应式设置  底层原理 还是通过 object.defineproperty()

2直接使用`Object.assign()`添加到对象的新属性不会触发更新

应创建一个新的对象，合并原对象和混入对象的属性

### 小结

- 如果为对象添加少量的新属性，可以直接采用`Vue.set()`
- 如果需要为新对象添加大量的新属性，则通过`Object.assign()`创建新对象

ps：vue3`是用过`proxy`实现数据响应式的，直接动态添加新属性仍可以实现数据响应式

