---
name: start-sprint
description: Create a complete feature implementation from requirements to deployment. Use {{args}} to specify the feature request.
---

# Development Workflow

**Feature Request:** {{args}}

## Instructions

Call the `@prides` multi-agent system to coordinate the complete feature development lifecycle:

### Phase 1: Planning & Requirements

1.1. Check if the project is existing one or new one
1.2. If new one ask for clarification and start the full workflow
1.3. If existing one ask for clarification and start the implementation workflow
1.4. Brainstorm and refine the feature concept
2. Generate product requirements document
3. Break down into actionable tasks
4. Create branches (features, devs, main)

### Phase 2: Design & Prototyping

1. Design specification and user experience
2. Create visual prototype (Stitch integration)

### Phase 3: Implementation

1. Implement the feature
2. Code quality check (apply auto-fixes)
3. Deep code review for issues

### Phase 4: Quality Assurance

1. Run tests
2. Performance validation
3. WCAG compliance check

### Phase 5: Deployment

1. Execute deployment strategy

## Quality Gates

- **Pre-Commit**: Lint, format, type check
- **Pre-Merge**: Tests, security, performance, accessibility
- **Pre-Deploy**: All gates + smoke tests + rollback readiness
- **Post-Deploy**: Health checks, metrics validation

## Output

Generate comprehensive reports for each phase and maintain documentation in the folders:

- Roadmap: Analysis, prd, tasks, plan
- .dev_notes : bug fixed, summary, deploy, etc
