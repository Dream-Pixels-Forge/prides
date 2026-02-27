---
name: after-effects-scripts-master
description: Expert guidance for Adobe After Effects scripting (ExtendScript/JavaScript). Use for automation, batch processing, custom tools, and workflow optimization in After Effects.
license: Complete terms in LICENSE.txt
---

# After Effects Scripting Guide

You are an After Effects scripting expert specializing in ExtendScript/JavaScript automation, batch processing, and custom tool development.

## Core Capabilities

### 1. Script Automation
- Automate repetitive tasks
- Batch render compositions
- Project organization
- Asset management

### 2. Expression Development
- Write custom expressions
- Expression controllers
- Link properties
- Dynamic animations

### 3. Panel/Extension Development
- ScriptUI panels
- Custom interfaces
- Dockable panels
- CEP extensions

### 4. Pipeline Integration
- Render queue management
- File I/O operations
- Third-party integration
- Version control

---

## Script Structure

### Basic Script Template

```javascript
// After Effects Script Template
#target aftereffects

(function myScript() {
    'use strict';
    
    // Check for open project
    if (!app.project) {
        alert("Please open or create a project first.");
        return;
    }
    
    var project = app.project;
    
    // Main script logic
    main();
    
    function main() {
        // Your code here
        log("Script executed successfully");
    }
    
    function log(message) {
        $.writeln("[MyScript] " + message);
    }
    
})();
```

### ScriptUI Panel Template

```javascript
#target aftereffects

(function createPanel() {
    'use strict';
    
    var palette = (this instanceof Panel) ? this : new Window("palette", "My Panel", undefined, {resizeable: true});
    
    palette.orientation = "column";
    palette.alignChildren = ["fill", "top"];
    palette.margins = 10;
    
    // UI Elements
    var btnRender = palette.add("button", undefined, "Render Selected");
    var btnOrganize = palette.add("button", undefined, "Organize Project");
    var progress = palette.add("progressbar", undefined, 0, 100);
    
    // Event handlers
    btnRender.onClick = function() {
        renderSelected();
    };
    
    btnOrganize.onClick = function() {
        organizeProject();
    };
    
    // Functions
    function renderSelected() {
        var comp = app.project.activeItem;
        if (comp && comp instanceof CompItem) {
            addToRenderQueue(comp);
        }
    }
    
    function addToRenderQueue(comp) {
        var rqItem = app.project.renderQueue.items.add(comp);
        rqItem.render = true;
    }
    
    // Show panel
    if (palette instanceof Window) {
        palette.show();
    }
    
})();
```

---

## Project Operations

### Create New Project

```javascript
function createNewProject() {
    app.project = app.newProject();
    
    // Create folder structure
    var comps = app.project.items.addFolder("Compositions");
    var footage = app.project.items.addFolder("Footage");
    var renders = app.project.items.addFolder("Renders");
    var audio = app.project.items.addFolder("Audio");
    
    return {
        project: app.project,
        comps: comps,
        footage: footage,
        renders: renders,
        audio: audio
    };
}
```

### Import Files

```javascript
function importFiles(filePaths, parentFolder) {
    var items = [];
    
    for (var i = 0; i < filePaths.length; i++) {
        var file = new File(filePaths[i]);
        if (file.exists) {
            var item = app.project.importFile(new ImportOptions(file));
            if (parentFolder) {
                item.parentFolder = parentFolder;
            }
            items.push(item);
        }
    }
    
    return items;
}
```

### Organize Project

```javascript
function organizeProject() {
    var project = app.project;
    
    // Create folders
    var comps = getOrCreateFolder("Compositions");
    var solids = getOrCreateFolder("Solids");
    var lights = getOrCreateFolder("Lights");
    var cameras = getOrCreateFolder("Cameras");
    
    // Organize items
    for (var i = 1; i <= project.items.length; i++) {
        var item = project.item(i);
        
        if (item instanceof CompItem) {
            item.parentFolder = comps;
        } else if (item instanceof FootageItem) {
            if (item.mainSource instanceof SolidSource) {
                item.parentFolder = solids;
            }
        }
    }
    
    function getOrCreateFolder(name) {
        for (var j = 1; j <= project.items.length; j++) {
            var folder = project.item(j);
            if (folder instanceof FolderItem && folder.name === name) {
                return folder;
            }
        }
        return project.items.addFolder(name);
    }
}
```

---

## Composition Operations

### Create Composition

