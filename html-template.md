# HTML Documentation Template

Reference architecture for generating documentation pages. Every documentation page follows this structure.

## Base HTML Structure

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Documentation Title</title>

    <!-- Fonts: use Fontshare or Google Fonts — never system fonts -->
    <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=...">

    <style>
        /* ===========================================
           CSS CUSTOM PROPERTIES (THEME)
           Change these to change the whole look
           =========================================== */
        :root {
            /* Colors — from chosen style preset */
            --bg-primary: #ffffff;
            --bg-surface: #f8f9fa;
            --accent: #0066cc;
            --text-primary: #1a1a1a;
            --text-secondary: #666666;
            --border: #e0e0e0;
            --code-bg: #f5f5f5;

            /* Typography */
            --font-display: 'Inter', sans-serif;
            --font-body: 'Inter', sans-serif;
            --font-code: 'JetBrains Mono', monospace;
            --font-numeric: 'DM Mono', monospace; /* tabular nums for stats, counters, prices */

            /* Layout */
            --sidebar-width: 280px;
            --content-max-width: 1200px;
            --spacing: 1rem;
        }

        /* Base styles, navigation, TOC, sections, code highlighting... */
    </style>
</head>
<body>
    <!-- Sidebar Navigation -->
    <!-- Sidebar overlay (unpinned state) -->
    <!-- Main Content -->
    <!-- JavaScript -->
</body>
</html>
```

## Navigation Structures

### Sidebar Navigation (Left or Right)

The sidebar supports two states: **pinned** (always visible, pushes content aside) and **unpinned** (floats over content without blocking it — a transparent click-capture overlay closes it when clicking outside). The pin state is persisted in `localStorage`.

```html
<aside class="nav-sidebar nav-sidebar-left" id="nav-sidebar">
  <div class="nav-header">
    <h1>Documentation Title</h1>
    <!-- Pin toggle button -->
    <button class="sidebar-pin-btn" id="sidebar-pin-btn" title="Pin sidebar">
      <!-- Icon swaps between pinned/unpinned state -->
      <svg class="icon-pin" xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round" stroke-linejoin="round"><circle cx="11.5" cy="8.5" r="5.5"/><path d="M11.5 14v7"/></svg>
      <svg class="icon-unpin" xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1" stroke-linecap="round" stroke-linejoin="round"><circle cx="11.5" cy="8.5" r="5.5"/><path d="M11.5 14v7"/><line x1="3" y1="3" x2="21" y2="21"/></svg>
    </button>
  </div>

  <div class="nav-search">
    <input type="search" id="search-input" placeholder="Search..." />
    <button id="search-prev" class="search-nav-btn" style="display:none" title="Previous (Shift+Enter)">↑</button>
    <button id="search-next" class="search-nav-btn" style="display:none" title="Next (Enter)">↓</button>
    <span class="search-count" id="search-count"></span>
  </div>

  <nav class="toc">
    <ul class="toc-list">
      <!-- TOC items -->
    </ul>
  </nav>
</aside>

<!-- Toggle button — visible when sidebar is unpinned/closed -->
<button class="nav-toggle" id="nav-toggle" aria-label="Open navigation">☰</button>

<main class="content" id="main-content">
  <div class="content-inner">
    <!-- Sections here -->
  </div>
</main>
```

```css
/* ---- Sidebar base ---- */
.nav-sidebar {
  position: fixed;
  top: 0;
  width: var(--sidebar-width);
  height: 100vh;
  background: var(--bg-surface);
  overflow-y: auto;
  padding: 2rem 1.5rem;
  z-index: 1000;
  transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.nav-sidebar-left  { left: 0;  border-right: 1px solid var(--border); }
.nav-sidebar-right { right: 0; border-left:  1px solid var(--border); }

/* ---- Pinned state — sidebar is always visible, content shifts ---- */
.nav-sidebar.pinned {
  transform: translateX(0) !important;
  box-shadow: none;
}

body.sidebar-pinned-left  .content { margin-left:  var(--sidebar-width); }
body.sidebar-pinned-right .content { margin-right: var(--sidebar-width); }

/* ---- Unpinned state — sidebar overlays content ---- */
.nav-sidebar-left:not(.pinned)  { transform: translateX(-100%); box-shadow: 4px 0 24px rgba(0,0,0,0.12); }
.nav-sidebar-right:not(.pinned) { transform: translateX(100%);  box-shadow: -4px 0 24px rgba(0,0,0,0.12); }

.nav-sidebar:not(.pinned).open  { transform: translateX(0); }

/* Dim overlay when unpinned sidebar is open */
/* Transparent click-capture layer — no background, sidebar is a true float */
.sidebar-overlay {
  position: fixed;
  inset: 0;
  background: transparent;
  z-index: 999;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.2s ease;
}
.sidebar-overlay.visible {
  opacity: 1;
  pointer-events: auto;
}

/* ---- Nav header with pin button ---- */
.nav-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 1.5rem;
  gap: 0.5rem;
}

