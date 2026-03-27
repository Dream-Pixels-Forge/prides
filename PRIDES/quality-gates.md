---
name: quality-gates
version: 1.0.0
description: Quality validation results and gate status
lastUpdated: 2026-03-27
status: active
---

# Quality Gates

## Overview

This document tracks quality validation results across all quality gates in the PRIDES system. It provides visibility into code quality, security, performance, and compliance status.

**Last Updated:** 2026-03-27

**Overall Status:** [Pass/Fail/Warning]

**Last Full Validation:** [YYYY-MM-DD HH:MM]

---

## Quality Gate Summary

| Gate | Status | Last Check | Pass Rate | Trend |
|------|--------|------------|-----------|-------|
| **Pre-Commit** | [✅ Pass/❌ Fail/⚠️ Warning] | [Timestamp] | [X]% | [↑/↓/→] |
| **Pre-Merge** | [✅ Pass/❌ Fail/⚠️ Warning] | [Timestamp] | [X]% | [↑/↓/→] |
| **Pre-Deploy** | [✅ Pass/❌ Fail/⚠️ Warning] | [Timestamp] | [X]% | [↑/↓/→] |
| **Post-Deploy** | [✅ Pass/❌ Fail/⚠️ Warning] | [Timestamp] | [X]% | [↑/↓/→] |

---

## Pre-Commit Gate

### Status: [Pass/Fail/Warning]

**Last Check:** [YYYY-MM-DD HH:MM]

**Checked By:** [Agent Name]

### Checks

| Check | Status | Details | Duration |
|-------|--------|---------|----------|
| **Lint** | [✅/❌] | [X] errors, [Y] warnings | [X]s |
| **Format** | [✅/❌] | [Prettier/ESLint] | [X]s |
| **Type Check** | [✅/❌] | [X] errors | [X]s |
| **Critic Review** | [✅/❌] | [X] issues found | [X]s |

### Issues Found

| Severity | Count | Status |
|----------|-------|--------|
| **Critical** | [X] | [Fixed/Pending] |
| **High** | [X] | [Fixed/Pending] |
| **Medium** | [X] | [Fixed/Pending] |
| **Low** | [X] | [Fixed/Pending] |

### Auto-Fixes Applied

| Fix Type | Count | Status |
|----------|-------|--------|
| **Lint Fixes** | [X] | [Applied] |
| **Format Fixes** | [X] | [Applied] |
| **Type Fixes** | [X] | [Applied] |

---

## Pre-Merge Gate

### Status: [Pass/Fail/Warning]

**Last Check:** [YYYY-MM-DD HH:MM]

**Checked By:** [Agent Name]

### Checks

| Check | Status | Result | Threshold |
|-------|--------|--------|-----------|
| **Unit Tests** | [✅/❌] | [X]/[Y] passed | 100% |
| **Integration Tests** | [✅/❌] | [X]/[Y] passed | 100% |
| **E2E Tests** | [✅/❌] | [X]/[Y] passed | 100% |
| **Test Coverage** | [✅/❌] | [X]% | >80% |
| **Security Scan** | [✅/❌] | [X] vulnerabilities | 0 critical |
| **Performance** | [✅/❌] | [Metrics] | Within budget |
| **Accessibility** | [✅/❌] | [X] violations | WCAG 2.1 AA |

### Test Results Summary

| Suite | Total | Passed | Failed | Skipped | Duration |
|-------|-------|--------|--------|---------|----------|
| **Unit** | [X] | [Y] | [Z] | [W] | [X]s |
| **Integration** | [X] | [Y] | [Z] | [W] | [X]s |
| **E2E** | [X] | [Y] | [Z] | [W] | [X]s |

### Security Scan Results

| Severity | Count | Status |
|----------|-------|--------|
| **Critical** | [X] | [Resolved/Pending] |
| **High** | [X] | [Resolved/Pending] |
| **Medium** | [X] | [Resolved/Pending] |
| **Low** | [X] | [Resolved/Pending] |

### Performance Metrics

| Metric | Current | Budget | Status |
|--------|---------|--------|--------|
| **LCP** | [X]s | <2.5s | [✅/❌] |
| **FID** | [X]ms | <100ms | [✅/❌] |
| **CLS** | [X] | <0.1 | [✅/❌] |
| **Bundle Size** | [X]KB | <[Y]KB | [✅/❌] |

### Accessibility Violations

| Severity | Count | Category |
|----------|-------|----------|
| **Critical** | [X] | [Category] |
| **Serious** | [X] | [Category] |
| **Moderate** | [X] | [Category] |
| **Minor** | [X] | [Category] |

---

## Pre-Deploy Gate

