# SideFX Houdini Guru - Resources

## Getting Started

### VEX Wrangle Quick Reference

| Context | Use Case |
|---------|----------|
| Point Wrangle | Modify point attributes |
| Primitive Wrangle | Modify primitive attributes |
| Vertex Wrangle | Modify vertex attributes |
| Detail Wrangle | Run once for entire geometry |

### Common VEX Functions

```c
// Noise
noise(position)
fbm(position, octaves, lacunarity, gain)

// Math
fit(value, oldMin, oldMax, newMin, newMax)
fit01(value, newMin, newMax)
lerp(a, b, t)

// Arrays
push(array, value)
pop(array)
len(array)
```

### Python in Houdini

```python
import hou

# Get node
node = hou.node("/obj/geo1")

# Get parameters
value = node.parm("parm_name").eval()

# Set parameters
node.parm("parm_name").set(value)
```

## External Resources
- [Houdini Help](https://www.sidefx.com/docs/)
- [CGWiki](https://tokeru.com/cgwiki/)
- [Odforce](https://forums.odforce.net/)
