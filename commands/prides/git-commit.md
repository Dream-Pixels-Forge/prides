---
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
1. **Git Master SAgent**: Analyze staged changes
2. **Git Master SAgent**: Generate intelligent commit message based on:
   - File types changed
   - Function/class names modified
   - Code diff analysis
   - Conventional commit standards

### Pre-Commit Checks
Before committing, ensure:
1. **Lint SAgent**: Code passes all linting rules
2. **Testing SAgent**: Relevant tests pass
3. **Type Check**: TypeScript/types pass validation

### Commit Execution
1. Stage all relevant files (if not already staged)
2. Create commit with generated/provided message
3. Follow offline-first mode if no internet connection
4. Queue for sync when connection restored

### Post-Commit
1. Push to remote (if online)
2. Update task tracking
3. Generate commit report

## Output

Provide:
- Commit hash
- Commit message used
- Files changed summary
- Push status (if applicable)
- Any warnings or issues