.sidebar-pin-btn {
  flex-shrink: 0;
  background: none;
  border: 1px solid var(--border);
  border-radius: 6px;
  padding: 0.3rem;
  cursor: pointer;
  color: var(--text-secondary);
  display: flex;
  align-items: center;
  transition: color 0.2s, border-color 0.2s;
}
.sidebar-pin-btn:hover { color: var(--accent); border-color: var(--accent); }

/* Show/hide correct icon based on state */
.nav-sidebar.pinned  .icon-unpin { display: block; }
.nav-sidebar.pinned  .icon-pin   { display: none;  }
.nav-sidebar:not(.pinned) .icon-pin   { display: block; }
.nav-sidebar:not(.pinned) .icon-unpin { display: none;  }

/* ---- Toggle button (hamburger) ---- */
.nav-toggle {
  position: fixed;
  top: 1rem;
  left: 1rem; /* adjust to right: 1rem for right sidebar */
  z-index: 998;
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: 6px;
  padding: 0.4rem 0.6rem;
  cursor: pointer;
  font-size: 1.1rem;
  transition: opacity 0.2s;
}

/* Hide toggle when sidebar is pinned */
body.sidebar-pinned-left  .nav-toggle,
body.sidebar-pinned-right .nav-toggle { display: none; }

/* ---- Content area ---- */
.content {
  padding: 3rem;
  transition: margin 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

.content-inner {
  max-width: var(--content-max-width);
  margin: 0 auto;
}

/* ---- Mobile: always unpinned overlay ---- */
@media (max-width: 768px) {
  .nav-sidebar { transform: translateX(-100%) !important; box-shadow: 4px 0 24px rgba(0,0,0,0.12); }
  .nav-sidebar-right { transform: translateX(100%) !important; }
  .nav-sidebar.open { transform: translateX(0) !important; }
  body.sidebar-pinned-left  .content,
  body.sidebar-pinned-right .content { margin: 0; }
  .nav-toggle { display: flex !important; }
  .sidebar-pin-btn { display: none; } /* pin not available on mobile */
}
```

## Content Structure

```html
<section id="section-slug">
  <h2>Section Title</h2>
  <p>Paragraph content...</p>
  
  <h3>Subsection</h3>
  <p>More content...</p>
  
  <pre><code class="language-javascript">
// Code example
function example() {
  return true;
}
  </code></pre>
  
  <table>
    <thead>
      <tr>
        <th>Column 1</th>
        <th>Column 2</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>Data 1</td>
        <td>Data 2</td>
      </tr>
    </tbody>
  </table>
</section>
```

## Required JavaScript Features

Every documentation page must include:

### 1. Smooth Scroll Controller

```javascript
class SmoothScrollController {
  constructor() {
    this.setupListeners();
  }

  scrollToSection(targetId) {
    const target = document.getElementById(targetId);
    if (!target) return;

    const targetPosition = target.getBoundingClientRect().top + window.pageYOffset;
    window.scrollTo({ top: targetPosition - 20, behavior: 'smooth' });
    history.pushState(null, null, `#${targetId}`);
  }

  setupListeners() {
    document.querySelectorAll('.toc-link').forEach(link => {
      link.addEventListener('click', (e) => {
        e.preventDefault();
        this.scrollToSection(link.getAttribute('href').substring(1));
      });
    });
  }
}
```

### 2. Active Section Tracker

```javascript
class ActiveSectionTracker {
  constructor() {
    this.sections = Array.from(document.querySelectorAll('section[id]'));
    this.tocLinks = Array.from(document.querySelectorAll('.toc-link'));
    this.setupObserver();
  }

  setupObserver() {
    const options = {
      root: null,
      rootMargin: '-100px 0px -66%',
      threshold: 0
    };

    this.observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          this.updateActiveTOC(entry.target.id);
        }
      });
    }, options);

    this.sections.forEach(section => {
      this.observer.observe(section);
    });
  }

  updateActiveTOC(sectionId) {
    this.tocLinks.forEach(link => link.classList.remove('active'));
    const activeLink = document.querySelector(`.toc-link[href="#${sectionId}"]`);
    if (activeLink) activeLink.classList.add('active');
  }
}
```

### 3. Search Controller

```javascript
class SearchController {
  constructor() {
    this.searchInput = document.getElementById('search-input');
    this.searchCount = document.getElementById('search-count');
    this.prevBtn = document.getElementById('search-prev');
    this.nextBtn = document.getElementById('search-next');
    this.sections = Array.from(document.querySelectorAll('section'));
    this.matches = [];
    this.currentIndex = -1;
    this.setupListeners();
  }

