# Multi-Agent Development System P.R.I.D.E.S

**Prototype. Review. Implement. Deploy. Extend. Secure**

## Executive Summary

This document outlines a comprehensive **Multi-Agent Development System** that orchestrates a swarm of specialized AI agents to automate and enhance software development workflows. The system provides intelligent automation for the entire development lifecycle, from project initialization through deployment, security, and maintenance.

**Key Benefits:**

- **10x faster** development cycles through intelligent automation
- **90% reduction** in manual repetitive tasks
- **Predictive issue detection** before problems reach production
- **Seamless offline-first** operation with smart sync
- **Enterprise-grade** quality, security, and accessibility compliance

### PRIDES.md Folder System

The **PRIDES.md** folder serves as the project's central knowledge hub, maintaining real-time context and decision tracking across all development activities:

| File | Purpose |
|------|---------|
| **project-context.md** | Core project information, goals, tech stack, and architecture overview |
| **agent-coordination.md** | Active agents, task assignments, and coordination state |
| **active-workflow.md** | Current workflow phase, progress, and next steps |
| **decision-log.md** | Key architectural and implementation decisions with rationale |
| **quality-gates.md** | Quality standards, checklists, and compliance status |
| **skills-inventory.md** | Available skills, capabilities, and usage tracking |

**Benefits:**
- **Persistent Context** - Project knowledge survives session restarts
- **Decision Transparency** - All major decisions documented with rationale
- **Workflow Visibility** - Real-time view of active development phases
- **Skills Optimization** - Automatic routing to best-suited agents and skills
- **Quality Assurance** - Continuous tracking of quality gate compliance

---

## Quick Start

### Using Commands

```bash
# Initialize a new project
/prides:init-project "Project Name"

# Start a new feature development
/prides:new-feature "Add user authentication with social login"

# Commit changes
/prides:git-commit "feat: add OAuth2 authentication"

# Run tests
/prides:run-tests "all"

# Deploy to production
/prides:deploy-app "production"

# Debug an issue
/prides:debug-issue "Users cannot reset password, error 500"

# Generate documentation
/prides:generate-docs "API documentation"

# Optimize performance
/prides:optimize-performance "bundle"

# Security audit
/prides:security-audit "full"

# Improve accessibility
/prides:improve-accessibility "keyboard"
```

### PRIDES.md Management

```bash
# View project context
@prides-agent View project-context.md

# Check active workflow
@prides-agent What's the current workflow phase?

# Review decision log
@prides-agent Show recent architectural decisions

# Check skills inventory
@prides-agent What skills are available for this task?
```

### Using Agents Directly

```
@prides-agent - Central orchestrator for complex workflows
@critic-sagent - Deep code review (MUST USE before commit)
@coder-sagent - Full-stack implementation
@plan-sagent - Implementation planning
@tasks-sagent - Task management and prioritization
@idea-sagent - Brainstorming and idea refinement
@ui-ux-sagent - UI/UX design guidance
@testing-sagent - Test generation and execution
@git-master-sagent - Version control operations
```

---

## System Overview

### Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                           Prides Agent                          │
│                    (Central Coordinator)                        │
└─────────────────────────────────────────────────────────────────┘
                              │
                    ┌─────────┴─────────┐
                    │                   │
                    ▼                   ▼
            ┌───────────────┐   ┌───────────────┐
            │ Critic SAgent │   │ Idea SAgent   │
            │  (Review)     │   │ (Brainstorm)  │
            └───────────────┘   └───────────────┘
                    │                   │
        ┌───────────┼───────────┬───────┘
        │           │           │
        ▼           ▼           ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│ Git Master   │ │Planning-Docs │ │Quality-Sec   │
│ SAgent       │ │ SAgents      │ │ SAgents      │
│              │ │              │ │              │
│ • Version    │ │ • Plan       │ │ • Testing    │
│   Control    │ │ • Tasks      │ │ • Security   │
│ • Offline    │ │ • Idea       │ │ • Performance│
│ • Sync       │ │ • Analyst    │ │ • Lint       │
│ • Branches   │ │ • PRD Doc    │ │ • Access.    │
│              │ │ • Docs       │ │ • Critic     │
└──────────────┘ └──────────────┘ └──────────────┘
        │           │                   │
        ▼           ▼                   ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│Development   │ │ Support      │ │ Deployment   │
