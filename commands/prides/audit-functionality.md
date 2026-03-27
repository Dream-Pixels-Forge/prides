---
name: audit-functionality
description: Run comprehensive functionality audit to discover and replace mockups, placeholders, and incomplete implementations with working code. Use {{args}} to specify focus area or leave empty for full audit.
---

# Functionality Audit and Implementation

**Audit Scope:** {{args}}

## Workflow

Execute comprehensive functionality audit to identify and replace all mockups, placeholders, and incomplete implementations with real, working functionality.

### Phase 1: Discovery & Assessment

1. **Mockup & Placeholder Detection**
   
   Instruct agents to search for:
   - Mock data and fake APIs
   - Placeholder components and stubs
   - Non-functional buttons/links
   - TODO/FIXME/HACK comments
   - Console.log placeholders
   - Mock authentication/authorization
   - Sample/dummy content
   - Disabled features
   - Commented-out functionality

   Search patterns:
   - `// TODO`, `// FIXME`, `// HACK`
   - `mock`, `fake`, `dummy`, `placeholder`
   - `alert('not implemented')`
   - `console.log('placeholder')`
   - `href="#"`, `onClick={() => {}}`
   - `data-testid="mock"`
   - `.mockImplementation()`, `jest.fn()`

2. **@tasks-sagent**: Create prioritized backlog
   - Categorize by severity (critical, high, medium, low)
   - Estimate effort for each item
   - Identify dependencies
   - Group related functionality

3. **@plan-sagent**: Implementation strategy
   - Determine implementation order
   - Identify required APIs/services
   - Plan integration points
   - Assess risks and mitigation

### Phase 2: Implementation Planning

1. **@plan-sagent**: Detailed implementation plan
   - Architecture for each feature
   - Data flow diagrams
   - API integration strategy
   - State management approach
   - Error handling strategy

2. **@ui-ux-sagent**: UX review
   - Validate user flows
   - Ensure consistent interactions
   - Review accessibility requirements
   - Define loading/error states

3. **@git-master-sagent**: Create implementation branch
   - Branch name: `feat/audit-functionality-{date}`
   - Enable offline mode if needed

### Phase 3: Implementation

1. **@coder-sagent**: Replace mockups with real functionality
   - Implement actual API calls
   - Connect real data sources
   - Make buttons/links functional
   - Replace mock authentication
   - Implement real business logic
   - Add proper error handling
   - Connect to backend services

2. **@prototyper-sagent**: Create visual prototypes (if needed)
   - Design new interactive elements
   - Create Stitch prototypes for complex UI
   - Convert prototypes to React components

3. **@coder-sagent**: API Integration
   - Implement REST/GraphQL clients
   - Add request/response handling
   - Implement caching strategies
   - Add retry logic
   - Handle rate limiting

4. **@coder-sagent**: State Management
   - Implement proper state management
   - Add data persistence
   - Handle optimistic updates
   - Implement real-time updates if needed

### Phase 4: Quality Assurance

1. **@lint-sagent**: Code quality check
   - Run linting
   - Apply auto-fixes
   - Check code complexity
   - Ensure consistency

2. **@critic-sagent**: Deep code review
   - Review all implementations
   - Check for edge cases
   - Validate error handling
   - Ensure no hallucinations

3. **@testing-sagent**: Test generation and execution
   - Generate unit tests for new functionality
   - Create integration tests
   - Run E2E tests for user flows
   - Verify test coverage >80%

4. **@performance-sagent**: Performance validation
   - Check load times
   - Validate API response handling
   - Optimize bundle size
   - Check memory usage

5. **@accessibility-sagent**: WCAG compliance
   - Audit accessibility
   - Fix violations
   - Test keyboard navigation
   - Validate screen reader compatibility

6. **@security-sagent**: Security audit
   - Check for vulnerabilities
   - Validate authentication/authorization
   - Review input validation
   - Check for XSS/CSRF protection

### Phase 5: Documentation

1. **@documentation-sagent**: Update documentation
   - Document new features
   - Update API documentation
   - Create usage examples
   - Update changelog

2. **@documentation-sagent**: Code documentation
   - Add JSDoc comments
   - Document complex logic
   - Create inline examples
   - Update README sections

### Phase 6: Deployment Preparation

1. **@git-master-sagent**: Commit and merge
   - Commit all changes with clear messages
   - Create pull request
   - Ensure all quality gates pass
   - Merge to main branch

2. **@deployment-sagent**: Deployment strategy
   - Prepare deployment plan
   - Configure feature flags if needed
   - Set up monitoring
   - Plan rollback strategy

## Discovery Tools

Instruct agents to use these search patterns:

### File Content Searches

```bash
# Search for TODOs and placeholders
grep -r "TODO\|FIXME\|HACK\|placeholder\|mock" src/

# Search for non-functional handlers
grep -r "onClick={() => {}}" src/
grep -r "href=\"#\"" src/
grep -r "alert.*not implemented" src/

# Search for mock data
grep -r "mockData\|fakeData\|dummyData" src/
grep -r "jest.mock\|mockImplementation" src/
```

### Code Pattern Detection

Instruct agents to identify:
- Components with `return null` or empty renders
- Functions that return hardcoded values
- API calls to `example.com` or `localhost`
- Disabled form submissions
- Non-functional navigation
- Mock authentication checks

## Output

Provide comprehensive audit report:

### Discovery Summary
- Total mockups/placeholders found
- Categorized by type and severity
- Estimated effort to complete

### Implementation Summary
- Features implemented
- APIs connected
- Mockups replaced
- Buttons/links made functional

### Quality Metrics
- Test coverage achieved
- Performance benchmarks
- Accessibility score
- Security audit results

### Documentation
- Files updated
- New documentation created
- API docs generated

### Deployment Status
- Branch created
- Commits made
- Quality gates passed
- Deployment status

## Example Usage

```bash
# Full audit
/audit-functionality

# Focus on specific area
/audit-functionality "Checkout page has non-functional buttons"

# Replace mock data
/audit-functionality "Replace all mock data in user dashboard"

# Focus on authentication
/audit-functionality "Implement real authentication, replace mock login"
```
