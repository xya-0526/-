# buffer

buffer 是 node.js 专门处理  二进制数据 的 类 不是js原生提供 是 在 node.js 中 处理二进制数据的主要方式。

js 只能处理 utf-16的数据格式 不擅长处理二进制 而 node.js 经常需要对二进制数据进行操作。

例如 文件系统读写  图片视频流 压缩包 加密数据 网络数据这都需要buffer  



常用方法  .length   tostring() 

```js
const buf = Buffer.from('hello');

// 获取长度
buf.length;

// 转成字符串
buf.toString(); // "hello"

// 修改内容
buf[0] = 0x48; // 'H'

```

### **五、Buffer 的应用场景**

| 场景       | 示例                                                         |
| ---------- | ------------------------------------------------------------ |
| 文件操作   | 用 `fs.readFile()` 或 `fs.createReadStream()` 读文件时返回的是 `Buffer` |
| 网络传输   | TCP/HTTP 通讯中的数据传输通常是 Buffer（如 socket 通讯）     |
| 流媒体     | 视频、音频、图片的分片传输                                   |
| 数据转换   | Buffer 可用于 Base64、Hex、二进制与字符串的相互转换          |
| 加密哈希   | 与 `crypto` 模块结合，如生成 MD5、SHA256                     |
| 大文件上传 | 分片上传、断点续传需要 Buffer 来处理每一块数据               |

### **六、补充：Buffer vs Stream**

- `Buffer` 是一次性加载内存；
- `Stream` 是分段读取，适合大文件处理；
- 但二者经常**配合使用**，例如流事件触发时收到的 `chunk` 通常是一个 `Buffer`。

------

### **七、总结一句话**

> Buffer 是 Node.js 提供的用于处理二进制数据的核心模块，广泛应用于文件、网络、流媒体等 I/O 操作中，是构建底层高性能 Node 应用的基础能力。