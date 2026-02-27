---
description: Debug and diagnose issues with root cause analysis and fix recommendations. Use {{args}} to describe the issue or provide error messages/logs.
---

# Issue Debugging and Diagnosis

**Issue Description:** {{args}}

## Instructions

Execute systematic debugging and diagnosis to identify root cause and implement fixes.

### Phase 1: Issue Analysis

1. **Debugger SAgent**: Initial issue assessment
   - Reproduce the issue (if possible)
   - Collect error messages and stack traces
   - Identify affected components
   - Determine issue severity

2. **Information Gathering**
   - Read relevant log files
   - Check recent commits
   - Review error tracking (Sentry, etc.)
   - Collect user reports if available

### Phase 2: Root Cause Analysis

1. **Debugger SAgent**: Deep dive analysis
   - Trace execution flow
   - Identify failing code paths
   - Check for race conditions
   - Analyze data flow issues

2. **Critic SAgent**: Code review for potential causes
   - Check for similar issues in codebase
   - Identify anti-patterns
   - Review recent changes

3. **Analysis Categories**
   - **Logic Errors**: Incorrect algorithms, conditions
   - **Data Issues**: Invalid input, state corruption
   - **Integration Issues**: API failures, service outages
   - **Performance Issues**: Memory leaks, slow queries
   - **Environment Issues**: Config problems, dependencies

### Phase 3: Fix Implementation

1. **Debugger SAgent**: Propose fix strategy
   - Immediate workaround (if needed)
   - Proper long-term fix
   - Risk assessment

2. **Coder SAgent**: Implement fix
   - Create fix branch
   - Implement solution
   - Add regression tests

3. **Critic SAgent**: Review fix
   - Verify fix addresses root cause
   - Check for side effects
   - Ensure no new issues introduced

### Phase 4: Validation

1. **Testing SAgent**: Run regression tests
   - Test the specific issue
   - Run related test suites
   - Verify no regressions

2. **Performance SAgent**: Performance validation
   - Ensure no performance degradation
   - Check resource usage

3. **Security SAgent**: Security validation
   - Ensure no security impact
   - Verify no new vulnerabilities

### Phase 5: Deployment

1. **Git Master SAgent**: Create hotfix branch
2. **Git Master SAgent**: Merge to main (expedited)
3. **Deployment SAgent**: Deploy hotfix (priority)
4. **Monitoring SAgent**: Enhanced monitoring

### Debug Tools Available

| Tool | Purpose | Command |
|------|---------|---------|
| **Console Logs** | Runtime debugging | `!{cat logs/app.log}` |
| **Git Diff** | Recent changes | `!{git diff HEAD~5}` |
| **Dependency Check** | Version issues | `!{npm outdated}` |
| **Type Check** | Type errors | `!{tsc --noEmit}` |
| **Lint** | Code issues | `!{npm run lint}` |

### Documentation

1. **Documentation SAgent**: Create bug report
   - Issue description
   - Root cause analysis
   - Fix implemented
   - Lessons learned

2. **Bugs-Fixed Archive**: Add to learning system
   - Store for future reference
   - Enable pattern recognition
   - Prevent recurrence

## Output

Provide comprehensive debug report:
- Issue summary
- Root cause identified
- Components affected
- Fix implemented
- Tests added
- Deployment status
- Prevention recommendations
