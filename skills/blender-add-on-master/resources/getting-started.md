# Blender Add-on Master - Resources

## Getting Started

### Installation
1. Open Blender
2. Go to Edit > Preferences > Add-ons
3. Click "Install..." and select your .py file
4. Enable the add-on checkbox

### Development Setup
1. Enable "Python: Interactive Console" add-on
2. Use Blender's built-in text editor or VS Code with Blender addon
3. Set up console for debugging

## Quick Reference

### Common Imports
```python
import bpy
import bmesh
from bpy.types import Panel, Operator, PropertyGroup
from bpy.props import *
```

### Attribute Prefixes
- `@P` - Position
- `@N` - Normal
- `@Cd` - Color
- `@uv` - UV coordinates
- `@id` - ID

## Useful Snippets

### Get Selected Objects
```python
selected = bpy.context.selected_objects
active = bpy.context.active_object
```

### Get Scene Objects
```python
all_objects = bpy.data.objects
all_meshes = bpy.data.meshes
all_materials = bpy.data.materials
```

## External Resources
- [Blender Python API Docs](https://docs.blender.org/api/current/)
- [Blender Artists Scripting](https://blenderartists.org/c/scripting/)
