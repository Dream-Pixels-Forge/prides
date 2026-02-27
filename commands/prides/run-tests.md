---
description: Run comprehensive test suites including unit, integration, E2E, security, performance, and accessibility tests. Use {{args}} to specify test scope (e.g., "unit", "integration", "e2e", "all", or specific file path).
---

# Comprehensive Test Execution

**Test Scope:** {{args}}

## Instructions

Execute the appropriate test suites based on the specified scope:

### Test Categories

| Category | Command | Description |
|----------|---------|-------------|
| **Unit Tests** | `unit` | Test individual components/functions |
| **Integration Tests** | `integration` | Test component interactions |
| **E2E Tests** | `e2e` | End-to-end user flow tests |
| **Security Tests** | `security` | Security scanning and vulnerability tests |
| **Performance Tests** | `performance` | Load, stress, and benchmark tests |
| **Accessibility Tests** | `accessibility` | WCAG compliance testing |
| **All Tests** | `all` or empty | Complete test suite |

### Pre-Test Setup
1. **Dependencies**: Install/update test dependencies
2. **Environment**: Set up test environment variables
3. **Database**: Prepare test database (if needed)

### Test Execution

#### Unit Tests
- Run Jest/Vitest/pytest unit tests
- Generate coverage report
- Target: >80% code coverage

#### Integration Tests
- Run API integration tests
- Test database interactions
- Test external service mocks

#### E2E Tests
- Run Playwright/Cypress tests
- Test critical user journeys
- Capture screenshots on failure

#### Security Tests
- Run OWASP Top 10 checks
- Dependency vulnerability scan
- Static analysis security scan

#### Performance Tests
- Run load tests
- Measure response times
- Identify bottlenecks

#### Accessibility Tests
- Run WCAG 2.1 AA checks
- Test keyboard navigation
- Screen reader compatibility

### Post-Test Actions
1. **Testing Agent**: Aggregate all test results
2. **Documentation Agent**: Update test coverage docs

### Quality Gates

| Gate | Threshold | Action |
|------|-----------|--------|
| **Unit Coverage** | >80% | Block if below |
| **Pass Rate** | 100% | Block on failures |
| **Performance** | <3s response | Warn if exceeded |
| **Accessibility** | WCAG 2.1 AA | Block on violations |
| **Security** | Zero critical | Block on critical |

## Output

Provide comprehensive test report:
- Total tests run
- Pass/fail counts
- Coverage percentage
- Performance metrics
- Security findings
- Accessibility violations
- Failed test details with suggestions
