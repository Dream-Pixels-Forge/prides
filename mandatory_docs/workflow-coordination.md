# Prides Workflow Coordination Guide

## Overview

This document describes the standard workflow for coordinating the Prides multi-agent development system.

---

## Workflow Phases

### Phase 1: Planning & Requirements

#### 1.1 Idea Brainstorming
**Agent**: Idea SAgent

**Input**: Vague feature request or problem statement

**Process**:
1. Clarify requirements through questions
2. Brainstorm multiple approaches
3. Define clear feature scope
4. Prioritize features (MoSCoW/WSJF)
5. Define success metrics

**Output**:
- Refined feature definition
- User stories with acceptance criteria
- Prioritized feature list
- Success metrics

#### 1.2 Market Analysis
**Agent**: Analyst SAgent

**Input**: Refined feature definition

**Process**:
1. Research competitors
2. Analyze market trends
3. Identify best practices
4. Gap analysis

**Output**:
- Competitor analysis report
- Market trends summary
- Feature recommendations

#### 1.3 Requirements Documentation
**Agent**: PRD Doc SAgent

**Input**: Refined features + market analysis

**Process**:
1. Document functional requirements
2. Document non-functional requirements
3. Define acceptance criteria
4. Identify constraints

**Output**:
- Product Requirements Document (PRD)
- Clear acceptance criteria
- Technical constraints documented

#### 1.4 Implementation Planning
**Agent**: Plan SAgent

**Input**: PRD

**Process**:
1. Create technical design
2. Break down into tasks
3. Estimate effort
4. Identify dependencies
5. Define milestones
6. Assess risks

**Output**:
- Implementation plan document
- Task breakdown with estimates
- Milestone definitions
- Risk assessment

#### 1.5 Task Organization
**Agent**: Tasks SAgent

**Input**: Implementation plan

**Process**:
1. Create task board
2. Calculate WSJF scores
3. Identify critical path
4. Set up tracking

**Output**:
- Prioritized task board
- Dependency graph
- WSJF scores for each task

#### 1.6 Branch Management
**Agent**: Git Master SAgent

**Input**: Task board

**Process**:
1. Create feature branch
2. Set up branch protection
3. Configure CI/CD

**Output**:
- Feature branch created
- CI/CD pipeline configured

---

### Phase 2: Design & Prototyping

#### 2.1 Design Specification
**Agent**: UI/UX SAgent

**Input**: Requirements + acceptance criteria

**Process**:
1. Define design tokens
2. Create component specifications
3. Design all states
4. Define responsive behavior
5. Specify accessibility requirements

**Output**:
- Design token definitions
- Component specifications
- Accessibility requirements

#### 2.2 Visual Prototype
**Agent**: Prototyper SAgent

**Input**: Design specifications

**Process**:
1. Create visual prototype (Stitch)
2. Generate React components
3. Implement design tokens
4. Test interactions

**Output**:
- Visual prototype
- React component code
- Design implementation guide

#### 2.3 Design Commit
**Agent**: Git Master SAgent

**Input**: Design assets + prototype code

**Process**:
1. Stage design files
2. Commit with descriptive message
3. Push to remote

**Output**:
- Design assets committed
- Prototype code versioned

---

### Phase 3: Implementation

#### 3.1 Feature Implementation
**Agent**: Coder SAgent

**Input**: Implementation plan + design specs

**Process**:
1. Follow task breakdown
2. Implement features systematically
3. Follow project patterns
4. Self-verify code
5. Add tests

**Output**:
- Working feature implementation
- Unit tests
- Integration tests

#### 3.2 Code Quality Check
**Agent**: Lint SAgent

**Input**: Implemented code

**Process**:
1. Run linter
2. Check formatting
3. Verify type safety
4. Apply auto-fixes

**Output**:
- Lint report
- Auto-fixed issues
- Remaining issues list

#### 3.3 Deep Code Review
**Agent**: Critic SAgent

**Input**: Linted code

**Process**:
1. Deep code analysis
2. Find all issue types
3. Check for similar issues
4. Prevent hallucinations
5. Suggest fixes

**Output**:
- Issue report by severity
- Fix recommendations
- Similar issues found

#### 3.4 Code Commit
**Agent**: Git Master SAgent

**Input**: Reviewed + fixed code

**Process**:
1. Stage changes
2. Generate commit message
3. Create commit
4. Push to remote

**Output**:
- Code committed
- Commit history updated

---

### Phase 4: Quality Assurance

#### 4.1 Security Scan
**Agent**: Security SAgent

**Input**: Implemented feature

**Process**:
1. Run dependency scan
2. Static analysis security
3. Dynamic analysis
4. OWASP Top 10 check

**Output**:
- Security audit report
- Vulnerability list by severity
- Remediation plan

#### 4.2 Performance Validation
**Agent**: Performance SAgent

**Input**: Implemented feature

