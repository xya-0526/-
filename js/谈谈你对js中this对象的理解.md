# this 对象的理解

js中 `this` 是一个在函数运行时自动生成的特殊对象，它的指向**不是在定义时确定的，而是在调用时确定的**。`this` 的最终指向取决于函数的调用方式（不是声明方式）

根据不同的使用场合，`this`有不同的值，主要分为下面几种情况：

- 默认绑定（普通函数调用）
- 隐式绑定（对象调用函数）
- new绑定（构造函数和类）
- 显示绑定（主动指定this指向）

## 默认绑定

普通函数调用 this对象 默认 指向window 

```js
eg: function getname(){
   return this. name
} 
var name="hahah"
consloe.log(getname())//hahahah

```

## 隐式绑定（对象调用函数）

对象 调用函数后  this指向 调用函数的对象 

即 函数还可以作为某个对象的方法调用，这时`this`就指这个上级对象

```js
function test() {
  console.log(this.x);
}

var obj = {};
obj.x = 1;
obj.m = test;

obj.m(); // 1
```

这个函数中包含多个对象，尽管这个函数是被最外层的对象所调用，`this`指向的也只是它上一级的对象

```js
var o = {
    a:10,
    b:{
        fn:function(){
            console.log(this.a); //undefined
        }
    }
}
o.b.fn();
```

## new绑定

new 对象和 类  this 会指向 被创建出来的实例对象 

```js
function test() {
　this.x = 1;
}

var obj = new test();
obj.x // 1
```

这里再列举一些特殊情况：

`new`过程遇到`return`一个对象，此时`this`指向为返回的对象

```js
function fn()  
{  
    this.user = 'xxx';  
    return {};  
}
var a = new fn();  
console.log(a.user); //undefined
```

如果返回一个简单类型的时候，则`this`指向实例对象

```js
function fn()  
{  
    this.user = 'xxx';  
    return 1;
}
var a = new fn;  
console.log(a.user); //xxx
```

注意的是`null`虽然也是对象，但是此时`new`仍然指向实例对象

```js
function fn()  
{  
    this.user = 'xxx';  
    return null;
}
var a = new fn;  
console.log(a.user); //xxx
```

### 显示修改

`apply()、call()、bind()`是函数的一个方法，作用是改变函数的调用对象。它的第一个参数就表示改变后的调用这个函数的对象。因此，这时`this`指的就是这第一个参数

```js
var x = 0;
function test() {
　console.log(this.x);
}

var obj = {};
obj.x = 1;
obj.m = test;
obj.m.apply(obj) // 1
```

## 箭头函数

箭头函数的this 指向 箭头函数外层

在 ES6 的语法中还提供了箭头函语法，让我们在代码书写时就能确定 `this` 的指向（编译时绑定）

```js
const obj = {
  sayThis: () => {
    console.log(this);
  }
};

obj.sayThis(); // window 因为 JavaScript 没有块作用域，所以在定义 sayThis 的时候，里面的 this 就绑到 window 上去了
const globalSay = obj.sayThis;
globalSay(); // window 浏览器中的 global 对象
```

箭头函数不能作为构建函数

## 优先级

new绑定优先级 > 显示绑定优先级 > 隐式绑定优先级 > 默认绑定优先级

```js
function foo(something) {
    this.a = something;
}

var obj1 = {};

var bar = foo.bind( obj1 );
bar( 2 );
console.log( obj1.a ); // 2

var baz = new bar( 3 );
console.log( obj1.a ); // 2
console.log( baz.a ); // 3
```

总结：

正确理解 `this` 是掌握 JavaScript 执行上下文、作用域和函数行为的关键
