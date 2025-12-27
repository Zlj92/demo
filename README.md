# 白天黑夜模式切换 (Day/Night Mode Switch)

这是一个基于 Vue 3 和 CSS 变量（CSS Variables）实现的简单且高效的白天/黑夜主题切换示例项目。

## 🚀 项目简介

本项目演示了如何通过动态切换 CSS 样式表来实现网页的主题切换功能。利用 Vue 3 的响应式数据绑定和浏览器的 `localStorage`，实现了主题的持久化存储，确保用户刷新页面后依然保留选择的主题。

## ✨ 核心特性

- **Vue 3 驱动**：使用 Vue 3 框架进行状态管理。
- **动态样式加载**：通过绑定 `<link>` 标签的 `href` 属性，实现样式的按需切换。
- **CSS 变量 (Variables)**：使用 `:root` 定义全局颜色变量，简化样式维护。
- **持久化存储**：利用 `localStorage` 记录用户的主题偏好。
- **SCSS 预处理**：使用 SCSS 编写结构化样式，提高开发效率。

## 📂 项目结构

```text
白天黑夜模式/
├── index.html          # 项目入口文件，包含 Vue 逻辑和 HTML 结构
└── scss/               # 样式文件夹
    ├── default.css     # 默认（白天）主题变量定义
    ├── dark.css        # 深色（黑夜）主题变量定义
    ├── style.scss      # 核心布局样式（使用 CSS 变量）
    └── style.css       # style.scss 编译后的 CSS 文件
```

## 🛠️ 技术实现细节

### 1. CSS 变量定义
在 `default.css` 和 `dark.css` 中，我们定义了相同的变量名但不同的颜色值：

```css
/* default.css */
:root {
  --body_bg: white;
  --nav_bg: #f1f3f4;
  --nav_color: #333;
}

/* dark.css */
:root {
  --body_bg: black;
  --nav_bg: #333;
  --nav_color: #eee;
}
```

### 2. 样式引用
在 `style.scss` 中，我们不直接写死颜色，而是引用这些变量：

```scss
body {
  background-color: var(--body_bg);
}
nav {
  background-color: var(--nav_bg);
  a {
    color: var(--nav_color);
  }
}
```

### 3. Vue 3 逻辑
在 `index.html` 中，Vue 负责管理 `theme` 状态，并根据该状态动态更新 DOM：

```javascript
const { createApp } = Vue
createApp({
  data() {
    return {
      theme: 'default' // 默认为 default
    }
  },
  created() {
    // 页面加载时从本地存储读取主题
    this.theme = localStorage.getItem('theme') || 'default'
  },
  methods: {
    changeTheme(theme) {
      this.theme = theme
      // 将选择的主题保存到本地存储
      localStorage.setItem('theme', theme)
    }
  }
}).mount('#app')
```

## 📖 如何运行

1. 确保你的环境中安装了支持静态文件查看的工具（如 VS Code 的 Live Server 插件）。
2. 直接在浏览器中打开 `index.html`。
3. 点击导航栏右侧的“深色主题”或“默认主题”即可实时切换。

## 📝 总结

这种实现方式的优点在于：
- **性能好**：只需切换一个 CSS 文件，浏览器解析速度快。
- **解耦**：逻辑层（Vue）只负责切换文件名，表现层（CSS）负责具体的颜色定义。
- **易扩展**：如果需要增加“森林绿”或“深海蓝”主题，只需新建对应的 CSS 变量文件即可。