```javascript
function createComposition(name, width, height, duration, framerate) {
    var comp = app.project.items.addComp(
        name,
        width || 1920,
        height || 1080,
        1, // pixel aspect ratio
        duration || 10, // seconds
        framerate || 30
    );
    
    return comp;
}
```

### Add Layers

```javascript
function addLayerToComp(comp, item) {
    var layer = comp.layers.add(item);
    return layer;
}

function createSolidLayer(comp, name, width, height, color, duration) {
    var solid = comp.layers.addSolid(
        color || [1, 1, 1],
        name || "Solid",
        width || comp.width,
        height || comp.height,
        1, // pixel aspect ratio
        duration || comp.duration
    );
    return solid;
}

function createNullLayer(comp) {
    var nullLayer = comp.layers.addNull();
    return nullLayer;
}

function createCameraLayer(comp, name) {
    var camera = comp.layers.addCamera(name || "Camera", [comp.width/2, comp.height/2]);
    return camera;
}
```

### Layer Manipulation

```javascript
function duplicateLayer(layer) {
    var comp = layer.containingComp;
    layer.selected = true;
    
    // Duplicate
    app.executeCommand(app.findMenuCommandId("Duplicate"));
    
    // Get duplicated layer
    return comp.layer(layer.index + 1);
}

function precomposeLayers(layers, name) {
    if (layers.length === 0) return null;
    
    var comp = layers[0].containingComp;
    
    // Select all layers
    for (var i = 1; i <= comp.layers.length; i++) {
        comp.layer(i).selected = false;
    }
    
    for (var j = 0; j < layers.length; j++) {
        layers[j].selected = true;
    }
    
    // Precompose
    comp.layers.precompose(layers, name || "Precomp", true);
    
    return comp.layers[1]; // Return precomp layer
}
```

---

## Property & Keyframe Operations

### Get Properties

```javascript
function getProperty(layer, propertySpec) {
    // propertySpec: ["Transform", "Position"] or "Position"
    var prop = layer.property(propertySpec);
    return prop;
}

function getPropertyValue(layer, propertySpec, time) {
    var prop = getProperty(layer, propertySpec);
    if (time !== undefined) {
        return prop.valueAtTime(time, true);
    }
    return prop.value;
}
```

### Set Keyframes

```javascript
function setKeyframe(layer, propertySpec, time, value) {
    var prop = getProperty(layer, propertySpec);
    
    // Add keyframe at time
    var keyIndex = prop.addKey(time);
    
    // Set value
    if (value !== undefined) {
        prop.setValueAtTime(time, value);
    }
    
    return keyIndex;
}

function setLinearKeyframes(layer, propertySpec, keyframes) {
    // keyframes: [{time: 0, value: [0, 0]}, {time: 1, value: [100, 100]}]
    var prop = getProperty(layer, propertySpec);
    
    for (var i = 0; i < keyframes.length; i++) {
        var kf = keyframes[i];
        prop.setValueAtTime(kf.time, kf.value);
        
        // Set interpolation
        if (i < keyframes.length - 1) {
            prop.setInterpolationTypeAtKey(i + 1, KeyframeInterpolationType.LINEAR);
        }
    }
}

function easeKeyframes(layer, propertySpec, keyframes) {
    var prop = getProperty(layer, propertySpec);
    
    for (var i = 0; i < keyframes.length; i++) {
        var kf = keyframes[i];
        prop.setValueAtTime(kf.time, kf.value);
        
        // Easy ease
        prop.setEasyEaseAtKey(i + 1);
    }
}
```

### Animation Presets

```javascript
function applyAnimationPreset(layer, presetPath) {
    // presetPath: "Presets/Text/Animate In/Fade In.ffx"
    layer.selected = true;
    app.loadProjectPreset(presetPath);
}

function saveAnimationPreset(layer, propertySpec, presetPath) {
    var prop = getProperty(layer, propertySpec);
    prop.selected = true;
    app.saveProjectPreset(presetPath);
}
```

---

## Render Queue Operations

### Add to Render Queue

```javascript
function addToRenderQueue(comp, outputModule, renderQueueItem) {
    var rqItem = app.project.renderQueue.items.add(comp);
    rqItem.render = true;
    
    // Set output module
    if (outputModule) {
        var om = rqItem.outputModule(1);
        om.applyTemplate(outputModule);
    }
    
    // Set output path
    if (renderQueueItem && renderQueueItem.outputPath) {
        var om = rqItem.outputModule(1);
        om.file = new File(renderQueueItem.outputPath);
    }
    
    return rqItem;
}
```

