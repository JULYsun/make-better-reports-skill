# Animation Patterns Reference — Documentation

Use this reference when generating documentation pages. Docs are different from slides: animations should enhance readability and navigation, not distract from content.

## Effect-to-Feeling Guide

| Feeling | Animations | Visual Cues |
|---------|-----------|-------------|
| **Professional / Technical** | Subtle fade-ins (0.3s), clean transitions | Precise spacing, muted palette, monospace accents |
| **Modern / Minimal** | Gentle slide-up on scroll, soft fades | High whitespace, thin borders, restrained motion |
| **Warm / Editorial** | Slow reveals (0.6s), paragraph-by-paragraph | Serif typography, warm backgrounds, generous padding |
| **Developer / Terminal** | Typewriter text, cursor blink, scan lines | Monospace fonts, dark backgrounds, neon accents |
| **Playful / Friendly** | Bouncy hover states, color transitions | Rounded corners, pastel colors, icon animations |

---

## Scroll-Triggered Entrance Animations

These trigger as sections enter the viewport via Intersection Observer.

```css
/* === FADE + SLIDE UP (default for most docs) === */
.reveal {
    opacity: 0;
    transform: translateY(20px);
    transition: opacity 0.5s ease-out, transform 0.5s ease-out;
}
.reveal.visible {
    opacity: 1;
    transform: translateY(0);
}

/* === FADE IN ONLY (minimal, for professional themes) === */
.reveal-fade {
    opacity: 0;
    transition: opacity 0.4s ease-out;
}
.reveal-fade.visible {
    opacity: 1;
}

/* === SLIDE FROM LEFT (for sidebar-heavy layouts) === */
.reveal-left {
    opacity: 0;
    transform: translateX(-24px);
    transition: opacity 0.5s ease-out, transform 0.5s ease-out;
}
.reveal-left.visible {
    opacity: 1;
    transform: translateX(0);
}

/* Stagger children — use on section containers */
.stagger-children > * {
    opacity: 0;
    transform: translateY(16px);
    transition: opacity 0.4s ease-out, transform 0.4s ease-out;
}
.stagger-children.visible > *:nth-child(1) { transition-delay: 0.05s; }
.stagger-children.visible > *:nth-child(2) { transition-delay: 0.1s; }
.stagger-children.visible > *:nth-child(3) { transition-delay: 0.15s; }
.stagger-children.visible > *:nth-child(4) { transition-delay: 0.2s; }
.stagger-children.visible > * { opacity: 1; transform: translateY(0); }
```

```javascript
/* Intersection Observer for scroll reveals */
const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
        if (entry.isIntersecting) {
            entry.target.classList.add('visible');
        }
    });
}, { threshold: 0.1, rootMargin: '0px 0px -60px 0px' });

document.querySelectorAll('.reveal, .reveal-fade, .reveal-left, .stagger-children')
    .forEach(el => observer.observe(el));
```

---

## Navigation Animations

```css
/* === TOC ACTIVE LINK TRANSITION === */
.toc-link {
    transition: color 0.2s ease, background-color 0.2s ease, padding-left 0.2s ease;
}
.toc-link.active {
    padding-left: 1.25rem; /* subtle indent on active */
}

/* === SIDEBAR SLIDE IN (mobile / unpinned) === */
.nav-sidebar {
    transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
.nav-sidebar.open {
    transform: translateX(0) !important;
}

/* === PROGRESS BAR (reading progress) === */
.reading-progress {
    position: fixed;
    top: 0;
    left: 0;
    height: 3px;
    background: var(--accent);
    width: 0%;
    transition: width 0.1s linear;
    z-index: 9999;
}
```

```javascript
/* Reading progress bar */
window.addEventListener('scroll', () => {
    const scrollTop = window.scrollY;
    const docHeight = document.documentElement.scrollHeight - window.innerHeight;
    const progress = (scrollTop / docHeight) * 100;
    document.querySelector('.reading-progress').style.width = `${progress}%`;
});
```

---

## Interactive Content Components

These are self-contained interactive widgets to embed in documentation.

### Tabbed Code Blocks

```css
.tabs {
    border: 1px solid var(--border);
    border-radius: 8px;
    overflow: hidden;
    margin-bottom: 1.5rem;
}
.tab-list {
    display: flex;
    background: var(--bg-surface);
    border-bottom: 1px solid var(--border);
    padding: 0;
    margin: 0;
    list-style: none;
}
.tab-btn {
    padding: 0.6rem 1.25rem;
    font-family: var(--font-code);
    font-size: 0.85rem;
    background: none;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    color: var(--text-secondary);
    transition: color 0.2s, background 0.2s;
}
.tab-btn.active {
    color: var(--accent);
    background: color-mix(in srgb, var(--accent) 8%, transparent);
}
.tab-panel { display: none; }
.tab-panel.active { display: block; }
```

