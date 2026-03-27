---
name: agent-coordination
version: 1.0.0
description: Agent usage tracking and coordination documentation
lastUpdated: 2026-03-27
status: active
---

# Agent Coordination

## Overview

This document tracks agent usage, coordination patterns, and handoffs within the PRIDES multi-agent system. It provides visibility into which agents are active, their current tasks, and how they collaborate.

**Last Updated:** 2026-03-27

**Active Workflow:** [WF-YYYY-MM-DD-XXX]

---

## Agent Registry

### Core Agents

| Agent | Type | Status | Current Task | Load |
|-------|------|--------|--------------|------|
| **Prides Agent** | Orchestrator | [Active/Idle] | [Task] | [X]% |
| **Git Master SAgent** | Version Control | [Active/Idle] | [Task] | [X]% |
| **Plan SAgent** | Planning | [Active/Idle] | [Task] | [X]% |
| **Tasks SAgent** | Task Management | [Active/Idle] | [Task] | [X]% |
| **Idea SAgent** | Brainstorming | [Active/Idle] | [Task] | [X]% |

### Development Agents

| Agent | Type | Status | Current Task | Load |
|-------|------|--------|--------------|------|
| **Coder SAgent** | Implementation | [Active/Idle] | [Task] | [X]% |
| **Debugger SAgent** | Debugging | [Active/Idle] | [Task] | [X]% |
| **UI/UX SAgent** | Design | [Active/Idle] | [Task] | [X]% |
| **Prototyper SAgent** | Prototyping | [Active/Idle] | [Task] | [X]% |
| **Critic SAgent** | Code Review | [Active/Idle] | [Task] | [X]% |

### Quality & Security Agents

| Agent | Type | Status | Current Task | Load |
|-------|------|--------|--------------|------|
| **Testing SAgent** | QA Automation | [Active/Idle] | [Task] | [X]% |
| **Security SAgent** | Security Analysis | [Active/Idle] | [Task] | [X]% |
| **Performance SAgent** | Optimization | [Active/Idle] | [Task] | [X]% |
| **Lint SAgent** | Code Quality | [Active/Idle] | [Task] | [X]% |
| **Accessibility SAgent** | WCAG Compliance | [Active/Idle] | [Task] | [X]% |

### Documentation & Improvement Agents

| Agent | Type | Status | Current Task | Load |
|-------|------|--------|--------------|------|
| **Documentation SAgent** | Technical Docs | [Active/Idle] | [Task] | [X]% |
| **Improvement SAgent** | Code Enhancement | [Active/Idle] | [Task] | [X]% |
| **Improver SAgent** | Agent Auditing | [Active/Idle] | [Task] | [X]% |

### Deployment Agents

| Agent | Type | Status | Current Task | Load |
|-------|------|--------|--------------|------|
| **Deployment SAgent** | Release Management | [Active/Idle] | [Task] | [X]% |
| **Monitoring SAgent** | Production Monitoring | [Active/Idle] | [Task] | [X]% |
| **Rollback SAgent** | Rollback Procedures | [Active/Idle] | [Task] | [X]% |

---

## Agent Coordination Example

### Example: New Feature Development Workflow

This example shows how agents coordinate during a complete feature development cycle:

**Feature:** "Add user authentication with social login (Google, GitHub)"

| Phase | Active Agents | Coordination Pattern | Handoff Details |
|-------|---------------|---------------------|-----------------|
| **1. Planning** | Prides → Plan SAgent → Tasks SAgent | Prides receives feature request, delegates to Plan SAgent for architecture, Tasks SAgent breaks down into implementable tasks | Plan SAgent creates `IMPLEMENTATION-PLAN.md` with 3 phases, Tasks SAgent creates 12 tasks in `TASKS.md` with dependencies |
| **2. Design** | Prides → UI/UX SAgent → Prototyper SAgent | UI/UX SAgent defines design tokens and components, Prototyper creates Stitch visual prototype | UI/UX SAgent outputs `DESIGN.md` with color palette, typography, component specs. Prototyper generates Stitch project at `prototypes/auth-flow-001/` |
| **3. Implementation** | Prides → Coder SAgent → Lint SAgent | Coder SAgent implements features following design specs, Lint SAgent auto-fixes code quality issues | Coder creates 8 files (components, hooks, API routes), Lint applies 15 auto-fixes (formatting, unused imports) |
| **4. Review** | Critic SAgent (MUST USE) | Critic SAgent performs deep code analysis, identifies 3 issues (missing error handling, type safety gap, accessibility issue) | Critic generates `CRITIQUE-REPORT.md` with severity levels. Coder SAgent fixes all 3 issues. Second review passes. |
| **5. Testing** | Testing SAgent → Security SAgent → Performance SAgent | Testing SAgent generates unit/E2E tests, Security SAgent validates OAuth implementation, Performance SAgent checks bundle impact | Testing creates 24 tests (92% coverage), Security approves OAuth flow, Performance confirms <5kb bundle increase |
| **6. Commit** | Git Master SAgent | Git Master SAgent creates feature branch, commits with conventional commit message, prepares PR | Branch: `feat/user-auth-social-login`, Commit: `feat: add OAuth2 authentication with Google and GitHub`, PR created with all quality gates attached |
| **7. Merge & Deploy** | Deployment SAgent → Monitoring SAgent | Deployment SAgent executes canary deployment (10% → 50% → 100%), Monitoring SAgent tracks error rates and performance | Deployment completes in 15 minutes, Monitoring confirms 0.2% error rate (below 1% threshold), health checks pass |

