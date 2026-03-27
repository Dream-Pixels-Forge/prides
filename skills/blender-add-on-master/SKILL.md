---
name: blender-add-on-master
description: Expert guidance for creating Blender add-ons and Python scripts. Use when building custom tools, operators, panels, or automating Blender workflows with Python scripting.
license: Complete terms in LICENSE.txt
---

# Blender Add-on Development Guide

You are a Blender add-on development expert specializing in creating Python-based tools, operators, and workflows for Blender 3D.

## Core Capabilities

### 1. Add-on Architecture
- Create properly structured add-ons
- Implement operators, panels, and properties
- Manage preferences and settings
- Handle registration/unregistration

### 2. Python Scripting
- Automate Blender workflows
- Create custom tools
- Batch processing
- Data manipulation

### 3. UI Development
- Custom panels in 3D Viewport
- Tool shelves and sidebars
- Property editors
- Custom menus and pie menus

### 4. Advanced Features
- Modal operators
- GPU drawing
- Background processes
- External integration

---

## Add-on Structure

### Basic Add-on Template

```python
bl_info = {
    "name": "My Add-on",
    "author": "Your Name",
    "version": (1, 0, 0),
    "blender": (3, 0, 0),
    "location": "View3D > Sidebar > My Tools",
    "description": "Description of the add-on",
    "warning": "",
    "doc_url": "{URL}",
    "tracker_url": "{URL}",
    "category": "3D View",
}

import bpy
from bpy.types import Panel, Operator, PropertyGroup
from bpy.props import StringProperty, FloatProperty, IntProperty, BoolProperty


class MYADDON_OT_operator(Operator):
    """Operator tooltip"""
    bl_idname = "myaddon.operator"
    bl_label = "Operator Name"
    bl_options = {'REGISTER', 'UNDO'}
    
    def execute(self, context):
        # Operator logic here
        self.report({'INFO'}, "Operation complete")
        return {'FINISHED'}


class MYADDON_PT_panel(Panel):
    """Panel tooltip"""
    bl_idname = "MYADDON_PT_panel"
    bl_label = "Panel Name"
    bl_space_type = 'VIEW_3D'
    bl_region_type = 'UI'
    bl_category = "My Tools"
    
    def draw(self, context):
        layout = self.layout
        layout.operator("myaddon.operator")


classes = (
    MYADDON_OT_operator,
    MYADDON_PT_panel,
)


def register():
    for cls in classes:
        bpy.utils.register_class(cls)


def unregister():
    for cls in reversed(classes):
        bpy.utils.unregister_class(cls)


if __name__ == "__main__":
    register()
```

---

## Common Operators

### Object Creation Operator

```python
class MYADDON_OT_create_object(Operator):
    """Create a custom object"""
    bl_idname = "myaddon.create_object"
    bl_label = "Create Object"
    bl_options = {'REGISTER', 'UNDO'}
    
    size: FloatProperty(
        name="Size",
        default=1.0,
        min=0.01,
        max=100.0
    )
    
    def execute(self, context):
        # Create mesh
        mesh = bpy.data.meshes.new("CustomMesh")
        obj = bpy.data.objects.new("CustomObject", mesh)
        
        # Link to collection
        context.collection.objects.link(obj)
        
        # Select and make active
        bpy.ops.object.select_all(action='DESELECT')
        obj.select_set(True)
        context.view_layer.objects.active = obj
        
        self.report({'INFO'}, f"Created object with size {self.size}")
        return {'FINISHED'}
```

### Batch Processing Operator

```python
class MYADDON_OT_batch_process(Operator):
    """Process all selected objects"""
    bl_idname = "myaddon.batch_process"
    bl_label = "Batch Process"
    bl_options = {'REGISTER', 'UNDO'}
    
    def execute(self, context):
        selected = context.selected_objects
        
        for obj in selected:
            # Process each object
            self.process_object(obj)
        
        self.report({'INFO'}, f"Processed {len(selected)} objects")
        return {'FINISHED'}
    
    def process_object(self, obj):
        # Custom processing logic
        pass
```

### Modal Operator (Interactive)

```python
class MYADDON_OT_modal_tool(Operator):
    """Interactive modal tool"""
    bl_idname = "myaddon.modal_tool"
    bl_label = "Modal Tool"
    bl_options = {'REGISTER', 'UNDO'}
    
    _timer = None
    
    def modal(self, context, event):
        if event.type == 'TIMER':
            # Update logic here
            pass
        
        elif event.type == 'LEFTMOUSE' and event.value == 'PRESS':
            return self.finish(context)
        
        elif event.type in {'RIGHTMOUSE', 'ESC'}:
            return self.cancel(context)
        
        return {'PASS_THROUGH'}
    
    def execute(self, context):
        wm = context.window_manager
        self._timer = wm.event_timer_add(0.1, window=context.window)
        wm.modal_handler_add(self)
        return {'RUNNING_MODAL'}
    
    def finish(self, context):
        context.window_manager.event_timer_remove(self._timer)
        return {'FINISHED'}
    
    def cancel(self, context):
        context.window_manager.event_timer_remove(self._timer)
        return {'CANCELLED'}
```

---

## Panel Types

### Basic Panel

```python
class MYADDON_PT_main_panel(Panel):
    bl_idname = "MYADDON_PT_main_panel"
    bl_label = "Main Panel"
    bl_space_type = 'VIEW_3D'
    bl_region_type = 'UI'
    bl_category = "My Tools"
    
    def draw(self, context):
        layout = self.layout
        layout.operator("myaddon.operator")
```

### Panel with Properties

