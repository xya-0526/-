# vue 实例挂载流程 

1.首先创建 实例  经行 初始化 触发 _init函数 初始化 各种方法 各种事件 生命周期 （data数据初始实在 beforcreate 之后 create 之前 因此 beforcreate 时 拿不到data数据）数据初始化顺序：`props`、`methods`、`data`

2调用$mount经行挂载，挂载主要用到的函数是mountComponent

3 定义 updateComponent更新 函数

4 调用$rander 函数渲染虚拟dom

5调用 _update 函数将虚拟`DOM`生成真实`DOM`结构，并且渲染到页面中