│SAgents       │ │ SAgents      │ │ SAgents      │
│              │ │              │ │              │
│ • Coder      │ │ • Docs       │ │ • Deployment │
│ • UI/UX      │ │ • Improvement│ │ • Monitoring │
│ • Prototyper │ │ • Enhancer   │ │ • Rollback   │
│ • Debugger   │ │ • Refiner    │ │ • CI/CD      │
└──────────────┘ └──────────────┘ └──────────────┘
```

---

## Command Reference

### Command Format

All commands follow the Qwen Code Markdown format with YAML frontmatter:

```markdown
---
description: Clear description of what the command does
---

# Command content with {{args}} for parameter injection
```

### Available Commands

| Command | Description | Parameters |
|---------|-------------|------------|
| `/prides:init-project` | Initialize new project with PRIDES.md folder | Project name |
| `/prides:new-feature` | Create complete feature implementation | Feature request |
| `/prides:git-commit` | Commit with intelligent message | Optional message |
| `/prides:run-tests` | Run comprehensive test suites | Test scope |
| `/prides:deploy-app` | Deploy to environment | Environment name |
| `/prides:debug-issue` | Debug and diagnose issues | Issue description |
| `/prides:generate-docs` | Generate technical documentation | Doc type |
| `/prides:optimize-performance` | Analyze and optimize performance | Focus area |
| `/prides:security-audit` | Security vulnerability scan | Audit scope |
| `/prides:improve-accessibility` | WCAG compliance improvements | Focus area |

### Parameter Injection

Use `{{args}}` for user-provided parameters:

```bash
# Parameter appended to prompt
/prides:new-feature "Add dark mode toggle"

