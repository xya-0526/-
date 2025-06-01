# fs 模块

什么是 fs 模块 ？

fs 是 node.js的核心模块之一 常用来 对文件进行 读写 删除 创建等操作

支持同步和异步  建议 使用异步 防止阻塞主进程

应用场景 ：

文件读写 （日志，配置文件） readFile writeFile  appendFile 

读取大文件 （大文件 视频 切片上传 ）Createreadstream() createwritestream  

创建删除目录文件 mkdir rmdir 

文件名文件状态 readdir stat

读取静态资源

常用方法 ：

1. `fs.readFile(path[, options], callback)`

- 异步读取文件内容。

```
const fs = require('fs');
fs.readFile('test.txt', 'utf-8', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

2. fs.writeFile(file, data[, options], callback)

- 异步写入（覆盖）文件内容。

```js
fs.writeFile('test.txt', 'Hello, world!', (err) => {
  if (err) throw err;
});
```

 3. `fs.appendFile(file, data[, options], callback)`

- 在文件末尾追加内容。

```js
fs.appendFile('log.txt', '一条日志\n', (err) => {
  if (err) throw err;
});
```

✅ 4. `fs.unlink(path, callback)`

- 删除文件。

```
js复制编辑fs.unlink('test.txt', (err) => {
  if (err) throw err;
});
```

------

✅ 5. `fs.mkdir(path[, options], callback)` / `fs.rmdir(path, callback)`

- 创建/删除目录。

------

✅ 6. `fs.readdir(path, callback)`

- 读取目录下所有文件名。

```
js复制编辑fs.readdir('./logs', (err, files) => {
  console.log(files);
});
```

✅ **7. `fs.stat(path, callback)`**

- 获取文件或目录的状态信息（是否存在、是否为文件等）。

```
js复制编辑fs.stat('test.txt', (err, stats) => {
  if (!err && stats.isFile()) {
    console.log('是文件');
  }
});
```

------

✅ **8. 流操作：`fs.createReadStream()` / `fs.createWriteStream()`**

- 适用于大文件处理，节省内存，常用于上传、下载、视频播放等。

```
js复制编辑const readStream = fs.createReadStream('big.txt');
readStream.on('data', chunk => {
  console.log(chunk.toString());
});
```

### **五、总结一句话**

> `fs` 模块是 Node.js 操作文件系统的核心模块，支持异步和同步两种方式，常用于文件的读写、删除、目录管理和流式处理，适合构建服务端程序和处理本地资源。