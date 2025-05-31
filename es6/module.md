### 一、ES6 Module 的基本理解

ES6 中的模块（Module）是 **JavaScript 官方引入的模块化机制**，通过 `import` 和 `export` 来导入导出模块成员。

#### 特点：

- **静态加载（编译时加载）**：与 CommonJS 不同，ES6 模块在编译时就确定依赖关系。
- **严格模式默认开启**：模块中默认使用 `'use strict'`。
- **模块作用域**：模块内部的变量、函数、类等不会污染全局作用域。
- **只能顶层导入导出**：`import`/`export` 语句只能出现在模块的顶层，不能放在 if、function 内。
- **自动启用严格模式**：不需要手动添加 `'use strict'`

------

### 二、基本语法

#### 导出模块成员

```
js复制编辑// a.js
export const name = 'Alice';
export function greet() { console.log('Hi!'); }
export default function () { console.log('默认导出'); }
```

#### 导入模块成员

```
js复制编辑// b.js
import { name, greet } from './a.js'; // 解构式导入
import defaultFn from './a.js';       // 默认导入
```

------

### 三、和 CommonJS 的区别（常被问）

| 特性                  | ES6 Module                  | CommonJS         |
| --------------------- | --------------------------- | ---------------- |
| 加载方式              | 编译时静态分析              | 运行时动态加载   |
| 是否支持异步          | 是，支持动态导入 `import()` | 否，完全同步     |
| 默认导出              | `export default`            | `module.exports` |
| 是否支持 Tree-shaking | 是                          | 否               |
| 作用域                | 模块作用域                  | 也有模块作用域   |



------

### 四、使用场景

1. **前端项目模块化开发**

   - 将页面逻辑、组件、工具函数等拆分为多个模块，提高可维护性。
   - 配合打包工具（如 Webpack、Vite）使用，支持代码拆分和懒加载。

2. **构建库和工具函数包**

   - 比如 `utils.js` 导出常用函数，其他模块按需引入，支持 tree-shaking 优化体积。

3. **后端项目（Node.js 支持 ESM）**

   - 尽管 Node.js 最早支持的是 CommonJS，现在也支持 ES6 Module（`.mjs` 或配置 type: "module"）

4. **动态加载模块（懒加载）**

   ```
   js复制编辑// 在需要时动态加载某个模块
   import('./module.js').then(module => {
     module.doSomething();
   });
   ```

5. **与构建工具配合做 Tree-shaking（去掉未使用的代码）**

   - 现代工具（如 Rollup/Vite）利用静态结构删除未用的导出，提高性能

------

### 五、总结（可用于收尾）

ES6 模块是 JavaScript 官方标准化的模块系统，具有静态加载、模块作用域、支持 Tree-shaking 等优势，已经成为现代前端开发的主流选择。配合 Webpack/Vite 等构建工具，可以实现高效的模块化开发。

------

### 如果有时间你可以加一句高级表达：

> “ES6 模块语法不仅提升了代码的组织结构和可维护性，而且结合构建工具还实现了按需加载和性能优化，是现代 JavaScript 项目的基础设施之一。”