# Thirdweb - 现代化 Vue 3 前端工程化框架

## 📖 项目介绍
Thirdweb 是一个基于 **Vue 3**、**Vite** 和 **Tailwind CSS** 构建的现代化前端项目。本项目旨在为开发者提供一个高效、可扩展且易于维护的开发基座。通过模块化架构设计与原子化 CSS 实践，Thirdweb 能够快速响应业务需求，并集成了 **Element Plus** UI 框架以提供卓越的用户交互体验。

在工程化实践中，本项目成功解决了复杂网境下的协议转换、系统路径编码兼容性以及动态依赖补全等实战问题。

---

## 🛠 技术栈 (Tech Stack)

| 维度 | 技术选型 | 说明 |
| :--- | :--- | :--- |
| **核心框架** | Vue 3 (Composition API) | 响应式数据流与组件化开发 |
| **构建引擎** | Vite 6.x | 极速的热更新 (HMR) 与原生 ESM 支持 |
| **样式方案** | Tailwind CSS + PostCSS | 原子化 CSS，提升 UI 开发效率 |
| **UI 组件库** | Element Plus | 适配 Vue 3 的桌面端组件库 |
| **路由/状态** | Vue Router 4 / Vuex 4 | 标准化路由管理与全局状态同步 |
| **网络请求** | Axios | 基于 Promise 的 HTTP 客户端 |
| **包管理器** | PNPM | 磁盘空间高效、依赖安装速度快 |

---

## 📂 项目结构 (Project Structure)

```text
thirdweb/
├── public/                # 静态资源目录 (Favicon, Logo等)
├── src/                   # 源代码核心
│   ├── api/               # API 请求模块映射
│   ├── components/        # 跨页面可复用 Vue 组件
│   ├── views/             # 页面级业务组件
│   ├── router/            # Vue Router 路由配置
│   ├── store/             # Vuex 状态管理中心
│   ├── styles/            # 全局样式与 Tailwind 指令
│   ├── App.vue            # 应用根组件
│   └── main.js            # 程序入口文件 (挂载 Vue 实例与全局插件)
├── .env                   # 全局基础环境变量
├── .env.development       # 开发环境特定配置
├── tailwind.config.js     # Tailwind CSS 自定义配置
├── vite.config.js         # Vite 引擎与插件配置
├── package.json           # 项目清单及依赖管理
└── README.md              # 项目工程说明文档

```

---

## 🚀 开始运行 (Getting Started)

### 1. 环境准备

* **Node.js**: 推荐使用 **Node.js 20** 或更高版本（本项目已在 v24.12.0 环境下通过验证）。
* **PNPM**: 建议安装最新版本以获得最佳的依赖处理性能。
```powershell
npm install -g pnpm

```



### 2. 依赖安装与专项修复

针对本项目在运行过程中发现的动态依赖缺失问题，请执行以下命令进行全量安装与补丁修复：

```powershell
# 步骤 A: 安装 package.json 中的标准依赖
pnpm install

# 步骤 B: 专项修复：手动补全缺失的 UI 展示插件
pnpm add vue-json-pretty

```

### 3. 开发服务器运行

```powershell
# 启动热更新开发环境
pnpm dev

```

* **默认访问地址**: `http://localhost:8085/`
* **注意**: 若 8085 端口被占用，Vite 会自动递增端口，请参考终端输出。

### 4. 生产环境构建与预览

```powershell
# 执行静态资源构建
pnpm build

# 本地预览构建产物
pnpm preview

```

<img width="2559" height="1522" alt="c2719a556059c938ed20a48e207e0d98" src="https://github.com/user-attachments/assets/e4930cb6-1d58-44f7-902e-6ed52867509c" />

---

## 🛠 核心技术挑战与解决方案 (Troubleshooting)

在项目部署与环境对齐过程中，我们克服了以下四个维度的工程挑战：

### 1. 现代前端依赖的“碎片化”修复

* **现象**: 项目启动时提示 `Module not found: Error: Can't resolve 'vue-json-pretty'`。
* **成因**: 源代码中引用了 JSON 格式化组件，但该依赖未包含在初始 `package.json` 中。
* **对策**: 执行 `pnpm add vue-json-pretty` 进行动态补全，并通过更新 `pnpm-lock.yaml` 确保了依赖树的原子化闭环。

### 2. 网络链路突围：HTTPS 到 SSH 的协议切换

* **现象**: 在特定网境（如校园网）下，GitHub 443 端口连接超时，导致无法推送代码。
* **对策**: 将 Git 协议由 HTTPS 重构为 **SSH (Port 22)**，利用 **ED25519** 椭圆曲线加密算法重建安全隧道，成功绕过了应用层拦截。

### 3. 非 ASCII 路径导致的系统级编码冲突

* **现象**: Windows 中文用户名路径（`C:\Users\郑睿泽`）导致 SSH 客户端在保存主机指纹时出现八进制转义异常（报错 `\326\243`）。
* **对策**: 执行**环境标准化迁移**。将项目整体迁移至纯英文路径（`C:\Users\zrz`），彻底消除非 ASCII 字符对底层 Git 工具链的干扰。

### 4. 目录层级嵌套修复

* **现象**: 文件移动导致出现 `webFrame/webFrame/src` 的“套娃”结构，引发 `Command "dev" not found` 错误。
* **对策**: 执行路径审计（Directory Audit），通过精准的路径跳转 (`cd`) 与层级清理，确保执行上下文与 `package.json` 完美对齐。

---

## 🌿 版本控制规范 (Git Workflow)

项目采用现代化的 Git 工作流，确保代码变更的可追溯性：

* **分支规范**: 统一使用 `main` 作为默认主分支。
* **提交说明规范**:
* `feat`: 新增功能
* `fix`: 修复依赖或 Bug
* `docs`: 文档更新
* `chore`: 构建过程或辅助工具的变动



### 常用指令：

```powershell
git init
git branch -M main
git remote add origin git@github.com:xianxian51/vue3-web-frame.git
git push -u origin main

```

---

## 🤝 贡献指南

1. **Fork 本仓库** 并创建您的特性分支。
2. **提交代码前** 确保执行过 `pnpm install` 且本地运行无误。
3. **提交 Pull Request** 时请详细描述变更逻辑与测试结果。

---

## 📄 许可证

本项目采用 **MIT 许可证** 授权。

```

---

### 💡 后续交付建议：
1. **截图上传**：请在 `README.md` 的 `## 📸 运行截图` 章节中，将占位符替换为你本地运行成功后的浏览器全屏截图路径（例如 `./public/screenshot.png`）。
2. **文档同步**：完成编辑后，请在终端执行以下操作将文档同步到 GitHub：
   ```powershell
   git add README.md
   git commit -m "docs: finalize comprehensive README with troubleshooting logs"
   git push