```javascript
/* Tabbed code blocks */
document.querySelectorAll('.tabs').forEach(tabs => {
    const buttons = tabs.querySelectorAll('.tab-btn');
    const panels = tabs.querySelectorAll('.tab-panel');

    buttons.forEach((btn, i) => {
        btn.addEventListener('click', () => {
            buttons.forEach(b => b.classList.remove('active'));
            panels.forEach(p => p.classList.remove('active'));
            btn.classList.add('active');
            panels[i].classList.add('active');
        });
    });
});
```

**Usage in HTML:**
```html
<div class="tabs">
  <ul class="tab-list">
    <li><button class="tab-btn active">JavaScript</button></li>
    <li><button class="tab-btn">Python</button></li>
  </ul>
  <div class="tab-panel active"><pre><code>// JS code</code></pre></div>
  <div class="tab-panel"><pre><code># Python code</code></pre></div>
</div>
```

---

### Collapsible Sections (Accordion)

```css
.accordion-item {
    border: 1px solid var(--border);
    border-radius: 6px;
    margin-bottom: 0.5rem;
    overflow: hidden;
}
.accordion-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 1.25rem;
    cursor: pointer;
    background: var(--bg-surface);
    font-weight: 600;
    user-select: none;
    transition: background 0.2s;
}
.accordion-header:hover { background: var(--bg-primary); }
.accordion-icon {
    transition: transform 0.3s ease;
    font-style: normal;
}
.accordion-item.open .accordion-icon { transform: rotate(180deg); }
.accordion-body {
    max-height: 0;
    overflow: hidden;
    transition: max-height 0.35s ease, padding 0.35s ease;
    padding: 0 1.25rem;
}
.accordion-item.open .accordion-body {
    max-height: 1000px;
    padding: 1rem 1.25rem;
}
```

```javascript
document.querySelectorAll('.accordion-header').forEach(header => {
    header.addEventListener('click', () => {
        const item = header.parentElement;
        item.classList.toggle('open');
    });
});
```

**Usage in HTML:**
```html
<div class="accordion-item">
  <div class="accordion-header">
    What is this? <em class="accordion-icon">▾</em>
  </div>
  <div class="accordion-body">
    <p>Answer content here.</p>
  </div>
</div>
```

---

### Copy-to-Clipboard Code Blocks

```css
.code-block {
    position: relative;
}
.copy-btn {
    position: absolute;
    top: 0.5rem;
    right: 0.5rem;
    padding: 0.3rem 0.7rem;
    font-size: 0.75rem;
    font-family: var(--font-code);
    background: var(--bg-surface);
    border: 1px solid var(--border);
    border-radius: 4px;
    cursor: pointer;
    color: var(--text-secondary);
    opacity: 0;
    transition: opacity 0.2s, background 0.2s;
}
.code-block:hover .copy-btn { opacity: 1; }
.copy-btn.copied {
    color: var(--accent);
    border-color: var(--accent);
}
```

```javascript
document.querySelectorAll('.code-block').forEach(block => {
    const btn = document.createElement('button');
    btn.className = 'copy-btn';
    btn.textContent = 'copy';
    block.appendChild(btn);

    btn.addEventListener('click', () => {
        const code = block.querySelector('code').textContent;
        navigator.clipboard.writeText(code).then(() => {
            btn.textContent = 'copied!';
            btn.classList.add('copied');
            setTimeout(() => {
                btn.textContent = 'copy';
                btn.classList.remove('copied');
            }, 2000);
        });
    });
});
```

---

### Callout / Alert Boxes

