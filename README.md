[English](#make-better-report) · [中文](#make-better-report-1)

---

# make-better-report

Convert any content — text, topics, data, or Markdown — into polished, zero-dependency single-page HTML documentation. No build tools, no npm — runs entirely in the browser.

## Changelog

### 1.1.0 — 2026-05-07

- **Style presets:** Removed **Mono Mosaic**. Four presets remain, renumbered **0–3**.
- **Default:** When no style is chosen, the skill uses **Light Professional** (previously Mono Mosaic).
- **Docs:** `SKILL.md` and `STYLE_PRESETS.md` updated to match the above.

## Features

- Fixed sidebar navigation with pin/unpin support
- Auto-generated table of contents with active section tracking
- Real-time full-text search with match navigation
- Code syntax highlighting
- Dark/light theme toggle
- Responsive layout (mobile, tablet, desktop)
- Optional data charts via Chart.js

## Style Presets

4 visually distinct presets covering different use cases:

| # | Name | Style |
|---|------|-------|
| 0 | Light Professional | White · DM Sans · indigo · standard 16px |
| 1 | Paper Docs | Serif · warm white · rust · reading 17px |
| 2 | Swiss Docs | Grid layout · Archivo · red · right sidebar |
| 3 | Terminal Green | Full monospace · dark · green · developer |

**Light Professional** is used by default when no style is specified.

## File Structure

| File | Purpose |
|------|---------|
| `SKILL.md` | Main workflow: content → style → generate → deliver |
| `STYLE_PRESETS.md` | 4 style presets + card component rules |
| `html-template.md` | HTML architecture, JS classes, navigation patterns |
| `animation-patterns.md` | Scroll reveals, interactive components, chart animations |

## Usage

1. Provide any content — text, topic, data, or Markdown files
2. Choose a style preset (or skip to use the default)
3. Get a ready-to-open `.html` file

---

# make-better-report（中文）

将任何内容——文字、话题、数据或 Markdown——转换为精美的零依赖单页 HTML 文档。无需构建工具，无需 npm，全部在浏览器中运行。

## 版本更新

### 1.1.0 — 2026-05-07

- **风格预设：** 移除 **Mono Mosaic**，保留四种预设，编号为 **0–3**。
- **默认风格：** 未选择风格时，技能默认使用 **Light Professional**（此前为 Mono Mosaic）。
- **文档：** `SKILL.md` 与 `STYLE_PRESETS.md` 已与上述行为对齐。

## 核心能力

- 固定侧边栏导航，支持固定/浮动切换
- 根据标题自动生成目录，滚动时高亮当前章节
- 实时全文搜索，支持上下翻找匹配项
- 代码语法高亮
- 深色/浅色主题切换
- 响应式布局（手机、平板、桌面）
- 可选数据图表（Chart.js）

## 风格预设

4 种风格差异明显的预设，覆盖不同场景：

| # | 名称 | 风格 |
|---|------|------|
| 0 | Light Professional | 纯白 · DM Sans · 靛蓝 · 标准 16px |
| 1 | Paper Docs | 衬线字体 · 暖白 · 锈红 · 17px 阅读向 |
| 2 | Swiss Docs | 网格布局 · Archivo · 红色 · 右侧导航 |
| 3 | Terminal Green | 全等宽 · 深色 · 绿色 · 开发者风格 |

未指定风格时默认使用 **Light Professional**。

## 文件结构

| 文件 | 用途 |
|------|------|
| `SKILL.md` | 主流程：内容收集 → 风格选择 → 生成 → 交付 |
| `STYLE_PRESETS.md` | 4 种风格预设 + 卡片组件规范 |
| `html-template.md` | HTML 结构、JS 类、导航模式 |
| `animation-patterns.md` | 滚动动画、交互组件、图表动效 |

## 使用方式

1. 提供任何内容——文字、话题、数据或 Markdown 文件
2. 选择风格预设（或跳过使用默认）
3. 获得可直接打开的 `.html` 文件
