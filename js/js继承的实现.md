# js继承的实现

js实现继承有多种方法

 1.原型链继承

2. 构造函数继承

3. 组合式继承

4. 寄生组合式继承

5. class继承

   

## 原型链继承

```js
ge:Parent(){
this.name='parent'
}
Parent.prototype.sayHello = function() {
  console.log('Hello from parent');
};
Child(name){
this.name=name;
}
Child.prototype= new Parent()
Child.prototype.constructor=Child
```

 缺点:

- 引用类型的属性会被所有实例共享。
- 无法向父类传参。

## 构造函数类型

```js
eg: Parent(name){
this.name=name
}
Parent.prototype.Say=()=>{
console.log("hha")
}
Child(name){
Parent.call(this,name)//通过call将Child的this指向Parent
}

```

 缺点：
只能继承实例属性，无法继承父类原型上的方法。

## 组合型

```js
eg:eg: Parent(name){
this.name=name
}
Parent.prototype.Say=()=>{
console.log("hha")
}
Child(name){
Parent.call(this,name)//通过call将Child的this指向Parent
}
Child.prototype=new Parent()
Child.prototype.constructor=Child

```

缺点：

- `Parent` 构造函数会被调用两次（一次给实例，一次给原型）。



## 寄生组合

## 寄生组合式继承（推荐的传统方式）

```
js复制编辑function Parent(name) {
  this.name = name;
}
Parent.prototype.sayHello = function() {
  console.log('Hello from', this.name);
};

function Child(name) {
  Parent.call(this, name); // 继承属性
}

Child.prototype = Object.create(Parent.prototype); // 创建新原型对象，不调用 Parent 构造函数
Child.prototype.constructor = Child;

const child = new Child('child1');
child.sayHello(); // Hello from child1
```

优点：

- 避免了重复调用父类构造函数。
- 继承了属性和方法。

## class继承

```js
class Parent {
    constructor(public name:string){}
   say(){
       console.log("hello")
   } 
}
class Child extends Parent{
    constructor(name:string,Public age:number){
        super(name)
    }
}
```

优点：

- 语法更清晰，更接近面向对象语言（如 Java/C++）。
- 更易读、维护和使用。

## 总结表：

| 方式         | 是否继承属性 | 是否继承方法 | 是否可传参 | 是否推荐      |
| ------------ | ------------ | ------------ | ---------- | ------------- |
| 原型链继承   | ✅            | ✅            | ❌          | ❌             |
| 构造函数继承 | ✅            | ❌            | ✅          | ❌             |
| 组合继承     | ✅            | ✅            | ✅          | ⭘（可接受）   |
| 寄生组合继承 | ✅            | ✅            | ✅          | ✅（传统推荐） |
| `class` 继承 | ✅            | ✅            | ✅          | ✅（现代推荐） |