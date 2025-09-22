# Gradient Background Demo

一个基于Vue 3的动态渐变背景演示项目，实现了类似liquid-ether效果的动态球体背景。

## 功能特性

- 🎨 **动态渐变球体**：包含紫色椭圆形大球和蓝色正方形小球
- 🌊 **静态波动动画**：球体在静态时有缓慢的波动效果
- 🖱️ **鼠标交互**：当鼠标靠近时，球体会产生动态反馈
- 📏 **边界限制**：球体运动被限制在指定区域内
- 🎯 **精确定位**：背景与标题同步移动
- 🎨 **浅色背景**：适配浅色工作台设计

## 渐变效果参数

### 紫色椭圆形大球
- 尺寸：330px × 236px
- 渐变：linear 100%
- 颜色停止点：
  - 0%: #090909
  - 100%: #6F00FF
- 模糊效果：100px

### 蓝色正方形小球
- 尺寸：160px × 160px
- 渐变：linear 69%
- 颜色停止点：
  - 0%: #274BCA
  - 100%: #FFFFFF
- 模糊效果：200px

## 安装和运行

1. 安装依赖：
```bash
npm install
```

2. 启动开发服务器：
```bash
npm run dev
```

3. 在浏览器中打开 `http://localhost:3000` 查看效果

## 项目结构

```
src/
├── components/
│   └── GradientBackground.vue  # 动态渐变背景组件
├── App.vue                     # 主应用组件
└── main.js                     # 应用入口
```

## 技术栈

- Vue 3 (Composition API)
- Vite
- CSS3 动画和变换
- 原生JavaScript动画

## 自定义配置

你可以在 `GradientBackground.vue` 中调整以下参数：

- `waveX` 和 `waveY`：波动幅度
- `mouseInfluence`：鼠标交互强度
- `baseX` 和 `baseY`：球体初始位置
- 颜色值和模糊效果

## 浏览器支持

- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+
