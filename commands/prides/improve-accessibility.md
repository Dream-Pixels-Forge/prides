---
description: Improve accessibility to meet WCAG 2.1 AA standards. Use {{args}} to specify focus area (keyboard, screen-reader, color, forms, all).
---

# Accessibility Improvement

**Accessibility Focus:** {{args}}

## Instructions

Execute comprehensive accessibility audit and improvements to meet WCAG 2.1 AA standards.

### Accessibility Categories

| Category | Focus | WCAG Criteria |
|----------|-------|---------------|
| **Keyboard** | Keyboard navigation, focus management | 2.1, 2.4.3, 2.4.7 |
| **Screen Reader** | ARIA, semantic HTML, alt text | 1.1.1, 1.3.1, 4.1.2 |
| **Color & Visual** | Color contrast, visual indicators | 1.4.3, 1.4.1, 1.4.11 |
| **Forms** | Labels, error messages, validation | 1.3.1, 3.3.1, 3.3.3 |
| **All** | Complete accessibility audit | All AA criteria |

### Phase 1: Accessibility Audit

1. @accessibility-sagent: Initial audit
   - Run automated accessibility tests
   - Generate accessibility report
   - Identify violations by severity
   - Establish baseline score

2. **Tools Used**
   - axe-core
   - Lighthouse Accessibility
   - WAVE
   - Pa11y
   - Accessibility Insights

### Phase 2: WCAG 2.1 AA Analysis

#### Perceivable (Principle 1)

| Criteria | Requirement | Status |
|----------|-------------|--------|
| **1.1.1 Non-text Content** | Alt text for images | 🔴🟡🟢 |
| **1.2.1 Audio-only/Video-only** | Alternatives for media | 🔴🟡🟢 |
| **1.3.1 Info and Relationships** | Semantic structure | 🔴🟡🟢 |
| **1.3.2 Meaningful Sequence** | Correct reading order | 🔴🟡🟢 |
| **1.4.1 Use of Color** | Color not only means | 🔴🟡🟢 |
| **1.4.3 Contrast (Minimum)** | 4.5:1 normal, 3:1 large | 🔴🟡🟢 |
| **1.4.4 Resize Text** | Up to 200% without loss | 🔴🟡🟢 |
| **1.4.5 Images of Text** | Use text instead of images | 🔴🟡🟢 |
| **1.4.10 Reflow** | No horizontal scroll | 🔴🟡🟢 |
| **1.4.11 Non-text Contrast** | 3:1 for UI components | 🔴🟡🟢 |

#### Operable (Principle 2)

| Criteria | Requirement | Status |
|----------|-------------|--------|
| **2.1.1 Keyboard** | All functions keyboard accessible | 🔴🟡🟢 |
| **2.1.2 No Keyboard Trap** | Can navigate away | 🔴🟡🟢 |
| **2.4.1 Bypass Blocks** | Skip links | 🔴🟡🟢 |
| **2.4.2 Page Titled** | Descriptive page titles | 🔴🟡🟢 |
| **2.4.3 Focus Order** | Logical focus order | 🔴🟡🟢 |
| **2.4.4 Link Purpose** | Descriptive link text | 🔴🟡🟢 |
| **2.4.6 Headings/Labels** | Descriptive headings | 🔴🟡🟢 |
| **2.4.7 Focus Visible** | Visible focus indicator | 🔴🟡🟢 |
| **2.5.1 Pointer Gestures** | Single pointer operation | 🔴🟡🟢 |
| **2.5.2 Pointer Cancellation** | No down-path activation | 🔴🟡🟢 |

#### Understandable (Principle 3)

| Criteria | Requirement | Status |
|----------|-------------|--------|
| **3.1.1 Language of Page** | Page language declared | 🔴🟡🟢 |
| **3.1.2 Language of Parts** | Language of parts marked | 🔴🟡🟢 |
| **3.2.1 On Focus** | No context change on focus | 🔴🟡🟢 |
| **3.2.2 On Input** | No context change on input | 🔴🟡🟢 |
| **3.3.1 Error Identification** | Error description | 🔴🟡🟢 |
| **3.3.2 Labels/Instructions** | Form labels | 🔴🟡🟢 |
| **3.3.3 Error Suggestion** | Error correction suggestions | 🔴🟡🟢 |
| **3.3.4 Error Prevention** | Confirmation for important actions | 🔴🟡🟢 |

#### Robust (Principle 4)

| Criteria | Requirement | Status |
|----------|-------------|--------|
| **4.1.1 Parsing** | Valid HTML | 🔴🟡🟢 |
| **4.1.2 Name, Role, Value** | Proper ARIA usage | 🔴🟡🟢 |
| **4.1.3 Status Messages** | Announce status changes | 🔴🟡🟢 |

### Phase 3: Remediation

#### Keyboard Accessibility
- Implement keyboard navigation
- Add focus management
- Create skip links
- Fix focus traps
- Add visible focus indicators

#### Screen Reader Support
- Add semantic HTML
- Implement ARIA labels
- Add alt text to images
- Create live regions
- Fix heading hierarchy

#### Color & Visual
- Fix color contrast
- Add non-color indicators
- Ensure text resize support
- Add focus visible styles
- Implement reduced motion

#### Forms Accessibility
- Add proper labels
- Implement error handling
- Add required field indicators
- Create accessible validation
- Fix form structure

### Phase 4: Validation

1. @accessibility-sagent: Re-run audit
   - Verify fixes
   - Check for new issues
   - Validate WCAG compliance

### Accessibility Checklist

- [ ] All images have alt text
- [ ] Proper heading hierarchy (h1-h6)
- [ ] Keyboard navigation works
- [ ] Focus indicators visible
- [ ] Color contrast meets 4.5:1
- [ ] Forms have labels
- [ ] Error messages descriptive
- [ ] ARIA used correctly
- [ ] Skip links present
- [ ] Language declared
- [ ] No keyboard traps
- [ ] Links descriptive
- [ ] Tables have headers
- [ ] Videos have captions
- [ ] Interactive elements accessible

### Documentation

1. @documentation-sagent: Accessibility documentation

## Output

Provide accessibility report:
- WCAG compliance score
- Violations fixed
- Remaining issues
- Manual testing results
- Accessibility statement
- Next audit date
