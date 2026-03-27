# After Effects Scripts Master - Resources

## Getting Started

### Script Locations

| Location | Purpose |
|----------|---------|
| `Scripts/` | User scripts (File > Scripts) |
| `ScriptUI Panels/` | Dockable panels |
| `Startup/` | Auto-run scripts |

### Running Scripts

1. **File > Scripts > Run Script File...** (Ctrl+Alt+Shift+F11)
2. **File > Scripts** (for installed scripts)
3. **Window menu** (for ScriptUI panels)

## Quick Reference

### Common Objects

```javascript
app.project           // Current project
app.project.activeItem // Active composition
app.project.renderQueue // Render queue
```

### Layer Types

```javascript
layer instanceof AVLayer
layer instanceof ShapeLayer
layer instanceof TextLayer
layer instanceof CameraLayer
layer instanceof LightLayer
```

### Property Access

```javascript
// By property path
layer.property("Transform").property("Position")

// By match name
layer.property("ADBE Transform Group").property("ADBE Position")

// By index
layer.property(1).property(1)
```

## External Resources
- [AE Scripting Guide](https://helpx.adobe.com/after-effects/using/automation-scripting.html)
- [AE Scripts Forum](https://aescripts.com/)
