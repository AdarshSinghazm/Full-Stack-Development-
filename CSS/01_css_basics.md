# 01 — CSS Basics (Foundations)

## How CSS connects to HTML
```html
<link rel="stylesheet" href="style.css">   <!-- best, use this in real projects -->
<style> p { color: red; } </style>          <!-- internal -->
<p style="color:red;">text</p>              <!-- inline, avoid except quick debugging -->
```
In a real project: always external CSS, one `main.css` or split into multiple files imported via `@import` or bundler (Vite/Webpack).

## Selectors (the foundation of everything)
```css
* { box-sizing: border-box; }     /* universal selector — used in EVERY project */
.card { }                          /* class — most used in real projects */
#header { }                        /* id — use sparingly, only for unique elements */
nav ul li { }                      /* descendant selector */
nav > ul { }                       /* direct child only */
button:hover { }                   /* pseudo-class */
input:focus { }
p::first-letter { }                /* pseudo-element */
a[target="_blank"] { }             /* attribute selector */
.btn, .link { }                    /* group selector — avoid repeating styles */
```

**Project tip:** Use classes for styling, IDs for JS hooks/anchors only. Never style by ID — it creates specificity wars later in big projects.

## Specificity (why your CSS doesn't apply — #1 real-world bug)
Order of power (low → high):
1. element selectors (`p`, `div`) — 0,0,1
2. classes, attributes, pseudo-classes (`.card`, `:hover`) — 0,1,0
3. IDs (`#header`) — 1,0,0
4. inline styles — wins almost always
5. `!important` — nuclear option, avoid in real projects (use only for utility overrides like `.hidden`)

**Real bug example:** `#nav .link { color: blue; }` will always beat `.link.active { color: red; }` even if `.active` is added later by JS — this is the #1 cause of "why isn't my class working" bugs.

## Box Model (everything in CSS layout depends on this)
```
margin | border | padding | content
```
```css
.box {
  width: 300px;
  padding: 20px;
  border: 2px solid #333;
  margin: 10px;
  box-sizing: border-box; /* width includes padding+border — ALWAYS use this in projects */
}
```
Without `box-sizing: border-box`, padding/border ADD to width, breaking layouts. So every project starts with:
```css
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
```

## Units — which to use when (project decision, not theory)
| Unit | Use case |
|---|---|
| `px` | borders, shadows, things that shouldn't scale |
| `rem` | font-size, spacing — scales with root font, accessibility-friendly |
| `em` | spacing relative to parent's font (careful, compounds) |
| `%` | widths inside flexible containers |
| `vw` / `vh` | full-screen sections, hero banners |
| `fr` | grid track sizing |

**Project rule of thumb:** font-size & spacing → `rem`, layout widths → `%`/`fr`, fixed details (border, radius) → `px`.

## Colors
```css
color: #1e293b;              /* hex — most common */
color: rgb(30 41 59);        /* modern syntax, no commas needed */
color: rgba(30,41,59,0.6);   /* with opacity */
color: hsl(222 47% 11%);     /* great for theming — easy to tweak lightness */
```
**Project tip:** Define a color palette as CSS variables (see file 04) instead of repeating hex codes everywhere — saves you when client says "make the blue a bit darker."

## Typography basics used in every project
```css
body {
  font-family: 'Inter', system-ui, sans-serif; /* always have a fallback stack */
  line-height: 1.6;     /* readability — never leave default */
  font-size: 16px;       /* base size, rem multiplies from this */
}
h1 { font-weight: 700; letter-spacing: -0.02em; } /* tight tracking on big headings */
p { max-width: 65ch; }   /* keeps paragraphs readable — real typography trick */
```

## Display property (basis for all layout)
```css
display: block;    /* div, p, section — full width, stacks */
display: inline;   /* span, a — no width/height control */
display: inline-block; /* mix of both */
display: none;     /* removes from layout entirely (vs visibility:hidden which keeps space) */
display: flex;      /* → see file 02 */
display: grid;       /* → see file 02 */
```

## `visibility` vs `display` vs `opacity` (common interview + bug topic)
- `display:none` → removed from layout, no space taken, not accessible
- `visibility:hidden` → invisible but still takes up space
- `opacity:0` → invisible, takes space, still clickable/focusable (careful — accessibility bug)

---
**Quick revision checklist for this file:**
- [ ] Can you explain specificity order without looking?
- [ ] Do you know why `box-sizing:border-box` is in every project reset?
- [ ] Can you pick the right unit for font vs layout vs border?
- [ ] Difference between display:none, visibility:hidden, opacity:0?