### Status: [Pass/Fail/Warning]

**Last Check:** [YYYY-MM-DD HH:MM]

**Checked By:** [Agent Name]

### Checks

| Check | Status | Result | Required |
|-------|--------|--------|----------|
| **All Pre-Merge Gates** | [✅/❌] | [Passed/Failed] | Yes |
| **Smoke Tests** | [✅/❌] | [X]/[Y] passed | Yes |
| **Rollback Plan** | [✅/❌] | [Ready/Not Ready] | Yes |
| **Monitoring Config** | [✅/❌] | [Configured/Missing] | Yes |
| **Health Checks** | [✅/❌] | [Configured/Missing] | Yes |

### Deployment Readiness

| Component | Status | Version | Approved By |
|-----------|--------|---------|-------------|
| **Frontend** | [Ready/Not Ready] | [X.Y.Z] | [Name] |
| **Backend** | [Ready/Not Ready] | [X.Y.Z] | [Name] |
| **Database** | [Ready/Not Ready] | [X.Y.Z] | [Name] |
| **Infrastructure** | [Ready/Not Ready] | [X.Y.Z] | [Name] |

---

## Post-Deploy Gate

### Status: [Pass/Fail/Warning]

**Last Check:** [YYYY-MM-DD HH:MM]

**Checked By:** [Agent Name]

### Health Checks

| Check | Status | Response Time | Threshold |
|-------|--------|---------------|-----------|
| **API Health** | [✅/❌] | [X]ms | <[Y]ms |
| **Database Health** | [✅/❌] | [X]ms | <[Y]ms |
| **Cache Health** | [✅/❌] | [X]ms | <[Y]ms |
| **External Services** | [✅/❌] | [X]ms | <[Y]ms |

### Production Metrics

| Metric | Current | Baseline | Status |
|--------|---------|----------|--------|
| **Error Rate** | [X]% | <1% | [✅/❌] |
| **Latency P50** | [X]ms | <[Y]ms | [✅/❌] |
| **Latency P99** | [X]ms | <[Y]ms | [✅/❌] |
| **Throughput** | [X] req/s | >[Y] req/s | [✅/❌] |

### Monitoring Alerts

| Alert | Status | Triggered At | Resolved At |
|-------|--------|--------------|-------------|
| **[Alert Name]** | [Active/Resolved] | [Timestamp] | [Timestamp] |

---

## Quality Trends

### 7-Day Trend

| Date | Pre-Commit | Pre-Merge | Pre-Deploy | Post-Deploy |
|------|------------|-----------|------------|-------------|
| [YYYY-MM-DD] | [✅/❌] | [✅/❌] | [✅/❌] | [✅/❌] |

### Quality Metrics Over Time

| Week | Test Coverage | Security Score | Performance Score | Accessibility Score |
|------|---------------|----------------|-------------------|---------------------|
| [Week X] | [X]% | [X]/100 | [X]/100 | [X]/100 |

---

## Quality Issues

### Open Issues

| Issue ID | Gate | Severity | Description | Owner | Due Date |
|----------|------|----------|-------------|-------|----------|
| [QI-001] | [Gate] | [High/Medium/Low] | [Description] | [Owner] | [Date] |

### Resolved Issues

| Issue ID | Gate | Resolution | Resolved At | Resolved By |
|----------|------|------------|-------------|-------------|
| [QI-000] | [Gate] | [Resolution] | [Timestamp] | [Agent/Name] |

---

## Quality Gate Configuration

### Gate Thresholds

| Gate | Metric | Threshold | Current |
|------|--------|-----------|---------|
| **Pre-Merge** | Test Coverage | >80% | [X]% |
| **Pre-Merge** | Security Vulnerabilities | 0 Critical | [X] |
| **Pre-Deploy** | Performance Budget | Within limits | [Status] |
| **Post-Deploy** | Error Rate | <1% | [X]% |

### Enabled Checks

| Gate | Enabled Checks |
|------|----------------|
| **Pre-Commit** | Lint, Format, Type Check, Critic Review |
| **Pre-Merge** | Tests, Coverage, Security, Performance, Accessibility |
| **Pre-Deploy** | Smoke Tests, Rollback Plan, Monitoring |
| **Post-Deploy** | Health Checks, Metrics Validation |

---

## Related Documentation

- [Project Context](./project-context.md) - Project overview
- [Active Workflow](./active-workflow.md) - Current workflow state
- [Skills Inventory](./skills-inventory.md) - Available capabilities
- [Agent Coordination](./agent-coordination.md) - Agent usage tracking
- [Decision Log](./decision-log.md) - Quality-related decisions

---

## Notes

[Additional quality information, observations, or improvement plans]
