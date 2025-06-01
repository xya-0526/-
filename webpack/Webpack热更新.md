# webpack热更新

> Webpack 的热更新（HMR）是指在不刷新浏览器的情况下，**替换、更新已修改的模块**，从而提升开发效率和体验。
>
> ##  热更新的原理（底层机制）：
>
> Webpack 热更新依赖于以下三个核心组件：
>
> 1. **Webpack Dev Server（或 Vite 等 dev server）**
>    - 启动一个本地开发服务器；
>    - 内部使用了 **`webpack-dev-middleware`** + **`webpack-hot-middleware`**；
>    - 实现静态资源的实时服务与热更新。
> 2. **HMR Runtime（浏览器端的热更新代码）**
>    - 注入到每个模块中；
>    - 监听模块变化，下载更新的模块代码；
>    - 动态替换老模块，并触发对应回调（如 Vue 的 `hot.accept()`）。
> 3. **WebSocket 连接**
>    - 浏览器和 dev-server 之间建立 WebSocket 通道；
>    - 当代码变更、重新编译后，dev-server 向客户端推送更新通知。
>
> ------
>
> ## 🔁 HMR 工作流程图（简化版）：
>
> ```
> 源码变更 →
> Webpack 重新编译 →
> dev-server 通知浏览器（通过 WebSocket） →
> 浏览器下载更新的模块（JSON + 新模块） →
> HMR Runtime 替换旧模块代码 →
> 页面局部更新，无需刷新
> ```

## ✅ 总结句式（面试可说）：

> Webpack 热更新是通过 WebSocket 连接实现浏览器和 dev-server 的通信，当源码发生变更时，Webpack 只重新编译变更模块，并通过 HMR Runtime 替换对应模块。这样避免了整页刷新，实现了高效的开发体验。它依赖于 Webpack Dev Server、HMR Runtime 和模块热替换机制协同工作。