```css
.callout {
    display: flex;
    gap: 0.75rem;
    padding: 1rem 1.25rem;
    border-radius: 6px;
    border: 1px solid;          /* full perimeter, no single-side stripe */
    margin-bottom: 1.5rem;
    font-size: 0.95rem;
}
.callout-icon { font-size: 1.1rem; flex-shrink: 0; }
.callout.info    { background: #eff6ff; border-color: rgba(59,130,246,.3);  color: #1e40af; }
.callout.warning { background: #fffbeb; border-color: rgba(245,158,11,.3);  color: #92400e; }
.callout.danger  { background: #fef2f2; border-color: rgba(239,68,68,.3);   color: #991b1b; }
.callout.success { background: #f0fdf4; border-color: rgba(34,197,94,.3);   color: #166534; }

/* Dark theme overrides */
[data-theme="dark"] .callout.info    { background: #1e3a5f; border-color: rgba(59,130,246,.25);  color: #93c5fd; }
[data-theme="dark"] .callout.warning { background: #3d2e00; border-color: rgba(245,158,11,.25);  color: #fcd34d; }
[data-theme="dark"] .callout.danger  { background: #3d0000; border-color: rgba(239,68,68,.25);   color: #fca5a5; }
[data-theme="dark"] .callout.success { background: #052e16; border-color: rgba(34,197,94,.25);   color: #86efac; }
```

**Usage in HTML:**
```html
<div class="callout info">
  <span class="callout-icon">ℹ️</span>
  <div>This is an informational note.</div>
</div>
<div class="callout warning">
  <span class="callout-icon">⚠️</span>
  <div>Watch out for this edge case.</div>
</div>
```

---

### Dark / Light Theme Toggle

```css
.theme-toggle {
    background: none;
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 0.3rem 0.75rem;
    cursor: pointer;
    font-size: 0.85rem;
    color: var(--text-secondary);
    transition: all 0.2s;
}
.theme-toggle:hover { border-color: var(--accent); color: var(--accent); }
```

```javascript
/* Theme toggle — add data-theme="dark" to <html> */
const toggle = document.querySelector('.theme-toggle');
const html = document.documentElement;

// Persist preference
const saved = localStorage.getItem('theme') || 'light';
html.setAttribute('data-theme', saved);
toggle.textContent = saved === 'dark' ? '☀️ Light' : '🌙 Dark';

toggle.addEventListener('click', () => {
    const current = html.getAttribute('data-theme');
    const next = current === 'dark' ? 'light' : 'dark';
    html.setAttribute('data-theme', next);
    localStorage.setItem('theme', next);
    toggle.textContent = next === 'dark' ? '☀️ Light' : '🌙 Dark';
});
```

**CSS for dark theme overrides (add to :root):**
```css
[data-theme="dark"] {
    --bg-primary: /* dark bg */;
    --bg-surface: /* dark surface */;
    --text-primary: /* light text */;
    /* ... override all color variables */
}
```

---

### Inline Demo / Playground

For interactive demos embedded in docs:

```css
.demo-box {
    border: 1px solid var(--border);
    border-radius: 8px;
    overflow: hidden;
    margin-bottom: 1.5rem;
}
.demo-preview {
    padding: 2rem;
    background: var(--bg-surface);
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: 120px;
    border-bottom: 1px solid var(--border);
}
.demo-controls {
    padding: 1rem 1.25rem;
    display: flex;
    gap: 0.75rem;
    flex-wrap: wrap;
    background: var(--bg-primary);
}
.demo-btn {
    padding: 0.4rem 1rem;
    border: 1px solid var(--border);
    border-radius: 4px;
    cursor: pointer;
    font-size: 0.85rem;
    background: var(--bg-surface);
    color: var(--text-primary);
    transition: all 0.2s;
}
.demo-btn:hover, .demo-btn.active {
    background: var(--accent);
    color: #fff;
    border-color: var(--accent);
}
```

---

## Background Effects (Subtle — for docs)

Unlike slides, doc backgrounds should be subtle and not compete with content.

```css
/* Subtle gradient — works for hero sections or headers */
.section-hero {
    background:
        radial-gradient(ellipse at 70% 50%, rgba(var(--accent-rgb), 0.08) 0%, transparent 60%),
        var(--bg-surface);
}

/* Dot grid — for technical/developer themes */
.dot-grid-bg {
    background-image: radial-gradient(circle, var(--border) 1px, transparent 1px);
    background-size: 24px 24px;
}

/* Subtle noise texture */
.noise-bg {
    position: relative;
}
.noise-bg::before {
    content: '';
    position: absolute;
    inset: 0;
    opacity: 0.03;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
    pointer-events: none;
}
```

---

## Micro-interactions

