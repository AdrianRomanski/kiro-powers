# Keyboard Navigation Guidance

## Overview
All functionality must be accessible via keyboard. Many users rely on keyboard navigation due to motor disabilities, preference, or efficiency.

## Core Requirements
1. **All interactive elements must be keyboard accessible**
2. **Focus must be visible** (never `outline: none` without replacement)
3. **Focus order must be logical** (follows visual/reading order)
4. **No keyboard traps** (users can always navigate away)

## Standard Keyboard Patterns

### Basic Navigation
- `Tab` - Move focus forward
- `Shift + Tab` - Move focus backward
- `Enter` - Activate buttons, links, submit forms
- `Space` - Activate buttons, toggle checkboxes
- `Escape` - Close dialogs, cancel operations, clear selections
- `Arrow keys` - Navigate within components (menus, tabs, radio groups)

### Component-Specific Patterns

#### Buttons
```jsx
// ✓ GOOD: Native button (keyboard support built-in)
<button onClick={handleClick}>Click me</button>

// ✓ GOOD: Custom button with keyboard support
<div 
  role="button"
  tabIndex={0}
  onClick={handleClick}
  onKeyDown={(e) => {
    if (e.key === 'Enter' || e.key === ' ') {
      e.preventDefault();
      handleClick();
    }
  }}
>
  Click me
</div>

// ✗ BAD: No keyboard support
<div onClick={handleClick}>Click me</div>
```

#### Menus
```jsx
// Arrow keys navigate, Enter/Space activate, Escape closes
const Menu = () => {
  const handleKeyDown = (e) => {
    switch(e.key) {
      case 'ArrowDown':
        // Focus next item
        break;
      case 'ArrowUp':
        // Focus previous item
        break;
      case 'Home':
        // Focus first item
        break;
      case 'End':
        // Focus last item
        break;
      case 'Escape':
        // Close menu
        break;
    }
  };
  
  return (
    <ul role="menu" onKeyDown={handleKeyDown}>
      <li role="menuitem" tabIndex={0}>Item 1</li>
      <li role="menuitem" tabIndex={-1}>Item 2</li>
    </ul>
  );
};
```

#### Tabs
```jsx
// Arrow keys navigate tabs, Tab moves to panel
const Tabs = () => {
  const handleKeyDown = (e) => {
    if (e.key === 'ArrowRight') {
      // Focus next tab
    } else if (e.key === 'ArrowLeft') {
      // Focus previous tab
    }
  };
  
  return (
    <div role="tablist" onKeyDown={handleKeyDown}>
      <button role="tab" aria-selected="true">Tab 1</button>
      <button role="tab" aria-selected="false">Tab 2</button>
    </div>
  );
};
```

#### Modal Dialogs
```jsx
// Focus trap: keep focus within modal
const Modal = ({ onClose }) => {
  const modalRef = useRef();
  
  useEffect(() => {
    const focusableElements = modalRef.current.querySelectorAll(
      'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
    );
    const firstElement = focusableElements[0];
    const lastElement = focusableElements[focusableElements.length - 1];
    
    firstElement?.focus();
    
    const handleKeyDown = (e) => {
      if (e.key === 'Escape') {
        onClose();
      }
      
      if (e.key === 'Tab') {
        if (e.shiftKey && document.activeElement === firstElement) {
          e.preventDefault();
          lastElement.focus();
        } else if (!e.shiftKey && document.activeElement === lastElement) {
          e.preventDefault();
          firstElement.focus();
        }
      }
    };
    
    document.addEventListener('keydown', handleKeyDown);
    return () => document.removeEventListener('keydown', handleKeyDown);
  }, [onClose]);
  
  return (
    <div role="dialog" aria-modal="true" ref={modalRef}>
      {/* Modal content */}
    </div>
  );
};
```

## Focus Management

### Focus Indicators
```css
/* ✗ BAD: Removing focus outline */
*:focus {
  outline: none;
}

/* ✓ GOOD: Custom focus indicator */
button:focus-visible {
  outline: 2px solid #0066cc;
  outline-offset: 2px;
}

/* ✓ BETTER: High contrast focus */
*:focus-visible {
  outline: 3px solid currentColor;
  outline-offset: 2px;
}
```

### Managing Focus Programmatically
```jsx
// Move focus after actions
const DeleteButton = () => {
  const handleDelete = () => {
    deleteItem();
    // Focus next logical element
    document.getElementById('next-item')?.focus();
  };
  
  return <button onClick={handleDelete}>Delete</button>;
};

// Restore focus after modal closes
const [isOpen, setIsOpen] = useState(false);
const triggerRef = useRef();

const openModal = () => {
  triggerRef.current = document.activeElement;
  setIsOpen(true);
};

const closeModal = () => {
  setIsOpen(false);
  triggerRef.current?.focus();
};
```

### Skip Links
```html
<!-- Allow keyboard users to skip repetitive content -->
<a href="#main-content" class="skip-link">
  Skip to main content
</a>

<style>
.skip-link {
  position: absolute;
  top: -40px;
  left: 0;
  background: #000;
  color: #fff;
  padding: 8px;
  z-index: 100;
}

.skip-link:focus {
  top: 0;
}
</style>
```

## TabIndex Guidelines

- `tabIndex="0"` - Element in natural tab order
- `tabIndex="-1"` - Programmatically focusable, not in tab order
- `tabIndex="1+"` - **Avoid!** Creates confusing tab order

```html
<!-- ✓ GOOD: Natural tab order -->
<button>First</button>
<button>Second</button>
<button>Third</button>

<!-- ✓ GOOD: Programmatic focus only -->
<div tabIndex="-1" ref={errorRef}>Error message</div>

<!-- ✗ BAD: Positive tabindex -->
<button tabIndex="3">Third</button>
<button tabIndex="1">First</button>
<button tabIndex="2">Second</button>
```

## Testing Checklist
- [ ] Unplug your mouse and navigate the entire interface
- [ ] Can you reach all interactive elements?
- [ ] Is focus always visible?
- [ ] Does tab order make sense?
- [ ] Can you activate all buttons/links with Enter/Space?
- [ ] Can you close modals with Escape?
- [ ] Can you navigate menus with arrow keys?
- [ ] Are there any keyboard traps?
