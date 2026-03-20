# Style Presets Reference - Documentation

No generic "AI slop" aesthetics. Abstract shapes only — no illustrations, no emoji.

---

## ⚠️ Card Rules — Apply to Every Card / Panel / Box

**❌ NEVER:**
```css
border-left: 3px solid var(--accent);  /* single-side stripe — #1 AI slop tell */
border-top: 2px solid var(--accent);   /* applies to ALL states: default/hover/active/selected */
box-shadow: 0 8px 32px rgba(0,0,0,0.18); /* heavy modal shadow */
```

**✅ 4 allowed patterns — pick one per card type, don't mix:**

```css
/* A — Surface Lift (default) */
.card          { background: var(--bg-surface); border: 1px solid var(--border); border-radius: 8px; padding: 1.25rem; }

/* B — Inset (code blocks, data tables) */
.card-inset    { background: var(--bg-surface); border: 1px solid var(--border); border-radius: 8px; padding: 1.25rem; box-shadow: inset 0 1px 3px rgba(0,0,0,0.06); }

/* C — Outlined + hover fill (interactive/selectable) */
.card-outlined { background: transparent; border: 1px solid var(--border); border-radius: 8px; padding: 1.25rem; transition: background 0.15s, border-color 0.15s; }
.card-outlined:hover { background: var(--bg-surface); border-color: var(--accent); }

/* D — Elevated (hero/testimonial only, max 1 per section) */
.card-elevated { background: var(--bg-surface); border: 1px solid var(--border); border-radius: 10px; padding: 1.75rem; box-shadow: 0 2px 8px rgba(0,0,0,0.07), 0 0 0 1px var(--border); }
```

**Accent state → background tint, never a stripe:**
```css
.card-active { background: color-mix(in srgb, var(--accent) 6%, var(--bg-surface)); border: 1px solid color-mix(in srgb, var(--accent) 20%, var(--border)); border-radius: 8px; }
```

**Card grid → gap only, never margins:**
```css
.card-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(240px, 1fr)); gap: 1rem; }
```

---

## Presets

### 0 — Mono Mosaic ★ default

> Use when user has not specified any style preference.

**Vibe:** Warm cream + developer precision. Compact 14px body, Geist + Geist Mono, amber accent.
**Layout:** Left sidebar, hierarchical TOC

**Fonts:**
```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Geist:wght@300;400;500;600;700&family=Geist+Mono:wght@400;500&display=swap">
```

```css
:root {
    --bg-primary:   #FFFEF2;
    --bg-surface:   #F7F6E8;
    --text-primary: #191918;
    --text-secondary: rgba(25,25,24,.45);
    --border:       rgba(25,25,24,.12);
    --accent:       #FCAA2D;
    --green:        #28C840;
    --code-bg:      #18181a;
    --font-display: 'Geist', sans-serif;
    --font-body:    'Geist', sans-serif;
    --font-code:    'Geist Mono', monospace;
    --font-numeric: 'Geist Mono', monospace;
    /* scale: compact */
    --text-body:    0.875rem;   /* 14px */
    --text-small:   0.8125rem;  /* 13px */
    --text-mono-label: 0.6875rem; /* 11px uppercase */
    --lh-body:      1.7;
    --lh-heading:   1.1;
}
```

**Code syntax (on dark `--code-bg`):**
```css
.token-comment { color: rgba(255,255,255,0.25); }
.token-method  { color: #FCAA2D; }
.token-url     { color: #a5c8ff; }
.token-key     { color: #98d9a4; }
.token-value   { color: #f0a97a; }
```

**TOC active — background tint, no stripe:**
```css
.toc-link { font-family: var(--font-code); font-size: 0.68rem; text-transform: uppercase; letter-spacing: 0.08em; color: var(--text-secondary); padding: 0.3rem 0.75rem; border-radius: 4px; transition: color 0.2s, background 0.2s; }
.toc-link.active { color: var(--accent); background: color-mix(in srgb, var(--accent) 8%, transparent); }
```

---

### 1 — Light Professional

**Vibe:** Clean white, indigo accent, DM Sans headers. Precise, trustworthy, airy. Standard 16px body.
**Layout:** Left sidebar, full-height TOC

**Fonts:**
```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&family=DM+Mono:wght@400;500&display=swap">
```

