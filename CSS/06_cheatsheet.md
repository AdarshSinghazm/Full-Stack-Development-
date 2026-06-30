# 06 — Cheatsheet, Gotchas & Best Practices (Final Revision Sheet)

## Common bugs you WILL hit in real projects (and the fix)

| Bug | Cause | Fix |
|---|---|---|
| Element wider than expected | padding/border adding to width | `box-sizing: border-box` |
| `position:absolute` child in wrong spot | no positioned ancestor | add `position: relative` to parent |
| Margin collapsing between two stacked elements | adjacent vertical margins merge | use padding, or `display:flex` on parent with `gap` |
| `z-index` not working | element has no `position` set | add `position: relative/absolute/fixed` |
| Image has weird gap below it | images are `inline` by default | `display: block` on img |
| Flex items not wrapping | missing `flex-wrap: wrap` | add it explicitly |
| `height: 100%` not working on child | parent has no defined height | set height up the whole parent chain, or use `vh`/flex |
| Hover effects feel janky | animating `width`/`top`/`left` | animate `transform`/`opacity` instead |
| Text overflowing container | no `max-width` or `overflow` handling | `max-width: 65ch` / `overflow-wrap: break-word` |
| `!important` everywhere | specificity wars from ID selectors | style with classes only, keep specificity flat |

## Specificity quick formula
```
inline style        > 1,0,0,0
#id                  > 0,1,0,0
.class/[attr]/:hover > 0,0,1,0
element/::pseudo     > 0,0,0,1
```
Compare left to right — higher first number always wins regardless of how many of the lower ones you stack.

## CSS units cheat
```
rem   → font-size, spacing (scales with root, accessible)
em    → relative to parent font (compounds — use carefully)
%     → relative to parent
vw/vh → relative to viewport
fr    → grid track sizing
ch    → text width (readable paragraph widths)
```

## Flexbox cheat
```css
justify-content: flex-start | center | flex-end | space-between | space-around | space-evenly;
align-items:     flex-start | center | flex-end | stretch | baseline;
flex-direction:  row | column | row-reverse | column-reverse;
flex: 1;          /* grow=1, shrink=1, basis=0 → equal width items */
```

## Grid cheat
```css
grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));  /* responsive grid, no media queries */
grid-template-columns: 1fr 2fr;                                 /* sidebar + main */
place-items: center;                                              /* shorthand: justify+align items center */
```

## Selectors priority order to remember when debugging "why isn't my style applying"
1. Check if a more specific selector elsewhere overrides it (inspect element → computed tab)
2. Check load order — later CSS file wins if specificity is equal
3. Check for `!important` somewhere up the chain
4. Check if it's inline style overriding your class

## Best practices for real projects
- **Mobile-first**: write base styles for mobile, scale up with `min-width` media queries.
- **BEM naming** (Block Element Modifier) for class names in larger projects:
  ```css
  .card { }
  .card__title { }
  .card__title--highlighted { }
  ```
  Keeps specificity flat and class names self-documenting.
- **Use CSS variables** for colors/spacing — never hardcode hex codes repeatedly.
- **Avoid IDs for styling** — use them only for JS hooks/anchors.
- **Keep specificity low** — prefer classes everywhere, avoid nesting selectors too deep (`div > ul > li > a` is fragile).
- **Component-based CSS** — one file/section per component (button, card, navbar) rather than one giant file.
- **Use `gap` instead of margin hacks** in flex/grid layouts — cleaner and avoids the "last child has extra margin" bug.
- **Logical properties** for better internationalization: `margin-inline`, `padding-block` instead of left/right/top/bottom (auto-adjusts for RTL languages).

## Useful shorthand reference
```css
margin: 10px 20px;            /* top/bottom 10px, left/right 20px */
margin: 10px 20px 30px 40px;  /* top right bottom left (clockwise) */
border: 1px solid #333;        /* width style color */
background: url(bg.png) no-repeat center/cover;
font: italic bold 16px/1.5 Arial, sans-serif; /* style weight size/line-height family */
inset: 0;                       /* top/right/bottom/left all 0 */
```

## Accessibility quick wins (often forgotten, asked in real interviews)
```css
:focus-visible { outline: 2px solid var(--color-primary); outline-offset: 2px; }
.sr-only {
  position: absolute;
  width: 1px; height: 1px;
  overflow: hidden;
  clip: rect(0,0,0,0);
  white-space: nowrap;
} /* visually hide but keep for screen readers */
```

---
## Full Revision Map (order to revise all 6 files)
1. **01-css-basics.md** → selectors, specificity, box model, units
2. **02-flexbox-grid.md** → flex vs grid, real layout patterns
3. **03-positioning-responsive.md** → position, z-index, media queries, responsive tricks
4. **04-css-advanced.md** → variables, transitions, animations, gradients, shadows
5. **05-project-patterns.md** → copy-paste real components (buttons, cards, forms, toggles)
6. **06-cheatsheet-best-practices.md** (this file) → bugs, gotchas, shorthand, accessibility

**Before any interview/project, just re-read this file (06) — it's the compressed version of everything in 01-05.**