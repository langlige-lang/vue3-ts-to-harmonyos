# Vue3 + TypeScript 转 HarmonyOS ArkTS 学习指南

<p align="center">
  <img src="https://img.shields.io/badge/Vue-3-42b883?style=for-the-badge&logo=vue.js" alt="Vue3">
  <img src="https://img.shields.io/badge/HarmonyOS-ArkTS-fe8301?style=for-the-badge" alt="HarmonyOS">
</p>

一个帮助 Vue3 开发者快速上手 HarmonyOS ArkTS 开发的**交互式学习网站**。通过直观的概念对照、代码对比和速查手册，让你轻松实现从 Vue3 到鸿蒙开发的转型。

## 🚀 快速开始

### 方式一：直接打开（推荐）

直接在浏览器中打开 `dist/index.html` 即可使用，**无需安装任何依赖**。

### 方式二：开发模式

```bash
# 安装依赖
npm install

# 启动开发服务器
npm run dev
```

## ✨ 功能特性

- **概念对照卡片** - Vue3 与 HarmonyOS 核心概念一一对应，点击翻转查看
- **代码实战对比** - TodoList 完整实现，左右对照 Vue3 和 ArkTS 代码
- **语法速查手册** - 装饰器、布局组件、样式属性等常用语法快速查阅
- **生命周期对比** - Vue3 与 ArkTS 生命周期钩子对照
- **学习路径指引** - 从入门到进阶的完整学习路线
- **全局搜索** - 快速查找任意概念或语法（Ctrl+K）
- **炫酷动画效果** - 流畅的交互动画，提升学习体验
- **响应式设计** - 完美适配桌面端和移动端

## 🎯 核心对照内容

| Vue3 | HarmonyOS ArkTS | 说明 |
|------|-----------------|------|
| `ref()` / `reactive()` | `@State` | 响应式状态 |
| `v-for` | `ForEach` | 列表渲染 |
| `v-if` / `v-show` | `if()` / `visibility()` | 条件渲染 |
| `@click` | `.onClick()` | 事件绑定 |
| `props` | `@Prop` | 父子传参 |
| `computed()` | `@Computed` | 计算属性 |
| `watch()` | `@Watch` | 状态监听 |
| `onMounted` | `aboutToAppear` | 生命周期 |
| CSS Styles | 链式样式 `.fontColor()` | 样式定义 |

## 📁 项目结构

```
harmony-cards/
├── dist/
│   └── index.html      # 📌 独立单文件应用（可直接打开）
├── src/                # Vue 开发源码
│   ├── components/     # 通用组件
│   ├── views/          # 页面视图
│   ├── App.vue         # 根组件
│   └── main.ts         # 入口文件
├── package.json
└── vite.config.ts
```

## 📖 学习路径

1. **概念对照** - 理解 Vue3 与 ArkTS 的核心概念映射
2. **代码对比** - 通过 TodoList 实例学习语法差异
3. **生命周期** - 掌握组件生命周期的对应关系
4. **速查手册** - 开发时快速查阅常用语法
5. **实践练习** - 尝试将自己的 Vue3 项目转换为 ArkTS

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 License

MIT License

---

<p align="center">
  <b>从 Vue3 到 HarmonyOS，开启你的鸿蒙开发之旅！🚀</b>
</p>
