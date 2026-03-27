# Prides - Multi-Agent Development System

**Prototype. Review. Implement. Deploy. Extend. Secure**

A comprehensive Qwen CLI extension for orchestrating **squad specialized AI agents** across web development, 3D/VFX, motion graphics, game development, and post-production workflows.

## Overview

The Prides extension provides a complete ecosystem of specialized agents for the entire creative and development lifecycle. Built for Qwen CLI with Markdown-based commands, comprehensive agent orchestration, skills integration, and MCP server support.

## Features

### 🚀 Core Capabilities

- **28 Specialized Agents** - Web dev, 3D/VFX, motion graphics, game dev, post-production
- **45 Specialized Skills** - Domain expertise on demand
- **10 MCP Servers** - Direct tool integration
- **Multi-Domain Support** - Web, 3D, VFX, games, video, design
- **Skills Integration** - Leverage specialized knowledge per task
- **MCP Integration** - Direct filesystem, Git, and tool access
- **Template-Driven** - Extensive template library for consistency
- **Qwen CLI Compatible** - Full Markdown command format with `{{args}}` injection

### 🎯 Agent Categories

| Category | Agents | Purpose |
|----------|--------|---------|
| **Development** | Coder, UI/UX, Prototyper, Debugger | Web feature implementation |
| **3D & VFX** | Blender, Cinema 4D, Houdini, Nuke, After Effects | 3D modeling, VFX, motion graphics |
| **Game Dev** | Unity | Game development and scripting |
| **Post-Production** | DaVinci Resolve | Video editing, color grading |
| **Quality** | Testing, Security, Performance, Lint, Accessibility, Critic | QA and code review |
| **Planning** | Plan, Tasks, Idea, Analyst, PRD Doc | Project planning and requirements |
| **Deployment** | Deployment, Git Master, Monitoring | Release and version control |

### 🛠️ Commands

| Command | Purpose |
|---------|---------|
| `/prides` | Main orchestrator - complete feature development workflow |
| `/prides:new-feature` | Create complete feature implementation |
| `/prides:git-commit` | Commit with intelligent message generation |
| `/prides:run-tests` | Run comprehensive test suites |
| `/prides:deploy-app` | Deploy to environment |
| `/prides:debug-issue` | Debug and diagnose issues |
| `/prides:generate-docs` | Generate technical documentation |
| `/prides:optimize-performance` | Analyze and optimize performance |
| `/prides:security-audit` | Security vulnerability scan |
| `/prides:improve-accessibility` | WCAG compliance improvements |

### Quick Start

### Installation

1. Ensure Qwen CLI is installed
2. Clone this extension to your Qwen extensions directory
3. The extension will be automatically detected and loaded

**Alternative Installation (Auto-Update):**

```bash
# Install extension with auto-update from GitHub
qwen extensions install https://github.com/Dream-Pixels-Forge/prides --auto-update
```

### Basic Usage

```bash
# Start a new feature development workflow
/prides:new-feature "Add user authentication system"

# Deploy to production
/prides:deploy-app "production"

# Commit and push changes
/prides:git-commit "feat: add new authentication system"

# Run comprehensive tests
/prides:run-tests

# Generate documentation
/prides:generate-docs

# Performance optimization
/prides:optimize-performance

# Security audit
/prides:security-audit

# 3D modeling
"Use blender-sagent to create a low-poly asset"

# Motion graphics
"Use cinema4d-sagent to create animated logo reveal"

# VFX simulation
"Use houdini-sagent to create fluid simulation"
```

### Advanced Workflows

#### Complete Web Feature Development

```bash
# 1. Start feature development
/prides:new-feature "Add user login with social auth"

# 2. The orchestrator coordinates:
#    - Idea SAgent → Brainstorm requirements
#    - Plan SAgent → Implementation plan
#    - Coder SAgent → Implement feature
#    - Testing SAgent → Create tests
#    - Critic SAgent → Review code
#    - Git Master SAgent → Commit changes
```

#### 3D Asset Pipeline

```
# Multi-agent 3D workflow
1. Houdini SAgent → Create procedural building
2. Blender SAgent → Refine and texture
3. Unity SAgent → Import and set up LODs
```

#### VFX Pipeline

```
# Complete VFX workflow
1. Houdini SAgent → Simulate explosion
2. Nuke SAgent → Composite elements
3. After Effects SAgent → Final touches
4. DaVinci Resolve SAgent → Color grade
```

