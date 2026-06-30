# 03 — Positioning & Responsive Design

## Position property (real use cases, not just theory)
```css
position: static;    /* default — normal flow */
position: relative;   /* offsets from its OWN normal position, doesn't break flow */
position: absolute;   /* removed from flow, positioned relative to nearest positioned ancestor */
position: fixed;      /* relative to viewport, stays on scroll — navbars, chat buttons */
position: sticky;     /* hybrid — sticks once it hits a scroll threshold */
```

### Real Project: Sticky navbar on scroll
```css
.navbar {
  position: sticky;
  top: 0;
  z-index: 100;
  background: white;
}
```
This is THE pattern for headers that stay visible while scrolling. Used everywhere.

### Real Project: Badge/notification dot on an icon
```css
.icon-wrapper { position: relative; }
.badge {
  position: absolute;
  top: -4px;
  right: -4px;
  background: red;
  border-radius: 50%;
  width: 18px;
  height: 18px;
}
```
**Key rule:** `position: absolute` child always looks for the nearest parent with `position: relative` (or absolute/fixed). If none exists, it positions relative to the whole page — the #1 cause of "why is my badge in the corner of the screen" bugs.

### Real Project: Modal/overlay (fixed + centering)
```css
.overlay {
  position: fixed;
  inset: 0;                 /* shorthand for top:0; right:0; bottom:0; left:0; */
  background: rgba(0,0,0,0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}
```

## z-index (stacking order — only works on positioned elements)
```css
.modal { position: fixed; z-index: 1000; }
.dropdown { position: absolute; z-index: 50; }
.navbar { position: sticky; z-index: 100; }
```
**Project tip:** Keep a z-index scale in mind (e.g. dropdown:50, navbar:100, modal:1000, toast:9999) instead of random numbers — avoids stacking bugs in big projects.

---

## Responsive Design (mobile-first — how real projects are built)

### Media queries
```css
/* Mobile-first: base styles = mobile, then scale UP */
.container {
  padding: 1rem;
}

@media (min-width: 640px) {  /* tablet */
  .container { padding: 2rem; }
}

@media (min-width: 1024px) { /* desktop */
  .container { padding: 3rem; max-width: 1200px; margin: 0 auto; }
}
```
**Why mobile-first:** most traffic today is mobile, and it's easier to ADD complexity for bigger screens than remove it. This is the industry-standard approach.

### Common breakpoints used in real projects
```css
/* small phones:    default        */
/* tablets:    min-width: 640px    */
/* small laptop:    min-width: 1024px   */
/* desktop:    min-width: 1280px   */
```

### Real Project: Responsive navbar (hide links, show hamburger on mobile)
```css
.nav-links { display: flex; gap: 2rem; }

@media (max-width: 768px) {
  .nav-links { display: none; }      /* hidden by default on mobile */
  .nav-links.open { display: flex; flex-direction: column; }  /* toggled via JS */
  .hamburger { display: block; }
}
.hamburger { display: none; }  /* hidden on desktop */
```

### Fluid typography without media queries (modern trick)
```css
h1 {
  font-size: clamp(1.5rem, 4vw + 1rem, 3rem);
  /* min 1.5rem, scales with viewport, max 3rem — no breakpoints needed */
}
```
`clamp(min, preferred, max)` is heavily used in modern projects to avoid writing 5 media queries just for font sizing.

### Responsive images
```css
img {
  max-width: 100%;
  height: auto;     /* prevents overflow, keeps aspect ratio */
  display: block;     /* removes weird inline gap below images */
}
```

### Container queries (modern alternative to media queries — component-level responsiveness)
```css
.card-container { container-type: inline-size; }

@container (min-width: 400px) {
  .card { display: flex; }
}
```
Used when a component (like a card) needs to respond to ITS OWN container size, not the whole viewport — useful in widget/dashboard projects where the same component lives in different-width containers.

---
**Quick revision checklist:**
- [ ] Can you explain absolute positioning needing a relative parent?
- [ ] Can you write a mobile-first media query setup from memory?
- [ ] Do you know the `clamp()` syntax for fluid type?
- [ ] Do you understand z-index stacking and why it sometimes "doesn't work" (needs position set)?