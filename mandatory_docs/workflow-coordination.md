# Prides Workflow Coordination Guide

## Overview

This document describes the standard workflow for coordinating the Prides multi-agent development system.

---

## Phase 0: Project Initialization

### Overview

Initial phase that sets up project structure, context, and skills inventory before any development work begins.

**Owner:** Prides Agent

**Triggers:** New project, workspace change, manual command (`/prides:init`)

### 0.1 PRIDES.md Folder Setup

**Agent:** Prides Agent + Git Master SAgent

**Process:**

```xml
<setup>
  <check>PRIDES.md/ directory exists</check>
  <create-if-missing>
    - project-context.md
    - skills-inventory.md
    - decision-log.md
    - quality-gates.md
    - active-workflow.md
    - agent-coordination.md
  </create-if-missing>
  <initialize>
    <file>project-context.md</file>
    <template>templates/project-context-template.md</template>
  </initialize>
</setup>
```

**Output:** Complete PRIDES.md folder structure

### 0.2 Skills Inventory Workflow

**Agent:** Prides Agent

**Process:**

1. Run skills inventory workflow (see `workflows/skills-inventory.md`)
2. Scan `./skills/` directory
3. Parse each skill's SKILL.md for metadata
4. Build searchable inventory structure
5. Update PRIDES.md/skills-inventory.md

**Output:** Current skills inventory with metadata

### 0.3 Project Context Initialization

**Agent:** Prides Agent

**Process:**

```xml
<initialize>
  <extract>
    - Package.json metadata
    - Git remote URL
    - README.md content
    - Existing documentation
  </extract>
  <populate>
    <field>project-name</field>
    <field>description</field>
    <field>tech-stack</field>
    <field>repository</field>
  </populate>
</initialize>
```

**Output:** Populated project-context.md

### 0.4 Decision Log Setup

**Agent:** Prides Agent

**Process:**

1. Initialize decision log structure
2. Record initial architectural decisions
3. Set up decision tracking categories
4. Configure review schedule

**Output:** Ready decision-log.md

### 0.5 Quality Gates Configuration

**Agent:** Quality SAgents

**Process:**

1. Detect project type and requirements
2. Configure appropriate quality gates
3. Set thresholds based on project standards
4. Link to CI/CD if available

**Output:** Configured quality-gates.md

---

## Workflow Phases

### Phase 1: Planning & Requirements

#### Skills Awareness

**Skills Identification:**
- Identify required skills for planning tasks (analyst-sagent, prd-sagent, plan-sagent)
- Check skills inventory for relevant research capabilities
- Log skills assigned to this phase in agent-coordination.md

**Skills Usage Tracking:**
- Record which skills are invoked during planning
- Track skill effectiveness (quality of output, time saved)
- Note any skill gaps identified

**Skills Effectiveness Logging:**
- After phase completion, rate skill performance (1-5)
- Document skill combinations that worked well
- Record suggestions for skill improvement

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

#### Skills Awareness

**Skills Identification:**
- Identify UI/UX skills (ui-ux-pro-max, shadcn-ui, design-md, stitch-loop)
- Check skills inventory for design system capabilities
- Log skills assigned to this phase in agent-coordination.md

**Skills Usage Tracking:**
- Record which design skills are invoked
- Track skill effectiveness (design quality, consistency)
- Note skill gaps for specialized design needs

**Skills Effectiveness Logging:**
- Rate skill performance for design tasks (1-5)
- Document successful design skill combinations
- Record design pattern improvements

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

#### Skills Awareness

**Skills Identification:**
- Identify development skills (coder-sagent, vercel-react-best-practices, frontend-design)
- Check skills inventory for framework-specific capabilities
- Log skills assigned to this phase in agent-coordination.md

**Skills Usage Tracking:**
- Record which implementation skills are invoked
- Track skill effectiveness (code quality, development speed)
- Note skill gaps for specialized implementations

**Skills Effectiveness Logging:**
- Rate skill performance for implementation tasks (1-5)
- Document successful code pattern combinations
- Record code quality improvements from skill usage

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

#### Skills Awareness

**Skills Identification:**
- Identify quality skills (testing-sagent, security-sagent, performance-sagent, accessibility-sagent)
- Check skills inventory for QA and compliance capabilities
- Log skills assigned to this phase in agent-coordination.md

**Skills Usage Tracking:**
- Record which quality skills are invoked
- Track skill effectiveness (issues found, false positives)
- Note skill gaps for specialized testing needs

**Skills Effectiveness Logging:**
- Rate skill performance for QA tasks (1-5)
- Document successful quality skill combinations
- Record quality improvements from skill usage

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

#### Skills Awareness

**Skills Identification:**
- Identify deployment skills (deployment-sagent, monitoring-sagent, cicd-sagent)
- Check skills inventory for deployment platform capabilities
- Log skills assigned to this phase in agent-coordination.md

