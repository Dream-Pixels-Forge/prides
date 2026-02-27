# Skills Integration Guide

This guide explains how Prides agents use skills and MCP servers for enhanced capabilities.

---

## Overview

The Prides extension integrates with Qwen Code's **skills system** and **MCP servers** to provide specialized capabilities:

| Feature | Purpose | Example |
|---------|---------|---------|
| **Skills** | Specialized domain knowledge | `shadcn-ui`, `frontend-design`, `ui-ux-pro-max` |
| **MCP Servers** | External tool integration | Git, Filesystem, Playwright, Shadcn |
| **Agent Integration** | Combined capabilities | Coder SAgent uses skills + MCP for implementation |

---

## Available Skills

### Design & UI Skills

| Skill | File | Primary Use |
|-------|------|-------------|
| **shadcn-ui** | `skills/shadcn-ui/SKILL.md` | Component integration, customization |
| **frontend-design** | `skills/frontend-design/SKILL.md` | Production-grade interfaces |
| **ui-ux-pro-max** | `skills/ui-ux-pro-max/SKILL.md` | 50 styles, 21 palettes, 50 fonts, charts |
| **design-md** | `skills/design-md/SKILL.md` | Design documentation (DESIGN.md) |
| **stitch-loop** | `skills/stitch-loop/SKILL.md` | Stitch prototyping, React conversion |
| **react-components** | `skills/react-components/SKILL.md` | React patterns, Stitch conversion |

### Development Skills

| Skill | File | Primary Use |
|-------|------|-------------|
| **vercel-react-best-practices** | `skills/vercel-react-best-practices/SKILL.md` | React performance, server components |
| **vercel-composition-patterns** | `skills/vercel-composition-patterns/SKILL.md` | Component architecture, state patterns |
| **python-master** | `skills/python-master/SKILL.md` | Python development |
| **mcp-builder** | `skills/mcp-builder/SKILL.md` | MCP server creation |

### Search Skills

| Skill | File | Primary Use |
|-------|------|-------------|
| **code-search** | `skills/code-search/SKILL.md` | Code pattern search |
| **company-search** | `skills/company-search/SKILL.md` | Company research |
| **people-search** | `skills/people-search/SKILL.md` | People/expert research |
| **financial-report-search** | `skills/financial-report-search/SKILL.md` | Financial reports |
| **research-paper-search** | `skills/research-paper-search/SKILL.md` | Academic papers |
| **personal-site-search** | `skills/personal-site-search/SKILL.md` | Personal blogs/sites |
| **x-search** | `skills/x-search/SKILL.md` | Twitter/X search |

### Utility Skills

| Skill | File | Primary Use |
|-------|------|-------------|
| **enhance-prompt** | `skills/enhance-prompt/SKILL.md` | Prompt refinement |
| **find-skills** | `skills/find-skills/SKILL.md` | Discover available skills |
| **skill-creator** | `skills/skill-creator/SKILL.md` | Create new skills |
| **agentation** | `skills/agentation/SKILL.md` | Visual feedback toolbar |
| **ai-video-generation** | `skills/ai-video-generation/SKILL.md` | AI video creation |
| **remotion** | `skills/remotion/SKILL.md` | Video from code |

---

## Available MCP Servers

### Core Servers

| Server | Command | Purpose | Used By |
|--------|---------|---------|---------|
| **git** | `mcp-server-git` | Git operations | Git Master, Coder, Critic |
| **filesystem** | `@mcp/server-filesystem` | File operations | All agents |

### Optional Servers

| Server | Command | Purpose | Used By |
|--------|---------|---------|---------|
| **shadcn** | `mcp-server-shadcn` | shadcn/ui components | Coder, UI/UX |
| **playwright** | `@mcp/server-playwright` | E2E testing | Testing |
| **github** | `@mcp/server-github` | GitHub operations | Git Master, Deployment |
| **netlify** | `@mcp/server-netlify` | Netlify deployment | Deployment |
| **supabase** | `@mcp/server-supabase` | Supabase database | Backend operations |

---

## Agent-Skills Mapping

### Development Agents

#### Coder SAgent
```yaml
skills:
  - shadcn-ui         # PRIMARY: UI components
  - frontend-design   # Custom interfaces
  - react-components  # React patterns
  - ui-ux-pro-max     # Design system
  - vercel-react-best-practices  # Performance
  - vercel-composition-patterns  # Architecture
mcp-servers:
  - filesystem        # File operations
  - git              # Version control
  - shadcn           # Component installation
```

**Usage Example:**
```
"Use shadcn-ui skill to add a data table component"
"Use frontend-design skill to create a unique landing page"
"Apply vercel-react-best-practices to optimize this component"
```

#### UI/UX SAgent
```yaml
skills:
  - ui-ux-pro-max     # PRIMARY: Design intelligence
  - shadcn-ui         # Component design
  - frontend-design   # Custom UI
  - design-md         # Documentation
  - stitch-loop       # Prototyping
mcp-servers:
  - filesystem        # Design files
  - shadcn           # Component specs
```

**Usage Example:**
```
"Use ui-ux-pro-max skill to apply glassmorphism style"
"Use stitch-loop skill to create a prototype"
"Use design-md skill to document the design system"
```

### Quality & Security Agents

#### Critic SAgent
```yaml
skills:
  - code-search                    # Find patterns
  - vercel-react-best-practices   # React review
  - vercel-composition-patterns   # Architecture review
mcp-servers:
  - git              # Check changes
  - filesystem       # Read/write files
```

**Usage Example:**
```
"Use code-search skill to find all instances of this anti-pattern"
"Apply vercel-react-best-practices to review this component"
"Use git_diff MCP tool to see what changed"
```