# No parameter
/prides:run-tests
```

---

## Agent Capabilities

### Terminology

| Term | Definition |
|------|------------|
| **Agent** | Primary agent that can be invoked directly |
| **SAgent** | Sub-agent used for specialized tasks (delegated via `task` tool) |
| **PROACTIVELY** | Agent should be used automatically without explicit request |
| **MUST BE USED** | Critical agent that must be invoked for specific scenarios |

### Core Workflow Agents

| Agent | File | Primary Function | Smart Features |
|-------|------|-----------------|----------------|
| **Prides** | `prides-agent.md` | Project orchestration | Proactivity, smart detection, predictive issues, context caching, learning system, **skills awareness**, **PRIDES.md management**, **decision logging** |
| **Git Master** | `git-master-sagent.md` | Version control | Offline-first, auto-sync, branch management, conflict resolution |
| **Plan** | `plan-sagent.md` | Implementation planning | Adaptive planning, milestone tracking, risk assessment, effort estimation |
| **Tasks** | `tasks-sagent.md` | Task management | Dependency detection, bottleneck alerts, auto-prioritization (WSJF) |
| **Idea** | `idea-sagent.md` | Brainstorming | Idea refinement, transform vague ideas into clear requirements |

### Analysis & Documentation Agents

| Agent | File | Primary Function | Smart Features |
|-------|------|-----------------|----------------|
| **Analyst** | `analyst-sagent.md` | Market research | Competitor auto-research, sentiment analysis, feature gap analysis |
| **PRD Doc** | `prd-sagent.md` | Requirements | Auto-PRD generation, requirements validation, ambiguity detection |
| **Documentation** | `documentation-sagent.md` | Technical docs | Auto-doc from code, drift detection, coverage tracking |

### Development Agents

| Agent | File | Primary Function | Smart Features |
|-------|------|-----------------|----------------|
| **Coder** | `coder-sagent.md` | Implementation | Pattern compliance, UI/UX coordination, self-verification |
| **Debugger** | `debugger-sagent.md` | Bug diagnosis | Root cause analysis, UI styling debugging, fix coordination |
| **UI/UX** | `ui-ux-sagent.md` | Design guidance | Token-first handoff, modern principles, domain patterns |
| **Prototyper** | `prototyper-sagent.md` | Visual prototypes | Stitch integration, React transformation, archive management |
| **Critic** | `critic-sagent.md` | Deep code analysis | **MUST USE** before commit, prevents hallucinations, finds similar issues |

### Quality & Security Agents

| Agent | File | Primary Function | Smart Features |
|-------|------|-----------------|----------------|
| **Testing** | `testing-sagent.md` | QA automation | Auto-test generation, coverage prediction, failure prediction |
| **Security** | `security-sagent.md` | Security analysis | Threat prediction, auto-vulnerability scanning, anomaly detection |
| **Performance** | `performance-sagent.md` | Optimization | Auto-profiling, bottleneck prediction, regression detection |
| **Lint** | `lint-sagent.md` | Code quality | Auto-fix coordination, complexity analysis, debt calculation |
| **Accessibility** | `accessibility-sagent.md` | WCAG compliance | Auto-audit, violation prediction, auto-fix generation |

### Improvement Agents

| Agent | File | Primary Function | Smart Features |
|-------|------|-----------------|----------------|
| **Improvement** | `improvement-sagent.md` | Code enhancement | Smart refactoring, auto-suggestions, debt reduction |
| **Improver** | `improver-sagent.md` | Agent auditing | Accuracy scoring, approach correction, continuous improvement |

### Deployment & Operations

| Agent | File | Primary Function | Smart Features |
|-------|------|-----------------|----------------|
| **Deployment** | `deployment-sagent.md` | Release management | Smart strategy selection, rollback prediction, health checks |
| **Monitoring** | `monitoring-sagent.md` | Production monitoring | Real-time metrics, anomaly detection, alerting |
| **CI/CD** | `cicd-sagent.md` | Pipeline automation | Build automation, deployment pipelines |
| **Rollback** | `rollback-sagent.md` | Rollback procedures | Automatic rollback, health-based triggers |
| **Accessibility** | WCAG compliance | Auto-audit, violation prediction, auto-fix generation |

### Improvement Agents

| Agent | Primary Function | Smart Features |
|-------|-----------------|----------------|
| **Improvement** | Code enhancement | Smart refactoring, auto-suggestions, debt reduction |
| **Improver** | Agent auditing | Accuracy scoring, approach correction, continuous improvement |

### Deployment & Operations

| Agent | Primary Function | Smart Features |
|-------|-----------------|----------------|
| **Deployment** | Release management | Smart strategy selection, rollback prediction, health checks |

---

## Smart Features

### 1. Predictive Intelligence

| Capability | Description | Benefit |
|------------|-------------|---------|
| **Failure Prediction** | Predicts test failures, deployment issues, performance regressions | Catch problems before they occur |
| **Bottleneck Detection** | Identifies agent overload, task blockers, scaling limits | Prevent delays and outages |
| **Risk Assessment** | Evaluates security, quality, and deployment risks | Make informed decisions |
| **Trend Forecasting** | Projects quality trends, technical debt, velocity | Plan proactively |

### 2. Automation Capabilities

| Capability | Description | Benefit |
|------------|-------------|---------|
| **Auto-Test Generation** | Creates unit, integration, and E2E tests from code | 70% reduction in test writing time |
| **Auto-Documentation** | Generates API docs, component docs, README from code | Docs stay synchronized |
| **Auto-Fix Application** | Applies safe lint fixes, accessibility fixes, improvements | 45% of issues fixed automatically |
| **Auto-Deployment** | Executes deployment pipelines with health checks | Zero-downtime releases |
| **Auto-Critic** | Automatically critic the codes produced | Zero issues, clean codes |

### 3. Offline-First Operation

| Capability | Description | Benefit |
|------------|-------------|---------|
| **Local Queuing** | Queues commits, docs, and operations offline | Work continues without internet |
| **Smart Sync** | Automatically syncs when connection restored | No manual intervention needed |
| **Conflict Detection** | Predicts and resolves sync conflicts | Prevent data loss |
| **Backup & Recovery** | Creates backup bundles of pending work | Protect against data loss |

### 4. Quality Gates

| Gate | Checks | Enforcement |
|------|--------|-------------|
| **Pre-Commit** | Lint, format, type check | Block commit if failed |
| **Pre-Merge** | Tests, security, performance, accessibility | Block merge if failed |
| **Pre-Deploy** | All gates + smoke tests + rollback readiness | Block deployment if failed |
| **Post-Deploy** | Health checks, metrics validation | Auto-rollback if failed |

### 5. Skills Awareness

| Capability | Description | Benefit |
|------------|-------------|---------|
| **Auto-Discovery** | Scans `skills/` directory on initialization | All available skills automatically registered |
| **Skills Routing** | Routes tasks to agents with appropriate skills | Optimal skill utilization for each task |
| **Usage Tracking** | Tracks skill effectiveness and usage patterns | Continuous improvement of skill selection |
| **Skills Guidance** | Suggests relevant skills for current task | Discover capabilities you didn't know existed |

### 6. Skills Capabilities

All agents use corresponding available skills in the skills directory combined with mcp servers. The system includes **46+ specialized skills** covering:

- **Design & UI** - shadcn-ui, frontend-design, ui-ux-pro-max, design-md, stitch-loop
- **3D & Motion** - After Effects, Blender, Cinema 4D, Houdini, Nuke
- **Development** - Next.js, React, Tailwind, Tauri, Electron, Python
- **Research** - Company search, people search, code search, financial reports, academic papers
- **AI & Video** - AI video generation, prompt enhancement, skill creation

---

## Project Structure

```
prides/
├── qwen-extension.json         # Extension configuration (v2.0.0)
├── QWEN.md                    # This context and documentation
├── README.md                  # Extension overview
├── PRIDES.md/                 # Project knowledge hub (NEW in v2.0)
│   ├── project-context.md     # Core project information and goals
│   ├── agent-coordination.md  # Active agents and task assignments
│   ├── active-workflow.md     # Current workflow phase and progress
│   ├── decision-log.md        # Architectural decisions with rationale
│   ├── quality-gates.md       # Quality standards and compliance status
│   └── skills-inventory.md    # Available skills and usage tracking
├── commands/prides/           # Command files (Markdown format)
│   ├── init-project.md        # Project initialization workflow
│   ├── new-feature.md         # Feature development workflow
│   ├── git-commit.md          # Intelligent commit generation
│   ├── run-tests.md           # Comprehensive test execution
│   ├── deploy-app.md          # Zero-downtime deployment
│   ├── debug-issue.md         # Issue debugging and diagnosis
│   ├── generate-docs.md       # Technical documentation
│   ├── optimize-performance.md # Performance optimization
│   ├── security-audit.md      # Security vulnerability scan
│   └── improve-accessibility.md # WCAG compliance
├── agents/                    # Agent definitions (Markdown + YAML)
│   ├── prides-agent.md        # Central orchestrator
│   ├── Development/
│   │   ├── coder-sagent.md
│   │   ├── ui-ux-sagent.md
│   │   ├── debugger-sagent.md
│   │   └── prototyper-sagent.md
│   ├── Quality-Security/
│   │   ├── critic-sagent.md   # MUST USE before commit
│   │   ├── testing-sagent.md
│   │   ├── security-sagent.md
│   │   ├── performance-sagent.md
│   │   ├── lint-sagent.md
│   │   └── accessibility-sagent.md
│   ├── Planning-Docs/
│   │   ├── plan-sagent.md
│   │   ├── tasks-sagent.md
│   │   ├── idea-sagent.md
│   │   ├── analyst-sagent.md
│   │   └── prd-sagent.md
│   ├── Deployment/
│   │   ├── deployment-sagent.md
│   │   ├── monitoring-sagent.md
│   │   └── rollback-sagent.md
│   ├── Support-Improvements/
│   │   ├── documentation-sagent.md
│   │   └── improvement-sagent.md
│   └── Git-master/
│       └── git-master-sagent.md
├── templates/                 # Template library
│   ├── feature-template.md
│   ├── readme-template.md
│   ├── api-reference-template.md
│   ├── component-doc-template.md
│   └── test-plan-template.md
├── skills/                   # Extension skills (46+ available)
│   ├── Design & UI/
│   │   ├── shadcn-ui/
│   │   ├── frontend-design/
│   │   ├── ui-ux-pro-max/
│   │   ├── design-md/
│   │   └── stitch-loop/
│   ├── 3D & Motion/
│   │   ├── after-effects-scripts-master/
│   │   ├── blender-add-on-master/
│   │   ├── cinema4d-master/
│   │   ├── sidefx-houdini-guru/
│   │   └── foundry-nuke-master/
│   ├── Development/
│   │   ├── nextjs/
│   │   ├── react-components/
│   │   ├── tailwindcss/
│   │   ├── tauri/
│   │   └── electron/
│   ├── Research/
│   │   ├── company-search/
│   │   ├── people-search/
│   │   ├── code-search/
│   │   └── research-paper-search/
│   └── AI & Video/
│       ├── ai-video-generation/
│       ├── enhance-prompt/
│       └── skill-creator/
├── bugs-fixed/              # Learning system
│   └── (patterns stored here)
└── mandatory_docs/          # Core documentation
    ├── workflow-coordination.md
    ├── quality-standards.md
    └── agent-specifications.md
