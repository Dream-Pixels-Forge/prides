---
description: Create a complete feature implementation from requirements to deployment. Use {{args}} to specify the feature request.
---

# New Feature Development Workflow

**Feature Request:** {{args}}

## Instructions

Coordinate the complete feature development lifecycle through the Prides multi-agent system:

### Phase 1: Planning & Requirements
1. **Idea SAgent**: Brainstorm and refine the feature concept
2. **Analyst SAgent**: Conduct market research and competitor analysis
3. **PRD Doc SAgent**: Generate product requirements document
4. **Plan SAgent**: Create detailed implementation plan
5. **Tasks SAgent**: Break down into actionable tasks
6. **Git Master SAgent**: Create feature branch

### Phase 2: Design & Prototyping
1. **UI/UX SAgent**: Design specification and user experience
2. **Prototyper SAgent**: Create visual prototype (Stitch integration)
3. **Git Master SAgent**: Commit design assets

### Phase 3: Implementation
1. **Coder SAgent**: Implement the feature
2. **Lint SAgent**: Code quality check (apply auto-fixes)
3. **Critic SAgent**: Deep code review for issues
4. **Git Master SAgent**: Commit code (offline mode if needed)

### Phase 4: Quality Assurance
1. **Testing SAgent**: Run security scan and tests
2. **Performance SAgent**: Performance validation
3. **Accessibility SAgent**: WCAG compliance check
4. **Critic SAgent**: Final code review
5. **Git Master SAgent**: Merge to main (all gates passed)

### Phase 5: Deployment
1. **Deployment SAgent**: Execute deployment strategy
2. **Health Checks SAgent**: Validate all systems
3. **Monitoring SAgent**: Metrics validation
4. **Git Master SAgent**: Create release tag

## Quality Gates

- **Pre-Commit**: Lint, format, type check
- **Pre-Merge**: Tests, security, performance, accessibility
- **Pre-Deploy**: All gates + smoke tests + rollback readiness
- **Post-Deploy**: Health checks, metrics validation

## Output

Generate comprehensive reports for each phase and maintain documentation in the project roadmap.
