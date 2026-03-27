---
description: Initialize a new project with PRIDES multi-agent development system. Creates folder structure, runs skills inventory, sets up context, initializes decision log, configures quality gates, and activates monitoring. Use {{args}} for optional project name.
---

# PRIDES Project Initialization

**Input:** {{args}}

## Overview

This command initializes a new project with the complete PRIDES (Prototype. Review. Implement. Deploy. Extend. Secure) multi-agent development system. It sets up all necessary infrastructure for intelligent automation, quality gates, and agent coordination.

---

## Execution Workflow

### Step 1: Verify/Create PRIDES Folder Structure

**Action:** Check and create the mandatory PRIDES directory structure

```
@{D:\AI\DREAM-PIXELS-FORGE\MVP\EXTENSIONS\QWEN\prides\}
```

**Required Folders:**
- `agents/` - Agent definitions and configurations
- `commands/prides/` - PRIDES command library
- `workflows/` - Workflow definitions
- `skills/` - Project-specific skills
- `templates/` - Document and code templates
- `mandatory_docs/` - Core documentation
- `bugs-fixed/` - Learning system patterns
- `decision-log/` - Architectural decisions (ADR)
- `quality-gates/` - Quality configuration
- `monitoring/` - Monitoring and metrics setup

**Verification:**
- [ ] All folders exist
- [ ] Write permissions confirmed
- [ ] No conflicting files

---

### Step 2: Run Skills Inventory Workflow

**Action:** Execute skills inventory to identify available capabilities

**Process:**
1. Scan `@{skills/}` directory for available skills
2. Check installed MCP servers configuration
3. Map skills to agent capabilities
4. Generate skills manifest

**Output File:** `@{skills/SKILLS-INVENTORY.md}`

**Skills Categories (45 total):**
- **Design & UI (10):** shadcn-ui, frontend-design, ui-ux-pro-max, design-md, stitch-loop, react-components, gravity-ui-uikit, heroui, vanguard-uikit, sendbird-uikit-react
- **3D & Motion (6):** after-effects-scripts-master, blender-add-on-master, cinema4d-master, foundry-nuke-master, sidefx-houdini-guru, remotion
- **AI & Video (2):** ai-video-generation, enhance-prompt
- **Development (8):** nextjs, react-three-uikit, electron, tauri, tailwindcss, postcss, python-master, cra-to-next-migration
- **Search & Research (7):** code-search, company-search, people-search, financial-report-search, research-paper-search, personal-site-search, x-search
- **Agent & Workflow (5):** find-skills, skill-creator, create-agent-skills, create-subagents, agentation
- **MCP & Integration (2):** mcp-builder, figma-api-master
- **Quality & Best Practices (4):** vercel-react-best-practices, vercel-composition-patterns, systematic-debugging, audit-website
- **Database & Backend (1):** supabase-postgres-best-practices
- **Content & Media (1):** notebooklm-youtube-skill
- **Web Design (1):** web-design-guidelines

**Verification:**
- [ ] Skills inventory completed
- [ ] MCP servers detected
- [ ] Capability mapping complete

---

### Step 3: Setup Project Context

**Action:** Initialize project context files for agent coordination

**Files Created:**

1. **Project Brief:** `@{mandatory_docs/PROJECT-BRIEF.md}` - Project overview, goals, stakeholders, success metrics, technical stack
2. **Agent Configuration:** `@{.qwen/PRIDES-AGENTS.md}` - Active agents list, preferences (proactivity, quality gates, offline-first)
3. **Context Cache:** `@{.qwen/CONTEXT-CACHE.md}` - Architecture patterns, coding standards, design system references, learning history

**Verification:**
- [ ] Project brief created
- [ ] Agent configuration set
- [ ] Context cache initialized

---

### Step 4: Initialize Decision Log (ADR)

**Action:** Create Architectural Decision Record (ADR) system

**Folder:** `@{decision-log/}`

**Files Created:**
- **Template:** `@{decision-log/ADR-TEMPLATE.md}` - Standard ADR template (Status, Context, Decision, Consequences, Date, Authors, Reviewers)
- **Initial ADR:** `@{decision-log/ADR-001-project-initialization.md}` - Documents PRIDES adoption decision, benefits, and trade-offs

**Verification:**
- [ ] Decision log folder created
- [ ] ADR template available
- [ ] Initial ADR recorded

---

