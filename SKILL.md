---
name: make-better-report
description: Create single-page HTML documentation from any content with fixed navigation, table of contents, search, and multiple style presets. Use when the user wants to build documentation, API docs, guides, or technical content.
---

# make-better-report

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

**Default:** If the user skips style selection entirely, use **Mono Mosaic** and go to Phase 3.

Ask (header: "Style"):
- "Show me previews" — Go to Step 2.A
- "I know what I want" — Go to Step 2.B

### Step 2.A: Preview Path

Generate 3 distinct single-page HTML previews. Pick 3 presets that contrast well with each other (different moods/palettes). Save to `.claude-design/doc-previews/` (style-a.html, style-b.html, style-c.html) and open each automatically.

Then ask: Which do you prefer? A / B / C / Mix elements. If "Mix", ask for specifics.

### Step 2.B: Direct Pick

| # | Name | Vibe |
|---|------|------|
| 0 | **Mono Mosaic** ★ | Warm cream, Geist Mono, amber, 14px |
| 1 | Light Professional | Clean white, indigo, DM Sans |
| 2 | Paper Docs | Serif editorial, rust, 17px reading |
| 3 | Swiss Docs | Grid-based, red accent, right sidebar |
| 4 | Terminal Green | Full monospace, dark, green accent |

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
