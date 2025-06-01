###  **Node.js 中的事件循环机制简述：**

Node.js 是单线程的，但通过事件循环（Event Loop）机制，实现了 **非阻塞的异步 I/O** 操作。

事件循环不断检查是否有待执行的任务，并按顺序处理不同阶段的回调。整个流程分为几个主要阶段：

1. **timers**：处理 `setTimeout` 和 `setInterval` 的回调
2. **pending callbacks**：处理某些 I/O 异步回调
3. **poll**：获取新的 I/O 事件（最核心阶段）
4. **check**：执行 `setImmediate()` 的回调
5. **close callbacks**：处理如 socket 的 close 事件

此外，还有两种优先级更高的微任务队列：

- `process.nextTick()`：当前阶段末尾立即执行
- `Promise.then()`：宏任务之后、下一个阶段之前执行

### 1. `process.nextTick()` 和 `Promise.then()` 的区别？

| 特性   | `process.nextTick()`       | `Promise.then()` |
| ------ | -------------------------- | ---------------- |
| 队列   | nextTick 队列              | 微任务队列       |
| 优先级 | 更高                       | 稍低             |
| 用途   | 修改执行顺序，常用于库内部 | 更偏业务逻辑处理 |

**总结一句话：**

> Node.js 利用事件循环 + 异步回调机制，实现了单线程下的高并发和非阻塞能力。