# Prides Quality Standards

## Overview

This document defines the quality standards enforced by the Prides multi-agent development system.

---

## Code Quality Standards

### Zero Tolerance Policy

The following issues are **never allowed** in production code:

| Issue | Description | Detection |
|-------|-------------|-----------|
| **Mockups/Placeholders** | TODO comments, lorem ipsum, stub implementations | Critic SAgent |
| **Hardcoded Secrets** | API keys, passwords, tokens in code | Security SAgent |
| **Type Errors** | TypeScript type mismatches, unsafe casts | Lint SAgent |
| **Unhandled Errors** | Missing try-catch, unhandled promises | Critic SAgent |
| **Broken Imports** | References to non-existent modules | Critic SAgent |
| **Security Vulnerabilities** | OWASP Top 10 vulnerabilities | Security SAgent |

### Code Quality Metrics

| Metric | Target | Warning | Critical |
|--------|--------|---------|----------|
| **Cyclomatic Complexity** | <10 | <15 | >15 |
| **Function Length** | <30 lines | <50 lines | >50 lines |
| **File Length** | <500 lines | <800 lines | >800 lines |
| **Duplicate Code** | <5% | <10% | >10% |
| **Technical Debt Ratio** | <5% | <10% | >10% |

### Code Style Standards

#### Naming Conventions
```typescript
// ✅ Good
const userName = 'Patrick';
function calculateTotal(): number {}
interface UserProps {}
const MAX_RETRIES = 3;

// ❌ Bad
const x = 'Patrick'; // Unclear
function calc(): number {} // Abbreviated
interface Props {} // Too generic
const max = 3; // Not uppercase constant
```

#### Function Standards
```typescript
// ✅ Good: Single responsibility, clear name
function calculateOrderTotal(items: Item[], discount: number): number {
  // Implementation
}

// ❌ Bad: Multiple responsibilities, unclear name
function process(data: any): any {
  // Does everything
}
```

#### Error Handling
```typescript
// ✅ Good: Specific errors, user-friendly messages
try {
  const user = await getUser(id);
  return { success: true, data: user };
} catch (error) {
  if (error instanceof NotFoundError) {
    return { success: false, error: 'User not found' };
  }
  return { success: false, error: 'Unable to load user' };
}

// ❌ Bad: Silent failures, generic errors
try {
  const user = await getUser(id);
} catch (e) {
  console.log(e); // Silent
}
```

---

## Testing Standards

### Coverage Requirements

| Code Type | Coverage Target | Minimum |
|-----------|-----------------|---------|
| **Business Logic** | 90% | 80% |
| **Utilities** | 95% | 90% |
| **Components** | 85% | 75% |
| **APIs** | 90% | 80% |

### Test Quality Standards

#### Good Test Characteristics (FIRST)
- **Fast**: Tests execute in <100ms each
- **Independent**: No test depends on another
- **Repeatable**: Same results every time
- **Self-validating**: Clear pass/fail
- **Timely**: Written before/during development

#### Test Naming Convention
```typescript
// ✅ Good: Clear behavior description
it('should return discounted price when valid coupon applied');
it('should throw InvalidCouponError when coupon expired');

// ❌ Bad: Unclear
it('should work correctly');
it('test coupon');
```

#### Test Structure
```typescript
// ✅ Good: AAA pattern
it('should calculate total correctly', () => {
  // Arrange
  const items = [{ price: 100, qty: 2 }];
  
  // Act
  const total = calculateTotal(items);
  
  // Assert
  expect(total).toBe(200);
});

// ❌ Bad: No structure
it('test', () => {
  const items = [{ price: 100, qty: 2 }];
  const total = calculateTotal(items);
  expect(total).toBe(200);
});
```

### Test Execution Standards

| Test Type | Max Duration | Frequency |
|-----------|--------------|-----------|
| **Unit Tests** | <5 minutes | Every commit |
| **Integration Tests** | <10 minutes | Every PR |
| **E2E Tests** | <15 minutes | Before merge |
| **Full Suite** | <30 minutes | Before release |

---

## Security Standards

### OWASP Top 10 Compliance

All applications must be protected against:

| Risk | Requirement | Verification |
|------|-------------|--------------|
| **A01: Broken Access Control** | Enforce authorization on all endpoints | Security SAgent audit |
| **A02: Cryptographic Failures** | Use TLS 1.3, encrypt sensitive data | Security scan |
| **A03: Injection** | Parameterized queries, input validation | Static analysis |
| **A04: Insecure Design** | Threat modeling, secure design patterns | Design review |
| **A05: Security Misconfiguration** | Secure defaults, hardened configs | Config audit |
| **A06: Vulnerable Components** | Updated dependencies, no known CVEs | Dependency scan |
| **A07: Auth Failures** | MFA, secure session management | Auth audit |
| **A08: Data Integrity** | Validation, checksums, signatures | Data flow review |
| **A09: Logging Failures** | Comprehensive logs, no sensitive data | Log review |
| **A10: SSRF** | Validate URLs, network segmentation | Network audit |

### Security Checklist

**Every commit must pass:**
- [ ] No hardcoded secrets
- [ ] Input validation on all user input
- [ ] Output encoding to prevent XSS
- [ ] CSRF tokens on state-changing operations
- [ ] Secure authentication implementation
- [ ] Proper session management
- [ ] Access control on all endpoints
- [ ] Security headers configured
- [ ] Dependencies up to date
- [ ] No sensitive data in logs

### Vulnerability Response Times

