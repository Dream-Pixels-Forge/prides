---
name: foundry-nuke-master
description: Expert guidance for Foundry Nuke Python scripting, PyNodes, gizmo creation, and pipeline integration. Use for compositing automation, custom tools, and node graph manipulation.
license: Complete terms in LICENSE.txt
---

# Foundry Nuke Scripting Guide

You are a Nuke expert specializing in Python scripting, PyNodes, gizmo creation, and pipeline integration.

## Core Capabilities

### 1. Python Scripting
- Node graph manipulation
- Batch processing
- Pipeline integration
- Custom tools

### 2. PyNodes
- Procedural node creation
- Custom node operations
- Expression automation
- Node graph generation

### 3. Gizmo Development
- Custom gizmo creation
- Parameter interfaces
- Knob callbacks
- User controls

### 4. Pipeline Integration
- Read/Write nodes
- Version control
- Render farm integration
- Asset management

---

## Nuke Script Structure

### Basic Script Template

```python
import nuke
import nukescripts

def main():
    """Main script function."""
    
    # Check for selected nodes
    selected = nuke.selectedNodes()
    if not selected:
        nuke.message("Please select at least one node.")
        return
    
    # Process selected nodes
    for node in selected:
        process_node(node)
    
    nuke.message("Script completed successfully!")

def process_node(node):
    """Process a single node."""
    # Your logic here
    pass

if __name__ == "__main__":
    main()
```

### Menu Integration

```python
import nuke

# Add menu item
nuke.menu("Nuke").addCommand(
    "My Tools/My Script",
    "my_module.my_function()",
    icon="my_icon.png"
)

# Add to Node menu
nuke.menu("Nodes").addCommand(
    "My Tools/My Node",
    "nuke.createNode('MyNode')",
    icon="my_icon.png"
)
```

---

## Node Operations

### Create Nodes

```python
import nuke

# Create basic node
transform = nuke.createNode("Transform")

# Create with parameters
transform = nuke.createNode("Transform", "translate {100 50}")

# Create in specific group
with nuke.Group():
    inside_node = nuke.createNode("Grade")

# Create and connect
read = nuke.createNode("Read")
transform = nuke.createNode("Transform")
transform.setInput(0, read)
```

### Get Nodes

```python
# Selected nodes
selected = nuke.selectedNodes()

# All nodes in script
all_nodes = nuke.allNodes()

# Nodes by class
transforms = [n for n in nuke.allNodes() if n.Class() == "Transform"]

# Nodes by name
my_node = nuke.toNode("Transform1")

# Root node
root = nuke.root()
```

### Modify Nodes

```python
node = nuke.toNode("Transform1")

# Set knob values
node["translate"].setValue([100, 50])
node["scale"].setValue(2.0)
node["rotate"].setValue(45)

# Set expressions
node["translate"].setExpression("time * 10", 0)  # X channel
node["translate"].setExpression("time * 5", 1)   # Y channel

# Add user knobs
nuke.Double_Knob("my_value", "My Value")
node.addKnob(knob)

# Remove knobs
node.removeKnob(knob)
```

---

## Knob Operations

### Get/Set Values

```python
node = nuke.toNode("Grade1")

# Get value
value = node["gain"].value()

# Set value
node["gain"].setValue(1.5)

# Get animated value at frame
value = node["gain"].getValueAtTime(10)

# Set keyframe
node["gain"].setValueAtTime(1.0, 1)
node["gain"].setValueAtTime(2.0, 10)

# Get animation curve
curve = node["gain"].animation(0)
```

### Knob Types

```python
# String Knob
string_knob = nuke.String_Knob("filename", "Filename", "default.exr")

# Int Knob
int_knob = nuke.Int_Knob("iterations", "Iterations", 10)

# Double Knob
double_knob = nuke.Double_Knob("value", "Value", 1.0)

# Boolean Knob
bool_knob = nuke.Boolean_Knob("enabled", "Enabled", True)

# Color Knob
color_knob = nuke.Color_Knob("color", "Color", [1, 0, 0, 1])

# Array Knob (multiple values)
array_knob = nuke.Array_Knob("matrix", 16, [1,0,0,0, 0,1,0,0, 0,0,1,0, 0,0,0,1])

# File Knob
file_knob = nuke.File_Knob("file", "File", "/path/to/file.exr")

# Tab Knob
tab_knob = nuke.Tab_Knob("Settings", nuke.TABBEGIN)
```

