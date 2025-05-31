# 构造函数new原做了那些操作

当我们使用 `new` 创建实例对象时，执行过程包括：

1. 创建一个新的空对象。
2. 将这个对象的原型链指向构造函数的 `prototype`，从而实现实例对象可以访问构造函数原型上的属性和方法。
3. 将构造函数内部的 `this` 绑定到这个新创建的对象，实现对实例的属性赋值。
4. 如果构造函数没有返回其他对象，则返回这个新创建的实例对象。

# 手写一个

```

function myNew(fn,...args){
let obj={}
obj._proto_=student.prototype
const result=fn.aplay(obj,...args)
return result instanceof Object ? result:obj
}
```