```

### File Format Standards

**Commands** (`.md` with YAML frontmatter):
```markdown
---
description: Clear description. Use {{args}} to specify input.
---

# Command content

**Input:** {{args}}
```

**Agents** (`.md` with YAML frontmatter):
```markdown
---
name: agent-name
description: When and how to use this agent
tools:
  - read_file
  - write_file
---

System prompt content...
```

**Templates** (`.md` with placeholders):
```markdown
# {{Title}}

{{Description}}

## Section
- [ ] {{Item}}
```

### Terminology

| Term | Definition |
|------|------------|
| **Agent** | Primary agent that can be invoked directly |
| **SAgent** | Sub-agent used for specialized tasks (delegated via `task` tool) |

---

## Workflow Examples

### Example 1: New Feature Development

```
┌─────────────────────────────────────────────────────────────────┐
│ Phase 1: Planning & Requirements                                │
├─────────────────────────────────────────────────────────────────┤
│ 1. Prides → Idea SAgent: Brainstorm                             |
│ 2. Prides → Analyst SAgent: Market analysis                     |
│ 2. Prides → PRD Doc SAgent: Requirements document               │
│ 3. Prides → Plan SAgent: Implementation plan                    │
│ 4. Prides → Tasks SAgent: Task breakdown                        │
│ 5. Git Master SAgent: Create feature branch                     │
└─────────────────────────────────────────────────────────────────┘
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│ Phase 2: Design & Prototyping                                   │
├─────────────────────────────────────────────────────────────────┤
│ 1. Prides → UI/UX Agent: Design specification                   │
│ 2. Prides → Prototyper Agent: Visual prototype                  │
│ 3. Git Master SAgent: Commit design assets                      │
└─────────────────────────────────────────────────────────────────┘
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│ Phase 3: Implementation                                         │
├─────────────────────────────────────────────────────────────────┤
│ 1. Prides → Coder  SAgent: Implement feature                    │
│ 2. Lint SAgent: Code quality check (auto-fix applied)           | 
│ 3. Critic SAgent: Deep check code are free of issues            |
│ 4. Git Master SAgent: Commit code (offline mode if needed)      │
└─────────────────────────────────────────────────────────────────┘
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│ Phase 4: Quality Assurance                                      │
├─────────────────────────────────────────────────────────────────┤
│ 1. Testing SAgent: Security scan                                │
│ 3. Performance SAgent: Performance validation                   │
│ 4. Accessibility SAgent: WCAG compliance check                  |
│ 3. Critic SAgent: Deep check code are free of issues            |
│ 5. Git Master SAgent: Merge to main (all gates passed)          │
└─────────────────────────────────────────────────────────────────┘
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│ Phase 5: Deployment                                             │
├─────────────────────────────────────────────────────────────────┤
│ 1. Deployment SAgent: Execute deployment strategy               │
│ 2. Health checks SAgent: All pass                               │
│ 3. Monitoring SAgent: Metrics validated                         │
│ 4. Git Master SAgent: Create release tag                        │
└─────────────────────────────────────────────────────────────────┘
```

### Example 2: Bug Fix Workflow

```
1. User reports bug
         │
         ▼
