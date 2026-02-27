---
description: Create a complete feature implementation from requirements to deployment. Use {{args}} to specify the feature request.
---

# Development Workflow

**Feature Request:** {{args}}

## Instructions

Coordinate the complete feature development lifecycle through the Prides multi-agent system:

### Phase 1: Planning & Requirements

1. **Idea Agent**: Brainstorm and refine the feature concept
2. **PRD Doc Agent**: Generate product requirements document
3. **Tasks Agent**: Break down into actionable tasks
4. **Git Master Agent**: Create branches (features, devs, main)

### Phase 2: Design & Prototyping

1. **UI/UX Agent**: Design specification and user experience
2. **Prototyper Agent**: Create visual prototype (Stitch integration)

### Phase 3: Implementation

1. **Coder Agent**: Implement the feature
2. **Lint Agent**: Code quality check (apply auto-fixes)
3. **Critic Agent**: Deep code review for issues

### Phase 4: Quality Assurance

1. **Testing Agent**: Run tests
2. **Performance Agent**: Performance validation
3. **Accessibility Agent**: WCAG compliance check

### Phase 5: Deployment

1. **Deployment Agent**: Execute deployment strategy

## Quality Gates

- **Pre-Commit**: Lint, format, type check
- **Pre-Merge**: Tests, security, performance, accessibility
- **Pre-Deploy**: All gates + smoke tests + rollback readiness
- **Post-Deploy**: Health checks, metrics validation

## Output

Generate comprehensive reports for each phase and maintain documentation in the project roadmap.
