# js数据类型

基本类型:

- number
- string
- boolean
- undefine
- null
- symbol

复杂类型（引用类型）：

- object
- array
- function

# 基本类型

## number

在数值类型中，存在一个特殊数值`NaN`，意为“不是数值”，用于表示本来要返回数值的操作失败了（而不是抛出错误）

## undefine

`Undefined` 类型只有一个值，就是特殊值 `undefined`。当使用 `var`或 `let`声明了变量但没有初始化时，就相当于给变量赋予了 `undefined`值

### String

字符串可以使用双引号（"）、单引号（'）或反引号（`）标示

```js
let firstName = "John";
let lastName = 'Jacob';
let lastName = `Jingleheimerschmidt`
```

字符串是不可变的，意思是一旦创建，它们的值就不能变了

```js
let lang = "Java";
lang = lang + "Script";  // 先销毁再创建
```

### Null

```
Null`类型同样只有一个值，即特殊值 `null
```

逻辑上讲， null 值表示一个空对象指针，这也是给`typeof`传一个 `null` 会返回 `"object"` 的原因

```js
let car = null;
console.log(typeof car); // "object"
```

`undefined` 值是由 `null`值派生而来

```js
console.log(null == undefined); // true
```

只要变量要保存对象，而当时又没有那个对象可保存，就可用 `null`来填充该变量

### Boolean

```
Boolean`（布尔值）类型有两个字面值： `true` 和`false
```

通过`Boolean`可以将其他类型的数据转化成布尔值

规则如下：

| 数据类型      				转换为 true 的值      				转换为 false 的值 |      |      |
| :----------------------------------------------------------- | ---- | ---- |
| String        				 非空字符串          					"" |      |      |
| Number 				非零数值（包括无穷值）				0 、 NaN |      |      |
| Object 					 任意对象 						  null |      |      |
| Undefined 					N/A （不存在） 				undefined |      |      |

### [#](https://vue3js.cn/interview/JavaScript/data_type.html#symbol)Symbol

Symbol （符号）是原始值，且符号实例是唯一、不可变的。符号的用途是确保对象属性使用唯一标识符，不会发生属性冲突的危险

```js
let genericSymbol = Symbol();
let otherGenericSymbol = Symbol();
console.log(genericSymbol == otherGenericSymbol); // false

let fooSymbol = Symbol('foo');
let otherFooSymbol = Symbol('foo');
console.log(fooSymbol == otherFooSymbol); // false
```

手写一个symbol

```js
function mySymbol(desc = "") {
  const uniqueKey = `__mysymbol_${desc}_${Math.random().toString(36).slice(2)}__`;
  return uniqueKey;
}
```

# 引用类型

### Object

创建`object`常用方式为对象字面量表示法，属性名可以是字符串或数值

```js
let person = {
    name: "Nicholas",
    "age": 29,
    5: true
};
```

1
2
3
4
5

### [#](https://vue3js.cn/interview/JavaScript/data_type.html#array)Array

`JavaScript`数组是一组有序的数据，但跟其他语言不同的是，数组中每个槽位可以存储任意类型的数据。并且，数组也是动态大小的，会随着数据添加而自动增长

```js
let colors = ["red", 2, {age: 20 }]
colors.push(2)
```

1
2

### [#](https://vue3js.cn/interview/JavaScript/data_type.html#function)Function

函数实际上是对象，每个函数都是 `Function`类型的实例，而 `Function`也有属性和方法，跟其他引用类型一样

函数存在三种常见的表达方式：

- 函数声明

```js
// 函数声明
function sum (num1, num2) {
    return num1 + num2;
}
```

- 函数表达式

```js
let sum = function(num1, num2) {
    return num1 + num2;
};
```

- 箭头函数

函数声明和函数表达式两种方式

```js
let sum = (num1, num2) => {
    return num1 + num2;
};
```

### [#](https://vue3js.cn/interview/JavaScript/data_type.html#其他引用类型)其他引用类型

除了上述说的三种之外，还包括`Date`、`RegExp`、`Map`、`Set`等......

## [#](https://vue3js.cn/interview/JavaScript/data_type.html#三、存储区别)三、存储区别

## 存储区别

基本数据类型和引用数据类型存储在内存中的位置不同：

- 基本数据类型存储在栈中
- 引用类型的对象存储于堆中

当我们把变量赋值给一个变量时，解析器首先要确认的就是这个值是基本类型值还是引用类型值

下面来举个例子

### [#](https://vue3js.cn/interview/JavaScript/data_type.html#基本类型)基本类型

```js
let a = 10;
let b = a; // 赋值操作
b = 20;
console.log(a); // 10值
```

`a`的值为一个基本类型，是存储在栈中，将`a`的值赋给`b`，虽然两个变量的值相等，但是两个变量保存了两个不同的内存地址

### [#](https://vue3js.cn/interview/JavaScript/data_type.html#引用类型)引用类型

```js
var obj1 = {}
var obj2 = obj1;
obj2.name = "Xxx";
console.log(obj1.name); // xxx
```

引用类型数据存放在堆中，每个堆内存对象都有对应的引用地址指向它，引用地址存放在栈中。

`obj1`是一个引用类型，在赋值操作过程汇总，实际是将堆内存对象在栈内存的引用地址复制了一份给了`obj2`，实际上他们共同指向了同一个堆内存对象，所以更改`obj2`会对`obj1`产生影响