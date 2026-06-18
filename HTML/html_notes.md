# HTML Notes

---

## 1. Basic Structure

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Page Title</title>
  </head>
  <body>
    <!-- content here -->
  </body>
</html>
```

---

## 2. Headings & Paragraph

```html
<h1>Main Heading</h1>   <!-- use only once per page -->
<h2>Sub Heading</h2>
<h3>Sub-sub Heading</h3>

<p>This is a paragraph.</p>
<br>  <!-- line break -->
<hr>  <!-- horizontal line -->
```

---

## 3. Text Formatting

```html
<b>Bold</b>             <!-- visual bold -->
<strong>Important</strong>  <!-- semantic bold -->
<i>Italic</i>
<em>Emphasis</em>
<u>Underline</u>
<s>Strikethrough</s>
<mark>Highlighted</mark>
<sup>superscript</sup>   <!-- x² -->
<sub>subscript</sub>     <!-- H₂O -->
<code>inline code</code>
<pre>preformatted text</pre>
```

---

## 4. Links

```html
<a href="https://google.com">External Link</a>
<a href="about.html">Internal Page</a>
<a href="#section">Same Page Jump</a>
<a href="mailto:you@email.com">Email</a>
<a href="file.pdf" download>Download</a>

<!-- Open in new tab -->
<a href="https://google.com" target="_blank" rel="noopener noreferrer">New Tab</a>
```

---

## 5. Images

```html
<img src="photo.jpg" alt="description" width="300" height="200">

<!-- alt is required (accessibility + SEO) -->
<!-- for decorative images: alt="" -->
```

---

## 6. Lists

```html
<!-- Unordered -->
<ul>
  <li>HTML</li>
  <li>CSS</li>
</ul>

<!-- Ordered -->
<ol>
  <li>Step 1</li>
  <li>Step 2</li>
</ol>

<!-- Nested -->
<ul>
  <li>Frontend
    <ul>
      <li>HTML</li>
      <li>CSS</li>
    </ul>
  </li>
</ul>
```

---

## 7. Tables

```html
<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Marks</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Adarsh</td>
      <td>95</td>
    </tr>
  </tbody>
</table>

<!-- Merge columns -->
<td colspan="2">spans 2 cols</td>

<!-- Merge rows -->
<td rowspan="2">spans 2 rows</td>
```

---

## 8. Forms

```html
<form action="/submit" method="POST">

  <!-- Text inputs -->
  <input type="text"     placeholder="Name">
  <input type="email"    placeholder="Email">
  <input type="password" placeholder="Password">
  <input type="number"   min="0" max="100">
  <input type="date">
  <input type="file">

  <!-- Label (always link with id) -->
  <label for="name">Name:</label>
  <input type="text" id="name" name="name">

  <!-- Textarea -->
  <textarea rows="5" placeholder="Message..."></textarea>

  <!-- Dropdown -->
  <select name="city">
    <option value="">Choose city</option>
    <option value="lko">Lucknow</option>
    <option value="del" selected>Delhi</option>
  </select>

  <!-- Radio (same name = one choice) -->
  <input type="radio" name="gender" value="male"> Male
  <input type="radio" name="gender" value="female"> Female

  <!-- Checkbox -->
  <input type="checkbox" name="agree"> I agree

  <!-- Buttons -->
  <button type="submit">Submit</button>
  <button type="reset">Reset</button>
  <button type="button" onclick="doSomething()">Click</button>

</form>
```

### Common Input Attributes

| Attribute     | Use                        |
|---------------|----------------------------|
| `placeholder` | Hint text inside input     |
| `required`    | Can't submit if empty      |
| `disabled`    | Greyed out, not sent       |
| `readonly`    | Visible but not editable   |
| `maxlength`   | Max characters allowed     |
| `value`       | Pre-filled value           |
| `name`        | Key sent to server         |

---

## 9. Semantic Elements

```html
<header>   <!-- top of page -->
<nav>      <!-- navigation links -->
<main>     <!-- main content (1 per page) -->
<section>  <!-- thematic group -->
<article>  <!-- self-contained (blog post, card) -->
<aside>    <!-- sidebar -->
<footer>   <!-- bottom of page -->

<figure>
  <img src="chart.png" alt="chart">
  <figcaption>Chart caption</figcaption>
</figure>

<details>
  <summary>Click to expand</summary>
  <p>Hidden content here</p>
</details>
```

> Use these instead of just `<div>` everywhere — better for SEO + accessibility.

---

## 10. Head Tags (Important)

```html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Page description for SEO">
  <title>Page Title</title>

  <!-- Link CSS -->
  <link rel="stylesheet" href="style.css">

  <!-- Favicon -->
  <link rel="icon" href="favicon.ico">

  <!-- JS (defer = runs after HTML loads) -->
  <script src="app.js" defer></script>
</head>
```

---

## 11. Div & Span

```html
<!-- div = block container (for layout) -->
<div class="card">
  <h2>Title</h2>
  <p>Content</p>
</div>

<!-- span = inline container (for styling text) -->
<p>My name is <span style="color:red">Adarsh</span></p>
```

---

## 12. Audio & Video

```html
<video src="video.mp4" controls width="600"></video>

<audio src="music.mp3" controls></audio>

<!-- Useful attributes: autoplay muted loop poster -->
<video src="clip.mp4" controls autoplay muted loop></video>
```

---

## 13. Iframe

```html
<!-- Embed YouTube -->
<iframe width="560" height="315"
  src="https://www.youtube.com/embed/VIDEO_ID"
  allowfullscreen>
</iframe>
```

---

## 14. Special Characters

| Character | Code     |
|-----------|----------|
| `<`       | `&lt;`   |
| `>`       | `&gt;`   |
| `&`       | `&amp;`  |
| `©`       | `&copy;` |
| ` ` (space) | `&nbsp;` |

---

## 15. Global Attributes (Used Everywhere)

```html
id="unique"           <!-- unique identifier, used in CSS/JS -->
class="name"          <!-- for CSS styling -->
style="color:red"     <!-- inline CSS (avoid overusing) -->
title="tooltip text"  <!-- hover tooltip -->
hidden                <!-- hides element -->
data-id="42"          <!-- custom data, access via JS dataset -->
```

---

## Block vs Inline (Quick Reminder)

| Block | Inline |
|-------|--------|
| Starts on new line | Flows in text |
| `div, p, h1-h6, ul, table, form` | `span, a, img, b, i, code` |