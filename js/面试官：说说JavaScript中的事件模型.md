# 事件模型

js 是一门单线程语言（同一时间只能执行一件事）  通过 事件模型  实现非阻塞编程。

## 事件模型的核心三部分

1. 事件注册 给dom绑定点击事件或监听事件
2. 事件触发：用户点击 键盘输入
3. 事件执行： 触发后 对应的回调函数添加进任务队列 等待主线程空闲时执行（事件循环）

## 事件流

事件从触发开始，到执行回调，会经历以下三个阶段：

1. **捕获阶段（Capture Phase）**
   - 从 window → document → html → … → 目标元素（由外向内）
2. **目标阶段（Target Phase）**
   - 到达目标元素
3. **冒泡阶段（Bubble Phase）**
   - 从目标元素 → … → document → window（由内向外）

> 默认事件处理是在冒泡阶段发生，但也可以通过参数设置为捕获阶段处理。

```js
element.addEventListener('click', handler, true);  // 捕获阶段
element.addEventListener('click', handler, false); // 冒泡阶段（默认）
```

## 事件流示例

HTML 示例：

```html
<div id="outer">
  <button id="inner">点击我</button>
</div>
```

JavaScript：

```js
js复制编辑document.getElementById('outer').addEventListener('click', () => {
  console.log('外层 div 冒泡');
}, false);

document.getElementById('outer').addEventListener('click', () => {
  console.log('外层 div 捕获');
}, true);

document.getElementById('inner').addEventListener('click', () => {
  console.log('按钮点击');
}, false);
```

点击按钮时，打印顺序为：

```makefile
css复制编辑外层 div 捕获
按钮点击
外层 div 冒泡
```

## 事件委托

事件代理（Event Delegation）是 JavaScript 中的一种**事件处理机制**

利用 事件冒泡机制 把 事件处理绑定在父元素上 通过event.target 判断触发源

实现 子元素 事件处理

### ✅ 事件冒泡机制

事件在 DOM 中是“冒泡”的：当一个元素触发事件后，该事件会向上传递（冒泡）到它的父元素、祖先元素，直到 `document`。

### ✅ 利用这个机制

我们可以把事件监听器放在**公共的父级元素**上，当事件冒泡到这个父级时，通过 `event.target` 判断是哪个子元素触发了事件，从而做出相应处理。

### **✅ 优点**：

减少内存  

### ❌ 缺点

- 事件不能被所有事件类型代理（如 `focus`, `blur` 不冒泡）
- `event.target` 可能不是期望的目标，需要判断
- 嵌套结构复杂时，事件处理逻辑可能较难控制

```js
document.getElementById('ul').addEventListener('click', function (e) {
  if (e.target.tagName === 'LI') {
    console.log('你点击了 li：', e.target.textContent);
  }
});

```

| 使用场景           | 是否适合                                 |
| ------------------ | ---------------------------------------- |
| 子元素很多         | ✅ 很适合，避免过多绑定                   |
| 子元素是动态添加的 | ✅ 很适合，父元素能接管所有新子元素事件   |
| 子元素数量少、固定 | ❌ 没必要代理，直接绑定即可               |
| 需要停止事件冒泡   | ⚠️ 需要谨慎处理 `event.stopPropagation()` |



## 四、常用事件对象属性和方法

- `event.target`：触发事件的元素
- `event.currentTarget`：绑定事件的元素（通常是委托用）
- `event.stopPropagation()`：阻止事件继续传播
- `event.preventDefault()`：阻止默认行为（如表单提交）
- `event.stopImmediatePropagation()`：阻止后续所有监听器执行

## 事件循环

js处理异步任务防止线程阻塞的一种机制。

### 事件循环流程

1.主线程执行同步代码 即把同步任务放到执行栈按顺序

2.遇到异步任务交给浏览器 webAPIs处理，处理后把回调函数放入任务队列

3判断主线程即执行栈是否为空为空就向任务队列取任务 放入执行栈 进行执行

4重复以上过程

### 任务队列类型

任务队列分为两种：

#### 1. 宏任务（Macro-task）：

每次事件循环从宏任务队列中取出一个任务执行。

- 常见宏任务包括：
  - `setTimeout`
  - `setInterval`
  - `setImmediate`（Node.js）
  - `I/O`
  - `UI rendering`

#### 2. 微任务（Micro-task）：

每个宏任务执行完后，会立即执行所有微任务队列中的任务。

- 常见微任务包括：
  - `Promise.then/catch/finally`
  - `MutationObserver`
  - `queueMicrotask`



### ✅ 一、事件循环阻塞的本质

JavaScript 是单线程的，事件循环依赖主线程处理任务：

> **只要调用栈中还有任务在执行，事件循环就不能处理队列中的其他任务。**

因此，如果你在主线程上执行了一个长时间运行的操作（如死循环、复杂计算、大量 DOM 操作），事件循环就会被**卡住**或**阻塞**，异步任务无法按时执行。

### ✅常见导致事件循环阻塞的原因

| 场景                                | 描述                                   |
| ----------------------------------- | -------------------------------------- |
| **1. 死循环或无限递归**             | 比如 `while(true)`，没有终止条件       |
| **2. 大量同步计算**                 | 如复杂的数学计算、数据排序、图像处理等 |
| **3. 批量 DOM 操作**                | 一次性对页面进行大量 DOM 插入/修改     |
| **4. 同步的 Ajax 请求**（已被废弃） | `XMLHttpRequest` 的同步调用会完全阻塞  |
| **5. 错误处理不当**                 | 异常没有及时处理，卡住调用栈           |

事件循环之所以会**阻塞**，通常是因为**主线程执行某些任务耗时太久**，导致事件循环无法继续执行后续的任务（包括异步任务的回调、UI更新等）。



### ✅ 三、示：阻塞代码演示

```
js复制编辑console.log('start');

setTimeout(() => {
  console.log('setTimeout');
}, 0);

// 模拟长时间执行的同步任务
const start = Date.now();
while (Date.now() - start < 5000) {} // 阻塞 5 秒

console.log('end');
```

**输出结果：**

```
sql复制编辑start
end
setTimeout   <-- 延迟了 5 秒才执行
```

> `setTimeout` 明明设定了 0ms，但由于主线程被 `while` 阻塞，直到主线程空了才执行回调。

------

### ✅ 四、如何避免阻塞事件循环

1. **将大任务拆成小任务（分片处理）**

   ```
   js复制编辑function heavyTask() {
     let i = 0;
     function chunk() {
       for (let j = 0; j < 1000 && i < 100000; j++, i++) {
         // 执行小块任务
       }
       if (i < 100000) {
         setTimeout(chunk, 0); // 将剩余任务放到下一个事件循环
       }
     }
     chunk();
   }
   ```

2. **使用 Web Worker**（浏览器）或多线程（Node.js）处理重计算

3. **避免使用同步阻塞操作**（例如同步 Ajax）



总结

- 事件循环是 JavaScript 异步编程的核心机制；
- 宏任务和微任务是事件循环的两个重要组成部分；
- 微任务优先于宏任务；
- 合理使用异步任务可以避免主线程阻塞，提高性能。