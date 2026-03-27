# Foundry Nuke Master - Resources

## Getting Started

### Script Locations

| Location | Purpose |
|----------|---------|
| `~/.nuke/` | User scripts directory |
| `plugins/` | Custom plugins |
| `gizmos/` | Custom gizmos |
| `scripts/` | Python scripts |

### init.py Setup

```python
import nuke

# Add custom paths
nuke.pluginAddPath('./gizmos')
nuke.pluginAddPath('./plugins')

# Add menu items
m = nuke.menu("Nuke")
m.addCommand("My Tools/My Script", "my_script.main()")
```

## Quick Reference

### Common Node Classes

| Class | Purpose |
|-------|---------|
| `Read` | Import footage |
| `Write` | Export renders |
| `Grade` | Color correction |
| `Transform` | Transform operations |
| `Merge` | Composite layers |
| `Keylight` | Green screen keying |
| `Roto` | Rotoscoping |
| `Tracker` | Motion tracking |
| `Blur` | Blur effects |
| `Glow` | Glow effects |

### Python Commands

```python
import nuke

# Node operations
nuke.createNode("ClassName")
nuke.selectedNodes()
nuke.allNodes()
nuke.toNode("NodeName")

# Script operations
nuke.scriptOpen("file.nk")
nuke.scriptSave()
nuke.scriptClose()

# Render operations
nuke.execute(node, start, end)
```

## External Resources
- [Foundry Learn](https://learn.foundry.com/)
- [Nukepedia](https://www.nukepedia.com/)