2. Prides → Debugger SAgent: Diagnose root cause
         │
         ▼
3. Debugger SAgent → Coder SAgent: Implement fix
         │
         ▼
4. Testing SAgent: Run regression tests
         │
         ▼
5. Security SAgent: Validate no security impact
         │
         ▼
6. Critic SAgent: Deep check code are free of issues 
         │
         ▼
7. Git Master SAgent: Create hotfix branch, merge to main
         │
         ▼
8. Deployment SAgent: Deploy hotfix (priority deployment)
```

### Example 3: Offline Development Session

```
1. User starts work (offline detected by Git Master)
         │
         ▼
2. Git Master SAgent: Enable offline-first mode
         │
         ▼
3. Coder SAgent: Implement features
         │
         ▼
4. Critic SAgent: Deep check code are free of issues
         │
         ▼
5. Git Master SAgent: Queue commits locally
         │
         ▼
6. Documentation SAgent: Generate docs (queued for sync)
         │
         ▼
7. Testing SAgent: Run tests locally
         │
         ▼
8. Connection restored
         │
         ▼
9. Git Master SAgent: Auto-sync all queued operations
         │
         ▼
10. Sync report: 12 commits, 3 branches, 1 merge synced
```

### Example 4: Project Initialization

```
┌─────────────────────────────────────────────────────────────────┐
│ Step 1: Run Initialization Command                              │
├─────────────────────────────────────────────────────────────────┤
│ User: /prides:init-project "My Awesome Project"                 │
│                                                                 │
│ Prides Agent:                                                  │
│   ✓ Analyzing project requirements                              │
│   ✓ Setting up project structure                                │
│   ✓ Creating PRIDES.md folder                                   │
└─────────────────────────────────────────────────────────────────┘
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│ Step 2: PRIDES.md Folder Creation                               │
├─────────────────────────────────────────────────────────────────┤
│ Creating: PRIDES.md/project-context.md                          │
│   - Project name, goals, vision                                 │
│   - Tech stack selection                                        │
│   - Architecture overview                                       │
│                                                                 │
│ Creating: PRIDES.md/agent-coordination.md                       │
│   - Initial agent assignments                                   │
│   - Task coordination state                                     │
│                                                                 │
│ Creating: PRIDES.md/active-workflow.md                          │
│   - Current phase: Initialization                               │
│   - Next steps defined                                          │
│                                                                 │
│ Creating: PRIDES.md/decision-log.md                             │
│   - Initial architecture decisions                              │
│   - Technology choices documented                               │
│                                                                 │
│ Creating: PRIDES.md/quality-gates.md                            │
│   - Quality standards configured                                │
│   - Checklists initialized                                      │
│                                                                 │
│ Creating: PRIDES.md/skills-inventory.md                         │
│   - Scanning skills/ directory (46 skills found)                │
│   - Skills categorized and indexed                              │
│   - Usage tracking initialized                                  │
└─────────────────────────────────────────────────────────────────┘
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│ Step 3: Skills Discovery & Configuration                        │
├─────────────────────────────────────────────────────────────────┤
│ Skills Auto-Discovered:                                         │
│   • Design & UI (5 skills)                                      │
│   • 3D & Motion (5 skills)                                      │
│   • Development (5 skills)                                      │
│   • Research (4 skills)                                         │
│   • AI & Video (3 skills)                                       │
│   • And 24+ more specialized skills                             │
│                                                                 │
│ MCP Servers Configured:                                         │
│   ✓ git - Version control operations                            │
│   ✓ filesystem - File operations                                │
│   ✓ github - GitHub integration (optional)                      │
│   ✓ playwright - E2E testing (optional)                         │
└─────────────────────────────────────────────────────────────────┘
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│ Step 4: Ready for Development                                   │
├─────────────────────────────────────────────────────────────────┤
│ ✓ Project initialized successfully                              │
│ ✓ PRIDES.md folder created with 6 core files                    │
│ ✓ 46+ skills available and indexed                              │
│ ✓ Quality gates configured                                      │
│ ✓ Agent coordination ready                                      │
│                                                                 │
│ Next Steps:                                                     │
│   /prides:new-feature "Your first feature"                      │
│   @prides-agent What can I build?                               │
│   View PRIDES.md/* files for project context                    │
└─────────────────────────────────────────────────────────────────┘
```

---

## Best Practices

### Command Best Practices

Following official Qwen Code documentation:

| Practice | Recommended | Avoid |
|----------|-------------|-------|
| **Format** | Markdown with YAML frontmatter | TOML (deprecated) |
| **Parameters** | Use `{{args}}` for injection | Relying on default appending |
| **File References** | Use `@{file path}` | Hardcoding file content |
| **Shell Commands** | Instruct agents to run commands | Direct `!{command}` execution |
| **Description** | Always provide clear description | Auto-generated descriptions |
| **Organization** | Namespaced directories | All commands in root |

### Sub-Agent Best Practices

Following official Qwen Code documentation:

| Practice | Recommended | Avoid |
|----------|-------------|-------|
| **Specialization** | Single, clear responsibility | Multiple unrelated capabilities |
| **Description** | Clear when/how to use | Vague, generic descriptions |
| **Tools** | Only necessary tools | All tools "just in case" |
| **System Prompt** | Specific expertise + workflow | Generic assistant language |
| **Proactivity** | Use "PROACTIVELY" in description | Waiting for explicit requests |
| **Naming** | Descriptive, unique names | Generic names like "helper" |

### Code Quality Best Practices

| Practice | Standard |
|----------|----------|
| **Zero Tolerance** | No mockups, placeholders, TODOs |
| **Type Safety** | Full TypeScript, no `any` |
| **Error Handling** | Comprehensive, user-friendly |
| **Testing** | >80% coverage, meaningful tests |
| **Security** | OWASP Top 10 protected |
| **Accessibility** | WCAG 2.1 AA compliant |
| **Performance** | Core Web Vitals "Good" |

### Workflow Best Practices

| Phase | Key Practice |
|-------|--------------|
| **Initialization** | Run `/prides:init-project` to set up PRIDES.md folder and skills inventory |
| **Planning** | Always use Plan SAgent PROACTIVELY |
| **Implementation** | Coder SAgent follows patterns |
| **Review** | Critic SAgent MUST be used before commit |
| **Testing** | Testing SAgent creates tests automatically |
| **Deployment** | All quality gates must pass |

### Quality Gate Checklist

**Pre-Commit:**
- [ ] Lint passes
- [ ] Format correct
- [ ] Type check passes
- [ ] Critic SAgent review complete

**Pre-Merge:**
- [ ] All tests pass
- [ ] Coverage >80%
- [ ] Security scan clean
- [ ] Performance within budget
- [ ] Accessibility compliant

**Pre-Deploy:**
- [ ] All pre-merge gates passed
- [ ] Smoke tests pass
- [ ] Rollback plan ready
- [ ] Monitoring configured

**Post-Deploy:**
- [ ] Health checks pass (5 min)
- [ ] Error rate <1% (30 min)
- [ ] Metrics normal (24h)

---

## References

### Official Documentation
- [Qwen Code Commands](https://qwenlm.github.io/qwen-code-docs/en/users/features/commands/)
- [Qwen Code Sub-Agents](https://qwenlm.github.io/qwen-code-docs/en/users/features/sub-agents/)
- [Qwen Code MCP Servers](https://qwenlm.github.io/qwen-code-docs/en/users/features/mcp/)
- [Qwen Code Skills](https://qwenlm.github.io/qwen-code-docs/en/users/features/skills/)

### Mandatory Documentation
- [Workflow Coordination](mandatory_docs/workflow-coordination.md)
- [Quality Standards](mandatory_docs/quality-standards.md)
- [Agent Specifications](mandatory_docs/agent-specifications.md)
- [Skills Integration Guide](mandatory_docs/skills-integration-guide.md)
- [MCP Configuration](.dev_notes/MCP-CONFIG.md)

### Templates
- [Feature Template](templates/feature-template.md)
- [README Template](templates/readme-template.md)
- [API Reference Template](templates/api-reference-template.md)
- [Component Doc Template](templates/component-doc-template.md)
- [Test Plan Template](templates/test-plan-template.md)

### Skills Library

#### Design & UI
- **shadcn-ui** - Component integration and customization
- **frontend-design** - Production-grade interfaces
- **ui-ux-pro-max** - 50 styles, 21 palettes, 50 font pairings
- **design-md** - Design documentation (DESIGN.md)
- **stitch-loop** - Stitch prototyping
- **react-components** - React patterns and conversion

#### Development
- **vercel-react-best-practices** - React performance optimization
- **vercel-composition-patterns** - Component architecture
- **mcp-builder** - MCP server creation
- **python-master** - Python development

#### Search & Research
- **code-search** - Code pattern search
- **company-search** - Company research
- **people-search** - Expert identification
- **financial-report-search** - SEC filings, earnings
- **research-paper-search** - Academic papers
- **personal-site-search** - Blogs and portfolios

### MCP Servers

#### Core Servers
- **git** - Git operations (commit, branch, push, pull)
- **filesystem** - File operations (read, write, search)

#### Optional Servers
- **shadcn** - shadcn/ui component management
- **playwright** - E2E testing and browser automation
- **github** - GitHub operations (PRs, releases, tags)
- **netlify** - Netlify deployment
- **supabase** - Supabase database operations

---

**Version:** 0.4.0 | **Last Updated:** 2026-03-27 | **License:** See LICENSE
