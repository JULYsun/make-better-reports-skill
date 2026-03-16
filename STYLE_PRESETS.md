# Style Presets Reference - Documentation

Curated visual styles for Frontend Docs. Each preset is designed for readability and long-form content.— no generic "AI slop" aesthetics. **Abstract shapes only — no illustrations. - no emoji.**

---

## Professional/Technical Themes

### 1. Modern Clean

**Vibe:** Professional, clean, trustworthy

**Layout:** Left sidebar navigation with hierarchical TOC

**Typography:**
- Display: `Inter` (600/700) 
- Body: `Inter` (400/500)
- Code: `JetBrains Mono` (400)
- Numeric: `DM Mono` (400/500) — tabular figures for stats and counters

**Colors (Light):**
```css
:root {
    --bg-primary: #ffffff;
    --bg-surface: #f8f9fa;
    --accent: #3D71F6;
    --text-primary: #1a1a1a;
    --text-secondary: #666666;
    --border: #e0e0e0;
    --code-bg: #f5f5f5;
    --font-numeric: 'DM Mono', monospace;
}
```

**Colors (Dark):**
```css
:root {
    --bg-primary: #1a1a1a;
    --bg-surface: #2d2d2d;
    --accent: #7199FF;
    --text-primary: #ffffff;
    --text-secondary: #b3b3b3;
    --border: #404040;
    --code-bg: #2d2d2d;
    --font-numeric: 'DM Mono', monospace;
}
```

**Signature Elements:**
- Clean sidebar with pin/unpin toggle
- Left sidebar with hierarchical TOC
- Generous whitespace
- Subtle hover states

---

### 2. Dark Professional

**Vibe:** Technical, focused, modern

**Layout:** Left sidebar navigation with full-height TOC

**Typography:**
- Display: `Space Grotesk` (600/700)
- Body: `Inter` (400/500)
- Code: `JetBrains Mono` (400)
- Numeric: `Roboto Mono` (400/500) — tabular figures, pairs well with Space Grotesk

**Colors (Light):**
```css
:root {
    --bg-primary: #fafafa;
    --bg-surface: #ffffff;
    --accent: #06b6d4;
    --text-primary: #0f172a;
    --text-secondary: #64748b;
    --border: #e2e8f0;
    --code-bg: #f1f5f9;
    --font-numeric: 'Roboto Mono', monospace;
}
```

**Colors (Dark):**
```css
:root {
    --bg-primary: #0f172a;
    --bg-surface: #1e293b;
    --accent: #06b6d4;
    --text-primary: #f1f5f9;
    --text-secondary: #94a3b8;
    --border: #334155;
    --code-bg: #1e293b;
    --font-numeric: 'Roboto Mono', monospace;
}
```

**Signature Elements:**
- Full-height sidebar navigation
- Cyan accent for links and active states
- Compact TOC with indentation
- Code-focused design

---

### 3. Swiss Docs

**Vibe:** Minimal, precise, grid-based

**Layout:** Right sidebar navigation with hierarchical TOC

**Typography:**
- Display: `Archivo` (700/800)
- Body: `Nunito` (400/500)
- Code: `JetBrains Mono` (400)
- Numeric: `Space Mono` (400/700) — geometric monospace, matches Swiss grid aesthetic

**Colors:**
```css
:root {
    --bg-primary: #ffffff;
    --bg-surface: #f5f5f5;
    --accent: #ff3300;
    --text-primary: #000000;
    --text-secondary: #666666;
    --border: #cccccc;
    --code-bg: #f0f0f0;
    --font-numeric: 'Space Mono', monospace;
}
```

**Signature Elements:**
- Asymmetric layout
- Red accent color
- Visible grid structure
- Geometric precision

---

## Modern/Minimal Themes

### 4. Minimal Light

**Vibe:** Simple, elegant, focused

**Layout:** Left sidebar navigation with floating TOC

**Typography:**
- Display: `Plus Jakarta Sans` (600/700)
- Body: `Plus Jakarta Sans` (400/500)
- Code: `JetBrains Mono` (400)
- Numeric: `DM Mono` (400/500) — clean and neutral, won't distract

**Colors:**
```css
:root {
    --bg-primary: #ffffff;
    --bg-surface: #fafafa;
    --accent: #2563eb;
    --text-primary: #171717;
    --text-secondary: #737373;
    --border: #e5e5e5;
    --code-bg: #f5f5f5;
    --font-numeric: 'DM Mono', monospace;
}
```

**Signature Elements:**
- Minimal sidebar with pin/unpin toggle
- Floating TOC on scroll
- Maximum whitespace
- Subtle animations

---

### 5. Paper Docs

**Vibe:** Editorial, readable, comfortable

**Layout:** Centered content with sticky sidebar

