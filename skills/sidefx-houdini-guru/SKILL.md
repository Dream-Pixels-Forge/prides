---
name: sidefx-houdini-guru
description: Expert guidance for SideFX Houdini VEX scripting, Python tools, and HDA creation. Use for procedural modeling, VEX shaders, digital assets, and Houdini automation.
license: Complete terms in LICENSE.txt
---

# SideFX Houdini Development Guide

You are a Houdini expert specializing in VEX scripting, Python tools, HDA creation, and procedural workflows.

## Core Capabilities

### 1. VEX Programming
- VEX shaders and wrangles
- Point, primitive, vertex operations
- Custom functions and includes
- Performance optimization

### 2. Python Scripting
- Scene manipulation
- Custom tools and dialogs
- Batch processing
- Pipeline integration

### 3. HDA Development
- Digital Asset creation
- Parameter interfaces
- Version control for HDAs
- Asset distribution

### 4. Procedural Workflows
- Procedural modeling
- Particle systems
- VDB volumes
- Procedural animation

---

## VEX Fundamentals

### Attribute Wrangle (Points)

```c
// Add noise to point positions
vector noise = noise(chf("scale") * @P);
@P += noise * chf("amount");

// Color by height
@Cd = fit(@P.y, 0, 10, {0, 0.5, 1}, {1, 0.8, 0.2});

// Store distance from center
@dist = length(@P);

// Create unique ID
@id = @ptnum;
```

### Attribute Wrangle (Primitives)

```c
// Random primitive selection
if (rand(@primnum + chf("seed")) < chf("probability")) {
    @selected = 1;
} else {
    @selected = 0;
}

// Area-based coloring
float area = @area;
@Cd = fit(area, 0, 1, {0, 0, 1}, {1, 0, 0});
```

### Point Wrangle - Nearest Neighbor

```c
int pt = nearpoint(0, @ptnum);
vector neighbor_pos = point(0, "P", pt);
vector dir = normalize(neighbor_pos - @P);
@N = dir;
```

### VEX Functions

```c
// Custom function
function vector customNoise(vector pos; float scale)
{
    return noise(pos * scale) * scale;
}

// Usage
@P += customNoise(@P, chf("scale"));
```

### Include Files

```c
// my_includes.h
#define PI 3.14159265
#define TAU (PI * 2)

vector polarToCart(float r, float theta)
{
    return set(r * cos(theta), r * sin(theta), 0);
}
```

---

## Common VEX Patterns

### Attribute Creation

```c
// Float attribute
@my_float = 1.0;

// Vector attribute
@my_vector = set(1, 0, 0);

// String attribute
@s@my_string = "value";

// Integer array
i[]@my_array = array(1, 2, 3);

// Matrix
matrix3 m = ident();
rotate(m, radians(45), {0, 1, 0});
@orient = m;
```

### Attribute Transfer

```c
// From nearest point
int pt = nearpoint(0, @ptnum);
@Cd = point(0, "Cd", pt);

// From attribute sample
float val = sample_attribute(0, "my_attr", @P);

// Blur attribute
@Cd_avg = average(0, "Cd", @ptnum, chf("radius"));
```

### Group Operations

```c
// Add to group
if (@P.y > chf("threshold")) {
    i@group_high_points = 1;
}

// Remove from group
if (@P.y < 0) {
    i@group_low_points = 0;
}

// Toggle group
i@group_toggle = !i@group_toggle;
```

### Random Operations

```c
// Random per point
float r = rand(@ptnum);

// Random with seed
float r = rand(@ptnum + chf("seed"));

// Random in range
float r = fit01(rand(@ptnum), chf("min"), chf("max"));

// Random choice
int choices[] = array(1, 2, 3, 4, 5);
int choice = choices[int(rand(@ptnum) * len(choices))];
```

---

## Python Scripting

### Scene Manipulation

```python
import hou

# Get nodes
obj = hou.node("/obj")
geo = obj.createNode("geo", "my_geometry")

# Create nodes inside geo
box = geo.createNode("box")
transform = geo.createNode("xform")
transform.setInput(0, box)
transform.parm("tx").set(5.0)

# Layout and display
geo.layoutChildren()
transform.setDisplayFlag(True)
transform.setRenderFlag(True)
```

### Attribute Operations

```python
geo = hou.node("/obj/geo1")
attrib = geo.findPointAttrib("Cd")

# Create attribute
geo.addAttrib(hou.attribType.Point, "my_float", 0.0)

# Set attribute values
for point in geo.points():
    point.setAttribValue("my_float", point.number() * 0.1)
```

### Batch Processing

```python
import hou

# Process all selected nodes
for node in hou.selectedNodes():
    if node.type().name() == "box":
        node.parm("size").set(2.0)

# Batch render
for frame in range(1, 101):
    hou.setFrame(frame)
    hou.hscript("render -f 1")
```

### Custom Dialog

```python
import hou
import PySide2.QtWidgets as QtWidgets

class MyDialog(QtWidgets.QDialog):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("My Tool")
        
        layout = QtWidgets.QVBoxLayout()
        
        # Add widgets
        self.value_spin = QtWidgets.QDoubleSpinBox()
        self.value_spin.setRange(0, 100)
        layout.addWidget(self.value_spin)
        
        # Buttons
        button = QtWidgets.QPushButton("Apply")
        button.clicked.connect(self.apply)
        layout.addWidget(button)
        
        self.setLayout(layout)
    
    def apply(self):
        value = self.value_spin.value()
        # Apply value to selected nodes
        for node in hou.selectedNodes():
            node.parm("size").set(value)

# Show dialog
dialog = MyDialog()
dialog.show()
```

---

## HDA Creation

### Creating Digital Assets

