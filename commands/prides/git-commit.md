---
name: git-commit
description: Commit staged changes with intelligent commit message generation. Use {{args}} for optional commit message or leave empty for auto-generation.
---

# Git Commit with Intelligent Message Generation

**Commit Message:** {{args}}

## Instructions

### If commit message is provided:
Use the provided message and ensure it follows conventional commit format:
- `feat:` for new features
- `fix:` for bug fixes
- `docs:` for documentation
- `style:` for formatting
- `refactor:` for code refactoring
- `test:` for tests
- `chore:` for maintenance

### If no commit message is provided:
1. @git-master-sagent: Analyze staged changes and generate commit message

### Pre-Commit Checks (MANDATORY)
Before committing, ALL must pass:
1. @lint-sagent: Code passes all linting rules
2. **Type Check**: TypeScript/types pass validation
3. **@critic-sagent: MUST review code before commit** (MUST BE USED - find all issues, prevent hallucinations)

### Critic Review Enforcement
**CRITICAL:** Do NOT commit without critic review
- @critic-sagent must complete review
- All critical/high issues must be resolved
- Document any accepted medium/low issues
- If critic finds issues: fix → re-review → commit

### Commit Execution
1. Stage all relevant files (if not already staged)
2. Verify all pre-commit checks passed
3. Create commit with generated/provided message

### Post-Commit
1. Push to remote (if online)
2. Generate commit report

## Output

Provide:
- Commit hash
- Commit message used
- Files changed summary
- Push status (if applicable)
- **Critic review status:** Pass/Fail with summary
- Any warnings or issues
