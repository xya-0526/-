# typeof 与instanceof的区别

## 🔹 一、`typeof` 运算符

用于判断基本类型数据的数据类型返回值是一个字符串

### 用法：

```js
typeof  value
```

### 返回值

返回值是 一个字符串

| 值        | typeof 返回值                     |
| --------- | --------------------------------- |
| 数字      | "number"                          |
| 字符串    | "string"                          |
| 布尔值    | "boolean"                         |
| undefined | "undefined"                       |
| null      | **"object"** ← 这是个历史遗留 bug |
| Symbol    | "symbol"                          |
| BigInt    | "bigint"                          |
| 函数      | "function"                        |
| 对象      | "object"                          |

### 3. 适用场景：

用于判断**基本数据类型**最方便。例如：

```js
javascript复制编辑typeof 123 // "number"
typeof "hello" // "string"
typeof true // "boolean"
typeof undefined // "undefined"
typeof function(){} // "function"
typeof null // "object"（注意这是个坑）
typeof {} // "object"
```

## 🔹 二、`instanceof` 运算符

判断对象的原型链上是否能找到构造函数的 `prototype` 属性。返回值是Boolean

### 1. 用法：

```
javascript


复制编辑
对象 instanceof 构造函数
```

### 3. 示例：

```
javascript复制编辑[] instanceof Array // true
[] instanceof Object // true
new Date() instanceof Date // true
new Date() instanceof Object // true

123 instanceof Number // false（因为 123 是原始值，不是 Number 对象）
new Number(123) instanceof Number // true
```

### 适用场景：

判断一个对象是否是某个构造函数的实例，**适用于引用类型**。比如：

- 判断数组：`arr instanceof Array`
- 判断日期：`date instanceof Date`

### 三、对比总结

| 特性            | `typeof`                        | `instanceof`                                  |
| --------------- | ------------------------------- | --------------------------------------------- |
| 用途            | 判断基本类型（原始值）          | 判断对象是否某类的实例                        |
| 返回值          | 字符串（如 "number"、"string"） | 布尔值（true 或 false）                       |
| 适用类型        | 原始值和函数                    | 对象（包括数组、函数、实例）                  |
| 是否能判断数组  | 否，返回 "object"               | 是，返回 true                                 |
| 是否能判断 null | 返回 "object"（误）             | 不能使用，`null instanceof Object` 返回 false |
| 是否能判断函数  | 是，返回 "function"             | 是，`fn instanceof Function` 为 true          |

### 四、额外补充（判断更精准的方法）

- 判断数组推荐使用：

  ```js
  
  Array.isArray(value)
  ```

- 判断 null：

  ```js
  
  value === null
  ```

- 判断对象是某个类的实例：

  ```js
  
  obj instanceof MyClass
  ```