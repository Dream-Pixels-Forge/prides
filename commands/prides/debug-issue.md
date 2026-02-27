---
description: Debug and diagnose issues with root cause analysis and fix recommendations. Use {{args}} to describe the issue or provide error messages/logs.
---

# Issue Debugging and Diagnosis

**Issue Description:** {{args}}

## Instructions

Execute systematic debugging and diagnosis to identify root cause and implement fixes.

### Phase 1: Issue Analysis

1. Delegate to **debugger-sagent** Subagents for initial issue assessment
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

1. Delegate to **debugger-sagent** Subagents for deep dive analysis
   - Trace execution flow
   - Identify failing code paths
   - Check for race conditions
   - Analyze data flow issues

3. **Analysis Categories**
   - **Logic Errors**: Incorrect algorithms, conditions
   - **Data Issues**: Invalid input, state corruption
   - **Integration Issues**: API failures, service outages
   - **Performance Issues**: Memory leaks, slow queries
   - **Environment Issues**: Config problems, dependencies

### Phase 3: Fix Implementation

1. Delegate to **debugger-sagent** Subagents to propose fix strategy
   - Immediate workaround (if needed)
   - Proper long-term fix
   - Risk assessment

2. Delegate to **coder-sagent** Subagents to implement fix

### Phase 4: Validation

1. Delegate to **testing-sagent** Subagents to run regression tests
   - Test the specific issue
   - Run related test suites
   - Verify no regressions

### Debug Tools Available

| Tool | Purpose | Command |
|------|---------|---------|
| **Console Logs** | Runtime debugging | `!{cat logs/app.log}` |
| **Git Diff** | Recent changes | `!{git diff HEAD~5}` |
| **Dependency Check** | Version issues | `!{npm outdated}` |
| **Type Check** | Type errors | `!{tsc --noEmit}` |
| **Lint** | Code issues | `!{npm run lint}` |

### Documentation

1. Delegate to **documentation-sagent** Subagents to create bug report

## Output

Provide comprehensive debug report:
- Issue summary
- Root cause identified
- Components affected
- Fix implemented
- Tests added
- Deployment status
- Prevention recommendations
