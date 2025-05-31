# 面试官：你是怎么理解ES6中 Generator的？使用场景

Generator 是 ES6 引入的一种异步编程解决方案，本质上是一个可以「**暂停执行**」和「**恢复执行**」的函数。

  

定义形式：

```js
function* myGenerator() {
  yield 1;
  yield 2;
  return 3;
}
```

特点：

- 使用 `function*` 定义。
- 内部通过 `yield` 语句分段执行。
- 调用时不会立即执行，而是返回一个 **迭代器对象**。
- 通过调用 `.next()` 执行到下一个 `yield`。

```js
const gen = myGenerator();
gen.next(); // { value: 1, done: false }
gen.next(); // { value: 2, done: false }
gen.next(); // { value: 3, done: true }
```

## ✅ 二、**使用场景（做什么）**

### 1. **控制异步流程（配合 co、Koa）**

最早被用于替代回调地狱 / Promise 链式调用。

```
js复制编辑const fetchData = () => new Promise(resolve => {
  setTimeout(() => resolve('data'), 1000);
});

function* gen() {
  const data = yield fetchData();
  console.log(data);
}

// 使用 co 库自动执行 Generator（类似 async/await）
const co = gen => {
  const g = gen();
  const next = data => {
    const { value, done } = g.next(data);
    if (!done && value instanceof Promise) {
      value.then(res => next(res));
    }
  };
  next();
};

co(gen);
```

> Koa 1.x 就是基于 Generator 实现的中间件机制。

------

### 2. **实现可中断的循环、任务控制器**

适用于需要在执行中间「暂停」的场景。

```
js复制编辑function* taskRunner() {
  while (true) {
    const task = yield;
    console.log('处理任务:', task);
  }
}

const runner = taskRunner();
runner.next(); // 启动生成器
runner.next('任务1');
runner.next('任务2');
```

------

### 3. **实现状态机（State Machine）**

每个 `yield` 表示一个状态迁移。

------

### 4. **实现惰性求值、无限序列**

如生成斐波那契数列、无限整数流等。

```
function* counter() {
  let i = 0;
  while (true) {
    yield i++;
  }
}
```

------

## ✅ 三、与 `async/await` 的对比

| 特性     | Generator            | async/await      |
| -------- | -------------------- | ---------------- |
| 引入版本 | ES6                  | ES2017（ES8）    |
| 控制流   | 手动调用 `.next()`   | 自动             |
| 返回值   | Iterator             | Promise          |
| 异步语法 | yield + co（或手动） | await + Promise  |
| 使用体验 | 稍复杂               | 更易用（更常用） |



结论：Generator 是 async/await 的前身，虽然现在用得较少，但理解它对掌握 JS 异步机制非常重要。

------

## ✅ 四、总结回答模板（建议这样说）

> Generator 是一种可以暂停和恢复执行的函数，用于实现更加灵活的控制流。在 ES6 引入 async/await 之前，Generator 曾是异步编程的核心方案，像 Koa 1.x 的中间件机制就是基于它构建的。
>
> 它主要的使用场景包括：异步控制流、状态机实现、任务调度器、惰性求值等。不过现在实战中，async/await 更加普遍，但 Generator 在需要更细粒度控制的时候仍然有价值。