**Skills Usage Tracking:**
- Record which deployment skills are invoked
- Track skill effectiveness (deployment success, rollback frequency)
- Note skill gaps for specialized deployment needs

**Skills Effectiveness Logging:**
- Rate skill performance for deployment tasks (1-5)
- Document successful deployment skill combinations
- Record deployment reliability improvements

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

## Decision Logging

### Overview

Decision logging captures architectural, technical, and process decisions made throughout the development lifecycle. This ensures traceability and provides context for future decisions.

**Owner**: Prides Agent

**Storage**: `PRIDES.md/decision-log.md`

### When to Log Decisions

Log decisions when any of these thresholds are met:

**Architectural Decisions:**
- Technology or framework selection
- Major architectural pattern changes
- Database schema design
- API design decisions
- Security architecture choices

**Technical Decisions:**
- Library or dependency selection (impact >1 week)
- Performance optimization strategies
- Scaling approach decisions
- Integration pattern choices

**Process Decisions:**
- Workflow changes
- Quality gate threshold changes
- Agent coordination changes
- Tool selection

**Impact-Based Thresholds:**
- Effort estimate >3 days
- Affects multiple components
- Irreversible or hard-to-reverse
- Significant cost implication
- Security or compliance impact

### Decision Log Format

Use the format in `PRIDES.md/decision-log.md`:

```xml
<decision>
  <id>DEC-[XXX]</id>
  <title>Decision Title</title>
  <date>YYYY-MM-DD</date>
  <status>[Proposed|Under Review|Approved|Implemented|Superseded]</status>
  <decisionMaker>[Name/Agent]</decisionMaker>
  <stakeholders>[Names/Roles]</stakeholders>
  
  <context>
    [Situation requiring decision]
  </context>
  
  <problemStatement>
    [Clear problem statement]
  </problemStatement>
  
  <proposedSolution>
    [Proposed solution description]
  </proposedSolution>
  
  <alternativesConsidered>
    <alternative>
      <name>[Option A]</name>
      <description>[Description]</description>
      <pros>[Pros]</pros>
      <cons>[Cons]</cons>
    </alternative>
  </alternativesConsidered>
  
  <decisionRationale>
    [Why this decision was made]
  </decisionRationale>
  
  <consequences>
    <positive>[Benefits]</positive>
    <negative>[Trade-offs]</negative>
    <neutral>[Neutral outcomes]</neutral>
  </consequences>
  
  <implementationPlan>
    <step owner="[Owner]" due="[Date]">[Step 1]</step>
  </implementationPlan>
  
  <relatedDecisions>
    <decision ref="DEC-XXX">[Relationship]</decision>
  </relatedDecisions>
</decision>
```

### Review Process

**Scheduled Reviews:**

| Review Type | Frequency | Participants |
|-------------|-----------|--------------|
| **Architecture Review** | Bi-weekly | Tech Lead, Architects |
| **Technical Debt Review** | Monthly | Development Team |
| **Decision Quality Review** | Quarterly | Stakeholders |

**Review Checklist:**

```xml
<review>
  <check>Decision still valid?</check>
  <check>Implementation on track?</check>
  <check>Consequences as expected?</check>
  <check>Related decisions affected?</check>
  <check>Documentation updated?</check>
</review>
```

**Review Outcomes:**

- **Valid**: Decision stands, continue implementation
- **Needs Update**: Decision modified, log change
- **Superseded**: New decision replaces old, link both
- **Invalid**: Decision reversed, document lessons

### Implementation Tracking

**Track Implementation Status:**

| Status | Description | Action |
|--------|-------------|--------|
| **Not Started** | Decision approved, no work begun | Schedule implementation |
| **In Progress** | Implementation underway | Track progress |
| **Blocked** | Implementation blocked | Resolve blockers |
| **Complete** | Implementation done | Verify and close |
| **On Hold** | Implementation paused | Document reason |

**Link to Tasks:**

- Reference decision ID in task descriptions
- Link tasks in decision implementation plan
- Track task completion against decision timeline

**Verification:**

```xml
<verify>
  <check>Implementation matches decision?</check>
  <check>Tests validate decision?</check>
  <check>Documentation updated?</check>
  <check>Stakeholders informed?</check>
</verify>
```

---

## Quality Gates Integration

### Overview

Quality gates are integrated throughout all workflow phases to ensure consistent quality standards. This section documents which gates run in which phase and how to track results.

**Owner**: Quality SAgents

**Storage**: `PRIDES.md/quality-gates.md`

### Gate Distribution by Phase

