# node.js的全局对象

node .js 中有一些全局对象或者函数 不需要进行引入 就能是直接使用

常见的有 

1. _global  : 相当于window
2. __dirname: 获取 当前模块绝对路径
3. __ filname：获取当前模块的绝对路径（包括文件名）
4. module :模块 包含当前模块的各种信息
5. exports ：用于导出模块
6. require()： 引入模块 或者资源
7. process : 用以提供当前进程的信息
   - 常用属性/方法：
     - `process.env`：获取环境变量；
     - `process.argv`：获取命令行参数；
     - `process.exit()`：退出进程；
     - `process.nextTick()`：下一次事件循环执行回调。
8. 定时器 
9. buffer 处理二进制数据

### **二、总结一句话**

> Node.js 的全局对象主要包括 `global`、`__dirname`、`__filename`、`module`、`exports`、`require`、`process`、`Buffer` 以及定时器函数等，他们构成 Node.js 的运行基础，帮助我们进行模块加载、路径获取、进程控制和异步操作。