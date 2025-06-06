# es6中 数组的扩展

## 1 ...展开运算符

用于复制、合并数组，或将数组转为参数列表：

```js
   const arr1 = [1, 2];
const arr2 = [...arr1, 3]; // [1, 2, 3]
```

## 2数组构造方法

### Array.from

用于 将 类数组 或可迭代的对象转为真正的数组

```js
Array.from('abc'); // ['a', 'b', 'c']
Array.from({ length: 3 }, (_, i) => i); // [0, 1, 2]
```

### Array.of

用于 将一组值转为数组（区别于 `new Array()`）

```js
Array.of(3); // [3]
new Array(3); // [empty × 3]
```

## 数组实例方法

### 4. **find() / findIndex()**

查找符合条件的第一个元素或索引：

```
[1, 2, 3].find(x => x > 1); // 2
[1, 2, 3].findIndex(x => x > 1); // 1
```

------

### 5. **fill()**

用固定值填充数组：

```
[1, 2, 3].fill(0); // [0, 0, 0]
new Array(3).fill('a'); // ['a', 'a', 'a']
```

------

### 6. **copyWithin()**

在原数组内部复制部分内容到其他位置：

```

[1, 2, 3, 4].copyWithin(1, 2); // [1, 3, 4, 4]
```

------

### 7. **includes()**

判断数组是否包含某个值（比 indexOf 更直观）：

```
[1, 2, 3].includes(2); // true
[NaN].includes(NaN);  // true
```

## ✅ 二、面试高分回答建议（口语版）

> ES6 对数组新增了许多方法和语法特性，常见的包括：
>
> - 展开运算符 `...`，用于解构、合并；
> - `Array.from()` 和 `Array.of()` 提供了更安全的数组创建方式；
> - 查找相关方法如 `find()` 和 `findIndex()`；
> - 数据处理方法如 `fill()`、`copyWithin()`；
> - 判断方法 `includes()`，它比 `indexOf` 更准确，特别是能识别 `NaN`；
>    这些方法让数组操作更语义化、更安全，代码也更简洁。