### Step 5: Configure Quality Gates

**Action:** Setup comprehensive quality gates for pre-commit, pre-merge, and pre-deploy

**Folder:** `@{quality-gates/}`

**Configuration Files:**

1. **Pre-Commit Gate:** `@{quality-gates/pre-commit-gate.md}` - Lint, format, type check, @critic-sagent review. Blocks commit on errors.
2. **Pre-Merge Gate:** `@{quality-gates/pre-merge-gate.md}` - All tests pass, coverage >80%, security clean, performance OK, accessibility compliant. Blocks merge on any failure.
3. **Pre-Deploy Gate:** `@{quality-gates/pre-deploy-gate.md}` - All pre-merge gates passed, smoke tests, rollback plan ready, monitoring configured. Manual approval for production.
4. **Post-Deploy Gate:** `@{quality-gates/post-deploy-gate.md}` - Health checks pass (5 min), error rate <1% (30 min), metrics normal (24h). Auto-rollback on critical failures.

**Verification:**
- [ ] All quality gate files created
- [ ] Enforcement rules defined
- [ ] Rollback procedures documented

---

### Step 6: Activate Monitoring

**Action:** Setup monitoring and alerting infrastructure

**Folder:** `@{monitoring/}`

**Configuration Files:**

1. **Metrics Dashboard:** `@{monitoring/METRICS-DASHBOARD.md}` - Development velocity, quality metrics, agent performance. Real-time dashboard with daily/weekly reports.
2. **Alert Configuration:** `@{monitoring/ALERT-CONFIG.md}` - Critical (immediate), Warning (daily digest), Info (weekly report). Multi-channel notifications.
3. **Health Checks:** `@{monitoring/HEALTH-CHECKS.md}` - Application (readiness/liveness), Agent health, Infrastructure health. Checks every 30s-5min.

**Verification:**
- [ ] Metrics dashboard configured
- [ ] Alert rules defined
- [ ] Health checks established

---

### Step 7: Generate Initialization Report

**Action:** Create comprehensive initialization report

**Output File:** `@{PRIDES-INIT-REPORT.md}`

**Report Contents:**
- **Initialization Summary:** Folder structure, skills inventory, context setup, decision log, quality gates, monitoring
- **Quality Baseline:** Test coverage, accessibility, performance, security targets
- **Next Steps:** Day 1 (goals, environment), Week 1 (first story, coverage), Month 1 (80% coverage, audit, optimization)
- **Checklists:** Development readiness, team onboarding, infrastructure
- **Quick Start:** All `/prides:*` commands and agent reference

**Verification:**
- [ ] Report generated at `@{PRIDES-INIT-REPORT.md}`
- [ ] All sections complete
- [ ] Quick start guide included

---

## Success Criteria

✅ **All folders created** - PRIDES directory structure verified
✅ **Skills inventoried** - All 45 skills mapped and documented
✅ **Context established** - Project brief, agent config, context cache created
✅ **Decision log active** - ADR system ready with initial decision
✅ **Quality gates configured** - Pre-commit, pre-merge, pre-deploy, post-deploy defined
✅ **Monitoring enabled** - Metrics, alerts, health checks operational
✅ **Report generated** - Comprehensive report at `@{PRIDES-INIT-REPORT.md}`

---

## Post-Initialization Checklist

### ✅ Verify System Ready
```bash
/prides:new-feature "Test feature"  # Test commands
@prides-agent - Status check         # Verify agents
ls quality-gates/                    # Check gates
ls monitoring/                       # Verify monitoring
```

### ✅ Team Onboarding
- [ ] Review `@{PRIDES-INIT-REPORT.md}`
- [ ] Understand quality gate requirements
- [ ] Familiarize with agent capabilities
- [ ] Setup development environment

### ✅ First Development Cycle
- [ ] Create first feature with `/prides:new-feature`
- [ ] Follow complete PRIDES workflow
- [ ] Pass all quality gates
- [ ] Deploy successfully

---

## 🎉 Confirmation: Ready for Development

**The PRIDES multi-agent development system is fully initialized and operational.**

You can now:
- Use all `/prides:*` commands
- Invoke specialized agents (@critic-sagent, @coder-sagent, etc.)
- Enforce quality gates automatically
- Monitor development metrics
- Leverage intelligent automation

**Start your first feature:** `/prides:new-feature "Your first feature description"`
