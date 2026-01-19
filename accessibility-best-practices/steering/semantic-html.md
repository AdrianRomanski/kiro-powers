# Semantic HTML Guidance

## Overview
Semantic HTML is the foundation of accessibility. Use the right element for the job before reaching for ARIA.

## Core Principles
1. **Use native HTML elements** - They have built-in accessibility features
2. **Avoid div/span soup** - Replace with semantic alternatives
3. **Maintain document structure** - Proper heading hierarchy, landmarks

## Common Patterns

### Headings
```html
<!-- ✓ GOOD: Logical hierarchy -->
<h1>Page Title</h1>
  <h2>Section</h2>
    <h3>Subsection</h3>
  <h2>Another Section</h2>

<!-- ✗ BAD: Skipping levels -->
<h1>Page Title</h1>
  <h3>Section</h3>
```

### Landmarks
```html
<!-- ✓ GOOD: Semantic landmarks -->
<header>
  <nav aria-label="Main navigation">...</nav>
</header>
<main>
  <article>...</article>
  <aside>...</aside>
</main>
<footer>...</footer>

<!-- ✗ BAD: Generic divs -->
<div class="header">
  <div class="nav">...</div>
</div>
```

### Buttons vs Links
```html
<!-- ✓ GOOD: Button for actions -->
<button onClick={handleSubmit}>Submit</button>

<!-- ✓ GOOD: Link for navigation -->
<a href="/about">About Us</a>

<!-- ✗ BAD: Div as button -->
<div onClick={handleSubmit}>Submit</div>

<!-- ✗ BAD: Link for actions -->
<a href="#" onClick={handleSubmit}>Submit</a>
```

### Lists
```html
<!-- ✓ GOOD: Semantic lists -->
<ul>
  <li>Item 1</li>
  <li>Item 2</li>
</ul>

<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/about">About</a></li>
  </ul>
</nav>

<!-- ✗ BAD: Div lists -->
<div class="list">
  <div class="item">Item 1</div>
  <div class="item">Item 2</div>
</div>
```

## Element Selection Guide

| Purpose | Use | Not |
|---------|-----|-----|
| Navigation | `<nav>` | `<div class="nav">` |
| Button/Action | `<button>` | `<div onclick>`, `<a href="#">` |
| Link/Navigation | `<a href>` | `<button>`, `<div onclick>` |
| Form input | `<input>`, `<select>`, `<textarea>` | `<div contenteditable>` |
| Table data | `<table>`, `<th>`, `<td>` | CSS grid with divs |
| Main content | `<main>` | `<div id="main">` |
| Article/Post | `<article>` | `<div class="post">` |
| Sidebar | `<aside>` | `<div class="sidebar">` |

## Testing
- Use browser dev tools to inspect semantic structure
- Navigate with keyboard only - does it make sense?
- Use screen reader to verify element announcements