#### Motion Graphics

```
# Motion graphics workflow
1. Cinema 4D SAgent → 3D animation
2. After Effects SAgent → Composite
3. DaVinci Resolve SAgent → Final grade
```
qwen prides run-tests
qwen prides security-audit
qwen prides optimize-performance
qwen prides improve-accessibility
qwen prides verify-accuracy
```

## Architecture

### Agent Ecosystem (28 Agents)

```
Prides Agent (Central Orchestrator)
│
├── Development (11 agents)
│   ├── Web: Coder, UI/UX, Prototyper, Debugger
│   ├── 3D: Blender, Cinema 4D, Houdini
│   ├── VFX: Nuke, After Effects
│   ├── Game: Unity
│   └── Post-Prod: DaVinci Resolve
│
├── Quality & Security (6 agents)
│   ├── Testing, Security, Performance
│   ├── Lint, Accessibility, Critic
│
├── Planning & Documentation (6 agents)
│   ├── Plan, Tasks, Idea
│   ├── Analyst, PRD Doc, Documentation
│
└── Deployment & Support (6 agents)
    ├── Deployment, CI/CD, Rollback, Monitoring, Git Master
```

### Skills Library (45 Skills)

| Category | Skills |
|----------|--------|
| **Design & UI** | shadcn-ui, frontend-design, ui-ux-pro-max, design-md, stitch-loop, react-components, figma-api-master |
| **3D & VFX** | blender-add-on-master, cinema4d-master, sidefx-houdini-guru, after-effects-scripts-master, foundry-nuke-master |
| **Development** | vercel-react-best-practices, vercel-composition-patterns, mcp-builder, python-master, code-search |
| **Search & Research** | company-search, people-search, financial-report-search, research-paper-search, personal-site-search, x-search |
| **Utility** | enhance-prompt, find-skills, skill-creator, agentation, ai-video-generation, remotion |

### MCP Servers (10 Configured)

| Server | Purpose |
|--------|---------|
| **filesystem** | File operations (read, write, search) |
| **git** | GitHub operations (commit, branch, PRs, releases) |
| **brave-search** | Web search via Brave API |
| **puppeteer** | Browser automation |
| **playwright** | E2E testing and browser automation |
| **chrome-dev-tools** | Chrome DevTools protocol |
| **memory** | Persistent memory for conversation context |
| **fetch** | HTTP requests and web fetching |
| **notion** | Notion workspace integration |
| **image-editing** | Image editing and manipulation |

The extension orchestrates a comprehensive agent ecosystem:

#### Core Agent and SAgents

- **Prides Agent**: Main orchestrator and project manager
- **Plan SAgent**: Creates detailed implementation plans
- **Tasks SAgent**: Organizes and tracks implementation tasks
- **Coder SAgent**: Full-stack feature implementation

#### Development SAgents

- **UI/UX SAgent**: User experience design and implementation
- **Prototyper SAgent**: UI prototyping with Google Stitch
- **Debugger SAgent**: Issue debugging and resolution

#### Quality-Security SAgents

- **Testing SAgent**: Comprehensive testing workflows
- **Security SAgent**: Security analysis and vulnerability assessment
- **Performance SAgent**: Performance optimization and profiling
- **Accessibility SAgent**: WCAG compliance and accessibility improvements
- **Accuracy Verification SAgent**: Deep accuracy validation
- **Lint SAgent**: Code linting and formatting

#### Planning-Docs SAgents

- **Analyst SAgent**: Market analysis and research
- **PRD SAgent**: Product requirements documentation
- **Trends SAgent**: Technology and design trend research
- **Proposal SAgent**: Research-backed solution proposals

#### Deployment SAgents

- **Deployment SAgent**: Production deployment workflows
- **CI/CD SAgent**: Pipeline automation
- **Rollback SAgent**: Automated rollback procedures
- **Monitoring SAgent**: Production monitoring and observability

#### Support-Improvements SAgents

- **Documentation SAgent**: Technical documentation generation
- **Prompt Refiner SAgent**: Prompt enhancement
- **Improvement SAgent**: Code quality improvements
- **Updater SAgent**: Dependency management
- **Improver SAgent**: Subagent performance monitoring

#### Git Master SAgent

- **Git Master Agent**: Version control with branches-based workflow (features, devs, main or master)

### Workflow Process

1. **Project Status Check**: Analyze existing project state and roadmap. brainstorm if needed(ask user)
2. **Market & Requirements Analysis**: Research and document requirements
3. **Planning & Task Organization**: Create detailed plans and task lists
4. **Implementation**: Execute through specialized agents
5. **Quality Assurance**: Multi-layered verification and testing
6. **Documentation**: Generate comprehensive documentation

## Project Structure

```
prides/
├── qwen-extension.json         # Extension configuration
├── QWEN.md                    # Main context documentation
├── README.md                  # This file
├── SKILLS-MCP-INTEGRATION.md  # Skills & MCP guide
├── commands/prides/           # Command files (9 commands)
├── agents/                    # Agent definitions (26 agents)
│   ├── Development/          # 11 development agents
│   ├── Quality-Security/     # 6 QA agents
│   ├── Planning-Docs/        # 6 planning agents
│   ├── Deployment/           # 3 deployment agents
│   └── Git-master/           # Git operations
├── skills/                    # Skills library (33 skills)
│   ├── Design & UI (7)
│   ├── 3D & VFX (6)
│   ├── Development (5)
│   ├── Search & Research (7)
│   └── Utility (8)
├── templates/                 # Template library (5 templates)
├── mandatory_docs/           # Core documentation
│   ├── workflow-coordination.md
│   ├── quality-standards.md
│   ├── agent-specifications.md
│   ├── skills-integration-guide.md
│   └── 3d-vfx-agents-overview.md
└── .qwen/                    # Configuration
    ├── settings.json         # MCP server config
    └── MCP-CONFIG.md         # MCP documentation
