# 原型与原理链

在 JavaScript 中，**原型** 和 **原型链** 是实现“继承”和“对象共享行为”的核心机制。





## 原型

每一个js函数（构造函数）都拥有一个prototypes属性指向原型对象 用于给构造函数创建的实例 共享方法和属性 

```js
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function () {
  console.log(`Hello, I am ${this.name}`);
};

const p = new Person("Alice");
p.sayHello(); // Hello, I am Alice
```

## 原型链

当你访问一个对象的属性时，如果对象本身没有，会沿着它的 `__proto__`（也叫 `[[Prototype]]`）一直向上查找，直到 `null`。这条查找路径就叫做**原型链**。

```js
console.log(p.__proto__ === Person.prototype); // true
console.log(Person.prototype.__proto__ === Object.prototype); // true
console.log(Object.prototype.__proto__ === null); // true
```

## 🔶 三、原型链的图解（类比）

```
p (实例对象)
 ↓ __proto__
 ===
Person.prototype
 ↓ __proto__
 ==
Object.prototype
 ↓ __proto__
null
```

## 🧠 原型 vs 原型链 常见混淆

| 概念        | 含义                                           |
| ----------- | ---------------------------------------------- |
| `prototype` | 构造函数的一个属性                             |
| `__proto__` | 实例对象的隐藏属性，指向构造函数的 `prototype` |
| 原型链      | 是通过 `__proto__` 连接起来的查找链条          |



- 一切对象都是继承自`Object`对象，`Object` 对象直接继承根源对象`null`
- 一切的函数对象（包括 `Object` 对象），都是继承自 `Function` 对象
- `Object` 对象直接继承自 `Function` 对象
- `Function`对象的`__proto__`会指向自己的原型对象，最终还是继承自`Object`对象

