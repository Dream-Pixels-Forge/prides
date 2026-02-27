---
name: security-audit
description: Perform comprehensive security audit including vulnerability scanning, threat analysis, and security best practices validation. Use {{args}} to specify audit scope (quick, full, compliance).
---

# Security Audit

**Audit Scope:** {{args}}

## Instructions

Execute comprehensive security audit following OWASP standards and industry best practices.

### Audit Scopes

| Scope | Coverage | Duration | Use Case |
|-------|----------|----------|----------|
| **quick** | Critical vulnerabilities only | ~15 min | Pre-deployment check |
| **full** | Complete security analysis | ~1 hour | Regular audit |
| **compliance** | Full + compliance checks | ~2 hours | Regulatory requirements |

### Phase 1: Automated Scanning

1. @security-sagent: Run automated scans

**Dependency Scan:**
- Check for known vulnerabilities (npm audit, pip audit)
- Review dependency licenses
- Identify outdated packages
- Check for malicious packages

**Static Analysis:**
- Run security linters
- Check for hardcoded secrets
- Identify insecure patterns
- Review authentication code

**Dynamic Analysis:**
- Test running application
- Check for injection vulnerabilities
- Test authentication/authorization
- Validate input sanitization

### Phase 2: OWASP Top 10 Analysis

| Vulnerability | Check | Status |
|---------------|-------|--------|
| **A01: Broken Access Control** | Authorization checks, privilege escalation | 🔴🟡🟢 |
| **A02: Cryptographic Failures** | Encryption, hashing, TLS | 🔴🟡🟢 |
| **A03: Injection** | SQL, NoSQL, XSS, command injection | 🔴🟡🟢 |
| **A04: Insecure Design** | Design flaws, missing controls | 🔴🟡🟢 |
| **A05: Security Misconfiguration** | Server config, CORS, headers | 🔴🟡🟢 |
| **A06: Vulnerable Components** | Outdated dependencies | 🔴🟡🟢 |
| **A07: Auth Failures** | Session management, MFA | 🔴🟡🟢 |
| **A08: Data Integrity** | Data validation, tampering | 🔴🟡🟢 |
| **A09: Logging Failures** | Log injection, sensitive data | 🔴🟡🟢 |
| **A10: SSRF** | Server-side request forgery | 🔴🟡🟢 |

### Phase 3: Deep Analysis

#### Authentication & Authorization
- Password policies
- Session management
- Multi-factor authentication
- OAuth implementation
- JWT security
- Role-based access control

#### Data Protection
- Encryption at rest
- Encryption in transit
- Key management
- Secret storage
- PII handling
- Data retention

#### Input Validation
- SQL injection prevention
- XSS prevention
- CSRF protection
- File upload security
- API rate limiting
- Input sanitization

#### Infrastructure Security
- HTTPS enforcement
- Security headers
- CORS configuration
- Cookie security
- CSP implementation
- Server hardening

### Phase 4: Threat Modeling

1. @security-sagent: Identify threats
   - Asset identification
   - Trust boundaries
   - Threat enumeration (STRIDE)
   - Risk assessment

### Phase 5: Remediation

1. @security-sagent: Prioritize fixes
   - Critical: Fix immediately
   - High: Fix within 24h
   - Medium: Fix within 1 week
   - Low: Fix within 1 month

### Compliance Checks (if compliance scope)

| Standard | Requirements | Status |
|----------|--------------|--------|
| **GDPR** | Data protection, consent, right to erasure | ✅❌ |
| **HIPAA** | PHI protection, audit logs | ✅❌ |
| **PCI DSS** | Payment data handling | ✅❌ |
| **SOC 2** | Security controls | ✅❌ |

### Security Checklist

- [ ] No hardcoded secrets
- [ ] All dependencies updated
- [ ] HTTPS enforced
- [ ] Security headers configured
- [ ] Input validation implemented
- [ ] Authentication secure
- [ ] Authorization enforced
- [ ] Logging configured (no sensitive data)
- [ ] Rate limiting enabled
- [ ] CORS configured correctly
- [ ] CSP implemented
- [ ] Cookies secure (HttpOnly, Secure, SameSite)

### Documentation

1. @documentation-sagent: Security documentation

## Output

Provide security audit report:
- Executive summary
- Vulnerabilities found (by severity)
- OWASP Top 10 status
- Compliance status
- Remediation plan
- Risk assessment
- Next audit date
