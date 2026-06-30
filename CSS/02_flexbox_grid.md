# 02 — Flexbox & Grid (Layout — used in 90% of real UI)

## Flexbox — for ONE-dimensional layout (row OR column)
Real use cases: navbars, button groups, card content alignment, centering.

```css
.container {
  display: flex;
  flex-direction: row;       /* row (default) | column | row-reverse */
  justify-content: space-between; /* main axis alignment */
  align-items: center;            /* cross axis alignment */
  gap: 16px;                       /* modern way — no more margin hacks */
  flex-wrap: wrap;                 /* lets items wrap on small screens */
}
```

### Real Project: Navbar with flexbox
```html
<nav class="navbar">
  <div class="logo">Brand</div>
  <ul class="nav-links">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```
```css
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1rem 2rem;
}
.nav-links {
  display: flex;
  gap: 2rem;
  list-style: none;
}
```
This exact pattern is in literally every website you've ever visited.

### Centering anything (the classic interview question)
```css
.center {
  display: flex;
  justify-content: center;  /* horizontal */
  align-items: center;      /* vertical */
  height: 100vh;
}
```

### Flex item properties (control individual children)
```css
.item {
  flex: 1;            /* grow & shrink equally — common for equal-width columns */
  flex-grow: 1;        /* take available space */
  flex-shrink: 0;       /* don't shrink (e.g. icons) */
  flex-basis: 200px;    /* starting size before grow/shrink */
}
```
**Project trick:** `flex: 1` on cards in a row makes them equal width automatically — no need to calculate percentages.

---

## CSS Grid — for TWO-dimensional layout (rows AND columns)
Real use cases: page layouts, dashboards, image galleries, card grids.

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);  /* 3 equal columns */
  grid-template-rows: auto 1fr auto;       /* header, content, footer */
  gap: 20px;
}
```

### Real Project: Responsive card grid (auto-fit — the most useful grid trick)
```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 24px;
}
```
This single line makes a fully responsive grid with ZERO media queries — cards reflow automatically based on available width. This is used constantly in real dashboards/e-commerce grids.

### Real Project: Holy Grail page layout
```css
.page {
  display: grid;
  grid-template-columns: 220px 1fr 220px;
  grid-template-rows: 60px 1fr 60px;
  grid-template-areas:
    "header header header"
    "sidebar main aside"
    "footer footer footer";
  min-height: 100vh;
}
.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main    { grid-area: main; }
.aside   { grid-area: aside; }
.footer  { grid-area: footer; }
```
`grid-template-areas` is the most readable way to build full-page layouts — used in admin panels/dashboards.

### Placing a single item precisely
```css
.featured {
  grid-column: 1 / 3;  /* span from line 1 to line 3 (2 columns wide) */
  grid-row: 1 / 2;
}
```

## Flexbox vs Grid — which to pick (real decision you'll make every project)
| Situation | Use |
|---|---|
| Navbar, button group, single row/column | Flexbox |
| Whole page layout, dashboard, gallery | Grid |
| Content needs to align in both directions | Grid |
| Don't know item count in advance, just want them to flow | Flexbox + wrap, or Grid auto-fit |

**Reality:** Most projects use BOTH — Grid for the page skeleton, Flexbox inside individual components (like inside a card or navbar).

---
**Quick revision checklist:**
- [ ] Can you build a navbar from memory with flex?
- [ ] Can you write the auto-fit responsive grid line from memory?
- [ ] Do you know grid-template-areas syntax?
- [ ] Can you explain when to use flex vs grid in an interview?