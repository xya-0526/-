## ✅ 一、DOM 是什么？

> DOM（Document Object Model）是浏览器提供的用于操作 HTML 和 XML 文档的 API。我们可以通过 JavaScript 来动态修改页面结构、样式和内容。

## ✅ 二、常见的 DOM 操作分类

### 1. **获取元素（选择器）**

```
js复制编辑document.getElementById('id');
document.getElementsByClassName('className');
document.getElementsByTagName('div');
document.querySelector('.class');       // 单个元素
document.querySelectorAll('.class');   // NodeList
```

------

### 2. **创建 / 插入 / 删除元素**

```
js复制编辑const div = document.createElement('div'); // 创建
div.textContent = 'Hello World';

document.body.appendChild(div); // 插入到 body 末尾
parent.insertBefore(newNode, referenceNode); // 插入到指定位置

parent.removeChild(childNode); // 删除子元素
element.replaceChild(newNode, oldNode); // 替换节点
```

------

### 3. **修改元素内容和属性**

```
js复制编辑element.textContent = 'Hello';       // 设置纯文本
element.innerHTML = '<b>Hello</b>';  // 设置 HTML 内容

element.setAttribute('class', 'box');  // 设置属性
const value = element.getAttribute('class'); // 获取属性
element.removeAttribute('class'); // 删除属性
```

------

### 4. **样式操作（CSS）**

```
js复制编辑element.style.color = 'red';
element.style.fontSize = '16px';

element.classList.add('active');
element.classList.remove('hidden');
element.classList.toggle('dark-mode');
element.classList.contains('dark-mode'); // 检查是否存在
```

------

### 5. **事件绑定 / 移除**

```
js复制编辑element.addEventListener('click', function() {
  alert('clicked');
});

element.removeEventListener('click', handler); // 移除事件
```