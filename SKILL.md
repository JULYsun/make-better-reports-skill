---
name: report docs
description: Create single-page HTML documentation from Markdown with fixed navigation, table of contents, search, and multiple style presets. Use when the user wants to build documentation, API docs, guides, or technical content.
---

# Report Docs

Create zero-dependency, single-page HTML documentation that runs entirely in the browser.

## Core Principles

1. **Zero Dependencies** — Single HTML files with inline CSS/JS. No npm, no build tools.
2. **Show, Don't Tell** — Generate visual previews, not abstract choices. People discover what they want by seeing it.
3. **Distinctive Design** — No generic "AI slop." Every documentation page must feel custom-crafted.
4. **Fixed Navigation** — Sidebar navigation stays visible while scrolling. Supports pin (always visible, pushes content) and unpin (overlay) states.

## Design Aesthetics

Follow the same aesthetic principles as frontend-slides:

- Typography: Choose fonts that are beautiful, unique, and interesting. Avoid generic fonts like Arial and Inter.
- Color & Theme: Commit to a cohesive aesthetic. Use CSS variables for consistency.
- Motion: Smooth scroll animations, active section highlighting, search interactions.
- Backgrounds: Create atmosphere and depth rather than defaulting to solid colors.

Avoid generic AI-generated aesthetics - make creative, distinctive choices.

---

## Phase 0: Detect Mode

Determine what the user wants:

- **Mode A: New Documentation** — Create from scratch. Go to Phase 1.
- **Mode B: Enhancement** — Improve existing HTML documentation. Read it, understand it, enhance.

---

## Phase 1: Content Discovery (New Documentation)

**Ask ALL questions in a single call:**

**Question 1 — Content Source** (header: "Content"):
What content do you have? Options: Markdown file ready / Multiple MD files / Will provide text / Just topic

**Question 2 — Navigation Style** (header: "Navigation"):
Where should navigation be? Options: Left sidebar / Right sidebar / Let me choose style first

**Question 3 — Length** (header: "Length"):
How long is the documentation? Options: Short (1-5 sections) / Medium (5-15 sections) / Long (15+ sections)

If user has Markdown files, ask them to share the path(s).

---

## Phase 2: Style Discovery

**This is the "show, don't tell" phase.**

### Step 2.0: Style Path

Ask how they want to choose (header: "Style"):
- "Show me options" (recommended) — Generate 3 previews based on mood
- "I know what I want" — Pick from preset list directly

**If direct selection:** Show preset picker and skip to Phase 3. Available presets are defined in [STYLE_PRESETS.md](STYLE_PRESETS.md).

### Step 2.1: Mood Selection (Guided Discovery)

Ask (header: "Vibe", multiSelect: true, max 2):
What feeling should readers have? Options:
- Professional/Technical — Clean, trustworthy, precise
- Modern/Minimal — Simple, elegant, focused
- Warm/Friendly — Approachable, readable, comfortable
- Developer/Terminal — Code-focused, technical, hacker aesthetic

### Step 2.2: Generate 3 Style Previews

Based on mood, generate 3 distinct single-page HTML previews showing typography, colors, navigation style, and overall aesthetic.

| Mood | Suggested Presets |
|------|-------------------|
| Professional/Technical | Modern Clean, Dark Professional, Swiss Docs |
| Modern/Minimal | Minimal Light, Paper Docs, Clean Slate |
| Warm/Friendly | Warm Editorial, Notebook Style, Soft Cream |
| Developer/Terminal | Terminal Green, Code Dark, Hacker Theme |

Save previews to `.claude-design/doc-previews/` (style-a.html, style-b.html, style-c.html). Each should show a sample documentation page with navigation, TOC, and content.

Open each preview automatically for the user.

### Step 2.3: User Picks

Ask (header: "Style"):
Which style preview do you prefer? Options: Style A: [Name] / Style B: [Name] / Style C: [Name] / Mix elements

If "Mix elements", ask for specifics.

---

## Phase 3: Generate Documentation

Generate the full documentation page using content from Phase 1 and style from Phase 2.

**Before generating, read these supporting files:**
- [html-template.md](html-template.md) — HTML architecture for docs
- [STYLE_PRESETS.md](STYLE_PRESETS.md) — Style presets for documentation
- [animation-patterns.md](animation-patterns.md) — Animation patterns for docs (scroll reveals, interactive components, chart animations, micro-interactions)

**Key requirements:**
- Single self-contained HTML file, all CSS/JS inline
- Fixed sidebar navigation (left or right based on style/user choice) with pin/unpin support
- Automatic table of contents from headings (h1-h3)
- Search functionality with real-time highlighting
- Smooth scroll to sections
- Active section highlighting in TOC
- Code syntax highlighting for common languages
- Responsive design (mobile, tablet, desktop)
- Use fonts from Fontshare or Google Fonts — never system fonts
- Add detailed comments explaining each section

**Navigation Structure:**

```html
<aside class="nav-sidebar nav-sidebar-left" id="nav-sidebar">
  <div class="nav-header">
    <h1>Documentation Title</h1>
    <button class="sidebar-pin-btn" id="sidebar-pin-btn" title="Pin sidebar">...</button>
  </div>
  <div class="nav-search">...</div>
  <nav class="toc"><!-- TOC items --></nav>
</aside>
<div class="sidebar-overlay" id="sidebar-overlay"></div>
<button class="nav-toggle" id="nav-toggle">☰</button>
<main class="content" id="main-content">
  <div class="content-inner"><!-- Sections --></div>
</main>
```

**Content Structure:**
```html
<section id="section-slug">
  <h2>Section Title</h2>
  <p>Content...</p>
</section>
```

**JavaScript Features Required:**
- Smooth scroll to sections on TOC click
- Active section tracking (highlight current section in TOC)
- Search with real-time filtering and highlighting
- Sidebar pin/unpin toggle with localStorage persistence
- Mobile overlay toggle (hamburger button)
- Back to top button (appears after scrolling one viewport height)

---

## Phase 4: Delivery

1. **Open** — Use `open [filename].html` to launch in browser
2. **Summarize** — Tell the user:
   - File location, style name, section count
   - Navigation: Click TOC links, use search, scroll
   - How to customize: `:root` CSS variables for colors, font links for typography
   - Search: Type to filter, ESC to clear

---

## Supporting Files

| File | Purpose | When to Read |
|------|---------|-------------|
| [STYLE_PRESETS.md](STYLE_PRESETS.md) | Curated visual presets for documentation | Phase 2 (style selection) |
| [html-template.md](html-template.md) | HTML structure, JS features, navigation patterns, Chart.js data charts | Phase 3 (generation) |
| [animation-patterns.md](animation-patterns.md) | Scroll reveals, interactive components (tabs, accordion, copy button, theme toggle), chart animations, micro-interactions | Phase 3 (generation) |

---

## Key Differences from Slides

- **Scrollable sections** instead of discrete slides
- **Sidebar navigation** (left or right) with pin/unpin instead of slide navigation
- **Table of contents** with hierarchical structure
- **Search functionality** for finding content
- **Active section tracking** as user scrolls
- **Code syntax highlighting** for technical content
- **Responsive tables** that work on mobile
- No viewport fitting constraints (content can be long)
