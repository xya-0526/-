# spa 首屏加载

## 首屏加载慢的原因

1. 资源文件过大
2. 网络延迟
3. 一些脚本资源造成渲染阻塞
4. 资源是否重复发送请求去加载了

## 解决加载慢的问题

1. 减少入口文件积
2. 图片资源压缩
3. 静态资源经行本地缓存
4. ui组件库按需引入
5. 组件重复打包
6. 使用SSR(服务端渲染)