### Batch Render

```javascript
function batchRender(compositions, outputPath) {
    var rq = app.project.renderQueue;
    
    for (var i = 0; i < compositions.length; i++) {
        var comp = compositions[i];
        var rqItem = rq.items.add(comp);
        rqItem.render = true;
        
        // Set output
        var om = rqItem.outputModule(1);
        om.applyTemplate("H.264");
        om.file = new File(outputPath + "/" + comp.name + ".mp4");
    }
    
    // Start render
    rq.render();
}
```

### Render Settings

```javascript
function configureRenderSettings(rqItem, settings) {
    // settings: {quality: "BEST", resolution: "FULL", frameRate: 30}
    
    rqItem.skipFrames = false;
    
    if (settings.quality) {
        rqItem.quality = settings.quality;
    }
    
    if (settings.resolution) {
        rqItem.resolutionFactor = [
            settings.resolution === "FULL" ? 1 : 2,
            settings.resolution === "FULL" ? 1 : 2
        ];
    }
    
    if (settings.frameRate) {
        rqItem.timeSpanStart = 0;
        rqItem.timeSpanDuration = rqItem.comp.duration;
    }
}
```

---

## Expressions

### Common Expressions

```javascript
// Wiggle
wiggle(5, 50);

// Loop
loopOut("cycle");
loopIn("cycle");

// Time-based
time * 100;
Math.sin(time * 2 * Math.PI);

// Link to other layer
thisComp.layer("Null 1").transform.position;

// Random
seedRandom(1, true);
random(0, 100);

// Clamp
clamp(value, 0, 100);

// Ease
ease(time, 0, 1, 0, 100);
```

### Expression Controllers

```javascript
// Slider control
var slider = effect("Slider Control")("Slider");
slider;

// Color control
var color = effect("Color Control")("Color");
color;

// Checkbox control
var checkbox = effect("Checkbox Control")("Checkbox");
if (checkbox) {
    // Do something
}
```

---

## File Operations

### Save Project

```javascript
function saveProject(path) {
    var file = new File(path);
    app.project.save(file);
}

function saveProjectIncremental() {
    var currentPath = app.project.file;
    if (currentPath) {
        var baseName = currentPath.name.replace(/\.aep$/, "");
        var folder = currentPath.parent;
        
        // Find next version
        var version = 1;
        var files = folder.getFiles();
        for (var i = 0; i < files.length; i++) {
            if (files[i].name.indexOf(baseName) === 0) {
                var match = files[i].name.match(/_v(\d+)\.aep$/);
                if (match && parseInt(match[1]) >= version) {
                    version = parseInt(match[1]) + 1;
                }
            }
        }
        
        var newPath = folder.fsName + "/" + baseName + "_v" + version + ".aep";
        app.project.save(new File(newPath));
    }
}
```

### Export

```javascript
function exportFrame(comp, time, path) {
    comp.saveFrameToJPEG(time, true, 100, new File(path));
}

function exportSequence(comp, startFrame, endFrame, pathTemplate) {
    for (var f = startFrame; f <= endFrame; f++) {
        var time = f / comp.frameRate;
        var path = pathTemplate.replace("#", f);
        exportFrame(comp, time, path);
    }
}
```

---

## Best Practices

### Code Organization
- Use IIFE pattern to avoid global pollution
- Separate UI logic from business logic
- Use meaningful variable names
- Add comments for complex operations

### Error Handling
```javascript
try {
    // Risky operation
} catch (e) {
    alert("Error: " + e.toString());
}
```

### Performance
- Minimize UI updates in loops
- Cache frequently accessed objects
- Use batch operations when possible
- Disable redraw during bulk operations

### User Experience
- Provide progress feedback
- Show clear error messages
- Allow cancellation of long operations
- Save user preferences

---

## Resources

### Official Documentation
- [After Effects Scripting Guide](https://helpx.adobe.com/after-effects/using/automation-scripting.html)
- [ExtendScript Toolkit](https://helpx.adobe.com/illustrator/using/creating-javascript-script.html)

### Community Resources
- AE Scripts Forum
- Creative COW
- GitHub AE Scripts

---

## Usage Examples

```
"Use after-effects-scripts-master skill to create a batch render script"
"Use after-effects-scripts-master skill to automate project organization"
"Use after-effects-scripts-master skill to create a custom ScriptUI panel"
"Use after-effects-scripts-master skill to write expressions for linking properties"
"Use after-effects-scripts-master skill to create a title generator tool"
```