---

## Node Graph Manipulation

### Auto-Layout

```python
def auto_layout_nodes(nodes=None, direction="horizontal"):
    """Auto-layout selected nodes."""
    if nodes is None:
        nodes = nuke.selectedNodes()
    
    if not nodes:
        return
    
    # Sort nodes by input order
    sorted_nodes = sorted(nodes, key=lambda n: n.xpos())
    
    # Position nodes
    x_pos = 100
    y_pos = 100
    spacing = 200
    
    for node in sorted_nodes:
        node.setXpos(x_pos)
        node.setYpos(y_pos)
        x_pos += spacing

# Usage
auto_layout_nodes()
```

### Connect Nodes

```python
def connect_nodes(input_node, output_node, input_socket=0):
    """Connect two nodes."""
    output_node.setInput(input_socket, input_node)
    return output_node

def chain_nodes(nodes):
    """Chain multiple nodes together."""
    for i in range(len(nodes) - 1):
        nodes[i + 1].setInput(0, nodes[i])
    return nodes[-1]

# Usage
read = nuke.createNode("Read")
transform = nuke.createNode("Transform")
write = nuke.createNode("Write")

chain_nodes([read, transform, write])
```

### Find Upstream/Downstream

```python
def get_upstream_nodes(node, visited=None):
    """Get all upstream nodes recursively."""
    if visited is None:
        visited = set()
    
    if node in visited:
        return []
    
    visited.add(node)
    upstream = [node]
    
    for i in range(node.inputs()):
        input_node = node.input(i)
        if input_node:
            upstream.extend(get_upstream_nodes(input_node, visited))
    
    return upstream

def get_downstream_nodes(node):
    """Get all downstream nodes."""
    downstream = []
    for n in nuke.allNodes():
        for i in range(n.inputs()):
            if n.input(i) == node:
                downstream.append(n)
                downstream.extend(get_downstream_nodes(n))
    return downstream
```

---

## Batch Processing

### Batch Render

```python
import nuke
import os

def batch_render(scripts, output_dir):
    """Render multiple Nuke scripts."""
    for script in scripts:
        # Open script
        nuke.scriptOpen(script)
        
        # Get write nodes
        writes = [n for n in nuke.allNodes() if n.Class() == "Write"]
        
        # Execute writes
        for write in writes:
            # Set output path
            output_path = os.path.join(output_dir, os.path.basename(script))
            write["file"].setValue(output_path)
            
            # Render
            nuke.execute(write, 1, 100)
        
        # Close script
        nuke.scriptClose()

# Usage
scripts = ["comp1.nk", "comp2.nk", "comp3.nk"]
batch_render(scripts, "/output/path")
```

### Replace Paths

```python
def replace_paths(old_path, new_path):
    """Replace file paths in all Read/Write nodes."""
    for node in nuke.allNodes():
        if node.Class() in ["Read", "Write"]:
            file_knob = node["file"]
            current = file_knob.value()
            if old_path in current:
                new = current.replace(old_path, new_path)
                file_knob.setValue(new)
                print(f"Updated {node.name()}: {new}")

# Usage
replace_paths("/old/project", "/new/project")
```

### Version Update

```python
def update_versions(old_version, new_version):
    """Update version numbers in file paths."""
    for node in nuke.allNodes():
        if node.Class() in ["Read", "Write"]:
            file_knob = node["file"]
            current = file_knob.value()
            if f"_v{old_version:03d}" in current:
                new = current.replace(f"_v{old_version:03d}", f"_v{new_version:03d}")
                file_knob.setValue(new)

# Usage
update_versions(1, 2)
```

---

## Gizmo Creation

