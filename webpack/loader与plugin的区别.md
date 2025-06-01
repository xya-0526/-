## ✅ Loader 和 Plugin 的区别（简要说明）：

| 对比项   | Loader（加载器）                     | Plugin（插件）                     |
| -------- | ------------------------------------ | ---------------------------------- |
| 作用     | **转换模块内容**（如 `.js`、`.css`） | **扩展构建功能**，参与构建生命周期 |
| 使用位置 | 配置在 `module.rules` 中             | 配置在 `plugins` 数组中            |
| 处理对象 | **单个模块文件**                     | **整个构建流程**                   |
| 类型     | 是一个函数                           | 是一个带有 `apply` 方法的类        |
| 触发机制 | 自动在模块被加载时调用               | 依靠 Webpack 生命周期钩子触发      |



📝 总结：

> Loader 是模块级的“**内容转换器**”，Plugin 是构建级的“**功能扩展器**”

## 🧱 Loader 编写思路：

1. **本质是一个函数**，接受源代码字符串作为参数。
2. **对内容进行处理**（如转译、压缩），返回新的内容。
3. 支持异步处理（使用 `this.async()`）。
4. 可使用 loader-utils 获取参数。

📌 示例结构：

```
js复制编辑module.exports = function (source) {
  const result = source.replace(/foo/g, 'bar');
  return result;
};
```

------

## 🔧 Plugin 编写思路：

1. **本质是一个类**，必须实现 `apply(compiler)` 方法。
2. 在 `compiler` 的生命周期钩子中注册回调。
3. 利用 Webpack 提供的事件流机制（基于 Tapable）。

`webpack`编译会创建两个核心对象：

- compiler：包含了 webpack 环境的所有的配置信息，包括 options，loader 和 plugin，和 webpack 整个生命周期相关的钩子
- compilation：作为 plugin 内置事件回调函数的参数，包含了当前的模块资源、编译生成资源、变化的文件以及被跟踪依赖的状态信息。当检测到一个文件变化，一次新的 Compilation 将被创建

📌 示例结构：

```
js复制编辑class MyPlugin {
  apply(compiler) {
    compiler.hooks.emit.tap('MyPlugin', (compilation) => {
      console.log('开始生成资源');
    });
  }
}
module.exports = MyPlugin;
```

------

## ✅ 面试总结句式（简洁）

Loader 用于转换模块内容，比如将 ES6 转为 ES5，而 Plugin 用于扩展构建流程，比如生成 HTML、压缩资源。Loader 是函数，操作文件内容；Plugin 是类，操作 Webpack 的生命周期钩子。编写 Loader 只需处理输入内容并返回结果；编写 Plugin 要实现 `apply` 方法，在合适的生命周期中注入逻辑。