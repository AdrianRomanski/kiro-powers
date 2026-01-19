# ARIA Patterns Guidance

## Overview
ARIA (Accessible Rich Internet Applications) enhances accessibility when semantic HTML isn't enough. **First rule of ARIA: Don't use ARIA if you can use semantic HTML.**

## Five Rules of ARIA
1. **Don't use ARIA** if you can use native HTML
2. **Don't change native semantics** unless you really have to
3. **All interactive ARIA controls must be keyboard accessible**
4. **Don't use `role="presentation"` or `aria-hidden="true"` on focusable elements**
5. **All interactive elements must have an accessible name**

## Common ARIA Attributes

### Labels and Descriptions
```html
<!-- aria-label: Provides a label when none is visible -->
<button aria-label="Close dialog">×</button>

<!-- aria-labelledby: References visible label -->
<h2 id="dialog-title">Confirm Action</h2>
<div role="dialog" aria-labelledby="dialog-title">...</div>

<!-- aria-describedby: Additional description -->
<input 
  type="password" 
  aria-describedby="password-hint"
/>
<span id="password-hint">Must be at least 8 characters</span>
```

### States
```html
<!-- aria-expanded: For collapsible content -->
<button 
  aria-expanded="false" 
  aria-controls="menu"
>
  Menu
</button>

<!-- aria-pressed: For toggle buttons -->
<button aria-pressed="false">Mute</button>

<!-- aria-checked: For custom checkboxes -->
<div role="checkbox" aria-checked="false">...</div>

<!-- aria-selected: For tabs, options -->
<div role="tab" aria-selected="true">Tab 1</div>

<!-- aria-current: For current page/step -->
<a href="/about" aria-current="page">About</a>
```

### Live Regions
```html
<!-- Announce changes to screen readers -->
<div aria-live="polite">
  Items in cart: 3
</div>

<!-- Urgent announcements -->
<div aria-live="assertive" role="alert">
  Error: Form submission failed
</div>

<!-- Status messages -->
<div role="status" aria-live="polite">
  Saving...
</div>
```

### Hiding Content
```html
<!-- Hide decorative images -->
<img src="decorative.png" alt="" role="presentation" />

<!-- Hide from screen readers only -->
<span aria-hidden="true">★★★★★</span>
<span class="sr-only">4 out of 5 stars</span>

<!-- Visually hidden but available to screen readers -->
<style>
.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0,0,0,0);
  white-space: nowrap;
  border: 0;
}
</style>
```

## Common Widget Patterns

### Modal Dialog
```html
<div 
  role="dialog" 
  aria-modal="true"
  aria-labelledby="dialog-title"
>
  <h2 id="dialog-title">Confirm Delete</h2>
  <p>Are you sure?</p>
  <button>Cancel</button>
  <button>Delete</button>
</div>
```

### Tabs
```html
<div role="tablist" aria-label="Settings">
  <button role="tab" aria-selected="true" aria-controls="panel-1">
    General
  </button>
  <button role="tab" aria-selected="false" aria-controls="panel-2">
    Privacy
  </button>
</div>
<div role="tabpanel" id="panel-1">...</div>
<div role="tabpanel" id="panel-2" hidden>...</div>
```

### Accordion
```html
<div>
  <h3>
    <button 
      aria-expanded="false" 
      aria-controls="section-1"
    >
      Section 1
    </button>
  </h3>
  <div id="section-1" hidden>
    Content...
  </div>
</div>
```

### Combobox (Autocomplete)
```html
<label for="search">Search</label>
<input 
  id="search"
  type="text"
  role="combobox"
  aria-expanded="false"
  aria-controls="suggestions"
  aria-autocomplete="list"
/>
<ul id="suggestions" role="listbox">
  <li role="option">Result 1</li>
  <li role="option">Result 2</li>
</ul>
```

## Anti-Patterns to Avoid

```html
<!-- ✗ BAD: Redundant role -->
<button role="button">Click me</button>

<!-- ✗ BAD: Conflicting semantics -->
<h1 role="button">Not a heading</h1>

<!-- ✗ BAD: aria-label on div -->
<div aria-label="content">...</div>

<!-- ✗ BAD: Hidden but focusable -->
<button aria-hidden="true">Click</button>

<!-- ✗ BAD: Missing keyboard support -->
<div role="button" onclick="...">Click</div>
```

## Resources
- [ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/)
- [ARIA in HTML](https://www.w3.org/TR/html-aria/)