```css
/* Back to top — fade + slide up on appear, nudge up on hover */
.back-to-top {
    transition: opacity 0.25s ease, transform 0.25s ease;
}
.back-to-top.visible { opacity: 1; transform: translateY(0); }
.back-to-top:not(.visible) { opacity: 0; transform: translateY(12px); pointer-events: none; }
.back-to-top:hover { transform: translateY(-2px); }

/* Smooth link underline */
.content a {
    background-image: linear-gradient(var(--accent), var(--accent));
    background-size: 0% 1px;
    background-repeat: no-repeat;
    background-position: left bottom;
    transition: background-size 0.3s ease;
}
.content a:hover {
    background-size: 100% 1px;
    text-decoration: none;
}

/* Table row hover */
tbody tr {
    transition: background-color 0.15s ease;
}
tbody tr:hover {
    background-color: var(--bg-surface);
}

/* Heading anchor link (appears on hover) */
.heading-anchor {
    opacity: 0;
    margin-left: 0.5rem;
    font-size: 0.8em;
    color: var(--text-secondary);
    text-decoration: none;
    transition: opacity 0.2s;
}
h2:hover .heading-anchor,
h3:hover .heading-anchor {
    opacity: 1;
}
```

---

## Chart Animations (Chart.js)

Chart.js has built-in animation support. Configure it to match the doc's overall motion style.

### Entry Animation by Theme

```javascript
// Professional / Technical — fast, subtle
const animationConfig = {
  duration: 400,
  easing: 'easeOutQuart',
};

// Warm / Editorial — slower, more expressive
const animationConfig = {
  duration: 800,
  easing: 'easeInOutCubic',
};

// Developer / Terminal — instant (no animation)
const animationConfig = {
  duration: 0,
};

// Apply globally before creating any charts
Chart.defaults.animation = animationConfig;
```

### Animate Chart on Scroll (Lazy Trigger)

Prevent charts from animating before the user sees them:

```javascript
// Set duration: 0 initially, restore when visible
const chartObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const canvas = entry.target.querySelector('canvas');
      if (canvas?._chart) {
        canvas._chart.options.animation.duration = 600;
        canvas._chart.reset();   // resets data to 0
        canvas._chart.update();  // animates in
      }
      chartObserver.unobserve(entry.target);
    }
  });
}, { threshold: 0.2 });

document.querySelectorAll('.chart-container').forEach(el => {
  chartObserver.observe(el);
});
```

### Hover Interaction Enhancements

```javascript
// Highlight the hovered dataset, dim others
options: {
  interaction: {
    mode: 'dataset',
    intersect: false,
  },
  plugins: {
    tooltip: {
      animation: { duration: 150 },
      callbacks: {
        // Custom label formatting
        label: ctx => ` ${ctx.dataset.label}: ${ctx.formattedValue}`
      }
    }
  }
}
```

### Animated Counter for Chart Stats

Pair a chart with an animated number that counts up when visible:

```css
.chart-stat {
  font-family: var(--font-numeric);
  font-variant-numeric: tabular-nums;
  font-size: 2rem;
  font-weight: 700;
  color: var(--accent);
}
```

```javascript
function animateCounter(el, target, duration = 800) {
  const start = performance.now();
  const update = (now) => {
    const elapsed = now - start;
    const progress = Math.min(elapsed / duration, 1);
    // ease out cubic
    const eased = 1 - Math.pow(1 - progress, 3);
    el.textContent = Math.round(eased * target).toLocaleString();
    if (progress < 1) requestAnimationFrame(update);
  };
  requestAnimationFrame(update);
}

// Trigger on scroll
const statObserver = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      const target = parseInt(entry.target.dataset.target, 10);
      animateCounter(entry.target, target);
      statObserver.unobserve(entry.target);
    }
  });
}, { threshold: 0.5 });

document.querySelectorAll('.chart-stat[data-target]').forEach(el => {
  statObserver.observe(el);
});
```

**Usage:**
```html
<span class="chart-stat" data-target="12400">0</span>
```

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Scroll reveal not triggering | Check `rootMargin` — increase bottom margin if sections are tall |
| TOC active state jumps | Adjust `rootMargin` on IntersectionObserver (e.g. `-100px 0px -66%`) |
| Accordion height glitch | Use `max-height` transition instead of `height` — set a large enough max value |
| Copy button not showing | Ensure `.code-block` has `position: relative` |
| Theme toggle flickers on load | Read `localStorage` before DOM paint, set `data-theme` on `<html>` immediately |
| Back to top not appearing | Check `z-index` — must be below sidebar (< 1000) but above content. Verify scroll threshold matches `window.innerHeight` |
| Sidebar overlay issues | Use `z-index` layering: sidebar > 1000, overlay = 999, toggle = 998, content = auto |
| Sidebar pin state flickers | Read `localStorage` before first paint and set classes on `<body>` immediately in a `<script>` tag in `<head>` |
| `prefers-reduced-motion` | Wrap all transitions in `@media (prefers-reduced-motion: no-preference)` |