### Basic Gizmo

```python
# Create group
group = nuke.createNode("Group")
group.setName("MyGizmo")

# Enter group
nuke.intoGroup()

# Create nodes inside group
input1 = nuke.createNode("Input", "name input1")
input2 = nuke.createNode("Input", "name input2")
merge = nuke.createNode("Merge")
output = nuke.createNode("Output")

# Connect
merge.setInput(0, input1)
merge.setInput(1, input2)
output.setInput(0, merge)

# Expose knobs
merge["operation"].setFlag(nuke.STARTLINE)
nuke.addUserKnob("Operation", nuke.A_KNOB, merge["operation"])

# Exit group
nuke.exitGroup()

# Save as gizmo
nuke.saveToolScript(group, "MyGizmo.gizmo")
```

### Custom Gizmo with Callbacks

```python
def my_callback():
    """Knob callback function."""
    node = nuke.thisNode()
    value = node["my_value"].value()
    nuke.message(f"Value changed to: {value}")

# Create gizmo
group = nuke.createNode("Group")
nuke.intoGroup()

# Add knobs
nuke.addUserKnob("my_value", nuke.DOUBLE_KNOB, 1.0)
nuke.addUserKnob("my_button", nuke.BUTTON_KNOB, "Click Me", my_callback)

nuke.exitGroup()
```

---

## Pipeline Integration

### Read Node Template

```python
def create_read_node(template):
    """Create Read node with template path."""
    read = nuke.createNode("Read")
    read["file"].setValue(template)
    read["label"].setValue(template.split("/")[-1])
    return read

# Usage with tokens
template = "/show/shot/seq/layer.%04d.exr"
create_read_node(template)
```

### Write Node Template

```python
def create_write_node(output_template):
    """Create Write node with output template."""
    write = nuke.createNode("Write")
    write["file"].setValue(output_template)
    write["file_type"].setValue("exr")
    write["colorspace"].setValue("linear")
    return write

# Usage
output = "/renders/show/shot/layer.%04d.exr"
create_write_node(output)
```

### Render Farm Submission

```python
def submit_to_renderfarm(script_path, frames="1-100"):
    """Submit script to render farm."""
    import subprocess
    
    cmd = [
        "Nuke13.0",
        "-t",  # Render in background
        "-X",  # Execute script
        script_path,
        "-F", frames
    ]
    
    subprocess.run(cmd)
    print(f"Submitted {script_path} for frames {frames}")
```

---

## Expressions

### Common Expressions

```python
# Time-based
time * 10
sin(time) * 50

# Parent/Child relationship
parent_node.translate.x

# Random (per object)
rand(id)

# Clamp
clamp(value, 0, 1)

# If/else
value > 0.5 ? 1 : 0

# Access other node
Node1.translate.x
```

### Expression via Python

```python
node = nuke.toNode("Transform1")
node["translate"].setExpression("time * 10", 0)
node["translate"].setExpression("sin(time) * 50", 1)
```

---

## Best Practices

### Code Organization
- Use functions for reusability
- Add error handling
- Comment complex operations
- Use meaningful variable names

### Performance
- Minimize undo stack operations
- Batch knob changes
- Use nuke.UndoDisabled() for bulk operations
- Cache node references

### User Experience
- Provide progress feedback
- Show clear error messages
- Validate inputs
- Add helpful tooltips

---

## Resources

### Official Documentation
- [Nuke Python API](https://learn.foundry.com/nuke/developers/13.0/pythondevguide/)
- [Nuke Scripting Guide](https://learn.foundry.com/nuke/developers/13.0/scriptdevguide/)

### Community Resources
- Nukepedia
- Foundry Community
- CGSociety Nuke Forum

---

## Usage Examples

```
"Use foundry-nuke-master skill to create batch render script"
"Use foundry-nuke-master skill to create custom gizmo"
"Use foundry-nuke-master skill to replace file paths in comp"
"Use foundry-nuke-master skill to auto-layout node graph"
"Use foundry-nuke-master skill to create pipeline integration tools"
```
