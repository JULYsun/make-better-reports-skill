[English](#make-better-reports) · [中文](#更好的报告)

---

# Make Better Reports

Convert any content — text, topics, data, or Markdown — into polished, zero-dependency single-page HTML documentation. No build tools, no npm — runs entirely in the browser.

## Features

- Fixed sidebar navigation with pin/unpin support
- Auto-generated table of contents with active section tracking
- Real-time full-text search with match navigation
- Code syntax highlighting
- Dark/light theme toggle
- Responsive layout (mobile, tablet, desktop)
- Optional data charts via Chart.js

## Style Presets

5 visually distinct presets covering different use cases:

| # | Name | Style |
|---|------|-------|
| 0 | Mono Mosaic | Warm cream · Geist Mono · amber · compact 14px |
| 1 | Light Professional | White · DM Sans · indigo · standard 16px |
| 2 | Paper Docs | Serif · warm white · rust · reading 17px |
| 3 | Swiss Docs | Grid layout · Archivo · red · right sidebar |
| 4 | Terminal Green | Full monospace · dark · green · developer |

**Mono Mosaic** is used by default when no style is specified.

## File Structure

| File | Purpose |
|------|---------|
| `SKILL.md` | Main workflow: content → style → generate → deliver |
| `STYLE_PRESETS.md` | 5 style presets + card component rules |
| `html-template.md` | HTML architecture, JS classes, navigation patterns |
| `animation-patterns.md` | Scroll reveals, interactive components, chart animations |

## Usage

1. Provide any content — text, topic, data, or Markdown files
2. Choose a style preset (or skip to use the default)
3. Get a ready-to-open `.html` file

---

# 更好的报告

将任何内容——文字、话题、数据或 Markdown——转换为精美的零依赖单页 HTML 文档。无需构建工具，无需 npm，全部在浏览器中运行。

## 核心能力

- 固定侧边栏导航，支持固定/浮动切换
- 根据标题自动生成目录，滚动时高亮当前章节
- 实时全文搜索，支持上下翻找匹配项
- 代码语法高亮
- 深色/浅色主题切换
- 响应式布局（手机、平板、桌面）
- 可选数据图表（Chart.js）

## 风格预设

5 种风格差异明显的预设，覆盖不同场景：

| # | 名称 | 风格 |
|---|------|------|
| 0 | Mono Mosaic | 暖奶油底色 · Geist Mono · 琥珀色 · 14px 紧凑 |
| 1 | Light Professional | 纯白 · DM Sans · 靛蓝 · 标准 16px |
| 2 | Paper Docs | 衬线字体 · 暖白 · 锈红 · 17px 阅读向 |
| 3 | Swiss Docs | 网格布局 · Archivo · 红色 · 右侧导航 |
| 4 | Terminal Green | 全等宽 · 深色 · 绿色 · 开发者风格 |

未指定风格时默认使用 **Mono Mosaic**。

## 文件结构

| 文件 | 用途 |
|------|------|
| `SKILL.md` | 主流程：内容收集 → 风格选择 → 生成 → 交付 |
| `STYLE_PRESETS.md` | 5 种风格预设 + 卡片组件规范 |
| `html-template.md` | HTML 结构、JS 类、导航模式 |
| `animation-patterns.md` | 滚动动画、交互组件、图表动效 |

## 使用方式

1. 提供任何内容——文字、话题、数据或 Markdown 文件
2. 选择风格预设（或跳过使用默认）
3. 获得可直接打开的 `.html` 文件
