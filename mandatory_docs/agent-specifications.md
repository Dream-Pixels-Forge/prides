# Agent Specifications

## Overview

This document provides detailed specifications for all agents in the Prides multi-agent development system.

---

## Agent Taxonomy

### Core Orchestrator
- **Prides Agent**: Central coordinator

### Development Agents
- **Coder SAgent**: Full-stack implementation
- **UI/UX SAgent**: Design guidance
- **Prototyper SAgent**: Visual prototypes
- **Debugger SAgent**: Bug diagnosis

### Quality & Security Agents
- **Testing SAgent**: QA automation
- **Security SAgent**: Security analysis
- **Performance SAgent**: Optimization
- **Lint SAgent**: Code quality
- **Accessibility SAgent**: WCAG compliance
- **Critic SAgent**: Deep code analysis

### Planning & Documentation Agents
- **Plan SAgent**: Implementation planning
- **Tasks SAgent**: Task management
- **Idea SAgent**: Brainstorming
- **Analyst SAgent**: Market research
- **PRD Doc SAgent**: Requirements
- **Documentation SAgent**: Technical docs

### Deployment Agents
- **Deployment SAgent**: Release management
- **CI/CD SAgent**: Pipeline automation
- **Rollback SAgent**: Rollback procedures
- **Monitoring SAgent**: Production monitoring

### Support Agents
- **Git Master SAgent**: Version control
- **Improvement SAgent**: Code enhancement
- **Improver SAgent**: Agent auditing
- **Prompt Refiner SAgent**: Prompt optimization

---

## Agent Specifications

### Prides Agent

**File**: `agents/prides-agent.md`

**Role**: Central Orchestrator

**Responsibilities**:
- Coordinate all specialized agents
- Manage workflow execution
- Enforce quality gates
- Track progress across phases
- Predict and prevent issues

**When to Use**:
- Starting any complex workflow
- Need multi-agent coordination
- Quality gate enforcement required

**Tools**:
- `read_file`, `write_file`, `read_many_files`
- `run_shell_command`, `web_search`, `task`

---

### Critic SAgent

**File**: `agents/Quality-Security/critic-sagent.md`

**Role**: Deep Code Analysis

**Responsibilities**:
- Find all types of code issues
- Prevent hallucinated code
- Check for similar issues across codebase
- Suggest immediate corrections
- Deep pattern detection

**When to Use**:
- **MUST BE USED** before any commit
- **MUST BE USED** before any merge
- After any AI-generated code
- When reviewing complex logic

**Tools**:
- `read_file`, `write_file`, `read_many_files`
- `grep_search`, `glob`

**Output**:
- Issue report by severity
- Similar issues found
- Fix recommendations
- Prevention strategies

---

### Git Master SAgent

**File**: `agents/Git-master/git-master-sagent.md`

**Role**: Version Control Specialist

**Responsibilities**:
- Offline-first Git operations
- Branch management
- Intelligent commit messages
- Smart sync when online
- Conflict resolution

**When to Use**:
- Any Git operation needed
- Working offline
- Creating feature branches
- Preparing commits

**Tools**:
- `read_file`, `write_file`
- `run_shell_command`, `read_many_files`

**Output**:
- Branch status
- Commits made
- Sync status
- Conflict resolutions

---

### Plan SAgent

**File**: `agents/Planning-Docs/plan-sagent.md`

**Role**: Implementation Planning

**Responsibilities**:
- Create adaptive implementation plans
- Define milestones
- Assess risks
- Estimate effort
- Track progress

**When to Use**:
- **PROACTIVELY** before implementation
- Complex feature planning
- Timeline estimation needed
- Risk assessment required

**Tools**:
- `read_file`, `write_file`, `read_many_files`
- `web_search`, `task`

**Output**:
- Implementation plan document
- Task breakdown
- Milestone definitions
- Risk assessment

---

### Tasks SAgent

**File**: `agents/Planning-Docs/tasks-sagent.md`

**Role**: Task Management

**Responsibilities**:
- Dependency detection
- Bottleneck alerts
- WSJF prioritization
- Task tracking
- Critical path analysis

**When to Use**:
- After planning complete
- Need task prioritization
- Managing complex workflows
- Tracking progress

**Tools**:
- `read_file`, `write_file`, `read_many_files`

**Output**:
- Prioritized task board
- Dependency graph
- WSJF scores
- Bottleneck alerts

---

### Idea SAgent

**File**: `agents/Planning-Docs/idea-sagent.md`

**Role**: Brainstorming & Refinement

**Responsibilities**:
- Transform vague ideas into clear requirements
- Brainstorm creative solutions
- Feasibility analysis
- Define success criteria
- Prioritize features

**When to Use**:
- **PROACTIVELY** when requirements unclear
- Initial feature request vague
- Need creative solutions
- Requirements need refinement

**Tools**:
- `read_file`, `write_file`, `read_many_files`
- `web_search`, `task`

**Output**:
- Refined feature definition
- User stories
- Success metrics
- Prioritized features

---

### Coder SAgent

**File**: `agents/Development/coder-sagent.md`

**Role**: Full-Stack Implementation

**Responsibilities**:
- Implement features following patterns
- UI/UX coordination
- Self-verification
- Write tests
- Add documentation

**When to Use**:
- **PROACTIVELY** for any code implementation
- Building new features
- Modifying existing code
- Creating components

**Tools**:
- `read_file`, `write_file`, `read_many_files`
- `run_shell_command`, `glob`, `grep_search`

**Output**:
- Working implementation
- Tests included
- Documentation added
- Type definitions