```python
import hou

# Create HDA
node = hou.node("/obj/geo1")
node.createDigitalAsset(
    name="MyAsset::1.0",
    description="My custom asset",
    save_as_embedded=False
)

# Set parameters
type_def = node.type().definition()
parms = type_def.parmTemplateGroup()

# Add new parameter
folder = hou.FolderParmTemplate("folder", "Settings")
folder.addParmTemplate(hou.FloatParmTemplate("scale", "Scale", 1))
parms.append(folder)

type_def.setParmTemplateGroup(parms)
```

### Parameter Interface

```python
# Create parameter folder
folder = hou.FolderParmTemplate("settings", "Settings")

# Float parameter
float_parm = hou.FloatParmTemplate("amount", "Amount", 1, 
                                    default_value=(1.0,),
                                    min=0.0, max=10.0)
folder.addParmTemplate(float_parm)

# Toggle parameter
toggle = hou.ToggleParmTemplate("enable", "Enable", default_value=True)
folder.addParmTemplate(toggle)

# Menu parameter
menu = hou.MenuParmTemplate("mode", "Mode", 1,
                            menu_items=["add", "multiply", "subtract"],
                            menu_labels=["Add", "Multiply", "Subtract"])
folder.addParmTemplate(menu)

# File parameter
file_parm = hou.FileParmTemplate("file", "File", 1,
                                 file_type=hou.fileType.Image)
folder.addParmTemplate(file_parm)
```

### Version Control for HDAs

```python
# Update HDA version
node = hou.selectedNode()
type_def = node.type().definition()

# Set version
type_def.setVersion("2.0")

# Save to file
type_def.saveToFile("$HIP/hdas/MyAsset-2.0.otl")

# Update all instances
hou.hda.installFile("$HIP/hdas/MyAsset-2.0.otl")
```

---

## Procedural Workflows

### Procedural Modeling

```
1. Scatter points on surface
2. Instance geometry on points
3. Apply variations with VEX
4. Pack and instance for performance
```

### VEX Variation Example

```c
// Variation wrangle
float scale = fit01(rand(@ptnum), 0.8, 1.2);
@scale = set(scale, scale, scale);

float rotation = rand(@ptnum + 1) * 360;
matrix3 m = ident();
rotate(m, radians(rotation), {0, 1, 0});
@orient = m;
```

### Particle System Setup

```
1. POP Network
2. POP Source (emit from surface)
3. POP Force (add turbulence)
4. POP Drag (add air resistance)
5. POP Wrangle (custom behavior)
```

### VDB Workflow

```
1. Convert to VDB (from mesh)
2. VDB Smooth
3. VDB Expand/Collapse
4. Convert back to mesh
```

---

## Performance Optimization

### VEX Optimization

```c
// ✅ Good: Use built-in functions
@Cd = noise(@P * 10);

// ❌ Bad: Manual implementation
float val = sin(@P.x * 10) * cos(@P.y * 10);

// ✅ Good: Minimize lookups
vector pos = @P;
float noise_val = noise(pos);

// ❌ Bad: Repeated lookups
float noise_val = noise(@P);
vector modified = @P + noise(@P);
```

### Python Optimization

```python
# ✅ Good: Batch operations
geo = hou.node("/obj/geo1")
with hou.Transaction("Batch Update"):
    for point in geo.points():
        point.setAttribValue("Cd", (1, 0, 0))

# ❌ Bad: Individual operations
for point in geo.points():
    point.setAttribValue("Cd", (1, 0, 0))
    # Each call triggers update
```

---

## Common Tools

### Scatter Tool

```python
import hou
import random

def scatter_points(geo, count, seed=0):
    random.seed(seed)
    for i in range(count):
        prim = random.choice(geo.prims())
        u = random.random()
        v = random.random()
        pos = prim.barycentricPosition(u, v)
        geo.createPoint().setPosition(pos)
```

### UV Unwrap Tool

```python
import hou

def auto_uv(node):
    uvquick = node.createNode("uvquick")
    uvquick.parm("layout").set(0)  # Flatten
    uvquick.setDisplayFlag(True)
    node.layoutChildren()
```

### LOD Generator

```python
import hou

def create_lod(node, levels=[100, 50, 25]):
    geo = node.parent()
    lods = []
    
    for i, level in enumerate(levels):
        remesh = geo.createNode("remesh")
        remesh.setInput(0, node)
        remesh.parm("targetprims").set(level)
        lods.append(remesh)
    
    geo.layoutChildren()
    return lods
```

---

## Best Practices

### VEX Best Practices
- Use `@` syntax for attributes
- Prefer wrangles over SOPs for performance
- Use channels (`chf()`) for parameters
- Comment complex VEX code
- Test with small point counts first

### Python Best Practices
- Use `hou` module consistently
- Handle exceptions gracefully
- Use transactions for batch operations
- Cache frequently accessed nodes
- Document custom tools

### HDA Best Practices
- Use meaningful parameter names
- Group related parameters
- Provide helpful tooltips
- Test with different inputs
- Version control your HDAs

---

## Resources

### Official Documentation
- [Houdini Help](https://www.sidefx.com/docs/)
- [VEX Reference](https://www.sidefx.com/docs/houdini/vex/index.html)
- [Python API](https://www.sidefx.com/docs/houdini/hom/index.html)

### Community Resources
- Odforce Forums
- Houdini Discord
- CGWiki (tokeru.com/cgwiki)
- Houdini Reddit

---

## Usage Examples

```
"Use sidefx-houdini-guru skill to create a procedural building generator"
"Use sidefx-houdini-guru skill to write VEX for point scattering"
"Use sidefx-houdini-guru skill to create a custom HDA with parameters"
"Use sidefx-houdini-guru skill to optimize a slow simulation"
"Use sidefx-houdini-guru skill to create Python batch processing tool"
```
