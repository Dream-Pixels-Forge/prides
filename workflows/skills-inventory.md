---
name: skills-inventory-workflow
version: 1.0.0
description: Automated workflow for scanning, parsing, and maintaining skills inventory
lastUpdated: 2026-03-27
status: active
triggers:
  - prides-agent-init
  - new-skill-added
  - manual-scan-command
---

# Skills Inventory Workflow

## Overview

Automates scanning skills directory, parsing metadata, and maintaining PRIDES.md/skills-inventory.md.

**Owner:** Prides Agent | **Frequency:** On-trigger | **Output:** Updated skills-inventory.md

---

## Triggers

| Trigger | When | Action | Purpose |
|---------|------|--------|---------|
| **Prides Agent Init** | Agent starts | Full scan | Ensure current state |
| **New Skill Added** | New directory detected | Scan new skill | Keep inventory current |
| **Manual Command** | `/prides:scan-skills` | Full refresh | On-demand update |

---

## Workflow Steps

### Step 1: Scan Skills Directory

**Agent:** Prides Agent | **Input:** `./skills/`

```xml
<scan>
  <target>./skills/</target>
  <exclude>- SKILLS-INDEX.md - node_modules - .git</exclude>
  <include>- */SKILL.md</include>
</scan>
```

**Output:** List of skill directories with SKILL.md files

### Step 2: Parse Skill Metadata

**Agent:** Prides Agent | **Input:** Each skill's SKILL.md

```xml
<parse>
  <file>{skill-directory}/SKILL.md</file>
  <extract>
    <field name="name" source="yaml.frontmatter.name"/>
    <field name="description" source="yaml.frontmatter.description"/>
    <field name="capabilities" source="content.sections.capabilities"/>
    <field name="triggers" source="content.sections.triggers"/>
    <field name="integrations" source="content.sections.integrations"/>
  </extract>
</parse>
```

**Output:** Structured metadata per skill

### Step 3: Categorize Skills

**Agent:** Prides Agent | **Input:** Parsed metadata

```xml
<categorize>
  <categories>
    <category name="Design & UI"><keywords>ui, design, frontend, stitch, shadcn</keywords></category>
    <category name="3D & Motion"><keywords>3d, blender, cinema4d, houdini, after-effects</keywords></category>
    <category name="AI & Video"><keywords>ai, video, veo, seedance, wan, generate</keywords></category>
    <category name="Development"><keywords>nextjs, react, electron, tauri, framework</keywords></category>
    <category name="Search & Research"><keywords>search, research, exa, company, people</keywords></category>
    <category name="Agent & Workflow"><keywords>agent, skill, subagent, workflow</keywords></category>
    <category name="MCP & Integration"><keywords>mcp, integration, figma, api</keywords></category>
    <category name="Quality"><keywords>quality, best-practices, lint, performance, debugging</keywords></category>
    <category name="Database"><keywords>database, backend, supabase, postgres</keywords></category>
    <category name="Content"><keywords>content, media, notebooklm, youtube, remotion</keywords></category>
  </categories>
  <fallback>Other</fallback>
</categorize>
```

**Output:** Skills organized by category

### Step 4: Build Inventory Structure

**Agent:** Prides Agent | **Input:** Categorized metadata

```xml
<build>
  <template>## {Category} ({count} skills)
| Skill | Description | Location |
|-------|-------------|----------|
| **{name}** | {description} | `./skills/{directory}/` |</template>
  <sections>- Overview - Categories - Index - Statistics</sections>
</build>
```

**Output:** Complete inventory markdown

### Step 5: Update Inventory File

**Agent:** Prides Agent + Git Master SAgent | **Input:** Generated markdown

```xml
<update>
  <file>PRIDES.md/skills-inventory.md</file>
  <action>replace</action>
  <preserve>- YAML frontmatter (update lastUpdated) - Links</preserve>
  <commit><message>docs: update skills inventory ({count} skills)</message></commit>
</update>
```

**Output:** Updated and committed inventory

---

## Skill Metadata Schema

```xml
<schema>
  <required>
    <field name="name" type="string"/>
    <field name="description" type="string"/>
    <field name="location" type="string"/>
  </required>
  <optional>
    <field name="version" type="string"/>
    <field name="category" type="string"/>
    <field name="capabilities" type="array"/>
    <field name="status" type="enum[active,deprecated,experimental]"/>
    <field name="usageCount" type="number"/>
  </optional>
</schema>
```

---

## Inventory Format

```markdown
---
name: skills-inventory
version: 1.0.0
lastUpdated: {YYYY-MM-DD}
totalSkills: {count}
---

# Skills Inventory
**Total:** {count} | **Last Scan:** {date}

## By Category
### {Category} ({count} skills)
| Skill | Description | Location |
|-------|-------------|----------|

## Alphabetical Index
1. {skill-name}
```

---

## Error Handling

| Error | Action | Message |
|-------|--------|---------|
| Missing SKILL.md | Log warning, skip | `Warning: {dir} missing SKILL.md` |
| Parse failure | Log error, continue | `Error: Failed to parse {skill}` |
| Write failure | Alert user, save temp | `Error: Update failed, saved to temp` |

---

## Performance Optimization

**Caching:** Cache metadata in `.prides/cache/skills-metadata.json`, invalidate on changes

**Incremental:** Detect new/changed skills only, re-parse selectively

**Batch:** Group filesystem ops, single commit

---

## Integration Points

| Agent | Role |
|-------|------|
| **Prides Agent** | Trigger, coordinate, update |
| **Git Master SAgent** | Commit, offline mode, version |
| **Other Agents** | Query inventory, report usage |

---

## Quality Checks

### Pre-Update Validation

```xml
<validate>
  <check>Required fields present</check>
  <check>Categories consistent</check>
  <check>Links valid</check>
  <check>Under 300 lines</check>
  <check>YAML valid</check>
</validate>
```

### Post-Update Verification

```xml
<verify>
  <check>File readable</check>
  <check>Count matches</check>
  <check>Index complete</check>
  <check>Commit success</check>
</verify>
```

---

## Manual Commands

| Command | Purpose |
|---------|---------|
| `/prides:scan-skills --force` | Ignore cache, full rescan |
| `/prides:scan-skills --sync` | Sync manual edits |
| `/prides:scan-skills --clean` | Remove deprecated skills |

---

## Related

- [Project Context](./project-context.md)
- [Active Workflow](./active-workflow.md)
- [Agent Coordination](./agent-coordination.md)
- [Skills Index](../skills/SKILLS-INDEX.md)

---

**Version:** 1.0.0 | **Created:** 2026-03-27