**Typography:**
- Display: `Fraunces` (600/700)
- Body: `Source Serif 4` (400/500)
- Code: `JetBrains Mono` (400)
- Numeric: `Roboto Mono` (400/500) — neutral contrast to the serif body

**Colors:**
```css
:root {
    --bg-primary: #faf9f7;
    --bg-surface: #ffffff;
    --accent: #c2410c;
    --text-primary: #1a1a1a;
    --text-secondary: #57534e;
    --border: #e7e5e4;
    --code-bg: #f5f5f4;
    --font-numeric: 'Roboto Mono', monospace;
}
```

**Signature Elements:**
- Paper-like background
- Serif typography
- Warm color palette
- Drop caps for sections

---

### 6. Clean Slate

**Vibe:** Minimal, modern, spacious

**Layout:** Left sidebar navigation

**Typography:**
- Display: `Manrope` (600/700)
- Body: `Manrope` (400/500)
- Code: `JetBrains Mono` (400)
- Numeric: `DM Mono` (400/500) — shares the same clean geometric feel as Manrope

**Colors:**
```css
:root {
    --bg-primary: #f9fafb;
    --bg-surface: #ffffff;
    --accent: #3b82f6;
    --text-primary: #111827;
    --text-secondary: #6b7280;
    --border: #e5e7eb;
    --code-bg: #f3f4f6;
    --font-numeric: 'DM Mono', monospace;
}
```

**Signature Elements:**
- Ultra-clean design
- Generous padding
- Soft shadows
- Smooth transitions

---

## Warm/Friendly Themes

### 7. Warm Editorial

**Vibe:** Approachable, readable, inviting

**Layout:** Right sidebar navigation

**Typography:**
- Display: `Fraunces` (600/700)
- Body: `Source Serif 4` (400/500)
- Code: `JetBrains Mono` (400)
- Numeric: `IBM Plex Mono` (400/500) — warm and humanist, complements the editorial feel

**Colors (Light):**
```css
:root {
    --bg-primary: #faf9f7;
    --bg-surface: #ffffff;
    --accent: #ea580c;
    --text-primary: #1a1a1a;
    --text-secondary: #57534e;
    --border: #e7e5e4;
    --code-bg: #f5f5f4;
    --font-numeric: 'IBM Plex Mono', monospace;
}
```

**Colors (Dark):**
```css
:root {
    --bg-primary: #1c1917;
    --bg-surface: #292524;
    --accent: #fb923c;
    --text-primary: #fafaf9;
    --text-secondary: #a8a29e;
    --border: #44403c;
    --code-bg: #292524;
    --font-numeric: 'IBM Plex Mono', monospace;
}
```

**Signature Elements:**
- Warm color palette
- Serif typography
- Right-side navigation
- Comfortable line height

---

### 8. Notebook Style

**Vibe:** Friendly, organized, tactile

**Layout:** Left sidebar navigation with tabbed sections

**Typography:**
- Display: `Bodoni Moda` (600/700)
- Body: `DM Sans` (400/500)
- Code: `JetBrains Mono` (400)
- Numeric: `DM Mono` (400/500) — same DM family, consistent and friendly

**Colors:**
```css
:root {
    --bg-primary: #f8f6f1;
    --bg-surface: #ffffff;
    --accent: #8b5cf6;
    --text-primary: #1a1a1a;
    --text-secondary: #666666;
    --border: #d4d4d4;
    --code-bg: #f5f5f5;
    --tab-colors: #98d4bb, #c7b8ea, #f4b8c5, #a8d8ea;
    --font-numeric: 'DM Mono', monospace;
}
```

**Signature Elements:**
- Paper texture background
- Colorful section tabs
- Binder hole decorations
- Handwritten-style accents

---

### 9. Soft Cream

**Vibe:** Gentle, comfortable, easy on eyes

**Layout:** Left sidebar with soft colors

**Typography:**
- Display: `Outfit` (600/700)
- Body: `Outfit` (400/500)
- Code: `JetBrains Mono` (400)
- Numeric: `IBM Plex Mono` (400/500) — warm undertone matches the cream palette

**Colors:**
```css
:root {
    --bg-primary: #fefce8;
    --bg-surface: #fffef5;
    --accent: #ca8a04;
    --text-primary: #1c1917;
    --text-secondary: #78716c;
    --border: #e7e5e4;
    --code-bg: #fef9c3;
    --font-numeric: 'IBM Plex Mono', monospace;
}
```

**Signature Elements:**
- Cream background
- Soft shadows
- Rounded corners
- Warm accent colors

---

## Developer/Terminal Themes

### 10. Terminal Green

**Vibe:** Developer-focused, hacker aesthetic

**Layout:** Left sidebar navigation with monospace everything

