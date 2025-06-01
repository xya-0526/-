## ✅ 一句话总结：

> 提高 Webpack 构建速度主要从 **减少编译体积、提升并发能力、使用缓存** 和 **合理配置 loader/plugin** 几方面入手。

------

## 🚀 提升构建速度的常用手段：

### 1. **开启持久化缓存（Webpack 5 推荐）**

```
js复制编辑cache: {
  type: 'filesystem', // 启用磁盘缓存，加快二次构建
}
```

------

### 2. **合理使用 `include/exclude` 限制编译范围**

```
js复制编辑module: {
  rules: [
    {
      test: /\.js$/,
      loader: 'babel-loader',
      include: path.resolve(__dirname, 'src'), // 只处理 src 目录
      exclude: /node_modules/                 // 排除不需要编译的库
    }
  ]
}
```

------

### 3. **开启 `babel-loader` 缓存**

```
js复制编辑loader: 'babel-loader',
options: {
  cacheDirectory: true, // 将 Babel 编译结果缓存到硬盘
}
```

------

### 4. **使用多线程 loader（thread-loader）**

对 JS、TS 编译这类耗时任务使用多进程加速：

```

use: ['thread-loader', 'babel-loader']
```

------

### 5. **使用 `exclude` 避免对 node_modules 做复杂处理**

- 避免对第三方包进行转译，能极大节省时间。

------

### 6. **减少打包体积（间接提速）**

- 启用 Tree Shaking；
- 拆分模块，避免大体积文件重复打包。

------

### 7. **减少 plugin 数量 / 避免复杂 plugin**

- 比如 `uglifyjs-webpack-plugin` 可替换为 `TerserPlugin`（更快）；
- `ForkTsCheckerWebpackPlugin` 可以将 TypeScript 类型检查放在单独线程中执行。



### 9. **开启模块缓存和依赖预构建（Webpack 5）**

- Webpack 5 自动做 module/resolve 缓存；
- 可手动指定 `resolve.cacheWithContext = false`。

------

## ✅ 回答总结句式（面试可说）：

> 提高 Webpack 构建速度主要从以下几个方面入手：启用持久化缓存（如 filesystem cache）、限制 loader 编译范围（include/exclude）、开启 loader 缓存和多线程（thread-loader）、合理使用插件、减小打包体积、使用 externals/CDN 等方式减少构建工作量。通过这些手段可以显著加快初次和二次构建速度。