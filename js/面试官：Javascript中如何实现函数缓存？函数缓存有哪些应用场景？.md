### ✅ 一、什么是函数缓存？

**函数缓存（Function Memoization）\**是一种优化技术，用于\**缓存函数的执行结果**，当传入相同的参数时，**直接返回缓存值**，避免重复计算，从而提升性能。

## 二、如何实现

实现函数缓存主要依靠闭包、柯里化、高阶函数，这里再简单复习下：

### [#](https://vue3js.cn/interview/JavaScript/function_cache.html#闭包)闭包

闭包可以理解成，函数 + 函数体内可访问的变量总和

```js
(function() {
    var a = 1;
    function add() {
        const b = 2
        let sum = b + a
        console.log(sum); // 3
    }
    add()
})()
```

`add`函数本身，以及其内部可访问的变量，即 `a = 1`，这两个组合在⼀起就形成了闭包

### [#](https://vue3js.cn/interview/JavaScript/function_cache.html#柯里化)柯里化

把接受多个参数的函数转换成接受一个单一参数的函数

```js
// 非函数柯里化
var add = function (x,y) {
    return x+y;
}
add(3,4) //7

// 函数柯里化
var add2 = function (x) {
    //**返回函数**
    return function (y) {
        return x+y;
    }
}
add2(3)(4) //7
```



将一个二元函数拆分成两个一元函数

### [#](https://vue3js.cn/interview/JavaScript/function_cache.html#高阶函数)高阶函数

通过接收其他函数作为参数或返回其他函数的函数

```js
function foo(){
  var a = 2;

  function bar() {
    console.log(a);
  }
  return bar;
}
var baz = foo();
baz();//2
```



函数 `foo` 如何返回另一个函数 `bar`，`baz` 现在持有对 `foo` 中定义的`bar` 函数的引用。由于闭包特性，`a`的值能够得到

下面再看看如何实现函数缓存，实现原理也很简单，把参数和对应的结果数据存在一个对象中，调用时判断参数对应的数据是否存在，存在就返回对应的结果数据，否则就返回计算结果

如下所示

```js
const memoize = function (func, content) {
  let cache = Object.create(null)
  content = content || this
  return (...key) => {
    if (!cache[key]) {
      cache[key] = func.apply(content, key)
    }
    return cache[key]
  }
}
```

调用方式也很简单

```js
const calc = memoize(add);
const num1 = calc(100,200)
const num2 = calc(100,200) // 缓存得到的结果
```

过程分析：

- 在当前函数作用域定义了一个空对象，用于缓存运行结果
- 运用柯里化返回一个函数，返回的函数由于闭包特性，可以访问到`cache`
- 然后判断输入参数是不是在`cache`的中。如果已经存在，直接返回`cache`的内容，如果没有存在，使用函数`func`对输入参数求值，然后把结果存储在`cache`中

### ✅ 三、函数缓存的应用场景

| 场景             | 说明                                         |
| ---------------- | -------------------------------------------- |
| ✅ 计算密集型函数 | 如斐波那契、递归计算、复杂数学函数           |
| ✅ 接口请求缓存   | 同样参数避免重复发请求（如搜索建议）         |
| ✅ 数据处理       | 对大数组进行过滤、映射时缓存处理结果         |
| ✅ React 渲染优化 | `useMemo` 缓存计算结果避免无意义重算         |
| ✅ 表单校验       | 某些字段校验逻辑固定，可缓存结果提高响应速度 |