```xml
<phaseGates>
  <phase number="0" name="Initialization">
    <gate name="Setup Validation">
      <check>PRIDES.md structure complete</check>
      <check>Skills inventory current</check>
      <check>Project context populated</check>
    </gate>
  </phase>
  
  <phase number="1" name="Planning">
    <gate name="Requirements Quality">
      <check>PRD complete and clear</check>
      <check>Acceptance criteria defined</check>
      <check>Dependencies identified</check>
    </gate>
  </phase>
  
  <phase number="2" name="Design">
    <gate name="Design Review">
      <check>Design tokens defined</check>
      <check>Accessibility requirements met</check>
      <check>Responsive design specified</check>
    </gate>
  </phase>
  
  <phase number="3" name="Implementation">
    <gate name="Pre-Commit">
      <check>Lint passes</check>
      <check>Format correct</check>
      <check>Type check passes</check>
      <check>Critic review complete</check>
    </gate>
  </phase>
  
  <phase number="4" name="Quality Assurance">
    <gate name="Pre-Merge">
      <check>All tests pass</check>
      <check>Coverage >80%</check>
      <check>Security scan clean</check>
      <check>Performance within budget</check>
      <check>Accessibility compliant</check>
    </gate>
  </phase>
  
  <phase number="5" name="Deployment">
    <gate name="Pre-Deploy">
      <check>All pre-merge gates passed</check>
      <check>Smoke tests pass</check>
      <check>Rollback plan ready</check>
      <check>Monitoring configured</check>
    </gate>
    <gate name="Post-Deploy">
      <check>Health checks pass (5 min)</check>
      <check>Error rate <1% (30 min)</check>
      <check>Metrics normal (24h)</check>
    </gate>
  </phase>
</phaseGates>
```

### Recording Results

**Result Format:**

```xml
<gateResult>
  <gate>[Gate Name]</gate>
  <phase>[Phase Number]</phase>
  <timestamp>YYYY-MM-DD HH:MM</timestamp>
  <status>[Pass|Fail|Warning]</status>
  <checkedBy>[Agent Name]</checkedBy>
  
  <checks>
    <check name="[Check Name]" status="[Pass|Fail]">
      <details>[Result details]</details>
      <duration>[X]s</duration>
    </check>
  </checks>
  
  <issues>
    <issue severity="[Critical|High|Medium|Low]">
      <description>[Issue description]</description>
      <resolution>[Fixed|Pending|Accepted]</resolution>
    </issue>
  </issues>
  
  <autoFixes>
    <fix type="[Fix Type]" count="[X]" status="[Applied]"/>
  </autoFixes>
</gateResult>
```

### Tracking Requirements

**Mandatory Tracking:**

| Requirement | Description | Storage |
|-------------|-------------|---------|
| **Gate Status** | Pass/Fail/Warning for each gate | quality-gates.md |
| **Check Results** | Individual check results with details | quality-gates.md |
| **Issues Found** | All issues with severity and status | quality-gates.md |
| **Auto-Fixes** | Automatic fixes applied | quality-gates.md |
| **Trends** | Gate results over time | quality-gates.md |

**Optional Tracking:**

| Requirement | Description | Benefit |
|-------------|-------------|---------|
| **Duration** | Time to complete each gate | Performance optimization |
| **Failure Rate** | Frequency of gate failures | Process improvement |
| **Agent Performance** | Which agents check gates | Agent optimization |

### Report Linking

**Link Gate Results To:**

```xml
<links>
  <link type="Commit" format="[Commit SHA](URL)">
    Pre-commit gate results link to commits
  </link>
  <link type="Pull Request" format="#[PR Number]">
    Pre-merge gate results link to PRs
  </link>
  <link type="Release" format="v[Version]">
    Pre-deploy gate results link to releases
  </link>
  <link type="Decision" format="DEC-[XXX]">
    Quality decisions link to decision log
  </link>
  <link type="Task" format="TASK-[XXX]">
    Quality tasks link to task board
  </link>
</links>
```

**Cross-Reference Format:**

In `quality-gates.md`:

```markdown
### Related

- **Commit:** [abc123](link)
- **PR:** #123
- **Release:** v1.2.3
- **Decision:** DEC-001
- **Task:** TASK-042
```

In linked documents:

```markdown
### Quality Gates

- **Pre-Commit:** ✅ Pass ([see details](quality-gates.md#pre-commit-gate))
- **Pre-Merge:** ✅ Pass ([see details](quality-gates.md#pre-merge-gate))
```

### Quality Metrics Dashboard

**Key Metrics:**

| Metric | Calculation | Target |
|--------|-------------|--------|
| **Gate Pass Rate** | (Passed Gates / Total Gates) × 100 | >95% |
| **First-Time Pass Rate** | (First-Time Passes / Total Gates) × 100 | >85% |
| **Auto-Fix Rate** | (Auto-Fixed Issues / Total Issues) × 100 | >40% |
| **Mean Time to Gate** | Average time per gate | <5 min |

**Trend Tracking:**

Track metrics weekly in `quality-gates.md`:

```markdown
### 7-Day Trend

| Date | Pre-Commit | Pre-Merge | Pre-Deploy | Post-Deploy |
|------|------------|-----------|------------|-------------|
| YYYY-MM-DD | ✅ | ✅ | ✅ | ✅ |
```

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
