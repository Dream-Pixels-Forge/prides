# Prides Extension - Quick Reference

**Version:** 0.1.1 | **Agents:** 26 | **Skills:** 33 | **MCP:** 7

---

## Quick Start Commands

```bash
# Web Development
/prides:new-feature "Add user authentication"
/prides:git-commit "feat: add login"
/prides:run-tests
/prides:deploy-app "production"

# 3D & VFX (via agents)
"Use blender-sagent to create low-poly asset"
"Use houdini-sagent for fluid simulation"
"Use cinema4d-sagent for motion graphics"
"Use nuke-sagent for compositing"
"Use after-effects-sagent for VFX"

# Game Dev
"Use unity-sagent to create player controller"

# Post-Production
"Use davinci-resolve-sagent for color grading"
```

---

## Agent Quick Reference

### Web Development
| Agent | Use For |
|-------|---------|
| **Coder** | Feature implementation |
| **UI/UX** | Design guidance |
| **Debugger** | Bug fixing |
| **Testing** | Test creation |
| **Critic** | Code review |

### 3D & VFX
| Agent | Use For |
|-------|---------|
| **Blender** | 3D modeling, animation |
| **Cinema 4D** | Motion graphics |
| **Houdini** | Procedural VFX, simulations |
| **Nuke** | Compositing |
| **After Effects** | Motion graphics, VFX |
| **Unity** | Game development |
| **DaVinci Resolve** | Color grading, editing |

### Planning & Quality
| Agent | Use For |
|-------|---------|
| **Plan** | Implementation planning |
| **Tasks** | Task management |
| **Idea** | Brainstorming |
| **Security** | Security audits |
| **Performance** | Optimization |
| **Accessibility** | WCAG compliance |

---

## Skills Quick Reference

### Design & UI (7)
- `shadcn-ui` - UI components
- `frontend-design` - Interfaces
- `ui-ux-pro-max` - 50 styles, palettes
- `figma-api-master` - Figma API

### 3D & VFX (6)
- `blender-add-on-master` - Blender scripting
- `cinema4d-master` - Cinema 4D
- `sidefx-houdini-guru` - Houdini VEX
- `foundry-nuke-master` - Nuke scripting
- `after-effects-scripts-master` - AE scripts

### Development (5)
- `vercel-react-best-practices` - React
- `vercel-composition-patterns` - Architecture
- `python-master` - Python
- `code-search` - Code patterns
- `mcp-builder` - MCP servers

### Usage Pattern
```
"Use [skill-name] skill to [action]"

Examples:
"Use shadcn-ui skill to add data table"
"Use blender-add-on-master skill to create addon"
"Use sidefx-houdini-guru skill to write VEX"
```

---

## MCP Servers

| Server | Purpose | Status |
|--------|---------|--------|
| **filesystem** | File operations | ✅ |
| **git** | Git operations | ✅ |
| **shadcn** | UI components | ✅ |
| **playwright** | E2E testing | ✅ |
| **github** | GitHub ops | ⚠️ |
| **netlify** | Deployment | ⚠️ |
| **supabase** | Database | ⚠️ |

⚠️ = Needs credentials

---

## Common Workflows

### Web Feature
```
1. /prides:new-feature "description"
2. Plan SAgent → planning
3. Coder SAgent → implementation
4. Testing SAgent → tests
5. Critic SAgent → review
6. Git Master → commit
```

### 3D Asset
```
1. Houdini SAgent → procedural gen
2. Blender SAgent → refine
3. Unity SAgent → import
```

### VFX Shot
```
1. Houdini → simulate
2. Nuke → composite
3. After Effects → final
4. Resolve → grade
```

### Motion Graphics
```
1. Cinema 4D → 3D animation
2. After Effects → composite
3. Resolve → grade
```

---

## File Structure

```
prides/
├── commands/prides/      (9 commands)
├── agents/              (26 agents)
├── skills/              (33 skills)
├── templates/            (5 templates)
├── mandatory_docs/       (5 docs)
└── .qwen/               (config)
```

---

## Quality Gates

### Pre-Commit
- [ ] Lint passes
- [ ] Format correct
- [ ] Type check passes
- [ ] Critic review done

### Pre-Merge
- [ ] All tests pass
- [ ] Coverage >80%
- [ ] Security clean
- [ ] Performance OK
- [ ] Accessibility OK

### Pre-Deploy
- [ ] All gates passed
- [ ] Smoke tests pass
- [ ] Rollback ready
- [ ] Monitoring configured

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Command not found | Check Markdown syntax |
| Agent not responding | Check configuration |
| Skill not triggering | Use explicit invocation |
| MCP disconnected | Verify installation |
| Permission errors | Check file permissions |

---

## Resources

- `README.md` - Full guide
- `QWEN.md` - Context docs
- `UPDATE-SUMMARY.md` - What's new
- `SKILLS-INDEX.md` - Skills reference
- `mandatory_docs/` - Core docs

---

**Support:** Dream Pixels Forge  
**Docs:** https://qwenlm.github.io/qwen-code-docs/
