# v-if 和v-show的区别

- 控制手段： v-if  是通过 dom 的 添加和删除 进行 的元素的 显示和隐藏  而v-show 是 通过 对dom 样式添加 dispaly :none实现dom的显示与 隐藏
- 编译过程 ： v-if  是 局    部 的 编译与卸载 而 v-show 只是仅仅改变 dom的 样式
- 编译条件 ： v-if   是真正的条件渲染   
-     v-if 会 触发 组件的 生命周期函数    `v-if`由`false`变为`true`的时候，触发组件的`beforeCreate`、`create`、`beforeMount`、`mounted`钩子，由`true`变为`false`的时候触发组件的`beforeDestory`、`destoryed`方法
-    v-if  消耗性能  v-show 不消耗



总结 ： v-show 不操作dom v-if 操作dom 

  频繁切换  选用v-show  不频繁用 v-if