**Typography:**
- Display: `JetBrains Mono` (600/700)
- Body: `JetBrains Mono` (400/500)
- Code: `JetBrains Mono` (400)
- Numeric: `JetBrains Mono` (400/500) — already monospace, use `font-variant-numeric: tabular-nums`

**Colors (Light):**
```css
:root {
    --bg-primary: #f5f5f5;
    --bg-surface: #ffffff;
    --accent: #16a34a;
    --text-primary: #0a0a0a;
    --text-secondary: #525252;
    --border: #d4d4d4;
    --code-bg: #e5e5e5;
    --font-numeric: 'JetBrains Mono', monospace;
}
```

**Colors (Dark):**
```css
:root {
    --bg-primary: #0d1117;
    --bg-surface: #161b22;
    --accent: #39d353;
    --text-primary: #c9d1d9;
    --text-secondary: #8b949e;
    --border: #30363d;
    --code-bg: #161b22;
    --font-numeric: 'JetBrains Mono', monospace;
}
```

**Signature Elements:**
- Monospace fonts everywhere
- Terminal green accent
- Scan line effects
- Blinking cursor

---

### 11. Code Dark

**Vibe:** Technical, focused, VS Code inspired

**Layout:** Left sidebar with dark theme

**Typography:**
- Display: `Fira Code` (600/700)
- Body: `Fira Code` (400/500)
- Code: `Fira Code` (400)
- Numeric: `Fira Code` (400/500) — already monospace with ligatures, use `font-variant-numeric: tabular-nums`

**Colors:**
```css
:root {
    --bg-primary: #1e1e1e;
    --bg-surface: #252526;
    --accent: #007acc;
    --text-primary: #d4d4d4;
    --text-secondary: #858585;
    --border: #3e3e42;
    --code-bg: #1e1e1e;
    --font-numeric: 'Fira Code', monospace;
}
```

**Signature Elements:**
- VS Code color scheme
- Ligature support
- Syntax highlighting colors
- Activity bar style sidebar

---

### 12. Hacker Theme

**Vibe:** Matrix-style, cyberpunk

**Layout:** Full-width with floating panels

**Typography:**
- Display: `Share Tech Mono` (400/700)
- Body: `Share Tech Mono` (400)
- Code: `Share Tech Mono` (400)
- Numeric: `Share Tech Mono` (400) — monospace throughout, use `font-variant-numeric: tabular-nums`

**Colors:**
```css
:root {
    --bg-primary: #000000;
    --bg-surface: #0a0a0a;
    --accent: #00ff00;
    --text-primary: #00ff00;
    --text-secondary: #008800;
    --border: #003300;
    --code-bg: #001100;
    --font-numeric: 'Share Tech Mono', monospace;
}
```

**Signature Elements:**
- Matrix green on black
- Glitch effects
- Scanlines
- Neon glow

---

## Navigation Patterns

### Sidebar Navigation (Left)
- Full-height sidebar
- Search at top
- Hierarchical TOC
- Content on right
- Pin/unpin toggle in sidebar header

### Sidebar Navigation (Right)
- Content on left
- Full-height sidebar on right
- Search at top of sidebar
- Pin/unpin toggle in sidebar header
- Good for RTL layouts

---

## Numeric Font Reference

All numeric fonts are free on Google Fonts and support `font-variant-numeric: tabular-nums` for aligned columns.

| Font | Google Fonts URL param | Best for |
|------|----------------------|----------|
| `DM Mono` | `DM+Mono:wght@400;500` | Clean/minimal themes |
| `Roboto Mono` | `Roboto+Mono:wght@400;500` | Technical/professional themes |
| `IBM Plex Mono` | `IBM+Plex+Mono:wght@400;500` | Warm/editorial themes |
| `Space Mono` | `Space+Mono:wght@400;700` | Swiss/geometric themes |
| `Fira Code` | `Fira+Code:wght@400;500` | Code-focused themes (has ligatures) |
| `JetBrains Mono` | `JetBrains+Mono:wght@400;500` | Developer/terminal themes |

**Usage pattern for numeric elements:**
```css
/* Apply to stats, counters, prices, version numbers, timestamps */
.stat-number,
.version-badge,
.line-count,
time,
.price {
    font-family: var(--font-numeric);
    font-variant-numeric: tabular-nums;
    font-feature-settings: "tnum";
}
```

---

## Responsive Behavior

All presets must support:

**Desktop (>1024px):**
- Full navigation visible
- Wide content area
- Sidebar always visible

**Tablet (768-1024px):**
- Collapsible sidebar
- Adjusted spacing
- Touch-friendly targets

**Mobile (<768px):**
- Hamburger menu
- Full-width content
- Overlay navigation
- Bottom-fixed search