```

### Markdown Command Format

The extension uses Markdown format for commands with YAML frontmatter:

```markdown
---
description: Create a complete feature implementation. Use {{args}} to specify the feature request.
---

# new-feature

Call @coder-sagent to implement the following feature request:

**Feature Request:** {{args}}
```

## Configuration

### Extension Config

`qwen-extension.json`:

```json
{
  "name": "prides",
  "version": "0.4.0",
  "contextFileName": "QWEN.md",
  "commands": "commands/prides",
  "skills": "skills",
  "agents": "agents",
  "mcpServers": {
    "filesystem": { ... },
    "git": { ... },
    "brave-search": { ... },
    "playwright": { ... },
    "chrome-dev-tools": { ... },
    "memory": { ... },
    "fetch": { ... },
    "notion": { ... },
    "image-editing": { ... }
  }
}
```

### MCP Configuration

See `.dev_notes/settings.json` for MCP server configuration and `.dev_notes/MCP-CONFIG.md` for setup instructions.

### Skills Configuration

Skills are automatically available from the `skills/` directory. Invoke them via:
```
"Use [skill-name] skill to [action]"
```

## Project Structure

```
prides/
├── qwen-extension.json         # Extension configuration (v0.3.0)
├── QWEN.md                    # Context and documentation
├── commands/prides/              # Command files (Markdown format)
│   ├── new-feature.md
│   ├── deploy-app.md
│   ├── git-commit.md
│   ├── run-tests.md
│   └── ... (command files)
├── agents/                    # Agent definitions
│   ├── Development/
│   ├── Quality-Security/
│   ├── Planning-Docs/
│   ├── Deployment/
│   ├── Support-Improvements/
│   └── Git master/
├── templates/                 # Template library
├── skills/                   # Extension skills
│   ├── shadcn-ui/
│   ├── remotion/
│   ├── stitch-loop/
│   ├── design-md/
│   ├── react-components/
│   └── ... (search skills)
└── mcp-server/              # MCP server for programmatic access
    ├── src/index.js
    └── package.json
