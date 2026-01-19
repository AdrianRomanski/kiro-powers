# Visual Accessibility Guidance

## Overview
Visual accessibility ensures content is perceivable by users with various visual abilities, including low vision, color blindness, and blindness.

## Color and Contrast

### Contrast Ratios (WCAG 2.1)
- **Normal text**: 4.5:1 minimum (AA), 7:1 enhanced (AAA)
- **Large text** (18pt+ or 14pt+ bold): 3:1 minimum (AA), 4.5:1 enhanced (AAA)
- **UI components and graphics**: 3:1 minimum (AA)

```css
/* ✓ GOOD: High contrast */
.button {
  background: #0066cc;
  color: #ffffff; /* 4.54:1 ratio */
}

/* ✗ BAD: Low contrast */
.button {
  background: #cccccc;
  color: #ffffff; /* 1.6:1 ratio - fails */
}

/* ✓ GOOD: Focus indicator contrast */
button:focus-visible {
  outline: 2px solid #000000;
  outline-offset: 2px;
}
```

### Color Independence
Never rely on color alone to convey information.

```html
<!-- ✗ BAD: Color only -->
<span style="color: red;">Error</span>
<span style="color: green;">Success</span>

<!-- ✓ GOOD: Color + icon + text -->
<span class="error">
  <svg aria-hidden="true"><!-- error icon --></svg>
  Error: Invalid input
</span>
<span class="success">
  <svg aria-hidden="true"><!-- check icon --></svg>
  Success: Saved
</span>

<!-- ✓ GOOD: Color + pattern -->
<div class="chart">
  <div class="bar bar-striped" style="background: red;">Q1</div>
  <div class="bar bar-dotted" style="background: blue;">Q2</div>
</div>
```

### Testing for Color Blindness
- Test with color blindness simulators
- Common types: Protanopia (red), Deuteranopia (green), Tritanopia (blue)
- Use tools like Chrome DevTools or Stark plugin

## Text and Typography

### Font Size
```css
/* ✓ GOOD: Relative units */
body {
  font-size: 16px; /* Base size */
}

h1 {
  font-size: 2rem; /* 32px, scales with user preferences */
}

p {
  font-size: 1rem; /* 16px */
}

/* ✗ BAD: Fixed small sizes */
.small-text {
  font-size: 10px; /* Too small, doesn't scale */
}
```

### Line Height and Spacing
```css
/* ✓ GOOD: Readable spacing */
p {
  line-height: 1.5; /* WCAG recommends 1.5 minimum */
  margin-bottom: 1em;
}

/* Paragraph spacing */
p + p {
  margin-top: 1em;
}

/* Letter spacing for readability */
.heading {
  letter-spacing: 0.05em;
}
```

### Text Resize
Content must be readable when text is resized up to 200%.

```css
/* ✓ GOOD: Flexible containers */
.container {
  max-width: 100%;
  overflow-wrap: break-word;
}

/* ✗ BAD: Fixed heights that clip text */
.box {
  height: 50px;
  overflow: hidden;
}
```

## Images and Media

### Alternative Text
```html
<!-- ✓ GOOD: Descriptive alt text -->
<img src="chart.png" alt="Bar chart showing 50% increase in sales from Q1 to Q2" />

<!-- ✓ GOOD: Decorative image -->
<img src="decorative-border.png" alt="" />

<!-- ✓ GOOD: Complex image with long description -->
<img 
  src="infographic.png" 
  alt="2024 Climate Report Summary"
  aria-describedby="infographic-desc"
/>
<div id="infographic-desc">
  Detailed description of the infographic data...
</div>

<!-- ✗ BAD: Generic alt text -->
<img src="chart.png" alt="image" />

<!-- ✗ BAD: Missing alt -->
<img src="photo.jpg" />
```

### Icons
```html
<!-- ✓ GOOD: Icon with text -->
<button>
  <svg aria-hidden="true"><!-- icon --></svg>
  Delete
</button>

<!-- ✓ GOOD: Icon-only with label -->
<button aria-label="Delete">
  <svg aria-hidden="true"><!-- icon --></svg>
</button>

<!-- ✗ BAD: Icon without label -->
<button>
  <svg><!-- icon --></svg>
</button>
```

### Video and Audio
```html
<!-- ✓ GOOD: Video with captions and transcript -->
<video controls>
  <source src="video.mp4" type="video/mp4" />
  <track kind="captions" src="captions.vtt" srclang="en" label="English" />
</video>
<details>
  <summary>Transcript</summary>
  <p>Full text transcript...</p>
</details>

<!-- ✓ GOOD: Audio with transcript -->
<audio controls>
  <source src="podcast.mp3" type="audio/mpeg" />
</audio>
<a href="transcript.html">Read transcript</a>
```

## Responsive and Zoom

### Viewport Settings
```html
<!-- ✓ GOOD: Allow zoom -->
<meta name="viewport" content="width=device-width, initial-scale=1" />

<!-- ✗ BAD: Prevent zoom -->
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
```

### Responsive Design
```css
/* ✓ GOOD: Flexible layouts */
.container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
}

/* ✓ GOOD: Responsive text */
@media (max-width: 768px) {
  body {
    font-size: 14px;
  }
}

/* Touch targets on mobile */
@media (max-width: 768px) {
  button {
    min-height: 44px;
    min-width: 44px;
  }
}
```

## Motion and Animation

### Respect User Preferences
```css
/* ✓ GOOD: Respect reduced motion preference */
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}

/* ✓ GOOD: Subtle animations */
.button {
  transition: background-color 0.2s ease;
}

/* ✗ BAD: Excessive animation */
.flashy {
  animation: spin 0.5s infinite, flash 0.3s infinite;
}
```

### Avoid Seizure Triggers
- No flashing more than 3 times per second
- Avoid large flashing areas
- Provide warnings for flashing content

```html
<!-- ✓ GOOD: Warning for flashing content -->
<div role="alert">
  Warning: The following video contains flashing lights
</div>
<video controls>...</video>
```

## Dark Mode
```css
/* ✓ GOOD: Support dark mode */
@media (prefers-color-scheme: dark) {
  body {
    background: #1a1a1a;
    color: #ffffff;
  }
  
  a {
    color: #66b3ff;
  }
  
  /* Maintain contrast ratios */
  .button {
    background: #0066cc;
    color: #ffffff;
  }
}
```

## Testing Tools
- **Contrast checkers**: WebAIM Contrast Checker, Stark
- **Color blindness simulators**: Chrome DevTools, Colorblind Web Page Filter
- **Screen magnifiers**: Built-in OS zoom, ZoomText
- **Browser zoom**: Test at 200% zoom minimum
