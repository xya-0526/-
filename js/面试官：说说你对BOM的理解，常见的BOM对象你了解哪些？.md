# 说说你对BOM的理解，常见的BOM对象你了解哪些？

BOM 浏览器对象模型 是浏览器提供的 一组关于浏览器窗本身的对象属性API

与 DOM 操作页面结构不同，**BOM 主要负责与浏览器本身交互**，比如地址栏、浏览记录、窗口大小等。



## ✅ 二、常见的 BOM 对象有哪些？

### 1. **`window`**

- BOM 的顶层对象，**所有全局变量、函数、DOM/BOM 对象都挂在 window 上**

- 常见属性和方法：

  ```
  js复制编辑window.alert('Hello');        // 弹窗
  window.innerWidth;            // 窗口宽度
  window.setTimeout(fn, 1000);  // 定时器
  window.location.href;         // 当前地址栏链接
  ```

### 2. **`navigator`**

- 描述浏览器本身的信息

  ```
  navigator.userAgent;         // 获取浏览器UA
  navigator.language;          // 当前语言
  navigator.onLine;            // 是否联网
  ```

### 3. **`location`**

- 用于获取或改变 URL 地址

  ```
  location.href;               // 当前URL
  location.reload();           // 刷新页面
  location.assign('https://'); // 跳转页面（可返回）
  location.replace('https://');// 跳转页面（不能返回）
  ```

### 4. **`history`**

- 控制浏览器的历史记录

  ```
  history.back();              // 后退
  history.forward();           // 前进
  history.go(-1);              // 类似 back()
  ```

### 5. **`screen`**

- 获取用户屏幕信息

  ```
  screen.width;
  screen.height;
  ```

### 6. **`console`**

- 调试输出

  ```
  console.log();
  console.error();
  ```



## ✅ 对比分析：BOM vs DOM

| 项目         | DOM（文档对象模型）                          | BOM（浏览器对象模型）                      |
| ------------ | -------------------------------------------- | ------------------------------------------ |
| **作用对象** | HTML 文档中的元素结构（页面内容）            | 浏览器窗口和环境（地址栏、历史记录等）     |
| **核心对象** | `document`                                   | `window`                                   |
| **代表方法** | `getElementById`、`appendChild`、`innerHTML` | `alert`、`setTimeout`、`location.href`     |
| **操作内容** | 节点的增删改查、事件绑定、内容修改等         | 浏览器地址跳转、历史控制、弹窗、屏幕信息等 |
| **依赖关系** | DOM 是 BOM 的一部分                          | BOM 包括 DOM、Location、Navigator 等       |
| **标准归属** | W3C 标准                                     | 非 W3C 标准（由浏览器厂商实现）            |
| **使用频率** | 非常高，构建页面 UI 必不可少                 | 视场景而定，常用于页面跳转、环境判断等     |

​     一句话概括

> **DOM** 是操作网页内容的接口，
>  **BOM** 是操作浏览器窗口和行为的接口。



## ✅ 四、常见面试延伸问题

- `location.assign` 和 `location.replace` 区别？

  - `assign` 会保留当前页面历史，可返回
  - `replace` 替换当前页面，**无法返回**

- `setTimeout` 和 `setInterval` 有什么区别？

  - `setTimeout` 是延迟一次执行，`setInterval` 是周期性执行

- 如何获取用户设备是移动端还是 PC？

  ```js
  
  /Mobile|Android|iPhone/.test(navigator.userAgent)
  ```

## ✅ 总结一句话（结束语）

> BOM 主要用于操作浏览器环境，如地址栏、历史记录、弹窗、定时器等，是前端和浏览器交互的重要接口，掌握常见对象和方法对于编写动态 Web 应用非常关键。