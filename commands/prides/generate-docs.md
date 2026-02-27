---
description: Generate comprehensive technical documentation including API docs, README, component docs, and user guides. Use {{args}} to specify documentation type or scope.
---

# Technical Documentation Generation

**Documentation Scope:** {{args}}

## Instructions

Generate comprehensive technical documentation for the project.

### Documentation Types

| Type | Description | Auto-Detect |
|------|-------------|-------------|
| **API Documentation** | API endpoints, parameters, responses | Yes |
| **README** | Project overview, setup, usage | Yes |
| **Component Docs** | React/Vue component documentation | Yes |
| **User Guides** | End-user documentation | No |
| **Architecture** | System architecture documentation | No |
| **All** | Generate all documentation | Yes |

### Pre-Documentation Analysis

1. **Documentation Agent**: Analyze codebase
   - Scan source files
   - Identify undocumented components
   - Check documentation drift
   - Assess coverage gaps

2. **Information Gathering**
   - Read existing documentation
   - Analyze code structure
   - Extract type definitions
   - Review commit history

### Documentation Generation

#### API Documentation
- Extract endpoint definitions
- Document request/response schemas
- Include authentication requirements
- Add usage examples
- Generate OpenAPI/Swagger spec

#### README Documentation
- Project description
- Installation instructions
- Quick start guide
- Configuration options
- Usage examples
- Contributing guidelines

#### Component Documentation
- Component purpose
- Props/parameters
- Events emitted
- Slots (if applicable)
- Usage examples
- Accessibility notes

#### User Guides
- Step-by-step tutorials
- Feature documentation
- Troubleshooting sections
- FAQ generation
- Best practices

### Quality Standards

| Standard | Requirement |
|----------|-------------|
| **Accuracy** | All examples must be tested and working |
| **Completeness** | Document all public APIs |
| **Clarity** | Clear, concise language |
| **Consistency** | Follow documentation templates |
| **Accessibility** | WCAG compliant documentation |

### Post-Generation

1. **Documentation Agent**: Review generated docs
   - Verify accuracy
   - Check completeness
   - Ensure consistency

### Documentation Templates

Use templates from `/templates/documentation/`:
- `api-reference.md`
- `component-doc.md`
- `readme-template.md`
- `user-guide.md`
- `architecture.md`

## Output

Provide documentation report:
- Documentation types generated
- Files created/updated
- Coverage percentage
- Drift issues identified
- Next review date
