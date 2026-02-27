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
1. Delegate to **git-master-sagent** Subagents to analyze staged changes and generate commit message

### Pre-Commit Checks
Before committing, ensure:
1. Delegate to **lint-sagent** Subagents: Code passes all linting rules
2. **Type Check**: TypeScript/types pass validation

### Commit Execution
1. Stage all relevant files (if not already staged)
2. Create commit with generated/provided message

### Post-Commit
1. Push to remote (if online)
2. Generate commit report

## Output

Provide:
- Commit hash
- Commit message used
- Files changed summary
- Push status (if applicable)
- Any warnings or issues
