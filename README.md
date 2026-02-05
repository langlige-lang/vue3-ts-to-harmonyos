# Vue3 + TypeScript 转 HarmonyOS ArkTS 学习指南

<p align="center">
  <img src="https://img.shields.io/badge/Vue-3.4-42b883?style=for-the-badge&logo=vue.js" alt="Vue3">
  <img src="https://img.shields.io/badge/TypeScript-5.2-3178c6?style=for-the-badge&logo=typescript" alt="TypeScript">
  <img src="https://img.shields.io/badge/HarmonyOS-ArkTS-fe8301?style=for-the-badge" alt="HarmonyOS">
  <img src="https://img.shields.io/badge/Vite-5.2-646cff?style=for-the-badge&logo=vite" alt="Vite">
</p>

一个帮助 Vue3 开发者快速上手 HarmonyOS ArkTS 开发的交互式学习网站。通过直观的概念对照、代码对比和速查手册，让你轻松实现从 Vue3 到鸿蒙开发的转型。

## ✨ 功能特性

- **概念对照卡片** - Vue3 与 HarmonyOS 核心概念一一对应，点击翻转查看
- **代码实战对比** - TodoList 完整实现，左右对照 Vue3 和 ArkTS 代码
- **语法速查手册** - 装饰器、布局组件、样式属性等常用语法快速查阅
- **炫酷动画效果** - GSAP 驱动的流畅动画，提升学习体验
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
| CSS Styles | 链式样式 `.fontColor()` | 样式定义 |

## 🚀 快速开始

### 环境要求

- Node.js >= 18
- npm >= 9

### 安装依赖

```bash
npm install
```

### 启动开发服务器

```bash
npm run dev
```

访问 http://localhost:5173 查看项目

### 构建生产版本

```bash
npm run build
```

### 预览生产版本

```bash
npm run preview
```

## 📁 项目结构

```
harmony-cards/
├── src/
│   ├── components/          # 通用组件
│   │   ├── DynamicBackground.vue  # 动态背景
│   │   └── NavBar.vue             # 导航栏
│   ├── views/               # 页面视图
│   │   ├── HeroSection.vue        # 首屏展示
│   │   ├── ConceptCards.vue       # 概念对照卡片
│   │   ├── CodeComparison.vue     # 代码对比
│   │   ├── CheatsheetSection.vue  # 速查手册
│   │   ├── CTASection.vue         # 行动召唤
│   │   └── FooterSection.vue      # 页脚
│   ├── App.vue              # 根组件
│   ├── main.ts              # 入口文件
│   └── style.css            # 全局样式
├── index.html
├── package.json
├── tsconfig.json
└── vite.config.ts
```

## 🛠️ 技术栈

- **Vue 3.4** - 渐进式 JavaScript 框架
- **TypeScript 5.2** - 类型安全的 JavaScript 超集
- **Vite 5.2** - 下一代前端构建工具
- **GSAP 3.12** - 专业级动画库

## 📖 学习路径

1. **概念对照** - 理解 Vue3 与 ArkTS 的核心概念映射
2. **代码对比** - 通过 TodoList 实例学习语法差异
3. **速查手册** - 开发时快速查阅常用语法
4. **实践练习** - 尝试将自己的 Vue3 项目转换为 ArkTS

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 License

MIT License

---

<p align="center">
  <b>从 Vue3 到 HarmonyOS，开启你的鸿蒙开发之旅！</b>
</p>
