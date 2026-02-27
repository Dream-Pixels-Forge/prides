# MCP Servers Configuration for Prides

This directory contains MCP server configurations for the Prides multi-agent system.

## Available MCP Servers

### Core Servers (Always Available)

| Server | Purpose | Configuration |
|--------|---------|---------------|
| **Git** | Git operations | `mcp-server-git` |
| **Filesystem** | File operations | `@modelcontextprotocol/server-filesystem` |

### Optional Servers (Project-Specific)

| Server | Purpose | Environment Variables |
|--------|---------|----------------------|
| **Netlify** | Deployment | `NETLIFY_API_KEY` |
| **Supabase** | Database | `SUPABASE_URL`, `SUPABASE_ANON_KEY` |
| **GitHub** | Repository management | `GITHUB_TOKEN` |
| **Playwright** | E2E testing | None |
| **Shadcn** | UI components | None |

## Setup Instructions

### 1. Install MCP Servers

```bash
# Git server (built-in)
npm install -g mcp-server-git

# Filesystem server
npx @modelcontextprotocol/server-filesystem

# Netlify server
npx @modelcontextprotocol/server-netlify

# Supabase server
npx @modelcontextprotocol/server-supabase

# GitHub server
npx @modelcontextprotocol/server-github

# Playwright server
npx @modelcontextprotocol/server-playwright

# Shadcn server
npx mcp-server-shadcn
```

### 2. Configure Environment Variables

Create a `.env` file in the project root:

```bash
# Netlify
NETLIFY_API_KEY=your_netlify_api_key

# Supabase
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_ANON_KEY=your_anon_key

# GitHub
GITHUB_TOKEN=your_github_token
```

### 3. Update Settings

Copy the template to your project:

```bash
cp .qwen/settings.json.template .qwen/settings.json
```

Edit `.qwen/settings.json` to enable/disable servers.

## Agent Integration

### Git Master SAgent

Uses: `git`, `filesystem`

```markdown
## MCP Tools Available
- git: `git_status`, `git_diff`, `git_commit`, `git_push`, `git_pull`, `git_branch`
- filesystem: `read_file`, `write_file`, `list_directory`, `search_files`
```

### Testing SAgent

Uses: `playwright`, `filesystem`

```markdown
## MCP Tools Available
- playwright: `launch`, `navigate`, `screenshot`, `click`, `fill`, `evaluate`
- filesystem: `read_file`, `write_file`, `list_directory`
```

### Deployment SAgent

Uses: `netlify`, `github`, `filesystem`

```markdown
## MCP Tools Available
- netlify: `deploy`, `list_sites`, `get_site`, `create_site`
- github: `create_release`, `create_tag`, `get_repository`
- filesystem: `read_file`, `write_file`
```

### Coder SAgent

Uses: `shadcn`, `filesystem`, `git`

```markdown
## MCP Tools Available
- shadcn: `list_components`, `get_component`, `add_component`
- filesystem: `read_file`, `write_file`, `list_directory`
- git: `git_status`, `git_diff`
```

## Skill Integration

### Available Skills

| Skill | File | Purpose |
|-------|------|---------|
| **shadcn-ui** | `skills/shadcn-ui/SKILL.md` | Component integration |
| **frontend-design** | `skills/frontend-design/SKILL.md` | UI creation |
| **react-components** | `skills/react-components/SKILL.md` | React patterns |
| **ui-ux-pro-max** | `skills/ui-ux-pro-max/SKILL.md` | Design system |
| **stitch-loop** | `skills/stitch-loop/SKILL.md` | Prototyping |
| **design-md** | `skills/design-md/SKILL.md` | Design documentation |
| **mcp-builder** | `skills/mcp-builder/SKILL.md` | MCP server creation |

### Using Skills in Agents

Reference skills in agent definitions:

```markdown
## Skills Integration

When working with UI components:
1. Use `skill:shadcn-ui` for component discovery and installation
2. Use `skill:frontend-design` for custom component creation
3. Use `skill:ui-ux-pro-max` for design system guidance

Example invocation:
"Use the shadcn-ui skill to add a data table component"
```

## Troubleshooting

### Server Connection Issues

```bash
# List configured servers
qwen mcp list

# Test server connection
qwen mcp test <server-name>

# Remove and re-add server
qwen mcp remove <server-name>
qwen mcp add <server-name> <command>
```

### Environment Variable Issues

```bash
# Verify environment variables
echo $NETLIFY_API_KEY
echo $SUPABASE_URL
echo $GITHUB_TOKEN
```

### Permission Issues

Ensure proper file permissions:
```bash
chmod +x mcp-server-*
```

## Best Practices

1. **Minimal Servers**: Only enable servers needed for the project
2. **Secure Configuration**: Never commit API keys to version control
3. **Timeout Settings**: Set appropriate timeouts for each server
4. **Tool Filtering**: Use `includeTools`/`excludeTools` for security
5. **Regular Updates**: Keep MCP servers updated to latest versions

## Resources

- [MCP Protocol Documentation](https://modelcontextprotocol.io/)
- [MCP Server Registry](https://github.com/modelcontextprotocol/servers)
- [Qwen Code MCP Guide](https://qwenlm.github.io/qwen-code-docs/en/users/features/mcp/)
