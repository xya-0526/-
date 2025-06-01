## ✅ 一句话概括：

> Webpack 的 `devServer.proxy` 通过将前端请求 **转发给后端服务器**，实现“同源请求”，从而绕过浏览器的跨域限制。

------

## 🌐 为什么会有跨域问题？

浏览器的**同源策略（Same-Origin Policy）**限制了前端 JS 只能请求 **同协议、同域名、同端口** 的接口，否则就会发生 **跨域（CORS）** 问题。

------

## 🧰 Webpack proxy 的作用：

- 在开发阶段，`webpack-dev-server` 启动的是一个本地服务器（比如：http://localhost:3000）；
- 当前端向这个服务器发请求（如 `/api/user`），而目标数据实际在别的后端服务器（如 http://localhost:8080）上；
- 使用 `proxy`，Webpack 会将 `/api/user` 这样的请求 **转发** 给后端服务器，模拟“同源请求”；
- 对浏览器来说，请求始终是向 `localhost:3000` 发出的，因此不会触发跨域。

------

## 🛠 原理示意：

```
text复制编辑浏览器请求：http://localhost:3000/api/user
↓
webpack-dev-server 接收请求
↓
proxy 配置：将 /api 转发到 http://localhost:8080
↓
后端返回数据
↓
webpack-dev-server 将响应返回给浏览器
```

📌 这样整个通信过程对浏览器来说是同源的，就**不会触发跨域限制**。

------

## ⚙️ proxy 常见配置示例：

```
js复制编辑devServer: {
  proxy: {
    '/api': {
      target: 'http://localhost:8080',
      changeOrigin: true,      // 修改请求头中的 origin
      pathRewrite: { '^/api': '' } // 去掉 /api 前缀
    }
  }
}
```

## ✅ 回答总结句式（面试可说）：

> Webpack 的 proxy 是基于开发服务器实现的请求转发机制，它将前端请求转发给后端 API 服务，从而避免浏览器触发跨域限制。由于请求始终是由本地服务发出的，所以属于“同源请求”，成功解决了开发环境下的跨域问题。