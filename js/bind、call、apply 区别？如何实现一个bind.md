# bind、call、apply 区别？如何实现一个bind?

bind call apply 用来函数运行时改变this的指向

## 区别

### apply与call

apply 和 call 很相似 都是立即执行 只改变一个this 指向  不同点是 apply（）第二个参数 传入的是数据是一个数组 而call传入的是一个数据列表

apply

```js
function fn(...args){
    console.log(this,args);
}
let obj = {
    myname:"张三"
}

fn.apply(obj,[1,2]); // this会变成传入的obj，传入的参数必须是一个数组；
fn(1,2) // this指向window
```

当第一个参数为`null`、`undefined`的时候，默认指向`window`(在浏览器中)

```js
fn.apply(null,[1,2]); // this指向window
fn.apply(undefined,[1,2]); // this指向window
```

call:

```js
function fn(...args){
    console.log(this,args);
}
let obj = {
    myname:"张三"
}

fn.call(obj,1,2); // this会变成传入的obj，传入的参数必须是一个列表；
fn(1,2) // this指向window
```

同样的，当第一个参数为`null`、`undefined`的时候，默认指向`window`(在浏览器中)

```js
fn.call(null,[1,2]); // this指向window
fn.call(undefined,[1,2]); // this指向window
```

### bind

bind方法和call很相似，第一参数也是`this`的指向，后面传入的也是一个参数列表(但是这个参数列表可以分多次传入)

改变`this`指向后不会立即执行，而是返回一个永久改变`this`指向的函数

```js
function fn(...args){
    console.log(this,args);
}
let obj = {
    myname:"张三"
}

const bindFn = fn.bind(obj); // this 也会变成传入的obj ，bind不是立即执行需要执行一次
bindFn(1,2) // this指向obj
fn(1,2) // this指向window
```

### 小结

从上面可以看到，`apply`、`call`、`bind`三者的区别在于：

- 三者都可以改变函数的`this`对象指向
- 三者第一个参数都是`this`要指向的对象，如果如果没有这个参数或参数为`undefined`或`null`，则默认指向全局`window`
- 三者都可以传参，但是`apply`是数组，而`call`是参数列表，且`apply`和`call`是一次性传入参数，而`bind`可以分为多次传入
- `bind`是返回绑定this之后的函数，`apply`、`call` 则是立即执行

## [#](https://vue3js.cn/interview/JavaScript/bind_call_apply.html#三、实现)三、实现

eg：

```js
Object.prototype.mybind=function(obj,...args){

let fn=this//将this指向的函数存下来

return function(...resetArgs){

return fn.apply(obj,[...args,...resetArgs])

}

}
```

eg：结合new情况

```js
Object.prototype.mybind=function(obj,...args){
    let fn= this,
        
function boundFunction (...resetArgs){
         if(this instanceof boundFunction){
             return fn([...args,...resetArgs]);
         }
         
        return fn.apply(obj,[...args,...resetArgs] ) 
     
}}

```



