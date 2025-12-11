# 后端开发规范手册 (Backend Development Standards)

版本: 1.0.0 | 生效日期: 2025-12-11 | 适用范围: 后端开发团队

## 1. 技术架构 (Technology Architecture)

- 运行环境: Node.js (LTS 版本)
- Web 框架: Express.js
- 包管理器: npm (Node Package Manager)


## 2. 命名约定 (Naming Conventions)

### 2.1 文件与目录

- 命名格式：文件及目录名推荐使用 kebab-case（短横线命名法）或 camelCase，团队内部需保持统一。
    - ✅ `server.js`，`routes/user-routes.js`
    - ❌ `Server.js`，`UserRoutes.js`


### 2.2 变量与函数

- 格式：强制使用 camelCase (小驼峰命名法)。
    - ✅ `getContacts`，`updateUserProfile`
    - ❌ `GetContacts`，`update_user_profile`


### 2.3 API 接口设计 (RESTful API)

- 路径命名：资源路径应使用 kebab-case，且必须使用名词复数形式。
- HTTP 动词：严格遵循 RESTful 语义。
    - ✅ `GET /api/contacts`（获取资源列表）
    - ✅ `POST /api/contacts`（创建新资源）
    - ✅ `PUT /api/contacts/:id`（全量更新资源）
    - ✅ `PATCH /api/contacts/:id`（部分更新资源）
    - ❌ `/api/getAllContacts`（禁止在 URL 中包含动词）


## 3. 代码结构与规范 (Code Structure \& Standards)

- 缩进：统一使用 2 个空格。
- 异步编程：
    - 强制使用 `async/await` 语法处理异步操作，禁止使用回调地狱 (Callback Hell) 模式。
    - 异常捕获：所有 `async` 函数内部必须使用 `try...catch` 块包裹核心逻辑，或使用中间件进行统一的错误处理，防止未捕获异常导致服务崩溃。

```javascript
// ✅ 标准示范
app.get('/api/data', async (req, res) => {
  try {
    const data = await fetchData();
    res.status(200).json(data);
  } catch (error) {
    console.error('[Data Fetch Error]:', error);
    res.status(500).json({ error: "Internal Server Error" });
  }
});
```


## 4. 安全与性能规约 (Security \& Performance Protocols)

### 4.1 输入验证 (Input Validation)

- 零信任原则：严禁直接信任客户端传输的任何数据（`req.body`，`req.query`，`req.params`）。在处理业务逻辑前，必须对关键字段进行存在性及格式校验。

```javascript
if (!req.body.name || typeof req.body.name !== 'string') {
  return res.status(400).json({ error: "Invalid or missing 'name' field" });
}
```


### 4.2 跨域资源共享 (CORS)

- 中间件配置：必须在应用层引入并配置 `cors` 中间件。在生产环境中，建议配置 `origin` 白名单，而非使用通配符 `*`。


### 4.3 HTTP 状态码规范

API 响应必须返回语义准确的 HTTP 状态码：

- `200 OK`：请求成功。
- `201 Created`：资源创建成功。
- `400 Bad Request`：客户端请求参数无效。
- `401 Unauthorized`：未授权/未登录。
- `404 Not Found`：请求的资源不存在。
- `500 Internal Server Error`：服务器内部错误。


## 5. 日志与监控 (Logging \& Monitoring)

- 操作日志：关键业务操作（如数据增删改）必须输出日志以便审计。
- 敏感信息屏蔽：在生产环境日志中，严禁输出用户密码、Token、密钥等敏感信息。


## 6. 版本控制规范 (Version Control)

Git 提交信息 (Commit Message) 需遵循 Conventional Commits 规范：
格式：`<type>: <subject>`

- Types:
    - `feat`：新增功能 (Feature)
    - `fix`：修复缺陷 (Bug Fix)
    - `docs`：文档变更 (Documentation)
    - `style`：代码格式调整 (Formatting, missing semi colons, etc)
    - `refactor`：代码重构 (Code Refactoring)
- 示例:
    - `feat: implement contact bookmarking API`
    - `fix: resolve CORS issues in cloud environment`

© 2025 XP Project Team. All Rights Reserved.

