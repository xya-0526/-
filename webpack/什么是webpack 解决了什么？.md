# webpack

webpack 是一个前端资源打包工具webpack  生态相对完善  具有 丰富的 插件 lodaer资源

## 打包流程

1. 输入
2. 模块化递归处理
3. 处理后
4. 输出

### **Webpack的理解：**

Webpack 是一个 **前端资源模块化打包工具**，本质上是一个**模块打包器（module bundler）**。它会从一个入口文件（`entry`）出发，递归分析项目的模块依赖，把各种资源（JS、CSS、图片等）都当作模块进行打包，最终生成浏览器可识别的静态资源。

### **Webpack解决了什么问题？**

1. **模块化管理：**
   - 在没有webpack之前，前端模块化依赖管理较混乱，需要手动引入多个 `<script>`，容易出现命名冲突、加载顺序问题。
   - Webpack支持 CommonJS、ES6 Module 等模块语法，实现了依赖关系的自动管理。
2. **资源统一打包：**
   - 不仅支持 JS，还能把 CSS、图片、字体、甚至 HTML 等视为模块统一打包，极大提升了项目组织性和构建能力。
3. **优化性能：**
   - 提供各种优化手段：**代码分割（Code Splitting）**、**懒加载（Lazy Loading）**、**Tree Shaking**（去除未使用代码），减少资源体积、提升加载效率。
4. **自动化构建：**
   - 借助插件和 loader 体系，webpack可以进行转译（如 Babel）、压缩、添加前缀（PostCSS）、图片压缩等自动化构建工作。
5. **开发体验提升：**
   - 提供 **dev server** 支持热更新（HMR），开发体验更流畅。
   - 可以集成 ESLint、StyleLint 等工具，规范代码风格。

###  **Webpack的核心概念：**

你可以简要提一下这些关键词，展示你对原理的掌握：

- **Entry（入口）**：webpack从哪里开始打包。
- **Output（输出）**：打包后输出的文件位置与命名。
- **Loader（资源）**：对模块的转换器，比如把 `.vue` 或 `.scss` 转换为浏览器可识别的 JS。
- **Plugin（插件）**：扩展 webpack 功能，如 HtmlWebpackPlugin、MiniCssExtractPlugin。
- **Mode（开发模式）**：开发模式（development）和生产模式（production）行为不同。
- **DevServer（服务器环境）**：开发环境服务器，支持自动刷新和热更新。