  escapeRegex(str) {
    return str.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
  }

  search(query) {
    this.clearHighlights();
    this.matches = [];
    this.currentIndex = -1;

    if (!query || query.length < 2) { this.updateUI(0); return; }

    const safe = this.escapeRegex(query);
    const re = new RegExp(`(${safe})`, 'gi');

    this.sections.forEach(section => {
      const walker = document.createTreeWalker(section, NodeFilter.SHOW_TEXT);
      const nodes = [];
      let node;
      while (node = walker.nextNode()) {
        if (node.parentElement.closest('script, style, mark')) continue;
        if (re.test(node.textContent)) nodes.push(node);
        re.lastIndex = 0;
      }
      nodes.forEach(n => {
        const span = document.createElement('span');
        span.innerHTML = n.textContent.replace(re, '<mark>$1</mark>');
        n.parentNode.replaceChild(span, n);
      });
    });

    this.matches = Array.from(document.querySelectorAll('mark'));
    this.updateUI(this.matches.length);
    if (this.matches.length > 0) { this.currentIndex = 0; this.scrollToMatch(0); }
  }

  scrollToMatch(index) {
    this.matches.forEach(m => m.classList.remove('mark-active'));
    const target = this.matches[index];
    if (!target) return;
    target.classList.add('mark-active');
    target.scrollIntoView({ behavior: 'smooth', block: 'center' });
    this.updateUI(this.matches.length);
  }

  next() {
    if (!this.matches.length) return;
    this.currentIndex = (this.currentIndex + 1) % this.matches.length;
    this.scrollToMatch(this.currentIndex);
  }

  prev() {
    if (!this.matches.length) return;
    this.currentIndex = (this.currentIndex - 1 + this.matches.length) % this.matches.length;
    this.scrollToMatch(this.currentIndex);
  }

  updateUI(total) {
    this.searchCount.textContent = total === 0
      ? (this.searchInput.value.length >= 2 ? 'No matches' : '')
      : `${this.currentIndex + 1} / ${total}`;
    const show = total > 0;
    if (this.prevBtn) this.prevBtn.style.display = show ? 'inline-flex' : 'none';
    if (this.nextBtn) this.nextBtn.style.display = show ? 'inline-flex' : 'none';
  }

  clearHighlights() {
    // normalize() merges fragmented text nodes after repeated searches
    document.querySelectorAll('mark').forEach(mark => {
      mark.replaceWith(mark.textContent);
    });
    this.sections.forEach(s => s.normalize());
  }

  setupListeners() {
    this.searchInput.addEventListener('input', (e) => {
      this.search(e.target.value);
    });

    this.searchInput.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') { this.searchInput.value = ''; this.search(''); }
      if (e.key === 'Enter') { e.shiftKey ? this.prev() : this.next(); }
    });

    this.prevBtn?.addEventListener('click', () => this.prev());
    this.nextBtn?.addEventListener('click', () => this.next());
  }
}
```

**Required HTML for search UI:**
```html
<div class="nav-search">
  <input type="search" id="search-input" placeholder="Search..." />
  <button id="search-prev" class="search-nav-btn" style="display:none" title="Previous (Shift+Enter)">↑</button>
  <button id="search-next" class="search-nav-btn" style="display:none" title="Next (Enter)">↓</button>
  <span class="search-count" id="search-count"></span>
</div>
```

**Required CSS for search UI:**
```css
.nav-search { display: flex; align-items: center; gap: 0.4rem; }

.search-nav-btn {
  padding: 0.3rem 0.5rem;
  border: 1px solid var(--border);
  border-radius: 4px;
  background: var(--bg-surface);
  color: var(--text-secondary);
  cursor: pointer;
  font-size: 0.85rem;
  line-height: 1;
  transition: all 0.15s;
}
.search-nav-btn:hover { border-color: var(--accent); color: var(--accent); }

