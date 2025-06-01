# 说说Node中的EventEmitter? 如何实现一个EventEmitter?

`EventEmitter` 是 Node.js 中的核心模块之一，它是事件驱动编程的基础。许多 Node.js 核心模块（如 `fs`, `http`, `net` 等）都继承了 `EventEmitter`，以实现异步事件处理机制。

eventEmitters是一个类  提供了 消息订阅预发布事件机制 允许 在事件对象上添加多个监听器

### 常用方法：

| 方法                                               | 描述                   |
| -------------------------------------------------- | ---------------------- |
| `emitter.on(event, listener)`                      | 注册监听器             |
| `emitter.once(event, listener)`                    | 注册只执行一次的监听器 |
| `emitter.emit(event, [...args])`                   | 触发事件               |
| `emitter.off(event, listener)` 或 `removeListener` | 移除监听器             |
| `emitter.removeAllListeners([event])`              | 移除所有监听器         |
| `emitter.listeners(event)`                         | 返回监听器数组         |



## 三、如何实现一个简易的 EventEmitter？

下面是一个手写实现：

```js
js复制编辑class MyEventEmitter {
  constructor() {
    this.events = {};
  }

  on(event, listener) {
    if (!this.events[event]) this.events[event] = [];
    this.events[event].push(listener);
  }

  off(event, listener) {
    if (!this.events[event]) return;
    this.events[event] = this.events[event].filter(l => l !== listener);
  }

  once(event, listener) {
    const onceWrapper = (...args) => {
      listener(...args);
      this.off(event, onceWrapper);
    };
    this.on(event, onceWrapper);
  }

  emit(event, ...args) {
    if (!this.events[event]) return false;
    this.events[event].forEach(listener => listener(...args));
    return true;
  }

  removeAllListeners(event) {
    if (event) {
      delete this.events[event];
    } else {
      this.events = {};
    }
  }
}
```

## 四、扩展（面试深入问）

- **事件异步还是同步？** 默认是同步调用监听器（即 emit 时立即执行所有 listener）。
- **如何实现异步事件？** 可以通过 `setImmediate()` 或 `process.nextTick()` 包装 listener。
- **如何避免内存泄漏？** 默认最多监听 10 个事件（`emitter.setMaxListeners(n)` 可调整）。