---

### UI/UX SAgent

**File**: `agents/Development/ui-ux-sagent.md`

**Role**: Design Guidance

**Responsibilities**:
- Token-first design handoff
- Modern design principles
- Domain pattern expertise
- Accessibility requirements
- Responsive design

**When to Use**:
- New UI features
- Design system implementation
- Accessibility audit needed
- Responsive design challenges

**Tools**:
- `read_file`, `write_file`, `read_many_files`
- `web_search`

**Output**:
- Design token definitions
- Component specifications
- Accessibility requirements
- Implementation guidance

---

### Testing SAgent

**File**: `agents/Quality-Security/testing-sagent.md`

**Role**: QA Automation

**Responsibilities**:
- Auto-test generation
- Coverage prediction
- Failure prediction
- Run all test types
- Analyze coverage gaps

**When to Use**:
- **PROACTIVELY** for creating tests
- Running test suites
- Coverage analysis needed
- Test strategy planning

**Tools**:
- `read_file`, `write_file`, `read_many_files`
- `run_shell_command`, `glob`, `grep_search`

**Output**:
- Test files created
- Coverage report
- Failed test details
- Coverage gap analysis

---

## Agent Communication Protocol

### Delegation Pattern

```
Prides Agent (Coordinator)
    │
    ├──→ Idea SAgent (Refine requirements)
    ├──→ Plan SAgent (Create plan)
    ├──→ Tasks SAgent (Organize tasks)
    ├──→ Coder SAgent (Implement)
    ├──→ Critic SAgent (Review)
    ├──→ Testing SAgent (Test)
    └──→ Git Master SAgent (Commit)
```

### Communication Standards

**When delegating:**
1. Provide clear task description
2. Include relevant context
3. Specify expected output format
4. Set quality standards
5. Define acceptance criteria

**When reporting:**
1. Status update (progress/blocked/done)
2. Output delivered
3. Issues encountered
4. Help needed (if any)
5. Next steps

---

## Agent Selection Guide

### By Task Type

| Task Type | Primary Agent | Supporting Agents |
|-----------|---------------|-------------------|
| **New Feature** | Coder SAgent | Plan, Tasks, UI/UX, Testing, Critic |
| **Bug Fix** | Debugger SAgent | Coder, Testing, Critic |
| **Code Review** | Critic SAgent | Lint, Security |
| **Planning** | Plan SAgent | Idea, Tasks, Analyst |
| **Testing** | Testing SAgent | Coder (for fixes) |
| **Security** | Security SAgent | Critic, Lint |
| **Performance** | Performance SAgent | Coder, Testing |
| **Accessibility** | Accessibility SAgent | UI/UX, Testing |
| **Documentation** | Documentation SAgent | All agents (for input) |
| **Git Operations** | Git Master SAgent | None |
| **Design** | UI/UX SAgent | Prototyper, Coder |

### By Workflow Phase

| Phase | Primary Agents |
|-------|----------------|
| **Planning** | Idea, Analyst, PRD Doc, Plan, Tasks |
| **Design** | UI/UX, Prototyper |
| **Implementation** | Coder, Lint, Critic |
| **Testing** | Testing, Security, Performance, Accessibility |
| **Deployment** | Deployment, CI/CD, Monitoring |
| **Maintenance** | Git Master, Improvement, Documentation |

---

## Agent Quality Metrics

### Response Time

| Agent Type | Expected Response | Timeout |
|------------|-------------------|---------|
| **Orchestrator** | <30 seconds | 2 minutes |
| **Development** | <1 minute | 5 minutes |
| **Analysis** | <2 minutes | 10 minutes |
| **Testing** | <5 minutes | 30 minutes |

### Accuracy Targets

| Agent Type | Accuracy Target | Measurement |
|------------|-----------------|-------------|
| **Code Generation** | >95% | Tests passing |
| **Code Review** | >90% | Issues found/missed |
| **Planning** | >85% | Estimate vs actual |
| **Testing** | >90% | Bugs caught/prevented |

---

## Agent Learning System

### Knowledge Sources

| Source | Purpose | Location |
|--------|---------|----------|
| **Bugs Fixed** | Pattern learning | `bugs-fixed/` |
| **Templates** | Standard patterns | `templates/` |
| **Workflows** | Process learning | `mandatory_docs/` |
| **Quality Standards** | Quality rules | `mandatory_docs/` |

### Learning Process

1. **Capture**: Store patterns from completed work
2. **Analyze**: Identify successful patterns
3. **Generalize**: Create reusable templates
4. **Apply**: Use patterns in future work
5. **Refine**: Continuously improve patterns

---

## Agent Tool Access

### Tool Permissions

| Tool | Agents | Purpose |
|------|--------|---------|
| `read_file` | All | Read file contents |
| `write_file` | Most | Create/modify files |
| `read_many_files` | Most | Read multiple files |
| `run_shell_command` | Coder, Testing, Git Master, etc. | Execute commands |
| `glob` | Coder, Critic, Testing | Find files |
| `grep_search` | Critic, Testing | Search content |
| `web_search` | Prides, Analyst, Plan | Research |
| `task` | Prides, Plan | Delegate to sub-agents |

### Tool Usage Guidelines

**For file operations:**
- Always verify file exists before reading
- Backup before modifying critical files
- Use atomic writes when possible

**For shell commands:**
- Validate command safety
- Handle errors gracefully
- Capture output for analysis

**For searches:**
- Use specific patterns
- Limit scope when possible
- Handle no results gracefully