```

### Features

- **Auto-Path Detection**: Automatically finds the extension installation
- **Utility Tools**: List skills, agents, and commands
- **Skill Tools**: Use any of skills directly
- **Agent Tools**: Delegate to any of agents
- **Command Tools**: Execute any of commands

### Usage

```json
{"name": "list_skills", "arguments": {}}
{"name": "skill_shadcn-ui", "arguments": {"task": "Add a data table"}}
{"name": "agent_code-generation", "arguments": {"task": "Implement user auth"}}
{"name": "command_new-feature", "arguments": {"args": "User dashboard"}}
```

The extension includes a comprehensive template library:

- **Feature Templates**: Common feature patterns and implementations
- **Testing Templates**: Test structures and coverage patterns
- **Security Templates**: Security best practices and checklists
- **Documentation Templates**: Documentation structures and formats
- **Deployment Templates**: Deployment patterns and checklists

## Quality Standards

## Quality Standards

### Code Quality

- **Zero Tolerance**: No mockups, placeholders, or incomplete implementations
- **Type Safety**: Full TypeScript support and type checking
- **Error Handling**: Comprehensive error handling and validation
- **Performance**: Optimized for speed and efficiency

### Testing Standards

- **Coverage**: >80% code coverage with meaningful tests
- **Reliability**: Deterministic, non-flaky tests
- **Performance**: Test suites execute efficiently (<10 minutes for CI)

### Security Standards

- **OWASP Top 10**: Protection against critical web security risks
- **Secure Coding**: Follow secure coding practices
- **Principle of Least Privilege**: Minimal necessary permissions

### Accessibility Standards

- **WCAG 2.1 AA**: Meet accessibility guidelines
- **Keyboard Navigation**: Full functionality without mouse
- **Screen Reader Support**: Proper content announcements

### 3D/VFX Standards

- **Clean Topology**: Proper edge flow and quad-based meshes
- **UV Efficiency**: Minimal stretching, optimal texel density
- **Render Optimization**: Efficient shading networks and sampling
- **Pipeline Compatibility**: Standard formats and conventions

## Integration

### Qwen CLI Integration

Full integration with Qwen CLI features:

- **Command Discovery**: Automatic command registration and discovery
- **Argument Handling**: Flexible argument parsing and validation
- **Help System**: Integrated help and documentation
- **Error Handling**: Comprehensive error reporting and recovery
- **Skills System**: 33+ specialized skills on demand
- **MCP Servers**: Direct tool integration

### External Tool Integration

- **Git Integration**: Version control operations through Git MCP
- **Netlify Integration**: Deployment and hosting through Netlify MCP
- **Supabase Integration**: Database and backend services through Supabase MCP
- **GitHub Integration**: PRs, releases through GitHub MCP
- **Playwright Integration**: E2E testing through Playwright MCP
- **Shadcn Integration**: UI components through Shadcn MCP

### Skills Integration

All agents leverage specialized skills:
- **Design**: shadcn-ui, frontend-design, ui-ux-pro-max, figma-api-master
- **3D/VFX**: blender-add-on-master, cinema4d-master, sidefx-houdini-guru, foundry-nuke-master, after-effects-scripts-master
- **Development**: vercel-react-best-practices, vercel-composition-patterns, python-master
- **Research**: company-search, people-search, financial-report-search

## Contributing

### Development Setup

1. Clone the repository
2. Ensure QWEN CLI is installed
3. Test commands with `qwen prides <command>`
4. Follow Markdown command format with YAML frontmatter

### Adding New Commands

1. Create command file in `commands/prides/` with `.md` extension
2. Follow the established Markdown format:

   ```markdown
   ---
   description: Command description. Use {{args}} to specify the input.
   ---

   # command-name

   Call @agent-name to perform the action:

   **Input:** {{args}}
   ```

3. Commands should delegate to agents using `@agent-name` syntax

## Support

### Documentation

- **QWEN.md**: Complete context and agent documentation
- **mandatory_docs/**: Core workflow and coordination documents

### Troubleshooting

Common issues and solutions:

1. **Command not found**: Verify Markdown syntax in command files
2. **Agent not responding**: Check agent configuration and dependencies
3. **Template missing**: Ensure templates directory is populated
4. **Permission errors**: Verify file permissions and access rights

## License

See LICENSE file for details.

## Resources

- [Qwen Code Documentation](https://qwenlm.github.io/qwen-code-docs/)
- [Skills Index](./skills/SKILLS-INDEX.md)
- [3D/VFX Agents](./mandatory_docs/3d-vfx-agents-overview.md)
- [Skills Integration Guide](./mandatory_docs/skills-integration-guide.md)
- [MCP Configuration](./.dev_notes/MCP-CONFIG.md)

---

**Version:** 0.4.0 | **Agents:** 28 | **Skills:** 45 | **MCP Servers:** 10 | **Last Updated:** 2026-03-27

**Made with ❤️ by Dream Pixels Forge**
