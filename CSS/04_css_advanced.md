# 04 — Advanced CSS (Variables, Animations, Transforms)

## CSS Custom Properties / Variables (used in EVERY modern project for theming)
```css
:root {
  --color-primary: #6366f1;
  --color-bg: #0f172a;
  --color-text: #e2e8f0;
  --radius: 8px;
  --spacing: 1rem;
  --transition: 0.2s ease;
}

.btn {
  background: var(--color-primary);
  border-radius: var(--radius);
  transition: background var(--transition);
}
```
**Why this matters in real projects:** change one variable in `:root`, the entire site's theme updates. This is literally how dark mode is built:
```css
:root {
  --bg: white;
  --text: black;
}
[data-theme="dark"] {
  --bg: #0f172a;
  --text: #e2e8f0;
}
body { background: var(--bg); color: var(--text); }
```
Toggle dark mode in JS by just flipping the `data-theme` attribute on `<html>` — no class juggling needed.

## Fallback values
```css
color: var(--accent, blue); /* uses blue if --accent isn't defined */
```

---

## Transitions (smooth state changes — used on every button/hover in real UI)
```css
.btn {
  background: var(--color-primary);
  transition: background 0.2s ease, transform 0.2s ease;
}
.btn:hover {
  background: #4f46e5;
  transform: translateY(-2px); /* subtle lift effect — common in modern UI */
}
```
**Project rule:** Always transition `transform` and `opacity` (GPU-accelerated, smooth) — avoid transitioning `width`/`height`/`top` (causes layout reflow, janky on low-end devices).

## Transforms (move, scale, rotate without affecting layout)
```css
.card:hover {
  transform: scale(1.03);            /* zoom on hover — product cards */
}
.icon { transform: rotate(45deg); }   /* rotate icon (e.g. plus → close) */
.modal { transform: translate(-50%, -50%); } /* perfect centering trick */
```

### Real Project: Perfectly centered modal (alternative to flex centering)
```css
.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

## Keyframe Animations
```css
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to   { opacity: 1; transform: translateY(0); }
}

.card {
  animation: fadeInUp 0.5s ease forwards;
}
```

### Real Project: Loading spinner (extremely common component)
```css
.spinner {
  width: 32px;
  height: 32px;
  border: 4px solid #e2e8f0;
  border-top-color: var(--color-primary);
  border-radius: 50%;
  animation: spin 0.8s linear infinite;
}
@keyframes spin {
  to { transform: rotate(360deg); }
}
```

### Real Project: Skeleton loading shimmer (used in modern apps while data loads)
```css
.skeleton {
  background: linear-gradient(90deg, #eee 25%, #ddd 50%, #eee 75%);
  background-size: 200% 100%;
  animation: shimmer 1.5s infinite;
}
@keyframes shimmer {
  0% { background-position: 200% 0; }
  100% { background-position: -200% 0; }
}
```

---

## Pseudo-classes/elements used heavily in real projects
```css
.list-item:nth-child(odd) { background: #f8f9fa; }   /* zebra striping tables */
.list-item:last-child { border-bottom: none; }         /* remove last border */
input:invalid { border-color: red; }                    /* form validation styling */
input:placeholder-shown { border-color: #ccc; }
.tooltip::after {
  content: attr(data-tooltip);  /* pulls value from data attribute — real tooltip trick */
  position: absolute;
}
```

## Gradients (used in hero sections, buttons, backgrounds constantly)
```css
background: linear-gradient(135deg, #6366f1, #8b5cf6);
background: radial-gradient(circle at top left, #fff, #e2e8f0);
```

## Shadows (depth in modern UI — neumorphism/material design)
```css
.card {
  box-shadow: 0 4px 6px -1px rgba(0,0,0,0.1), 0 2px 4px -2px rgba(0,0,0,0.1);
  /* layered shadow = more realistic depth than single shadow */
}
.input:focus {
  box-shadow: 0 0 0 3px rgba(99,102,241,0.3); /* focus ring — accessibility + modern look */
}
```

## Filters & backdrop-filter (glassmorphism — trendy modern effect)
```css
.glass-card {
  background: rgba(255,255,255,0.1);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255,255,255,0.2);
}
```

---
**Quick revision checklist:**
- [ ] Can you build dark mode toggle with CSS variables from memory?
- [ ] Can you write a loading spinner with @keyframes?
- [ ] Do you know why transform/opacity are preferred for animations?
- [ ] Can you write a glassmorphism card?