#### Testing SAgent
```yaml
skills:
  - code-search                    # Test patterns
  - vercel-react-best-practices   # React testing
mcp-servers:
  - filesystem        # Test files
  - playwright        # E2E tests
```

**Usage Example:**
```
"Use playwright_navigate MCP tool for E2E testing"
"Use code-search skill to find existing test patterns"
"Use playwright_screenshot MCP tool for visual regression"
```

### Planning & Documentation Agents

#### Plan SAgent
```yaml
skills:
  - mcp-builder       # Custom tools
  - company-search    # Market research
  - people-search     # Expert identification
mcp-servers:
  - filesystem        # Plan docs
  - git              # History for estimates
```

**Usage Example:**
```
"Use company-search skill to research competitor features"
"Use people-search skill to find experts who solved this"
"Use mcp-builder skill to create estimation tool"
```

#### Git Master SAgent
```yaml
skills:
  - mcp-builder       # Git automation
mcp-servers:
  - git              # PRIMARY: Git operations
  - filesystem        # File operations
  - github           # PRs, releases
```

**Usage Example:**
```
"Use git_status MCP tool to check repository"
"Use git_commit MCP tool to commit changes"
"Use create_pull_request MCP tool to open PR"
```

---

## How to Use Skills in Agents

### Skill Invocation Syntax

Skills are invoked through natural language:

```
"Use [skill-name] skill to [action]"
"Apply [skill-name] skill for [purpose]"
```

### Example Workflows

#### 1. Implementing a UI Component

```
User: "Add a user data table with sorting"

Coder SAgent workflow:
1. "Use shadcn-ui skill to add the table component"
   → Installs shadcn table component
   
2. "Use shadcn-ui skill to add sorting functionality"
   → Adds sorting headers
   
3. "Use frontend-design skill to customize the styling"
   → Applies custom design
   
4. "Apply vercel-react-best-practices for optimization"
   → Optimizes rendering
```

#### 2. Creating a Landing Page

```
User: "Design a unique landing page"

UI/UX SAgent workflow:
1. "Use ui-ux-pro-max skill to select brutalism style"
   → Chooses design direction
   
2. "Use ui-ux-pro-max skill to apply color palette #7"
   → Sets color scheme
   
3. "Use frontend-design skill to create the hero section"
   → Implements distinctive design
   
4. "Use stitch-loop skill to prototype quickly"
   → Creates visual prototype
```

#### 3. Code Review

```
User: "Review this component for issues"

Critic SAgent workflow:
1. "Use code-search skill to find similar patterns"
   → Searches codebase
   
2. "Apply vercel-react-best-practices to check patterns"
   → Validates React usage
   
3. "Use vercel-composition-patterns to check state"
   → Reviews state management
   
4. "Use git_diff MCP tool to see recent changes"
   → Understands context
```

---

## MCP Server Configuration

### Setup

1. **Install MCP servers:**
```bash
# Git server
npm install -g mcp-server-git

# Shadcn server
npx mcp-server-shadcn

# Playwright server
npx @modelcontextprotocol/server-playwright

# GitHub server
npx @modelcontextprotocol/server-github
```

2. **Configure in `.qwen/settings.json`:**
```json
{
  "mcpServers": {
    "git": {
      "command": "mcp-server-git",
      "timeout": 30000
    },
    "shadcn": {
      "command": "npx",
      "args": ["-y", "mcp-server-shadcn"],
      "timeout": 30000
    },
    "playwright": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-playwright"],
      "timeout": 60000
    }
  }
}
```

3. **Set environment variables:**
```bash
# .env file
GITHUB_TOKEN=your_token
NETLIFY_API_KEY=your_key
SUPABASE_URL=your_url
```

---

## Best Practices

### Skill Usage

| Practice | Recommended | Avoid |
|----------|-------------|-------|
| **Specificity** | "Use shadcn-ui skill to add button" | "Use skill for UI" |
| **Combination** | Combine multiple skills | Single skill for complex tasks |
| **Context** | Provide context for skill | Vague instructions |
| **Verification** | Verify skill output | Assume skill worked |

### MCP Usage

| Practice | Recommended | Avoid |
|----------|-------------|-------|
| **Tool Selection** | Use appropriate MCP tool | Force wrong tool |
| **Error Handling** | Check MCP tool results | Ignore errors |
| **Permissions** | Minimal required access | Over-permissioned |
| **Timeout** | Set appropriate timeouts | Default timeouts |

### Combined Usage

```
✅ Good:
"Use shadcn-ui skill to add the dialog component, then use 
filesystem MCP write_file to customize the styles"

❌ Bad:
"Add a dialog" (too vague, doesn't specify skills/MCP)
```

---

## Troubleshooting

### Skill Not Found

```
Error: Skill 'xyz' not found

Solution:
1. Check skill exists in skills/ directory
2. Verify skill name in SKILL.md
3. Use find-skills skill to list available skills
```

### MCP Server Disconnected

```
Error: MCP server 'xyz' disconnected

Solution:
1. Check server is installed
2. Verify settings.json configuration
3. Increase timeout value
4. Check environment variables
```

### Skill Not Triggering

```
Issue: Skill doesn't activate automatically

Solution:
1. Explicitly invoke: "Use [skill] skill to..."
2. Check skill description matches task
3. Review skill trigger conditions
```

---

## Resources

- [Qwen Code Skills Documentation](https://qwenlm.github.io/qwen-code-docs/en/users/features/skills/)
- [Qwen Code MCP Documentation](https://qwenlm.github.io/qwen-code-docs/en/users/features/mcp/)
- [MCP Server Registry](https://github.com/modelcontextprotocol/servers)
- [Skills Directory](./skills/)
