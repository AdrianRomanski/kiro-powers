# Forms Accessibility Guidance

## Overview
Forms are critical interaction points. Accessible forms ensure all users can input data, understand requirements, and correct errors.

## Labels

### Always Use Labels
```html
<!-- ✓ GOOD: Explicit label -->
<label for="email">Email Address</label>
<input type="email" id="email" name="email" />

<!-- ✓ GOOD: Implicit label -->
<label>
  Email Address
  <input type="email" name="email" />
</label>

<!-- ✗ BAD: Placeholder as label -->
<input type="email" placeholder="Email Address" />

<!-- ✗ BAD: No label -->
<input type="email" name="email" />
```

### Multiple Inputs
```html
<!-- ✓ GOOD: Fieldset for grouped inputs -->
<fieldset>
  <legend>Contact Information</legend>
  <label for="phone">Phone</label>
  <input type="tel" id="phone" />
  <label for="email">Email</label>
  <input type="email" id="email" />
</fieldset>
```

## Required Fields

```html
<!-- ✓ GOOD: Required attribute + visual indicator -->
<label for="name">
  Name <span aria-label="required">*</span>
</label>
<input type="text" id="name" required />

<!-- ✓ GOOD: aria-required -->
<label for="email">Email</label>
<input type="email" id="email" aria-required="true" />
```

## Error Handling

```html
<!-- ✓ GOOD: Error message linked to input -->
<label for="password">Password</label>
<input 
  type="password" 
  id="password"
  aria-invalid="true"
  aria-describedby="password-error"
/>
<span id="password-error" role="alert">
  Password must be at least 8 characters
</span>

<!-- ✓ GOOD: Form-level errors -->
<div role="alert" aria-live="assertive">
  <h2>Form contains 2 errors</h2>
  <ul>
    <li><a href="#email">Email is required</a></li>
    <li><a href="#password">Password is too short</a></li>
  </ul>
</div>
```

## Input Types
Use appropriate input types for better mobile experience and validation.

```html
<input type="email" />
<input type="tel" />
<input type="url" />
<input type="number" />
<input type="date" />
<input type="search" />
```

## Autocomplete
```html
<!-- ✓ GOOD: Autocomplete attributes -->
<input type="text" name="name" autocomplete="name" />
<input type="email" name="email" autocomplete="email" />
<input type="tel" name="phone" autocomplete="tel" />
```
