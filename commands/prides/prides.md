---
description: Create a complete feature implementation from requirements to deployment. Use {{args}} to specify the feature request.
---

# Development Workflow

**Feature Request:** {{args}}

## Instructions

Coordinate the complete feature development lifecycle through the Prides multi-agent system:

### Phase 1: Planning & Requirements

1. @idea-sagent: Brainstorm and refine the feature concept
2. @prd-doc-sagent: Generate product requirements document
3. @tasks-sagent: Break down into actionable tasks
4. @git-master-sagent: Create branches (features, devs, main)

### Phase 2: Design & Prototyping

1. @ui-ux-sagent: Design specification and user experience
2. @prototyper-sagent: Create visual prototype (Stitch integration)

### Phase 3: Implementation

1. @coder-sagent: Implement the feature
2. @lint-sagent: Code quality check (apply auto-fixes)
3. @critic-sagent: Deep code review for issues

### Phase 4: Quality Assurance

1. @testing-sagent: Run tests
2. @performance-sagent: Performance validation
3. @accessibility-sagent: WCAG compliance check

### Phase 5: Deployment

1. @deployment-sagent: Execute deployment strategy

## Quality Gates

- **Pre-Commit**: Lint, format, type check
- **Pre-Merge**: Tests, security, performance, accessibility
- **Pre-Deploy**: All gates + smoke tests + rollback readiness
- **Post-Deploy**: Health checks, metrics validation

## Output

Generate comprehensive reports for each phase and maintain documentation in the project roadmap.