| Severity | Detection to Fix | Example |
|----------|------------------|---------|
| **Critical** | <24 hours | Remote code execution |
| **High** | <1 week | SQL injection |
| **Medium** | <1 month | XSS vulnerability |
| **Low** | Next release | Information disclosure |

---

## Performance Standards

### Core Web Vitals

| Metric | Good | Needs Improvement | Poor |
|--------|------|-------------------|------|
| **LCP** (Largest Contentful Paint) | <2.5s | <4.0s | >4.0s |
| **FID** (First Input Delay) | <100ms | <300ms | >300ms |
| **CLS** (Cumulative Layout Shift) | <0.1 | <0.25 | >0.25 |
| **INP** (Interaction to Next Paint) | <200ms | <500ms | >500ms |

### Performance Budget

| Resource | Budget | Warning | Critical |
|----------|--------|---------|----------|
| **JavaScript** | <200KB | <350KB | >500KB |
| **CSS** | <50KB | <100KB | >150KB |
| **Images** | <500KB/page | <1MB/page | >2MB/page |
| **Fonts** | <100KB | <200KB | >300KB |
| **Total Page Size** | <1MB | <2MB | >3MB |

### API Performance

| Metric | Target | Warning | Critical |
|--------|--------|---------|----------|
| **Response Time (p50)** | <200ms | <500ms | >1000ms |
| **Response Time (p95)** | <500ms | <1000ms | >2000ms |
| **Response Time (p99)** | <1000ms | <2000ms | >5000ms |
| **Error Rate** | <0.1% | <1% | >5% |
| **Availability** | >99.9% | >99% | <99% |

### Performance Testing

| Test Type | Scenario | Success Criteria |
|-----------|----------|------------------|
| **Load Test** | Expected traffic | All requests succeed, p95 <1s |
| **Stress Test** | 2x expected traffic | System degrades gracefully |
| **Spike Test** | Sudden traffic surge | Auto-scaling responds |
| **Endurance Test** | 24h sustained load | No memory leaks, stable performance |

---

## Accessibility Standards

### WCAG 2.1 AA Compliance

**All applications must meet:**

#### Perceivable
- [ ] Alt text for all images
- [ ] Captions for videos
- [ ] Content can be presented differently
- [ ] Color contrast ratio ≥4.5:1 (normal text)
- [ ] Color contrast ratio ≥3:1 (large text)
- [ ] Text can be resized to 200%

#### Operable
- [ ] All functionality keyboard accessible
- [ ] No keyboard traps
- [ ] Skip links provided
- [ ] Focus order is logical
- [ ] Focus indicators visible
- [ ] No content flashes >3 times/second

#### Understandable
- [ ] Page language declared
- [ ] Language of parts marked
- [ ] No unexpected context changes
- [ ] Labels for form fields
- [ ] Error messages describe problem
- [ ] Error suggestions provided

#### Robust
- [ ] Valid HTML
- [ ] Proper ARIA usage
- [ ] Name, role, value for all UI elements
- [ ] Status messages announced

### Accessibility Testing

| Test Type | Tool | Frequency |
|-----------|------|-----------|
| **Automated** | axe-core, Lighthouse | Every commit |
| **Manual Keyboard** | Manual testing | Every PR |
| **Screen Reader** | NVDA, VoiceOver | Before release |
| **Color Blindness** | Simulation tools | Design review |

---

## Documentation Standards

### Code Documentation

| Element | Requirement | Example |
|---------|-------------|---------|
| **Public Functions** | JSDoc with description, params, returns | ✅ Required |
| **Components** | Props description, usage example | ✅ Required |
| **Complex Logic** | Inline comment explaining why | ✅ Required |
| **API Endpoints** | OpenAPI/Swagger spec | ✅ Required |
| **Types/Interfaces** | Description of purpose | ✅ Required |

### Documentation Quality

| Criteria | Standard |
|----------|----------|
| **Accuracy** | All examples tested and working |
| **Completeness** | All public APIs documented |
| **Clarity** | Clear, concise language |
| **Currency** | Updated with each change |
| **Accessibility** | Documentation itself accessible |

---

## Quality Gate Enforcement

### Automated Gates

| Gate | Tool | Block If Failed |
|------|------|-----------------|
| **Lint** | ESLint, Prettier | ✅ Yes |
| **Type Check** | TypeScript | ✅ Yes |
| **Tests** | Jest, Vitest | ✅ Yes |
| **Coverage** | Coverage report | ✅ Yes |
| **Security** | Security scan | ✅ Yes |
| **Accessibility** | axe-core | ✅ Yes |
| **Performance** | Lighthouse | ⚠️ Warning |

### Manual Gates

| Gate | Reviewer | Block If Failed |
|------|----------|-----------------|
| **Code Review** | Team member | ✅ Yes |
| **Security Review** | Security team | ✅ Yes (for sensitive changes) |
| **Accessibility Review** | A11y specialist | ✅ Yes (for UI changes) |
| **Performance Review** | Performance team | ⚠️ If significant regression |

---

## Continuous Improvement

### Quality Metrics Tracking

Track these metrics over time:
- Defect density (bugs per KLOC)
- Test coverage trend
- Security vulnerability count
- Performance regression count
- Accessibility violation count
- Technical debt ratio

### Quality Retrospectives

**After each release:**
1. Review quality metrics
2. Identify patterns in issues
3. Update quality standards if needed
4. Share learnings across teams

### Quality Training

**Regular training on:**
- Secure coding practices
- Accessibility best practices
- Performance optimization
- Testing strategies
- Code review techniques
