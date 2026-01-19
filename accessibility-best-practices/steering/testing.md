# Accessibility Testing Guidance

## Overview
Testing is essential to ensure accessibility. Combine automated tools, manual testing, and user testing.

## Automated Testing

### Browser Extensions
- **axe DevTools**: Comprehensive automated testing
- **WAVE**: Visual feedback on accessibility issues
- **Lighthouse**: Built into Chrome DevTools
- **IBM Equal Access**: Detailed WCAG compliance

### Testing Libraries
```javascript
// Jest + jest-axe
import { axe, toHaveNoViolations } from 'jest-axe';
expect.extend(toHaveNoViolations);

test('should have no accessibility violations', async () => {
  const { container } = render(<MyComponent />);
  const results = await axe(container);
  expect(results).toHaveNoViolations();
});

// Cypress + cypress-axe
cy.injectAxe();
cy.checkA11y();
```

## Manual Testing

### Keyboard Testing
1. Unplug your mouse
2. Navigate with Tab/Shift+Tab
3. Activate with Enter/Space
4. Check focus visibility
5. Verify no keyboard traps

### Screen Reader Testing
- **macOS**: VoiceOver (Cmd+F5)
- **Windows**: NVDA (free), JAWS
- **Mobile**: TalkBack (Android), VoiceOver (iOS)

### Visual Testing
- Zoom to 200%
- Test with color blindness simulators
- Check contrast ratios
- Test in dark mode

## Testing Checklist
- [ ] All images have alt text
- [ ] All form inputs have labels
- [ ] Heading hierarchy is logical
- [ ] Color contrast meets WCAG AA
- [ ] Keyboard navigation works
- [ ] Focus indicators are visible
- [ ] Screen reader announces content correctly
- [ ] No keyboard traps
- [ ] Error messages are clear
- [ ] Content works at 200% zoom