```python
class MYADDON_PT_settings_panel(Panel):
    bl_idname = "MYADDON_PT_settings_panel"
    bl_label = "Settings"
    bl_space_type = 'VIEW_3D'
    bl_region_type = 'UI'
    bl_parent_id = "MYADDON_PT_main_panel"
    bl_options = {'DEFAULT_CLOSED'}
    
    def draw(self, context):
        layout = self.layout
        scene = context.scene
        tool = scene.myaddon_tool
        
        layout.prop(tool, "string_property")
        layout.prop(tool, "float_property")
        layout.prop(tool, "bool_property")
```

### Subpanel

```python
class MYADDON_PT_sub_panel(Panel):
    bl_idname = "MYADDON_PT_sub_panel"
    bl_label = "Sub Panel"
    bl_space_type = 'VIEW_3D'
    bl_region_type = 'UI'
    bl_parent_id = "MYADDON_PT_main_panel"
    bl_options = {'DEFAULT_CLOSED'}
    
    def draw_header(self, context):
        self.layout.label(text="Header")
    
    def draw(self, context):
        layout = self.layout
        layout.operator("myaddon.operator")
```

---

## Property Types

### Property Group

```python
class MyAddonProperties(PropertyGroup):
    string_property: StringProperty(
        name="String",
        description="A string property",
        default=""
    )
    
    float_property: FloatProperty(
        name="Float",
        description="A float property",
        default=1.0,
        min=0.0,
        max=10.0,
        step=0.1
    )
    
    int_property: IntProperty(
        name="Integer",
        description="An integer property",
        default=1,
        min=0,
        max=100
    )
    
    bool_property: BoolProperty(
        name="Boolean",
        description="A boolean property",
        default=False
    )
    
    enum_property: EnumProperty(
        name="Enum",
        description="Choose an option",
        items=[
            ('OPTION_A', "Option A", "Description A"),
            ('OPTION_B', "Option B", "Description B"),
            ('OPTION_C', "Option C", "Description C"),
        ],
        default='OPTION_A'
    )
    
    color_property: FloatVectorProperty(
        name="Color",
        description="A color property",
        subtype='COLOR',
        size=4,
        min=0.0,
        max=1.0,
        default=(1.0, 1.0, 1.0, 1.0)
    )
```

### Registration

```python
def register():
    bpy.utils.register_class(MyAddonProperties)
    bpy.types.Scene.myaddon_tool = bpy.props.PointerProperty(type=MyAddonProperties)

def unregister():
    del bpy.types.Scene.myaddon_tool
    bpy.utils.unregister_class(MyAddonProperties)
```

---

## Common Workflows

### Mesh Manipulation

```python
import bmesh

def modify_mesh(obj):
    mesh = obj.data
    bm = bmesh.new()
    bm.from_mesh(mesh)
    
    # Modify mesh
    for vert in bm.verts:
        vert.co.z += 1.0
    
    bm.to_mesh(mesh)
    bm.free()
```

### Material Creation

```python
def create_material(name, color=(1, 1, 1, 1)):
    mat = bpy.data.materials.new(name=name)
    mat.use_nodes = True
    
    nodes = mat.node_tree.nodes
    bsdf = nodes.get("Principled BSDF")
    
    if bsdf:
        bsdf.inputs['Base Color'].default_value = color
    
    return mat
```

### Animation Scripting

```python
def animate_object(obj, start_frame=1, end_frame=60):
    obj.location = (0, 0, 0)
    obj.keyframe_insert(data_path="location", frame=start_frame)
    
    obj.location = (5, 5, 5)
    obj.keyframe_insert(data_path="location", frame=end_frame)
```

### File Import/Export

```python
# Import
bpy.ops.import_mesh.obj(filepath="path/to/file.obj")

# Export
bpy.ops.export.mesh.obj(filepath="path/to/export.obj")

# Batch export
for obj in bpy.data.objects:
    bpy.ops.object.select_all(action='DESELECT')
    obj.select_set(True)
    bpy.ops.export.mesh.obj(filepath=f"path/to/{obj.name}.obj")
```

---

## Best Practices

### Code Organization
- Use clear naming conventions (MYADDON_prefix)
- Separate operators, panels, and properties
- Keep functions small and focused
- Add docstrings to all classes and functions

### User Experience
- Provide clear tooltips
- Use appropriate icons
- Show progress for long operations
- Give helpful error messages

### Performance
- Use context overrides efficiently
- Avoid unnecessary scene updates
- Batch operations when possible
- Use undo buffers appropriately

### Compatibility
- Specify minimum Blender version
- Test on multiple Blender versions
- Handle deprecated APIs
- Check for required modules

---

## Debugging

### Console Output

```python
import bpy

print("Debug message")
bpy.app.handlers.load_post.append(lambda x: print("File loaded"))
```

### Error Handling

```python
try:
    obj = bpy.context.object
    if obj is None:
        raise ValueError("No active object")
    # Process object
except Exception as e:
    self.report({'ERROR'}, str(e))
    return {'CANCELLED'}
```

---

## Resources

### Official Documentation
- [Blender Python API](https://docs.blender.org/api/current/)
- [Add-on Development](https://docs.blender.org/manual/en/latest/advanced/scripting/addon_tutorial.html)
- [bpy Module](https://docs.blender.org/api/current/bpy.html)

### Community Resources
- Blender Artists Scripting Forum
- Blender Stack Exchange
- GitHub Blender Add-on Examples

---

## Usage Examples

```
"Use blender-add-on-master skill to create a mesh generator add-on"
"Use blender-add-on-master skill to create a batch export tool"
"Use blender-add-on-master skill to create custom modeling operators"
"Use blender-add-on-master skill to automate UV unwrapping workflow"
```
