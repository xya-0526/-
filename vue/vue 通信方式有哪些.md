# vue 通信方式

组件通信分为

1. 父子通信 
2. 兄弟之间通信
3. 祖孙通信
4. 无关系通信

父子通信常用

1.props

2.ref

- 父组件在使用子组件的时候设置`ref`
- 父组件通过设置子组件`ref`来获取数据

父组件

```js
<Children ref="foo" />  
  
this.$refs.foo  // 获取子组件实例，通过子组件实例我们就能拿到对应的数据  
```

3.$emit

- 适用场景：子组件传递数据给父组件
- 子组件通过`$emit触发`自定义事件，`$emit`第二个参数为传递的数值
- 父组件绑定监听器获取到子组件传递过来的参数

```js
Chilfen.vue
this.$emit('add', good)  
```



```js
Father.vue
<Children @add="cartAdd($event)" />  
```



兄弟之间传递

4.Eventbus

```js
Vue.prototype.$bus = new Vue() // Vue已经实现了Bus的功能  
Children1.vue

this.$bus.$emit('foo')  
Children2.vue

this.$bus.$on('foo', this.handle)  
```

5 通过共同祖辈`$parent`或者`$root`搭建通信桥连

兄弟组件

```js
this.$parent.on('add',this.add)
```

另一个兄弟组件

```js
this.$parent.emit('add')
```

6 provide 与 inject

- 在祖先组件定义`provide`属性，返回传递的值
- 在后代组件通过`inject`接收组件传递过来的值

祖先组件

```js
provide(){  
    return {  
        foo:'foo'  
    }  
}  
```

后代组件

```js
inject:['foo'] // 获取到祖先组件传递过来的值  
```

7$attrs 与$ listeners

- 适用场景：祖先传递数据给子孙
- 设置批量向下传属性`$attrs`和 `$listeners`
- 包含了父级作用域中不作为 `prop` 被识别 (且获取) 的特性绑定 ( class 和 style 除外)。
- 可以通过 `v-bind="$attrs"` 传⼊内部组件

```js
// child：并未在props中声明foo  
<p>{{$attrs.foo}}</p>  
  
// parent  
<HelloWorld foo="foo"/>  
```

```js
// 给Grandson隔代传值，communication/index.vue  
<Child2 msg="lalala" @some-event="onSomeEvent"></Child2>  
  
// Child2做展开  
<Grandson v-bind="$attrs" v-on="$listeners"></Grandson>  
  
// Grandson使⽤  
<div @click="$emit('some-event', 'msg from grandson')">  
{{msg}}  
</div>  
```