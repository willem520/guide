---
name: svg-master
description: 使用SVG语法创建高质量矢量图形，支持图标、流程图、架构图、插图、数据可视化图表等，可直接在浏览器和Markdown中展示
---

# SVG Master Skill

根据用户需求生成纯 SVG 矢量图形代码，适用于图标、架构图、数据可视化、交互原型等场景。

## 工作流

1. 确认用户想要的图形类型、尺寸和风格
2. 生成标准的可缩放矢量图形(SVG)代码
3. 保存为 `.svg` 文件到用户指定路径
4. 如需展示，在Markdown中用 `![描述](path/to/file.svg)` 引用

## SVG基础模板

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 800 600" width="800" height="600">
  <!-- 内容 -->
</svg>
```

## 常用图形元素

### 基本形状
| 元素 | 属性 | 用途 |
|------|------|------|
| `<rect>` | x, y, width, height, rx(圆角) | 矩形/容器 |
| `<circle>` | cx, cy, r | 圆形 |
| `<ellipse>` | cx, cy, rx, ry | 椭圆 |
| `<line>` | x1, y1, x2, y2 | 线段 |
| `<polyline>` | points | 折线 |
| `<polygon>` | points | 多边形 |
| `<path>` | d | 任意路径 |

### 文字与样式
```svg
<text x="50" y="50" font-family="Arial" font-size="16" text-anchor="middle" fill="#333">文本</text>
```

### 路径(path)命令速查
| 命令 | 含义 | 示例 |
|------|------|------|
| M | 移动到 | M 10 10 |
| L | 画直线 | L 100 100 |
| H | 水平线 | H 200 |
| V | 垂直线 | V 200 |
| C | 贝塞尔曲线 | C 10 10, 40 40, 100 100 |
| Q | 二次曲线 | Q 50 50, 100 100 |
| A | 弧线 | A 25 25 0 0 1 50 50 |
| Z | 闭合路径 | Z |

### 渐变与滤镜
```svg
<defs>
  <linearGradient id="grad" x1="0%" y1="0%" x2="100%" y2="100%">
    <stop offset="0%" style="stop-color:#667eea" />
    <stop offset="100%" style="stop-color:#764ba2" />
  </linearGradient>
  <filter id="shadow">
    <feDropShadow dx="2" dy="2" stdDeviation="3" flood-opacity="0.3"/>
  </filter>
</defs>
```

### 分组与复用
```svg
<g id="component" transform="translate(100, 100)">
  <!-- 复用 -->
  <use href="#component" x="200" y="0" />
</g>
```

## 设计规范

### 配色方案
- **主色调**: 使用 Tailwind CSS 色板中的颜色
- **中性色**: `#1e293b`(深灰), `#475569`(灰), `#94a3b8`(浅灰), `#f1f5f9`(背景)
- **语义色**: `#22c55e`(成功), `#ef4444`(错误), `#f59e0b`(警告), `#3b82f6`(信息)

### 尺寸规范
- 图标: 24x24, 48x48, 64x64
- 小型架构图: 800x600
- 中型架构图: 1200x800
- 大型架构图: 1600x1000

## 最佳实践

1. 始终使用 `viewBox` 而非固定宽高确保缩放
2. 复杂图形使用 `g` 分组并添加注释
3. 文本使用通用字体家族: `Arial, Helvetica, sans-serif`
4. 使用 `currentColor` 支持外部颜色覆盖
5. 语义化使用 `role="img"` 和 `aria-label`
6. 矢量风格保持简洁，去除冗余属性
7. 优先使用 `<path>` 绘制复杂形状
8. 添加 `xmlns` 命名空间确保标准兼容

## 常见场景模板

### 简单图标
```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24">
  <path d="M12 2L2 7l10 5 10-5-10-5z" fill="currentColor"/>
  <path d="M2 17l10 5 10-5" fill="none" stroke="currentColor" stroke-width="2"/>
  <path d="M2 12l10 5 10-5" fill="none" stroke="currentColor" stroke-width="2"/>
</svg>
```

### 架构图组件样式
- 服务: 圆角矩形 + 渐变填充 + 阴影
- 数据库: 圆柱形
- 用户: 圆形或人物图标
- 消息队列: 两个重叠的矩形
- 连线: 带箭头的 `<path>`，不同颜色区分协议
