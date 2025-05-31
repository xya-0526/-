# ajax原理

ajax 是一项网络请求技术 能够在不刷新整个页面的情况下实现与服务器 交换数据 和局部页面的更新。

## 原理

ajax 核心 是通过 原生 XML或者更现代的 fetch API 与服务器进行异步通信 

 从而在不刷新页面的情况下获取或发送数据

### 工作流程

1.用户 页面上进行某些操作 

2. 创建一个异步请求
3. 请求被发送发到服务器
4. 服务器处理请求返回数据
5. 客户端接收到数据用js更新dom

## ✅ 三、AJAX 的实现方式

### 方式一：使用原生 `XMLHttpRequest`

```
js复制编辑const xhr = new XMLHttpRequest();
xhr.open('GET', 'https://api.example.com/data', true); // true 表示异步
xhr.onreadystatechange = function () {
  if (xhr.readyState === 4 && xhr.status === 200) {
    const response = JSON.parse(xhr.responseText);
    console.log(response);
    // 处理数据，比如更新页面内容
  }
};
xhr.send(); // 发送请求
```

> `readyState === 4` 表示请求已完成
>  `status === 200` 表示请求成功

------

### 方式二：使用现代的 `fetch`（更简洁）

```
js复制编辑fetch('https://api.example.com/data')
  .then(response => response.json())
  .then(data => {
    console.log(data);
    // 更新页面
  })
  .catch(error => {
    console.error('出错了：', error);
  });
```

------

## ✅ 四、特点总结

| 特点         | 说明                                    |
| ------------ | --------------------------------------- |
| 异步         | 不阻塞页面渲染或其他操作                |
| 局部更新     | 只更新需要的部分 DOM，不刷新整个页面    |
| 基于标准接口 | 早期用 `XMLHttpRequest`，现代用 `fetch` |
| 多种数据格式 | 支持 JSON、XML、HTML、Text 等           |



------

## ✅ 五、简单封装一个 AJAX 工具函数（用 XMLHttpRequest）

```
js复制编辑function ajax({ method = 'GET', url, data = null, success, error }) {
  const xhr = new XMLHttpRequest();
  xhr.open(method, url, true);

  if (method === 'POST') {
    xhr.setRequestHeader('Content-Type', 'application/json');
  }

  xhr.onreadystatechange = function () {
    if (xhr.readyState === 4) {
      if (xhr.status >= 200 && xhr.status < 300) {
        success && success(JSON.parse(xhr.responseText));
      } else {
        error && error(xhr.status);
      }
    }
  };

  xhr.send(method === 'POST' ? JSON.stringify(data) : null);
}
```

------

## ✅ 六、实际应用场景举例

- 搜索建议（输入时动态加载结果）
- 表单异步提交
- 滚动加载更多内容（无限下拉）
- 数据可视化（实时拉取图表数据）
- SPA 页面（局部刷新）



