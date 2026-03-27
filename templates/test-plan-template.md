# Test Plan - {{Feature/Project Name}}

## Overview

{{Description of what is being tested}}

## Test Scope

### In Scope
- {{Feature/Area 1}}
- {{Feature/Area 2}}

### Out of Scope
- {{Feature/Area not being tested}}

---

## Test Strategy

### Unit Tests
- **Framework**: {{Testing framework}}
- **Coverage Target**: >80%
- **Focus**: Individual functions and components

### Integration Tests
- **Framework**: {{Testing framework}}
- **Focus**: Component interactions, API calls

### E2E Tests
- **Framework**: {{Testing framework}}
- **Focus**: Critical user journeys

---

## Test Cases

### Unit Tests

#### {{Function/Component Name}}

| Test ID | Description | Input | Expected Output | Status |
|---------|-------------|-------|-----------------|--------|
| UT-001 | {{Test description}} | {{Input}} | {{Expected}} | ⬜ |
| UT-002 | {{Test description}} | {{Input}} | {{Expected}} | ⬜ |

### Integration Tests

| Test ID | Description | Components | Expected Result | Status |
|---------|-------------|------------|-----------------|--------|
| IT-001 | {{Test description}} | {{Components}} | {{Result}} | ⬜ |
| IT-002 | {{Test description}} | {{Components}} | {{Result}} | ⬜ |

### E2E Tests

| Test ID | User Journey | Steps | Expected Result | Status |
|---------|--------------|-------|-----------------|--------|
| E2E-001 | {{Journey}} | 1. {{Step 1}}<br>2. {{Step 2}} | {{Result}} | ⬜ |

---

## Test Data

### Required Data

| Data Type | Description | Source |
|-----------|-------------|--------|
| {{Data 1}} | {{Description}} | {{Source}} |
| {{Data 2}} | {{Description}} | {{Source}} |

### Test Accounts

| Role | Username | Password | Permissions |
|------|----------|----------|-------------|
| Admin | {{username}} | {{password}} | {{Permissions}} |
| User | {{username}} | {{password}} | {{Permissions}} |

---

## Environment

| Environment | URL | Purpose |
|-------------|-----|---------|
| Development | {{URL}} | Initial testing |
| Staging | {{URL}} | Pre-production validation |
| Production | {{URL}} | Smoke tests only |

---

## Test Execution

### Schedule

| Phase | Start Date | End Date | Owner |
|-------|------------|----------|-------|
| Unit Testing | {{date}} | {{date}} | {{owner}} |
| Integration Testing | {{date}} | {{date}} | {{owner}} |
| E2E Testing | {{date}} | {{date}} | {{owner}} |
| UAT | {{date}} | {{date}} | {{owner}} |

### Entry Criteria

- [ ] Code complete
- [ ] Unit tests passing
- [ ] Build successful
- [ ] Test environment ready

### Exit Criteria

- [ ] All critical test cases passed
- [ ] Code coverage >80%
- [ ] No critical bugs open
- [ ] Performance requirements met
- [ ] Accessibility requirements met

---

## Defect Management

### Severity Levels

| Level | Description | Response Time |
|-------|-------------|---------------|
| Critical | System down, data loss | Immediate |
| High | Major functionality broken | 24 hours |
| Medium | Minor functionality affected | 1 week |
| Low | Cosmetic, documentation | Next release |

### Defect Template

```markdown
### [Severity] Defect Title

**Test Case ID**: {{ID}}
**Environment**: {{Environment}}
**Steps to Reproduce**:
1. {{Step 1}}
2. {{Step 2}}

**Expected Result**: {{Expected}}
**Actual Result**: {{Actual}}
**Evidence**: {{Screenshot/Log}}
```

---

## Test Report

### Summary

| Metric | Count | Percentage |
|--------|-------|------------|
| Total Tests | {{count}} | 100% |
| Passed | {{count}} | {{%}} |
| Failed | {{count}} | {{%}} |
| Blocked | {{count}} | {{%}} |
| Not Run | {{count}} | {{%}} |

### Coverage

| Metric | Target | Actual |
|--------|--------|--------|
| Statements | 80% | {{%}} |
| Branches | 80% | {{%}} |
| Functions | 80% | {{%}} |
| Lines | 80% | {{%}} |

### Issues Summary

| Severity | Open | Closed | Total |
|----------|------|--------|-------|
| Critical | {{count}} | {{count}} | {{count}} |
| High | {{count}} | {{count}} | {{count}} |
| Medium | {{count}} | {{count}} | {{count}} |
| Low | {{count}} | {{count}} | {{count}} |

---

## Sign-off

| Role | Name | Date | Signature |
|------|------|------|-----------|
| QA Lead | {{name}} | {{date}} | |
| Dev Lead | {{name}} | {{date}} | |
| Product Owner | {{name}} | {{date}} | |
