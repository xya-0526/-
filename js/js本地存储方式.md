## **JavaScript 本地存储的方式主要有以下几种：**

### 1. **Cookie**

- **大小限制**：约 4KB
- **生命周期**：可设置过期时间
- **作用域**：每次请求都会自动携带在 HTTP 请求头中（影响性能）
- **API**：`document.cookie`
- **用途场景**：
  - 用于需要服务器识别的状态，比如用户登录态（如 token）
  - 跨页面简单数据传递
  - 多页面

------

### 2. **localStorage**

- **大小限制**：约 5MB

- **生命周期**：**持久存储**，除非手动删除，否则永久存在

- **作用域**：同源下的所有页面共享

- **API**：

  ```
  js复制编辑localStorage.setItem('key', 'value');
  localStorage.getItem('key');
  localStorage.removeItem('key');
  localStorage.clear();
  ```

- **用途场景**：

  - 缓存用户偏好设置（如主题、语言）
  - 存储不频繁变动的数据，如页面配置、静态数据缓存
  - 也能存放token
  - spa单页面 vue react框架

------

### 3. **sessionStorage**

- **大小限制**：约 5MB
- **生命周期**：**会话级别存储**，**关闭标签页即失效**
- **作用域**：同源 + 同标签页有效
- **API**：与 `localStorage` 相同
- **用途场景**：
  - 存储临时数据（如表单数据、分页状态）
  - 单页面应用（SPA）中的页面跳转状态传递

------

### 4. **IndexedDB**

- **大小限制**：通常比 localStorage 更大（几十 MB 甚至更高，取决于浏览器）
- **生命周期**：持久存储
- **特点**：
  - 异步操作
  - 支持对象存储、索引、事务
  - 适合存储结构化数据
- **用途场景**：
  - 大型离线应用（如本地笔记、离线文档）
  - PWA（Progressive Web App）缓存数据
  - 浏览器本地数据库操作