## 一、XSS（跨站脚本攻击）

**攻击原理**：
注入恶意脚本，窃取用户信息、伪造操作等。

**防御方式**：

- **输入过滤**：对用户输入进行过滤，禁止或转义 HTML 标签（如 `<script>`）。
- **输出编码**：对输出到 HTML 页面中的数据进行编码，例如使用 `htmlspecialchars`（PHP）或 `v-html` 避免。
- **使用 CSP（Content Security Policy）**：限制可执行脚本的来源。
- **前端避免使用 `innerHTML`、`eval` 等危险 API**。

------

## 二、CSRF（跨站请求伪造）

**攻击原理**：
利用用户登录态，伪造请求。

**防御方式**：

- **使用 CSRF Token**：每个请求携带唯一 token，服务器验证。
- **SameSite Cookie 属性**：设置 `SameSite=Strict` 或 `Lax` 限制跨站发送 cookie。
- **Referer 验证**：后端验证请求来源是否来自本网站。

------

## 三、SQL 注入

**攻击原理**：
 攻击者通过构造恶意 SQL 语句插入到应用程序输入中，使数据库执行未预期的命令。

**防御方式**：

- **使用参数化查询**（预编译）：如使用 `prepareStatement()`（Java）或 ORM（如 Sequelize、TypeORM）。
- **过滤或转义用户输入**。
- **限制数据库账户权限**，避免使用 root 权限。

------

## 四、命令注入（Command Injection）

**攻击原理**：
 攻击者通过用户输入构造系统命令，被服务器执行，可能导致系统控制权被获取。

**防御方式**：

- **严格验证和过滤用户输入**。
- **避免拼接 shell 命令**，使用安全的 API（如 Python 的 `subprocess.run()` 中设置 `shell=False`）。
- **使用白名单机制**控制可执行命令。