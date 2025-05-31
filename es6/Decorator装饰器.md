### 一、什么是 Decorator？

> **Decorator（装饰器）是一种用于“注解”或“修改”类和类成员行为的语法糖。**

它本质上是一个函数，用来扩展类、属性、方法等的功能。虽然 ES6 没正式标准化 Decorator，但在 **ES 装饰器提案（目前是 Stage 3）** 中已经有相对稳定的语法，且在 **TypeScript 和 Babel 中广泛使用**。

### 二、基本使用示例（以类为例）

```
function readonly(target, key, descriptor) {
  descriptor.writable = false;
  return descriptor;
}

class Person {
  @readonly
  name = '张三';
}
```

这里的 `@readonly` 就是一个装饰器，用于修改 `name` 属性的描述符。

### 三、Decorator 可以修饰什么？

根据提案，装饰器可以用于：

| 装饰对象 | 示例说明                       |
| -------- | ------------------------------ |
| 类       | `@controller class MyClass {}` |
| 类方法   | `@log method() {}`             |
| 类属性   | `@readonly name = ''`          |
| 存取器   | `@log get name() {}`           |
| 静态成员 | `@log static method() {}`      |

四、使用场景举例

####  **Vue / Angular / NestJS 等框架中的广泛使用**

- 在 Vue3 + TypeScript 中装饰器常用于 Vue Class Component。

- 在 NestJS 中：

  ```
  @Controller('/user')
  export class UserController {
    @Get()
    getUser() {}
  }
  ```