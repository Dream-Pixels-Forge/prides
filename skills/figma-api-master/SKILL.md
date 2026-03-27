---
name: figma-api-master
description: Expert guidance for Figma API and plugin development. Use for design automation, plugin creation, design system management, and Figma workflow integration.
license: Complete terms in LICENSE.txt
---

# Figma API & Plugin Development Guide

You are a Figma expert specializing in API integration, plugin development, design automation, and design system management.

## Core Capabilities

### 1. Figma REST API
- File operations
- Component management
- Webhook integration
- Batch operations

### 2. Plugin Development
- UI creation
- Node manipulation
- Auto Layout
- Custom commands

### 3. Design Systems
- Component libraries
- Style management
- Token synchronization
- Version control

### 4. Automation
- Batch exports
- Design tokens
- Documentation
- CI/CD integration

---

## Figma REST API

### Authentication

```javascript
const FIGMA_TOKEN = 'your_personal_access_token';
const FILE_KEY = 'your_file_key';

const headers = {
  'X-Figma-Token': FIGMA_TOKEN
};
```

### Get File

```javascript
async function getFile(fileKey) {
  const response = await fetch(
    `https://api.figma.com/v1/files/${fileKey}`,
    { headers }
  );
  return await response.json();
}

// Get specific nodes
async function getNodes(fileKey, nodeIds) {
  const response = await fetch(
    `https://api.figma.com/v1/files/${fileKey}/nodes?ids=${nodeIds.join(',')}`,
    { headers }
  );
  return await response.json();
}
```

### Get Components

```javascript
async function getComponents(fileKey) {
  const response = await fetch(
    `https://api.figma.com/v1/files/${fileKey}/components`,
    { headers }
  );
  return await response.json();
}

async function getComponentStyles(fileKey) {
  const response = await fetch(
    `https://api.figma.com/v1/files/${fileKey}/styles`,
    { headers }
  );
  return await response.json();
}
```

### Get Images

```javascript
async function getImages(fileKey, nodeIds, options = {}) {
  const params = new URLSearchParams({
    ids: nodeIds.join(','),
    scale: options.scale || '1',
    format: options.format || 'png'
  });
  
  const response = await fetch(
    `https://api.figma.com/v1/images/${fileKey}?${params}`,
    { headers }
  );
  return await response.json();
}
```

---

## Plugin Development

### Basic Plugin Structure

```javascript
// manifest.json
{
  "name": "My Plugin",
  "id": "123456789",
  "api": "1.0.0",
  "main": "code.js",
  "ui": "ui.html",
  "commands": [
    {
      "name": "My Command",
      "command": "my_command"
    }
  ]
}
```

### code.js (Plugin Logic)

```javascript
// Show UI
figma.showUI(__html__, { width: 400, height: 600 });

// Handle UI messages
figma.ui.onmessage = (msg) => {
  if (msg.type === 'create-rectangle') {
    createRectangle(msg.width, msg.height);
  }
  figma.closePlugin();
};

// Create rectangle
function createRectangle(width, height) {
  const rect = figma.createRectangle();
  rect.x = 0;
  rect.y = 0;
  rect.resize(width, height);
  rect.fills = [{ type: 'SOLID', color: { r: 1, g: 0, b: 0 } }];
  
  figma.currentPage.appendChild(rect);
  figma.currentPage.selection = [rect];
  figma.viewport.scrollAndZoomIntoView([rect]);
}
```

### ui.html (Plugin UI)

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    body { padding: 16px; font-family: sans-serif; }
    button { width: 100%; padding: 8px; margin-top: 8px; }
    input { width: 100%; padding: 8px; margin-top: 4px; }
  </style>
</head>
<body>
  <h2>Create Rectangle</h2>
  <label>Width</label>
  <input type="number" id="width" value="100" />
  <label>Height</label>
  <input type="number" id="height" value="100" />
  <button onclick="create()">Create</button>
  
  <script>
    function create() {
      parent.postMessage({
        type: 'create-rectangle',
        width: document.getElementById('width').value,
        height: document.getElementById('height').value
      }, '*');
    }
  </script>
</body>
</html>
```

---

## Node Operations

### Create Nodes

```javascript
// Rectangle
const rect = figma.createRectangle();
rect.resize(100, 100);
rect.fills = [{ type: 'SOLID', color: { r: 1, g: 0, b: 0 } }];

// Text
const text = figma.createText();
text.characters = "Hello World";

// Frame
const frame = figma.createFrame();
frame.resize(400, 300);
frame.layoutMode = "HORIZONTAL";

// Component
const component = rect.createComponent();

// Instance
const instance = component.createInstance();
```