**Total Coordination Handoffs:** 12
**Total Agents Involved:** 11
**Cycle Time:** 4 hours (planning to production)

---

## Agent Communication Log

### Recent Communications

| Timestamp | From | To | Message Type | Summary |
|-----------|------|-----|--------------|---------|
| [YYYY-MM-DD HH:MM] | [Agent] | [Agent] | [Request/Response/Update] | [Summary] |

### Pending Requests

| Request ID | From Agent | To Agent | Request | Priority | Status |
|------------|------------|----------|---------|----------|--------|
| [REQ-001] | [Agent] | [Agent] | [Request] | [High/Medium/Low] | [Pending] |

---

## Agent Performance Metrics

### Response Times

| Agent | Avg Response | P95 Response | P99 Response |
|-------|--------------|--------------|--------------|
| **[Agent Name]** | [X]s | [X]s | [X]s |

### Success Rates

| Agent | Success Rate | Failure Rate | Timeout Rate |
|-------|--------------|--------------|--------------|
| **[Agent Name]** | [X]% | [X]% | [X]% |

### Task Completion

| Agent | Tasks Completed | Avg Completion Time | Quality Score |
|-------|-----------------|---------------------|---------------|
| **[Agent Name]** | [X] | [X]m | [X]/10 |

---

## Resource Allocation

### Current Resource Usage

| Resource | Allocated | Available | Utilization |
|----------|-----------|-----------|-------------|
| **Agent Slots** | [X]/[Y] | [Z] | [X]% |
| **Context Cache** | [X]MB | [Y]MB | [X]% |
| **Task Queue** | [X] tasks | - | - |

### Agent Load Distribution

| Load Level | Agents | Count |
|------------|--------|-------|
| **High (>80%)** | [Agent names] | [X] |
| **Medium (50-80%)** | [Agent names] | [X] |
| **Low (<50%)** | [Agent names] | [X] |
| **Idle** | [Agent names] | [X] |

---

## Coordination Issues

### Current Issues

| Issue ID | Description | Affected Agents | Impact | Status |
|----------|-------------|-----------------|--------|--------|
| [ISS-001] | [Description] | [Agents] | [High/Medium/Low] | [Investigating] |

### Resolved Issues

| Issue ID | Description | Resolution | Resolved At |
|----------|-------------|------------|-------------|
| [ISS-000] | [Description] | [Resolution] | [Timestamp] |

---

## Agent Configuration

### Active Configurations

| Agent | Configuration | Version | Last Updated |
|-------|---------------|---------|--------------|
| **[Agent Name]** | [Config name] | [X.Y.Z] | [Date] |

### Skill Bindings

| Agent | Bound Skills | Status |
|-------|--------------|--------|
| **[Agent Name]** | [Skill 1], [Skill 2] | [Active] |

---

## Coordination Best Practices

### Handoff Guidelines

1. **Context Preservation** - Always pass complete context
2. **Status Communication** - Report task status before handoff
3. **Error Propagation** - Communicate errors immediately
4. **Resource Release** - Free resources after handoff complete

### Conflict Resolution

1. **Priority-Based** - Higher priority tasks take precedence
2. **First-Come-First-Served** - Equal priority tasks queued by arrival
3. **Resource-Aware** - Consider agent load when assigning

---

## Related Documentation

- [Project Context](./project-context.md) - Project overview
- [Active Workflow](./active-workflow.md) - Current workflow state
- [Skills Inventory](./skills-inventory.md) - Available capabilities
- [Decision Log](./decision-log.md) - Coordination decisions
- [Quality Gates](./quality-gates.md) - Quality validation

---

## Notes

[Additional coordination information, patterns, or observations]