**Process**:
1. Run performance audit
2. Measure Core Web Vitals
3. Identify bottlenecks
4. Compare against budget

**Output**:
- Performance report
- Bottleneck analysis
- Optimization recommendations

#### 4.3 Accessibility Check
**Agent**: Accessibility SAgent

**Input**: Implemented feature

**Process**:
1. Run automated tests
2. WCAG 2.1 AA validation
3. Keyboard navigation test
4. Screen reader test

**Output**:
- Accessibility report
- Violation list
- Fix recommendations

#### 4.4 Final Code Review
**Agent**: Critic SAgent

**Input**: All QA reports

**Process**:
1. Review all fixes applied
2. Verify no new issues
3. Final approval

**Output**:
- Final approval or issue list

#### 4.5 Merge to Main
**Agent**: Git Master SAgent

**Input**: Approved code + all gates passed

**Process**:
1. Create pull request
2. Wait for CI/CD
3. Merge to main
4. Delete feature branch

**Output**:
- Feature merged
- Main branch updated

---

### Phase 5: Deployment

#### 5.1 Deployment Strategy
**Agent**: Deployment SAgent

**Input**: Merged feature + release decision

**Process**:
1. Select deployment strategy
2. Create deployment plan
3. Prepare rollback plan

**Output**:
- Deployment plan
- Rollback strategy

#### 5.2 Health Checks Setup
**Agent**: Health Checks SAgent

**Input**: Deployment plan

**Process**:
1. Define health check endpoints
2. Configure monitoring
3. Set alert thresholds

**Output**:
- Health check configuration
- Alert rules

#### 5.3 Deployment Execution
**Agent**: Deployment SAgent

**Input**: Deployment plan + green health

**Process**:
1. Build production artifact
2. Deploy to staging
3. Run smoke tests
4. Deploy to production
5. Monitor health

**Output**:
- Deployment completed
- Release notes

#### 5.4 Monitoring
**Agent**: Monitoring SAgent

**Input**: Deployed feature

**Process**:
1. Monitor metrics (24h)
2. Track error rates
3. Validate business metrics
4. Alert on anomalies

**Output**:
- Monitoring dashboard
- Incident alerts (if any)

#### 5.5 Release Tagging
**Agent**: Git Master SAgent

**Input**: Successful deployment

**Process**:
1. Create version tag
2. Generate release notes
3. Push tags to remote

**Output**:
- Release tag created
- Release published

---

## Quality Gates

### Pre-Commit Gate
**Owner**: Lint SAgent + Critic SAgent

**Checks**:
- [ ] Lint passes
- [ ] Format correct
- [ ] Type check passes
- [ ] No critical issues

**Action**: Block commit if failed

### Pre-Merge Gate
**Owner**: Testing SAgent + Security SAgent

**Checks**:
- [ ] All tests pass
- [ ] Coverage >80%
- [ ] Security scan clean
- [ ] Performance within budget
- [ ] Accessibility compliant

**Action**: Block merge if failed

### Pre-Deploy Gate
**Owner**: Deployment SAgent

**Checks**:
- [ ] All pre-merge gates passed
- [ ] Smoke tests pass
- [ ] Rollback plan ready
- [ ] Monitoring configured

**Action**: Block deployment if failed

### Post-Deploy Gate
**Owner**: Monitoring SAgent

**Checks**:
- [ ] Health checks pass (5 min)
- [ ] Error rate <1% (30 min)
- [ ] Metrics normal (24h)

**Action**: Auto-rollback if failed

---

## Offline-First Operation

### When Offline Detected
**Agent**: Git Master SAgent

**Actions**:
1. Enable offline-first mode
2. Queue commits locally
3. Continue development
4. Create backup bundle

### When Connection Restored
**Agent**: Git Master SAgent

**Actions**:
1. Detect connection
2. Sync queued operations
3. Resolve conflicts
4. Report sync status

---

## Learning System

### After Each Workflow
**Agent**: All agents

**Process**:
1. Document lessons learned
2. Store patterns in bugs-fixed/
3. Update agent knowledge
4. Improve workflows

### Continuous Improvement
**Agent**: Improver SAgent

**Process**:
1. Analyze workflow efficiency
2. Identify bottlenecks
3. Suggest improvements
4. Update documentation

---

## Communication Protocol

### Agent-to-Agent
- Clear task descriptions
- Include context and constraints
- Specify expected output
- Set quality standards

### Agent-to-User
- Regular progress updates
- Blocker alerts
- Quality gate results
- Next steps

### Escalation Path
1. Agent attempts auto-fix
2. Agent alerts user if blocked
3. Prides Agent coordinates resolution
4. User makes decision if needed

---

## Metrics & Reporting

### Velocity Metrics
- Tasks completed per sprint
- Cycle time per task
- Blocker frequency

### Quality Metrics
- Defect density
- Test coverage trend
- Security vulnerability count

### Performance Metrics
- Build time
- Deployment frequency
- Mean time to recovery (MTTR)