### Modify Nodes

```javascript
// Position
node.x = 100;
node.y = 200;

// Size
node.resize(200, 100);

// Fills
node.fills = [
  { 
    type: 'SOLID', 
    color: { r: 0.5, g: 0.5, b: 1 },
    opacity: 0.8
  }
];

// Strokes
node.strokes = [{ type: 'SOLID', color: { r: 0, g: 0, b: 0 } }];
node.strokeWeight = 2;

// Effects
node.effects = [
  {
    type: 'DROP_SHADOW',
    color: { r: 0, g: 0, b: 0, a: 0.25 },
    offset: { x: 0, y: 4 },
    radius: 8,
    spread: 0,
    visible: true,
    blendMode: 'NORMAL'
  }
];

// Auto Layout
node.layoutMode = "HORIZONTAL";
node.paddingLeft = 16;
node.paddingRight = 16;
node.paddingTop = 8;
node.paddingBottom = 8;
node.itemSpacing = 8;
```

### Find Nodes

```javascript
// Find all rectangles
function findAllRectangles(node) {
  const rects = [];
  
  if (node.type === 'RECTANGLE') {
    rects.push(node);
  }
  
  if ('children' in node) {
    for (const child of node.children) {
      rects.push(...findAllRectangles(child));
    }
  }
  
  return rects;
}

// Find by name
function findByName(node, name) {
  if (node.name === name) return node;
  
  if ('children' in node) {
    for (const child of node.children) {
      const found = findByName(child, name);
      if (found) return found;
    }
  }
  
  return null;
}

// Find components
function findAllComponents(page) {
  return page.findAll(node => node.type === 'COMPONENT');
}
```

---

## Design Tokens

### Export Tokens

```javascript
function exportDesignTokens() {
  const tokens = {
    colors: {},
    typography: {},
    spacing: {}
  };
  
  // Get styles
  const styles = figma.getLocalPaintStyles();
  
  styles.forEach(style => {
    if (style.paints[0].type === 'SOLID') {
      const color = style.paints[0].color;
      tokens.colors[style.name] = {
        r: color.r,
        g: color.g,
        b: color.b,
        a: style.paints[0].opacity
      };
    }
  });
  
  return tokens;
}
```

### Import Tokens

```javascript
async function importDesignTokens(tokens) {
  // Create color styles
  for (const [name, color] of Object.entries(tokens.colors)) {
    const paint = {
      type: 'SOLID',
      color: { r: color.r, g: color.g, b: color.b },
      opacity: color.a
    };
    
    const style = figma.createPaintStyle();
    style.name = name;
    style.paints = [paint];
  }
}
```

---

## Batch Operations

### Batch Export

```javascript
async function batchExportNodes(nodes, options = {}) {
  const exports = [];
  
  for (const node of nodes) {
    const exportSettings = {
      format: options.format || 'PNG',
      constraint: {
        type: 'SCALE',
        value: options.scale || 1
      }
    };
    
    node.exportSettings = [exportSettings];
    
    const bytes = await node.exportAsync(exportSettings);
    exports.push({
      node: node,
      bytes: bytes
    });
  }
  
  return exports;
}
```

### Batch Create Components

```javascript
function createComponentsFromSelection() {
  const selection = figma.currentPage.selection;
  
  for (const node of selection) {
    if (node.type !== 'COMPONENT') {
      const component = node.createComponent();
      component.name = `${node.name} Component`;
    }
  }
}
```

---

## Best Practices

### Plugin Development
- Keep UI responsive
- Handle errors gracefully
- Provide user feedback
- Document your plugin

### API Usage
- Cache responses when possible
- Handle rate limits
- Use pagination for large files
- Validate responses

### Design Systems
- Use consistent naming
- Document components
- Version your libraries
- Sync tokens regularly

---

## Resources

### Official Documentation
- [Figma REST API](https://www.figma.com/developers/api)
- [Figma Plugin API](https://www.figma.com/plugin-docs/)
- [Figma Plugin Samples](https://github.com/figma/plugin-samples)

### Community Resources
- Figma Community
- Figma Forum
- Plugin Discord

---

## Usage Examples

```
"Use figma-api-master skill to create plugin for batch export"
"Use figma-api-master skill to sync design tokens to code"
"Use figma-api-master skill to create component library"
"Use figma-api-master skill to automate design documentation"
"Use figma-api-master skill to integrate Figma with CI/CD"
```
