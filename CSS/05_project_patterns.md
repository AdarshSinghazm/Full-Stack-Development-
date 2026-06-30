# 05 — Real Project Patterns (Copy-Paste-Ready Components)

This file is pure "I need this exact thing in my project" reference.

## 1. CSS Reset (start of EVERY project)
```css
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
html { scroll-behavior: smooth; }
body { line-height: 1.6; -webkit-font-smoothing: antialiased; }
img, picture, video { max-width: 100%; display: block; }
input, button, textarea, select { font: inherit; }
```

## 2. Button component (with variants — real design system pattern)
```css
.btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 0.6rem 1.4rem;
  border-radius: 8px;
  font-weight: 600;
  border: none;
  cursor: pointer;
  transition: all 0.2s ease;
}
.btn-primary {
  background: var(--color-primary);
  color: white;
}
.btn-primary:hover { background: #4f46e5; transform: translateY(-1px); }
.btn-outline {
  background: transparent;
  border: 2px solid var(--color-primary);
  color: var(--color-primary);
}
.btn:disabled { opacity: 0.5; cursor: not-allowed; }
```

## 3. Card component
```css
.card {
  background: white;
  border-radius: 12px;
  padding: 1.5rem;
  box-shadow: 0 1px 3px rgba(0,0,0,0.1);
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}
.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.12);
}
```

## 4. Form input with focus & error states
```css
.input {
  width: 100%;
  padding: 0.7rem 1rem;
  border: 1.5px solid #d1d5db;
  border-radius: 8px;
  transition: border-color 0.2s ease, box-shadow 0.2s ease;
}
.input:focus {
  outline: none;
  border-color: var(--color-primary);
  box-shadow: 0 0 0 3px rgba(99,102,241,0.2);
}
.input.error { border-color: #ef4444; }
.error-message { color: #ef4444; font-size: 0.85rem; margin-top: 4px; }
```

## 5. Hero section (landing page must-have)
```css
.hero {
  min-height: 90vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  background: linear-gradient(135deg, #6366f1, #8b5cf6);
  color: white;
  padding: 2rem;
}
.hero h1 { font-size: clamp(2rem, 5vw, 4rem); margin-bottom: 1rem; }
.hero p { max-width: 600px; opacity: 0.9; margin-bottom: 2rem; }
```

## 6. Responsive image gallery
```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 12px;
}
.gallery img {
  width: 100%;
  height: 200px;
  object-fit: cover;     /* prevents image distortion — crucial for galleries */
  border-radius: 8px;
}
```

## 7. Toggle switch (no JS library needed, pure CSS)
```html
<label class="switch">
  <input type="checkbox">
  <span class="slider"></span>
</label>
```
```css
.switch { position: relative; display: inline-block; width: 48px; height: 26px; }
.switch input { opacity: 0; width: 0; height: 0; }
.slider {
  position: absolute; inset: 0;
  background: #ccc; border-radius: 34px;
  transition: 0.3s;
  cursor: pointer;
}
.slider::before {
  content: "";
  position: absolute;
  height: 20px; width: 20px;
  left: 3px; bottom: 3px;
  background: white; border-radius: 50%;
  transition: 0.3s;
}
input:checked + .slider { background: var(--color-primary); }
input:checked + .slider::before { transform: translateX(22px); }
```

## 8. Custom scrollbar (used in dashboards/chat apps)
```css
::-webkit-scrollbar { width: 8px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 4px; }
::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
```

## 9. Truncate text with ellipsis (single & multi-line)
```css
/* single line */
.truncate {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
/* multi-line (e.g. card description limited to 2 lines) */
.truncate-2 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
```

## 10. Sticky footer (footer stays at bottom even with little content)
```css
body {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}
.main-content { flex: 1; }  /* pushes footer down */
```

## 11. Equal height cards in a row (flex)
```css
.row { display: flex; gap: 20px; align-items: stretch; }
.row .card { flex: 1; display: flex; flex-direction: column; }
.card .footer-actions { margin-top: auto; } /* pin button to bottom of card */
```

## 12. Dropdown menu
```css
.dropdown { position: relative; }
.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 0;
  background: white;
  box-shadow: 0 4px 12px rgba(0,0,0,0.15);
  border-radius: 8px;
  opacity: 0;
  visibility: hidden;
  transform: translateY(-8px);
  transition: all 0.2s ease;
}
.dropdown:hover .dropdown-menu,
.dropdown.open .dropdown-menu {
  opacity: 1;
  visibility: visible;
  transform: translateY(0);
}
```

---
**Quick revision checklist:**
- [ ] Could you build a button design system (primary/outline/disabled) from memory?
- [ ] Do you know the toggle switch trick (checkbox + sibling selector)?
- [ ] Can you make a card's footer stick to the bottom with `margin-top:auto`?
- [ ] Do you know `object-fit: cover` for gallery images?