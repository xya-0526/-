# mini 混合

vue 提供的一种代码复用机制 可以把公用的代码 抽离出来 

经行复用 是一个 js对象 可以配置 data methodes 生命周期等

简单的例子

```js
// 定义一个 mixin
const myMixin = {
  data() {
    return {
      count: 0
    };
  },
  methods: {
    increment() {
      this.count++;
    }
  },
  created() {
    console.log('来自 mixin 的 created');
  }
};

// 在组件中使用 mixin
export default {
  mixins: [myMixin],
  created() {
    console.log('来自组件的 created');
  }
};
```

//运行

```
来自 mixin 的 created
来自组件的 created
```

## 全局混入和局部混入

局部混入 

### 局部混入

定义一个`mixin`对象，有组件`options`的`data`、`methods`属性

```js
var myMixin = {
  created: function () {
    this.hello()
  },
  methods: {
    hello: function () {
      console.log('hello from mixin!')
    }
  }
}
```

组件通过`mixins`属性调用`mixin`对象

```js
Vue.component('componentA',{
  mixins: [myMixin]
})
```

该组件在使用的时候，混合了`mixin`里面的方法，在自动执行`created`生命钩子，执行`hello`方法

通过`Vue.mixin()`进行全局的混入

```js
Vue.mixin({
  created: function () {
      console.log("全局混入")
    }
})
```

- 替换型策略有`props`、`methods`、`inject`、`computed`，就是将新的同名参数替代旧的参数
- 合并型策略是`data`, 通过`set`方法进行合并和重新赋值
- 队列型策略有生命周期函数和`watch`，原理是将函数存入一个数组，然后正序遍历依次执行
- 叠加型有`component`、`directives`、`filters`，通过原型链进行层层的叠加

## 🧠 mixin 解决了什么问题？

当多个组件中有重复的逻辑（如定时器、滚动监听、数据处理等），你可以把这些公共逻辑抽成 mixin，然后在组件中复用，避免重复写代码。

## 实际应用场景

- 复用滚动监听逻辑
- 表单验证逻辑复用
- 本地存储（localStorage/sessionStorage）操作封装
- 权限判断
- websocket 连接复用

------

## 🤔 mixin 的缺点（Vue3 中被推荐替代）

虽然 mixin 在 Vue2 中非常常见，但它也存在一些缺点：

1. **命名冲突难以排查**：多个 mixin 混入后，不容易知道哪个方法/属性来自哪里。
2. **逻辑来源不清晰**：组件功能分散在多个 mixin 中，维护困难。
3. **调试困难**：当出现 bug 时，很难快速定位是哪一个 mixin 导致的。

------

## ✅ Vue 3 推荐使用 Composition API 替代 mixin

Vue 3 提供了更强大的 Composition API（组合式 API），让逻辑复用变得更明确、更好维护。例如：

```js
useCounter.js
import { ref } from 'vue';

export function useCounter() {
  const count = ref(0);
  const increment = () => count.value++;

  return {
    count,
    increment
  };
}
```

组件中使用：

```js
import { useCounter } from './useCounter';

setup() {
  const { count, increment } = useCounter();
  return { count, increment };
}
```

------

## ✅ 总结一句话：

> mixin 是 Vue 2 中用于“逻辑复用”的一种机制，通过把复用的代码混入组件中来减少重复。但在 Vue 3 中推荐使用 Composition API 来替代 mixin，提升代码可读性和维护性。