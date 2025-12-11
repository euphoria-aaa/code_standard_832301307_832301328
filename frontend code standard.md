# 前端开发规范手册 (Frontend Development Standards)

版本: 1.0.0 | 生效日期: 2025-12-11 | 适用范围: 前端开发团队

## 1. 技术架构与选型 (Technology Architecture)

本项目采用以下核心技术栈，开发过程中需严格遵循相关版本的最佳实践。

- 构建工具: Vite（最新稳定版）
- UI框架: React 18+ (Function Components + Hooks)
- 编程语言: JavaScript (ES6+ 规范)
- 样式方案: Tailwind CSS (Utility-first CSS)
- 图标组件: Lucide React


## 2. 命名约定 (Naming Conventions)

### 2.1 文件与组件命名 (Files \& Components)

- 组件文件：强制使用 PascalCase（大驼峰命名法），文件扩展名必须为 `.jsx`。
    - ✅ `UserProfile.jsx`, `ContactList.jsx`
    - ❌ `userProfile.js`, `contact_list.jsx`
- 组件函数名：必须与文件名保持严格一致，以便于调试和检索。

```javascript
export default function ContactList() { ... }
```


### 2.2 标识符命名 (Identifiers)

- 变量与函数：强制使用 camelCase（小驼峰命名法）。
- 布尔类型：必须使用 `is`, `has`, `should`, `can` 等谓词前缀，以明确表示其二值逻辑。
    - ✅ `isLoading`, `hasError`, `canEdit`
- 事件处理函数：推荐采用 `handle + EventName` 的格式。
    - ✅ `handleSubmit`, `handleInputChange`, `handleDeleteClick`


### 2.3 常量命名 (Constants)

- 全局常量：对于跨组件共享的配置项或魔法数字，强制使用 UPPER_SNAKE_CASE（全大写下划线）。
    - ✅ `API_BASE_URL`, `MAX_RETRY_LIMIT`


## 3. 代码风格与格式 (Code Style \& Formatting)

- 缩进 (Indentation)：统一使用 2 个空格（2 spaces）进行缩进，禁止使用 Tab。
- 语句结束符：所有语句末尾必须添加分号（;），以避免潜在的 ASI（自动分号插入）问题。
- 引号使用：字符串字面量推荐优先使用双引号（"）；JSX 属性值强制使用双引号。
- 代码块：控制流语句（if, for, while）的执行体必须包裹在花括号 `{}` 中，禁止省略花括号，即使只有一行代码。


## 4. React开发最佳实践 (React Best Practices)

### 4.1 Hooks规范

- 调用规则：Hooks 只能在函数组件的最顶层调用，严禁在循环、条件判断或嵌套函数中调用。
- 依赖管理：`useEffect` 和 `useCallback` 等 Hooks 的依赖数组（deps array）必须完整填写，禁止遗漏依赖项以防止闭包陷阱。


### 4.2 状态管理 (State Management)

- 原子化与聚合：优先使用局部状态（useState）。对于具有高相关性的多个状态字段（如表单数据），推荐合并为一个对象状态，而非声明多个离散的 useState。

```javascript
// ✅ 推荐：聚合状态
const [formData, setFormData] = useState({ name: "", email: "" });

// ❌ 不推荐：离散状态
const [name, setName] = useState("");
const [email, setEmail] = useState("");
```


### 4.3 组件内部结构 (Component Structure)

组件内部代码应遵循以下顺序，以保持可读性一致：

1. State 声明（useState, useReducer）
2. 副作用声明（useEffect, useLayoutEffect）
3. 事件处理与辅助函数
4. 渲染逻辑（return JSX）

## 5. 样式开发规范 (Styling Standards)

- Tailwind 类名顺序：为保证可维护性，类名建议遵循 布局（Layout）-> 盒模型（Box Model）-> 视觉（Visual）-> 交互（Interaction）的逻辑顺序。
- 内联样式：原则上禁止使用 `style={{...}}` 进行内联样式定义，特殊动态值除外。所有静态样式均应通过 Tailwind 工具类实现。


## 6. 注释与文档 (Comments \& Documentation)

- JSDoc 规范：所有公共组件和核心工具函数上方，必须添加 JSDoc 风格的注释，简述其功能、参数及返回值。
- 业务逻辑注释：对于复杂的算法或非显而易见的业务逻辑（如 Excel 数据清洗算法），必须添加单行注释（//）进行解释。

© 2025 XP Project Team. All Rights Reserved.

