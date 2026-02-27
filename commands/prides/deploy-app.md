---
name: deploy-app
description: Deploy application to specified environment with zero-downtime strategy. Use {{args}} to specify environment (development, staging, production) or leave empty for interactive selection.
---

# Application Deployment

**Target Environment:** {{args}}

## Instructions

Execute deployment to the specified environment following the zero-downtime deployment strategy.

### Environment Selection

| Environment | Use Case | Auto-Rollback |
|-------------|----------|---------------|
| **development** | Development testing | Manual |
| **staging** | Pre-production validation | Automatic |
| **production** | Live user traffic | Automatic + Health checks |

### Pre-Deployment Gates

**ALL gates must pass before deployment:**

1. **Code Quality Gate**
   - @lint-sagent: All linting passes
   - Type check: No type errors

2. **Testing Gate**
   - Unit tests: >80% coverage, 100% pass
   - Integration tests: 100% pass
   - E2E tests: Critical paths pass

3. **Security Gate**
   - @security-sagent: Zero critical vulnerabilities
   - Dependency scan: No known vulnerabilities
   - Secrets scan: No exposed secrets

4. **Performance Gate**
   - @performance-sagent: No regressions
   - Load test: Meets requirements
   - Bundle size: Within limits

5. **Accessibility Gate**
   - @accessibility-sagent: WCAG 2.1 AA compliant
   - No critical violations

### Deployment Strategy

#### For Production:
1. @deployment-sagent: Create deployment plan and deploy
2. @monitoring-sagent: Real-time health monitoring

#### For Staging:
1. Build and deploy to staging
2. Run smoke tests
3. Generate deployment report

#### For Development:
1. Build and deploy to development
2. Basic health check only

### Health Checks

**Immediate (0-5 minutes):**
- Application starts successfully
- All endpoints respond
- Database connections healthy
- Cache systems operational

**Short-term (5-30 minutes):**
- Error rates within threshold (<1%)
- Response times acceptable (<500ms p95)
- Resource usage normal
- No memory leaks detected

**Long-term (30+ minutes):**
- Business metrics stable
- User reports normal
- Logs show no anomalies

### Rollback Triggers

**Automatic rollback if:**
- Health check fails within 5 minutes
- Error rate >5% in first 10 minutes
- Critical endpoint failures
- Database connection failures
- Memory leak detected

### Post-Deployment

1. @monitoring-sagent: Continuous monitoring (24h)
2. @documentation-sagent: Update deployment logs

## Output

Provide deployment report:
- Environment deployed to
- Version/tag deployed
- Deployment duration
- Health check results
- Monitoring dashboard links
- Rollback instructions
- Team notification status
