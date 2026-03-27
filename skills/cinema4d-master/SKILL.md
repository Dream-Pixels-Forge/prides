---
name: cinema4d-master
description: Expert guidance for Maxon Cinema 4D Python scripting, XPresso, and MoGraph. Use for 3D modeling, motion graphics, automation, and Cinema 4D workflow optimization.
license: Complete terms in LICENSE.txt
---

# Cinema 4D Development Guide

You are a Cinema 4D expert specializing in Python scripting, XPresso, MoGraph, and workflow automation.

## Core Capabilities

### 1. Python Scripting
- Object manipulation
- Scene automation
- Batch processing
- Custom tools

### 2. XPresso
- Node-based expressions
- Parameter linking
- Animation drivers
- Custom rigs

### 3. MoGraph
- Effectors
- Cloners
- Fields
- Dynamics

### 4. Modeling & Animation
- Polygon modeling
- Sculpting
- Character animation
- Rigging

---

## Python Scripting

### Basic Script Template

```python
import c4d
from c4d import gui

def main():
    # Get active object
    obj = doc.GetActiveObject()
    
    if obj is None:
        gui.MessageDialog("Please select an object!")
        return
    
    # Process object
    process_object(obj)
    
    # Update document
    c4d.EventAdd()

def process_object(obj):
    """Process the selected object."""
    # Your code here
    pass

if __name__ == '__main__':
    main()
```

### Create Objects

```python
import c4d

def create_cube():
    # Create cube
    cube = c4d.BaseObject(c4d.Ocube)
    cube[c4d.PRIM_CUBE_SEG] = c4d.Vector(10, 10, 10)
    
    # Insert to document
    doc.InsertObject(cube)
    
    return cube

def create_null(name="Null"):
    null = c4d.BaseObject(c4d.Onull)
    null[c4d.ID_BASEOBJECT_NAME] = name
    return null

def create_sphere(radius=100):
    sphere = c4d.BaseObject(c4d.Osphere)
    sphere[c4d.PRIM_SPHERE_RADIUS] = radius
    return sphere
```

### Modify Objects

```python
# Get parameters
position = obj.GetAbsPos()
rotation = obj.GetAbsRot()
scale = obj.GetAbsScale()

# Set parameters
obj.SetAbsPos(c4d.Vector(100, 0, 0))
obj.SetAbsRot(c4d.Vector(0, c4d.utils.Rad(45), 0))
obj.SetAbsScale(c4d.Vector(2, 2, 2))

# Get/Set via data instance
obj[c4d.ID_BASEOBJECT_REL_POSITION] = c4d.Vector(0, 100, 0)
obj[c4d.ID_BASEOBJECT_REL_SCALE] = c4d.Vector(2, 2, 2)
```

### Iterate Scene

```python
def iterate_hierarchy(obj, level=0):
    """Recursively iterate through hierarchy."""
    if obj is None:
        return
    
    # Process current object
    print("  " * level + obj.GetName())
    
    # Process children
    child = obj.GetDown()
    while child:
        iterate_hierarchy(child, level + 1)
        child = child.GetNext()

# Get all objects in document
def get_all_objects(doc):
    objects = []
    obj = doc.GetFirstObject()
    while obj:
        objects.append(obj)
        obj = obj.GetNext()
    return objects
```

---

## XPresso Basics

### Common Nodes

| Node | Purpose |
|------|---------|
| **UserData** | Custom parameters |
| **Object** | Object reference |
| **Coordinate** | Position/Rotation/Scale |
| **Math** | Mathematical operations |
| **Range Mapper** | Remap values |
| **Formula** | Custom expressions |
| **Delay** | Smooth transitions |
| **Random** | Randomization |

### Expression Examples

```
// Formula node expressions
// Position based on time
time * 100

// Circular motion
x: cos(time * 2) * 100
y: sin(time * 2) * 100
z: 0

// Random position
rand(id) * 500

// Link to another object
OtherObject.Position.X

// Conditional
if (value > 0.5, 100, 0)
```

