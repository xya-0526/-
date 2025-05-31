# 字符串常用方法

五类：

1.获取查询 :inculdes  length  charAt  startsWith endsWith

2.拆分，截取 split, slice substring substr  

3.修改构造 repalce ,padStart padEnd   repeat tirm,

4.大小写转换toupperCase tolowerCase

5.类型转换toString



​           

## ✅ 1. **获取和检查**

| 方法                  | 作用                   | 示例                            |
| --------------------- | ---------------------- | ------------------------------- |
| `length`              | 获取字符串长度         | `'hello'.length → 5`            |
| `charAt(index)`       | 返回指定索引的字符     | `'abc'.charAt(1) → 'b'`         |
| `charCodeAt(index)`   | 返回字符的 UTF-16 编码 | `'A'.charCodeAt(0) → 65`        |
| `includes(substr)`    | 是否包含子字符串       | `'abc'.includes('b') → true`    |
| `startsWith(substr)`  | 是否以某子串开头       | `'abc'.startsWith('a') → true`  |
| `endsWith(substr)`    | 是否以某子串结尾       | `'abc'.endsWith('c') → true`    |
| `indexOf(substr)`     | 返回子串首次出现位置   | `'banana'.indexOf('a') → 1`     |
| `lastIndexOf(substr)` | 返回子串最后出现位置   | `'banana'.lastIndexOf('a') → 5` |



------

## ✅ 2. **截取与拆分**

| 方法                    | 作用                                 | 示例                                 |
| ----------------------- | ------------------------------------ | ------------------------------------ |
| `slice(start, end)`     | 截取字符串                           | `'abcdef'.slice(1, 4) → 'bcd'`       |
| `substring(start, end)` | 同上，但不支持负值                   | `'abcdef'.substring(1, 4) → 'bcd'`   |
| `substr(start, length)` | 从指定位置开始截取指定长度（不推荐） | `'abcdef'.substr(1, 3) → 'bcd'`      |
| `split(separator)`      | 拆分为数组                           | `'a,b,c'.split(',') → ['a','b','c']` |



------

## ✅ 3. **修改与构造**

| 方法                          | 作用                     | 示例                                   |
| ----------------------------- | ------------------------ | -------------------------------------- |
| `replace(search, replace)`    | 替换内容                 | `'abc'.replace('b', 'x') → 'axc'`      |
| `replaceAll(search, replace)` | 替换所有匹配项（ES2021） | `'aabb'.replaceAll('b', 'x') → 'aaxx'` |
| `concat(str)`                 | 拼接字符串               | `'a'.concat('b') → 'ab'`               |
| `repeat(n)`                   | 重复字符串               | `'ha'.repeat(3) → 'hahaha'`            |
| `padStart(length, padStr)`    | 左侧补齐                 | `'5'.padStart(3, '0') → '005'`         |
| `padEnd(length, padStr)`      | 右侧补齐                 | `'5'.padEnd(3, '0') → '500'`           |
| `trim()`                      | 去除前后空格             | `'  hi  '.trim() → 'hi'`               |
| `trimStart()` / `trimEnd()`   | 去除前/后空格            | `'  hi'.trimStart() → 'hi'`            |



------

## ✅ 4. **大小写转换**

| 方法            | 作用     | 示例                          |
| --------------- | -------- | ----------------------------- |
| `toUpperCase()` | 转为大写 | `'abc'.toUpperCase() → 'ABC'` |
| `toLowerCase()` | 转为小写 | `'ABC'.toLowerCase() → 'abc'` |



------

## ✅ 5. **原始值与对象转换**

| 方法         | 作用               | 示例                      |
| ------------ | ------------------ | ------------------------- |
| `valueOf()`  | 返回字符串的原始值 | `'abc'.valueOf() → 'abc'` |
| `toString()` | 转换为字符串       | `123..toString() → '123'` |



------

## 🧪 补充高级用法

| 场景              | 示例                                          |
| ----------------- | --------------------------------------------- |
| 使用正则替换      | `'a1b2'.replace(/\d/g, '-') → 'a-b-'`         |
| 模板字符串（ES6） | ``Hello, ${name}``                            |
| Unicode 字符处理  | `'😊'.length → 2`，可用 `Array.from(str)` 解决 |



------

## ✅ 小结思维导图（可截图）

```
perl复制编辑字符串操作
├─ 检查类 → includes, startsWith, endsWith, indexOf
├─ 获取类 → charAt, charCodeAt, length
├─ 截取类 → slice, substring, substr
├─ 替换类 → replace, replaceAll
├─ 转换类 → toUpperCase, toLowerCase, trim, pad
├─ 拼接类 → concat, repeat，padStart,padEndq
├─ 拆分类 → split
```