/* Current focused match — more prominent than other marks */
mark { background: #ffeb3b; color: #000; border-radius: 2px; padding: 0 2px; }
mark.mark-active { background: #ff9800; outline: 2px solid #ff9800; }
```

### 4. Sidebar Controller (Pin / Unpin + Mobile Toggle)

Handles both the pin/unpin toggle on desktop and the open/close overlay on mobile. State is persisted in `localStorage`.

```javascript
class SidebarController {
  constructor() {
    this.sidebar  = document.getElementById('nav-sidebar');
    this.pinBtn   = document.getElementById('sidebar-pin-btn');
    this.toggle   = document.getElementById('nav-toggle');
    this.overlay  = document.getElementById('sidebar-overlay');
    this.isMobile = () => window.innerWidth <= 768;

    // Restore pinned state (default: pinned on desktop)
    const saved = localStorage.getItem('sidebar-pinned');
    const pinned = this.isMobile() ? false : (saved === null ? true : saved === 'true');
    this.setPinned(pinned, false); // false = no animation on init

    this.setupListeners();
  }

  setPinned(pinned, animate = true) {
    if (!animate) this.sidebar.style.transition = 'none';

    // Always clear both body classes first to avoid stale state
    document.body.classList.remove('sidebar-pinned-left', 'sidebar-pinned-right');

    if (pinned) {
      this.sidebar.classList.add('pinned');
      this.sidebar.classList.remove('open');
      const bodyClass = this.sidebar.classList.contains('nav-sidebar-right')
        ? 'sidebar-pinned-right' : 'sidebar-pinned-left';
      document.body.classList.add(bodyClass);
      this.overlay.classList.remove('visible');
    } else {
      this.sidebar.classList.remove('pinned');
    }

    localStorage.setItem('sidebar-pinned', pinned);

    if (!animate) {
      requestAnimationFrame(() => { this.sidebar.style.transition = ''; });
    }
  }

  open() {
    this.sidebar.classList.add('open');
    // Overlay is transparent — only captures outside clicks, doesn't block reading
    this.overlay.classList.add('visible');
  }

  close() {
    this.sidebar.classList.remove('open');
    this.overlay.classList.remove('visible');
  }

  setupListeners() {
    // Pin / unpin button
    this.pinBtn?.addEventListener('click', () => {
      this.setPinned(!this.sidebar.classList.contains('pinned'));
    });

    // Hamburger toggle
    this.toggle?.addEventListener('click', () => {
      this.sidebar.classList.contains('open') ? this.close() : this.open();
    });

    // Overlay click closes sidebar (transparent layer outside the sidebar)
    this.overlay.addEventListener('click', () => this.close());

    // Re-evaluate on resize — mobile always unpinned
    window.addEventListener('resize', () => {
      if (this.isMobile()) this.setPinned(false);
    }, { passive: true });
  }
}
```

**Required overlay element (add just before `<main>`):**
```html
<!-- Transparent click-capture layer — closes unpinned sidebar when clicking outside it -->
<div class="sidebar-overlay" id="sidebar-overlay"></div>
```

### 5. Back to Top Button

Appears in the bottom-right corner once the user scrolls past one viewport height. Smooth-scrolls back to top on click.

**HTML (place just before `</body>`):**
```html
<button class="back-to-top" id="back-to-top" aria-label="Back to top" title="Back to top">
  <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
    <polyline points="18 15 12 9 6 15"/>
  </svg>
</button>
```

**CSS:**
```css
.back-to-top {
  position: fixed;
  bottom: 2rem;
  right: 2rem;
  z-index: 900;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: var(--accent);
  color: #fff;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);

  /* Hidden by default */
  opacity: 0;
  transform: translateY(12px);
  pointer-events: none;
  transition: opacity 0.25s ease, transform 0.25s ease;
}

.back-to-top.visible {
  opacity: 1;
  transform: translateY(0);
  pointer-events: auto;
}

.back-to-top:hover {
  filter: brightness(1.1);
  transform: translateY(-2px);
}

.back-to-top:active {
  transform: translateY(0);
}
```

**JavaScript:**
```javascript
class BackToTop {
  constructor() {
    this.btn = document.getElementById('back-to-top');
    if (!this.btn) return;
    this.threshold = window.innerHeight; // show after 1 viewport height
    this.setupListeners();
  }

  setupListeners() {
    window.addEventListener('scroll', () => {
      this.btn.classList.toggle('visible', window.scrollY > this.threshold);
    }, { passive: true });

    this.btn.addEventListener('click', () => {
      window.scrollTo({ top: 0, behavior: 'smooth' });
    });
  }
}
```

### 6. Initialize All

```javascript
document.addEventListener('DOMContentLoaded', () => {
  new SmoothScrollController();
  new ActiveSectionTracker();
  new SearchController();
  new SidebarController();
  new BackToTop();
});
```

## Code Syntax Highlighting

Use lightweight regex-based highlighting for common languages:

```javascript
function highlightCode() {
  document.querySelectorAll('pre code').forEach(block => {
    const language = block.className.replace('language-', '');
    const code = block.textContent;
    
    // Apply language-specific highlighting
    const highlighted = applyHighlighting(code, language);
    block.innerHTML = highlighted;
  });
}

function applyHighlighting(code, language) {
  // Simple keyword highlighting for common languages
  const keywords = {
    javascript: ['function', 'const', 'let', 'var', 'return', 'if', 'else', 'for', 'while'],
    python: ['def', 'class', 'import', 'from', 'return', 'if', 'else', 'for', 'while'],
    // Add more languages...
  };
  
  let highlighted = code;
  
  if (keywords[language]) {
    keywords[language].forEach(keyword => {
      const regex = new RegExp(`\\b${keyword}\\b`, 'g');
      highlighted = highlighted.replace(regex, `<span class="keyword">${keyword}</span>`);
    });
  }
  
  // Highlight strings
  highlighted = highlighted.replace(/(["'`])(?:(?=(\\?))\2.)*?\1/g, '<span class="string">$&</span>');
  
  // Highlight comments
  highlighted = highlighted.replace(/\/\/.*/g, '<span class="comment">$&</span>');
  highlighted = highlighted.replace(/\/\*[\s\S]*?\*\//g, '<span class="comment">$&</span>');
  
  return highlighted;
}
```

## Responsive Design

```css
/* Mobile (<768px) — sidebar always overlays, pin disabled */
@media (max-width: 768px) {
  .nav-sidebar {
    transform: translateX(-100%);
    transition: transform 0.3s ease;
  }
  .nav-sidebar-right { transform: translateX(100%); }

  .nav-sidebar.open {
    transform: translateX(0);
  }

  .content {
    margin-left: 0 !important;
    margin-right: 0 !important;
    padding: 1.5rem 1rem;
  }

  .content-inner { max-width: 100%; }

  .nav-toggle { display: flex; }
  .sidebar-pin-btn { display: none; }
}

/* Tablet (768-1024px) */
@media (min-width: 768px) and (max-width: 1024px) {
  .content { padding: 2rem; }
  .nav-sidebar { width: 240px; }
}

/* Desktop (>1024px) */
@media (min-width: 1024px) {
  /* nav-toggle hidden when sidebar is pinned (handled by body class) */
}
```

## Accessibility

- Semantic HTML (`<nav>`, `<main>`, `<section>`, `<aside>`)
- Keyboard navigation works fully
- ARIA labels for interactive elements
- `prefers-reduced-motion` support
- Focus visible styles
- Skip to content link

## Data Charts (Chart.js)

When documentation includes data visualizations, load Chart.js from CDN and wrap charts in a responsive container. Charts are the one exception to the zero-dependency rule — load only when content requires it.

### Loading Chart.js

```html
<!-- Place in <head> or just before </body> — only include when charts are needed -->
<script src="https://cdn.jsdelivr.net/npm/chart.js@4/dist/chart.umd.min.js"></script>
```

### Chart Container Pattern

```html
<!-- Always wrap in a sized container — Chart.js fills its parent -->
<div class="chart-container">
  <canvas id="my-chart"></canvas>
</div>
```

```css
.chart-container {
  position: relative;
  width: 100%;
  max-width: 720px;
  margin: 1.5rem 0;
  background: var(--bg-surface);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 1.5rem;
}

/* Constrain height so charts don't grow unbounded */
.chart-container canvas {
  max-height: 360px;
}
```

### Initializing Charts

Always initialize inside `DOMContentLoaded` and read CSS variables for colors so charts respect the active theme:

```javascript
document.addEventListener('DOMContentLoaded', () => {
  // Read theme colors from CSS variables
  const style = getComputedStyle(document.documentElement);
  const accent  = style.getPropertyValue('--accent').trim();
  const border  = style.getPropertyValue('--border').trim();
  const textSec = style.getPropertyValue('--text-secondary').trim();

  // Common defaults — apply to every chart
  Chart.defaults.font.family = style.getPropertyValue('--font-body').trim();
  Chart.defaults.color = textSec;

  // Example: Bar chart
  new Chart(document.getElementById('my-chart'), {
    type: 'bar',
    data: {
      labels: ['Jan', 'Feb', 'Mar', 'Apr', 'May'],
      datasets: [{
        label: 'Monthly Users',
        data: [1200, 1900, 1500, 2100, 1800],
        backgroundColor: accent + '99', // 60% opacity
        borderColor: accent,
        borderWidth: 1,
        borderRadius: 4,
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: true,
      plugins: {
        legend: { position: 'top' },
        tooltip: { mode: 'index', intersect: false }
      },
      scales: {
        x: { grid: { color: border } },
        y: { grid: { color: border }, beginAtZero: true }
      }
    }
  });
});
```

### Chart Type Reference

| Type | Use case | `type` value |
|------|----------|-------------|
| Bar | Comparisons, rankings | `'bar'` |
| Line | Trends over time | `'line'` |
| Doughnut / Pie | Part-to-whole | `'doughnut'` / `'pie'` |
| Radar | Multi-axis comparison | `'radar'` |
| Scatter | Correlation | `'scatter'` |

### Multi-Dataset Line Chart

```javascript
new Chart(document.getElementById('trend-chart'), {
  type: 'line',
  data: {
    labels: ['Q1', 'Q2', 'Q3', 'Q4'],
    datasets: [
      {
        label: 'Revenue',
        data: [42000, 58000, 51000, 73000],
        borderColor: accent,
        backgroundColor: accent + '22',
        fill: true,
        tension: 0.4,
      },
      {
        label: 'Costs',
        data: [30000, 35000, 32000, 40000],
        borderColor: textSec,
        backgroundColor: 'transparent',
        borderDash: [5, 5],
        tension: 0.4,
      }
    ]
  },
  options: {
    responsive: true,
    maintainAspectRatio: true,
    plugins: { legend: { position: 'top' } },
    scales: {
      x: { grid: { color: border } },
      y: { grid: { color: border }, beginAtZero: true }
    }
  }
});
```

### Doughnut Chart

```javascript
new Chart(document.getElementById('dist-chart'), {
  type: 'doughnut',
  data: {
    labels: ['Category A', 'Category B', 'Category C'],
    datasets: [{
      data: [45, 30, 25],
      backgroundColor: [accent, accent + 'aa', accent + '55'],
      borderColor: 'transparent',
      hoverOffset: 8,
    }]
  },
  options: {
    responsive: true,
    maintainAspectRatio: true,
    plugins: {
      legend: { position: 'right' },
      tooltip: { callbacks: {
        label: ctx => ` ${ctx.label}: ${ctx.parsed}%`
      }}
    }
  }
});
```

### Dark Theme Support

When the page has a theme toggle, update chart colors on theme switch:

```javascript
// Store chart instances to update them later
const charts = {};

function applyChartTheme() {
  const style = getComputedStyle(document.documentElement);
  const border  = style.getPropertyValue('--border').trim();
  const textSec = style.getPropertyValue('--text-secondary').trim();

  Chart.defaults.color = textSec;

  Object.values(charts).forEach(chart => {
    chart.options.scales?.x && (chart.options.scales.x.grid.color = border);
    chart.options.scales?.y && (chart.options.scales.y.grid.color = border);
    chart.update();
  });
}

// Call after toggling data-theme on <html>
document.querySelector('.theme-toggle')?.addEventListener('click', () => {
  // ... existing toggle logic ...
  applyChartTheme();
});
```

### Lazy Loading Charts

For pages with many charts, initialize only when the container enters the viewport:

```javascript
const chartObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const canvas = entry.target.querySelector('canvas');
      if (canvas && !canvas.dataset.initialized) {
        canvas.dataset.initialized = 'true';
        initChart(canvas); // your init function
        chartObserver.unobserve(entry.target);
      }
    }
  });
}, { threshold: 0.1 });

document.querySelectorAll('.chart-container').forEach(el => {
  chartObserver.observe(el);
});
```

## Code Quality

- Clear comments explaining each section
- Descriptive variable and function names
- Organized CSS with logical grouping
- Modular JavaScript classes
- External dependencies only when necessary (e.g. Chart.js for data visualizations)