---

## MoGraph Workflows

### Cloner Setup

```python
import c4d

def create_cloner():
    # Create cloner
    cloner = c4d.BaseObject(1018544)  # MoGraph cloner
    
    # Set mode
    cloner[c4d.ID_MG_MOTIONGRAPH_MODE] = 1  # Grid array
    
    # Set count
    cloner[c4d.ID_MG_MOTIONGRAPH_COUNT] = c4d.Vector(10, 1, 10)
    
    # Set size
    cloner[c4d.ID_MG_MOTIONGRAPH_SIZE] = c4d.Vector(100, 0, 100)
    
    return cloner

def create_random_effector():
    effector = c4d.BaseObject(1077665)  # Random effector
    
    # Enable position
    effector[c4d.ID_MG_MOTIONGRAPH_EFFECTOR] = 1  # Position
    
    # Set strength
    effector[c4d.ID_MG_MOTIONGRAPH_STRENGTH] = c4d.Vector(50, 100, 50)
    
    return effector
```

### Common Effectors

| Effector | Use Case |
|----------|----------|
| **Random** | Randomize transforms |
| **Plain** | Direct parameter control |
| **Step** | Sequential animation |
| **Time** | Time-based animation |
| **Sound** | Audio-reactive |
| **Formula** | Custom expressions |
| **Delay** | Smooth transitions |
| **Inheritance** | Inherit from emitter |

---

## Common Tools

### Batch Export

```python
import c4d
import os

def batch_export(directory, format="FBX"):
    """Export all selected objects."""
    doc = c4d.documents.GetActiveDocument()
    objects = doc.GetActiveObjects(c4d.GETACTIVEOBJECTFLAGS_NONE)
    
    for obj in objects:
        # Export
        filename = f"{directory}/{obj.GetName()}.{format.lower()}"
        
        if format == "FBX":
            c4d.documents.SaveDocument(
                doc, 
                filename, 
                c4d.SAVEDOCUMENTFLAGS_0, 
                c4d.FORMAT_FILMBOX_FBX
            )

# Usage
batch_export("C:/Exports")
```

### Material Creator

```python
def create_material(name, color=c4d.Vector(1, 0, 0)):
    # Create material
    mat = c4d.BaseMaterial(c4d.Mmaterial)
    mat[c4d.ID_BASELIST_NAME] = name
    
    # Set color
    mat[c4d.MATERIAL_COLOR_COLOR] = color
    
    # Insert and update
    doc.InsertMaterial(mat)
    c4d.EventAdd()
    
    return mat
```

### UV Unwrap

```python
def auto_uv(obj):
    # Create UVW tag
    uvw_tag = c4d.utils.SendModelingCommand(
        command=c4d.MCOMMAND_GENERATEUVW,
        list=[obj],
        mode=c4d.MODELINGCOMMANDMODE_ALL,
        doc=doc
    )
    
    return uvw_tag
```

---

## Best Practices

### Code Organization
- Use functions for reusability
- Add error handling
- Comment complex operations
- Use meaningful names

### Performance
- Minimize undo operations
- Batch changes
- Use GetCache() for generators
- Optimize loops

### User Experience
- Provide progress feedback
- Show clear error messages
- Add helpful dialogs
- Validate inputs

---

## Resources

### Official Documentation
- [Cinema 4D Python SDK](https://developers.maxon.net/docs/cpp/2023_2/pages/manuals/c4d_python/sdk_overview.html)
- [Cinema 4D SDK](https://developers.maxon.net/)

### Community Resources
- CGSociety Cinema 4D
- Reddit r/Cinema4D
- Maxon Community

---

## Usage Examples

```
"Use cinema4d-master skill to create Python script for batch export"
"Use cinema4d-master skill to create MoGraph cloner setup"
"Use cinema4d-master skill to write XPresso expression for rig"
"Use cinema4d-master skill to automate material assignment"
```