```css
:root {
    --bg-primary:   #ffffff;
    --bg-surface:   #f8f9fb;
    --text-primary: #111827;
    --text-secondary: #6b7280;
    --border:       #e5e7eb;
    --accent:       #4f46e5;
    --code-bg:      #f3f4f6;
    --font-display: 'DM Sans', sans-serif;
    --font-body:    'DM Sans', sans-serif;
    --font-code:    'JetBrains Mono', monospace;
    --font-numeric: 'DM Mono', monospace;
    /* scale: standard */
    --text-body:    1rem;
    --text-small:   0.875rem;
    --text-mono-label: 0.7rem;
    --lh-body:      1.65;
    --lh-heading:   1.15;
}
```

**TOC active:**
```css
.toc-link.active { color: var(--accent); background: color-mix(in srgb, var(--accent) 8%, transparent); border-radius: 4px; }
```

---

### 2 — Paper Docs

**Vibe:** Serif editorial, warm off-white, rust accent. Relaxed 17px reading scale.
**Layout:** Left sidebar, centered content max-width 720px

**Fonts:**
```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Fraunces:wght@600;700&family=Source+Serif+4:wght@400;500&family=JetBrains+Mono:wght@400&family=Roboto+Mono:wght@400;500&display=swap">
```

```css
:root {
    --bg-primary:   #faf9f7;
    --bg-surface:   #ffffff;
    --text-primary: #1a1a1a;
    --text-secondary: #57534e;
    --border:       #e7e5e4;
    --accent:       #c2410c;
    --code-bg:      #f5f5f4;
    --font-display: 'Fraunces', serif;
    --font-body:    'Source Serif 4', serif;
    --font-code:    'JetBrains Mono', monospace;
    --font-numeric: 'Roboto Mono', monospace;
    /* scale: reading */
    --text-body:    1.0625rem;  /* 17px */
    --text-small:   0.9375rem;  /* 15px */
    --text-mono-label: 0.75rem;
    --lh-body:      1.8;
    --lh-heading:   1.2;
}
```

**TOC active:**
```css
.toc-link.active { color: var(--accent); background: color-mix(in srgb, var(--accent) 7%, transparent); border-radius: 4px; }
```

---

### 3 — Swiss Docs

**Vibe:** Grid-based, Archivo bold headers, red accent, right sidebar. Standard scale.
**Layout:** Right sidebar

**Fonts:**
```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Archivo:wght@700;800&family=Nunito:wght@400;500&family=JetBrains+Mono:wght@400&family=Space+Mono:wght@400;700&display=swap">
```

```css
:root {
    --bg-primary:   #ffffff;
    --bg-surface:   #f5f5f5;
    --text-primary: #000000;
    --text-secondary: #666666;
    --border:       #cccccc;
    --accent:       #ff3300;
    --code-bg:      #f0f0f0;
    --font-display: 'Archivo', sans-serif;
    --font-body:    'Nunito', sans-serif;
    --font-code:    'JetBrains Mono', monospace;
    --font-numeric: 'Space Mono', monospace;
    /* scale: standard */
    --text-body:    1rem;
    --text-small:   0.875rem;
    --text-mono-label: 0.7rem;
    --lh-body:      1.65;
    --lh-heading:   1.05;
}
```

**TOC active:**
```css
.toc-link.active { color: var(--accent); background: color-mix(in srgb, var(--accent) 7%, transparent); border-radius: 2px; }
```

---

### 4 — Terminal Green

**Vibe:** Full monospace, dark GitHub-style bg, green accent. Compact scale.
**Layout:** Left sidebar

**Fonts:**
```html
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600;700&display=swap">
```

```css
:root {
    --bg-primary:   #0d1117;
    --bg-surface:   #161b22;
    --text-primary: #c9d1d9;
    --text-secondary: #8b949e;
    --border:       #30363d;
    --accent:       #39d353;
    --code-bg:      #161b22;
    --font-display: 'JetBrains Mono', monospace;
    --font-body:    'JetBrains Mono', monospace;
    --font-code:    'JetBrains Mono', monospace;
    --font-numeric: 'JetBrains Mono', monospace;
    /* scale: compact */
    --text-body:    0.875rem;
    --text-small:   0.8125rem;
    --text-mono-label: 0.6875rem;
    --lh-body:      1.7;
    --lh-heading:   1.1;
}
```

**TOC active:**
```css
.toc-link.active { color: var(--accent); background: color-mix(in srgb, var(--accent) 8%, transparent); border-radius: 3px; }
```

---

## Shared Rules

**Numeric elements (all presets):**
```css
.stat-number, time, .version-badge {
    font-family: var(--font-numeric);
    font-variant-numeric: tabular-nums;
    font-feature-settings: "tnum";
}
```

**Responsive:**
- Desktop: sidebar always visible
- Tablet 768–1024px: collapsible sidebar
- Mobile <768px: hamburger overlay, pin disabled
