---
description: Create a complete feature implementation from requirements to deployment. Use {{args}} to specify the feature request.
---

# Development Workflow

**Feature Request:** {{args}}

## Instructions

Coordinate the complete feature development lifecycle through the Prides multi-agent system:

### Phase 1: Planning & Requirements

1. Delegate to **idea-sagent** Subagents to brainstorm and refine the feature concept
2. Delegate to **prd-doc-sagent** Subagents to generate product requirements document
3. Delegate to **tasks-sagent** Subagents to break down into actionable tasks
4. Delegate to **git-master-sagent** Subagents to create branches (features, devs, main)

### Phase 2: Design & Prototyping

1. Delegate to **ui-ux-sagent** Subagents for design specification and user experience
2. Delegate to **prototyper-sagent** Subagents to create visual prototype (Stitch integration)

### Phase 3: Implementation

1. Delegate to **coder-sagent** Subagents to implement the feature
2. Delegate to **lint-sagent** Subagents for code quality check (apply auto-fixes)
3. Delegate to **critic-sagent** Subagents for deep code review for issues

### Phase 4: Quality Assurance

1. Delegate to **testing-sagent** Subagents to run tests
2. Delegate to **performance-sagent** Subagents for performance validation
3. Delegate to **accessibility-sagent** Subagents for WCAG compliance check

### Phase 5: Deployment

1. Delegate to **deployment-sagent** Subagents to execute deployment strategy

## Quality Gates

- **Pre-Commit**: Lint, format, type check
- **Pre-Merge**: Tests, security, performance, accessibility
- **Pre-Deploy**: All gates + smoke tests + rollback readiness
- **Post-Deploy**: Health checks, metrics validation

## Output

Generate comprehensive reports for each phase and maintain documentation in the project roadmap.
