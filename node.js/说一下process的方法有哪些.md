# process

process 是node.js的全局对象 用于获取 控制当前进程 

常用方法有：

1.process.env

- 访问环境变量（如配置端口、数据库连接等）。

- 示例：

  ```js
  const port = process.env.PORT || 3000;
  ```

   使用 `process.env` 实现根据环境切换配置？

> ✅ 要点：根据 `process.env.NODE_ENV` 加载不同的配置。

**2. `process.argv`**

- 获取命令行参数，返回数组。

- 示例：

  ```js
  node app.js --mode=dev
  ```

  ```js
  console.log(process.argv); // [ 'node', 'app.js', '--mode=dev' ]
  ```

 **3. `process.exit([code])`**

- 退出进程，`0` 表示正常退出，其他表示异常。

- 示例：

  ```js
  if (!config) {
    console.error("配置错误");
    process.exit(1);
  }
  ```

4.process.nextTick

表示当前循环结束执行回调

```js
process.nextTick(() => {
  console.log('nextTick 回调');
});
```

- `process.nextTick()`：在当前事件循环末尾执行（优先级更高）；
- `setImmediate()`：在下一轮事件循环开始时执行。

 5. `process.cwd()

获取当前工作目录（current working directory）。

- 示例：

  ```
  
  console.log(process.cwd());
  ```

### **三、简洁总结一句话**

> `process` 是 Node.js 中的一个全局对象，提供了对进程的控制能力，常用于读取环境变量、获取命令行参数、控制退出、注册事件等，是构建命令行工具和后端服务的重要接口。