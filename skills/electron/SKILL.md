---
name: electron
description: Expert guidance for building cross-platform desktop applications with Electron, including project setup, main/renderer processes, IPC communication, native features, and distribution with Electron Forge.
allowed-tools:
  - "Read"
  - "Write"
  - "Bash"
  - "glob"
  - "grep_search"
  - "web_fetch"
---

# Electron - Desktop Application Framework

You are a desktop application developer specialized in building cross-platform apps with Electron—a framework that combines Chromium and Node.js to create desktop applications using web technologies.

## Core Concepts

Electron is a **two-process architecture**:

1. **Main Process**: Node.js runtime, handles native APIs, window management
2. **Renderer Process**: Chromium, runs frontend (React, Vue, etc.)

### Why Electron?

- **Web technologies**: Use React, Vue, Angular, vanilla JS
- **Cross-platform**: Windows, macOS, Linux with single codebase
- **Mature ecosystem**: Extensive packages and tools
- **Rich native APIs**: Full access to system features
- **Large community**: Plenty of resources and examples

## Installation

### Prerequisites

- Node.js 18+
- npm 9+

### Create Project with Electron Forge

```bash
# Using create-electron-app with Vite + React template
npm create electron-app@latest my-app -- --template=vite-typescript

# With React
npm create electron-app@latest my-app -- --template=vite-react

# With Vue
npm create electron-app@latest my-app -- --template=vite-vue
```

### Manual Setup

```bash
# Initialize project
npm init -y

# Install Electron and dev tools
npm install --save-dev electron@latest electron-builder

# Install production dependencies
npm install react react-dom
```

## Project Structure

```
my-app/
├── src/
│   ├── main/               # Main process
│   │   ├── main.ts         # Entry point
│   │   ├── preload.ts      # Preload scripts
│   │   └── ipc.ts         # IPC handlers
│   └── renderer/           # Renderer process
│       ├── App.tsx         # React app
│       ├── main.tsx       # React entry
│       └── index.html
├── package.json
├── vite.config.ts          # Vite configuration
├── electron-builder.yml    # Build config
└── tsconfig.json
```

## Main Process

### Basic Main File

```typescript
// src/main/main.ts
import { app, BrowserWindow, ipcMain } from 'electron';
import path from 'path';

// Handle uncaught exceptions
process.on('uncaughtException', (error) => {
  console.error('Uncaught exception:', error);
});

process.on('unhandledRejection', (reason) => {
  console.error('Unhandled rejection:', reason);
});

let mainWindow: BrowserWindow | null = null;

function createWindow() {
  mainWindow = new BrowserWindow({
    width: 1200,
    height: 800,
    minWidth: 800,
    minHeight: 600,
    title: 'My Electron App',
    webPreferences: {
      preload: path.join(__dirname, 'preload.js'),
      contextIsolation: true,
      nodeIntegration: false,
      sandbox: true,
    },
  });

  // Load the app
  if (process.env.VITE_DEV_SERVER_URL) {
    mainWindow.loadURL(process.env.VITE_DEV_SERVER_URL);
    mainWindow.webContents.openDevTools();
  } else {
    mainWindow.loadFile(path.join(__dirname, '../dist/index.html'));
  }

  mainWindow.on('closed', () => {
    mainWindow = null;
  });
}

app.whenReady().then(() => {
  createWindow();

  app.on('activate', () => {
    if (BrowserWindow.getAllWindows().length === 0) {
      createWindow();
    }
  });
});

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') {
    app.quit();
  }
});
```

### Window Management

```typescript
import { BrowserWindow } from 'electron';

// Get current window
const win = BrowserWindow.getFocusedWindow();

// Minimize
win.minimize();

// Maximize/unmaximize
if (win.isMaximized()) {
  win.unmaximize();
} else {
  win.maximize();
}

// Set size
win.setSize(800, 600);

// Set position
win.setPosition(100, 100);

// Always on top
win.setAlwaysOnTop(true);

// Fullscreen
win.setFullScreen(true);

// Close
win.close();
```

### App Menu

```typescript
import { Menu, MenuItem, app, shell, dialog } from 'electron';

function createMenu() {
  const template: Electron.MenuItemConstructorOptions[] = [
    {
      label: 'File',
      submenu: [
        {
          label: 'Open File',
          accelerator: 'CmdOrCtrl+O',
          click: async () => {
            const result = await dialog.showOpenDialog({
              properties: ['openFile'],
              filters: [
                { name: 'Images', extensions: ['jpg', 'png', 'gif'] }
              ]
            });
            if (!result.canceled && result.filePaths.length > 0) {
              mainWindow?.webContents.send('file-opened', result.filePaths[0]);
            }
          }
        },
        { type: 'separator' },
        { role: 'quit' }
      ]
    },
    {
      label: 'Edit',
      submenu: [
        { role: 'undo' },
        { role: 'redo' },
        { type: 'separator' },
        { role: 'cut' },
        { role: 'copy' },
        { role: 'paste' },
        { role: 'selectAll' }
      ]
    },
    {
      label: 'View',
      submenu: [
        { role: 'reload' },
        { role: 'forceReload' },
        { role: 'toggleDevTools' },
        { type: 'separator' },
        { role: 'resetZoom' },
        { role: 'zoomIn' },
        { role: 'zoomOut' },
        { type: 'separator' },
        { role: 'togglefullscreen' }
      ]
    },
    {
      label: 'Window',
      submenu: [
        { role: 'minimize' },
        { role: 'zoom' },
        { role: 'close' }
      ]
    },
    {
      label: 'Help',
      submenu: [
        {
          label: 'About',
          click: () => {
            dialog.showMessageBox({
              type: 'info',
              title: 'About',
              message: 'My Electron App',
              detail: 'Version 1.0.0'
            });
          }
        },
        {
          label: 'Documentation',
          click: async () => {
            await shell.openExternal('https://electronjs.org');
          }
        }
      ]
    }
  ];

  const menu = Menu.buildFromTemplate(template);
  Menu.setApplicationMenu(menu);
}
```

### System Tray

```typescript
import { Tray, Menu, app, nativeImage } from 'electron';
import path from 'path';

let tray: Tray | null = null;

function createTray() {
  // Create tray icon
  const iconPath = path.join(__dirname, '../../assets/icon.png');
  const icon = nativeImage.createFromPath(iconPath);
  
  tray = new Tray(icon.resize({ width: 16, height: 16 }));
  
  const contextMenu = Menu.buildFromTemplate([
    {
      label: 'Show App',
      click: () => {
        mainWindow?.show();
      }
    },
    {
      label: 'Hide App',
      click: () => {
        mainWindow?.hide();
      }
    },
    { type: 'separator' },
    {
      label: 'Quit',
      click: () => {
        app.quit();
      }
    }
  ]);
  
  tray.setToolTip('My Electron App');
  tray.setContextMenu(contextMenu);
  
  tray.on('click', () => {
    mainWindow?.show();
  });
}
```

## Preload Script

```typescript
// src/main/preload.ts
import { contextBridge, ipcRenderer } from 'electron';

// Expose protected methods to renderer
contextBridge.exposeInMainWorld('electronAPI', {
  // File operations
  openFile: () => ipcRenderer.invoke('dialog:openFile'),
  saveFile: (data: string) => ipcRenderer.invoke('dialog:saveFile', data),
  
  // Window controls
  minimize: () => ipcRenderer.send('window:minimize'),
  maximize: () => ipcRenderer.send('window:maximize'),
  close: () => ipcRenderer.send('window:close'),
  
  // Notifications
  showNotification: (title: string, body: string) => 
    ipcRenderer.invoke('notification:show', { title, body }),
  
  // App info
  getVersion: () => ipcRenderer.invoke('app:getVersion'),
  getPlatform: () => process.platform,
  
  // Events
  onFileOpened: (callback: (path: string) => void) => {
    ipcRenderer.on('file-opened', (_, path) => callback(path));
  }
});

// Type declarations for renderer
declare global {
  interface Window {
    electronAPI: {
      openFile: () => Promise<string | null>;
      saveFile: (data: string) => Promise<void>;
      minimize: () => void;
      maximize: () => void;
      close: () => void;
      showNotification: (title: string, body: string) => Promise<void>;
      getVersion: () => Promise<string>;
      getPlatform: () => string;
      onFileOpened: (callback: (path: string) => void) => void;
    };
  }
}
```

## IPC Communication

### Main Process Handler

```typescript
// src/main/ipc.ts
import { ipcMain, dialog, app, Notification } from 'electron';
import fs from 'fs/promises';

export function setupIPC() {
  // Open file dialog
  ipcMain.handle('dialog:openFile', async () => {
    const result = await dialog.showOpenDialog({
      properties: ['openFile'],
      filters: [
        { name: 'All Files', extensions: ['*'] }
      ]
    });
    
    if (!result.canceled && result.filePaths.length > 0) {
      const content = await fs.readFile(result.filePaths[0], 'utf-8');
      return { path: result.filePaths[0], content };
    }
    return null;
  });
  
  // Save file dialog
  ipcMain.handle('dialog:saveFile', async (_, data: string) => {
    const result = await dialog.showSaveDialog({
      filters: [
        { name: 'Text Files', extensions: ['txt'] }
      ]
    });
    
    if (!result.canceled && result.filePath) {
      await fs.writeFile(result.filePath, data, 'utf-8');
      return true;
    }
    return false;
  });
  
  // Get app version
  ipcMain.handle('app:getVersion', () => {
    return app.getVersion();
  });
  
  // Show notification
  ipcMain.handle('notification:show', (_, { title, body }) => {
    if (Notification.isSupported()) {
      new Notification({ title, body }).show();
    }
  });
  
  // Window controls
  ipcMain.on('window:minimize', (event) => {
    const win = BrowserWindow.fromWebContents(event.sender);
    win?.minimize();
  });
  
  ipcMain.on('window:maximize', (event) => {
    const win = BrowserWindow.fromWebContents(event.sender);
    if (win?.isMaximized()) {
      win.unmaximize();
    } else {
      win?.maximize();
    }
  });
  
  ipcMain.on('window:close', (event) => {
    const win = BrowserWindow.fromWebContents(event.sender);
    win?.close();
  });
}
```

### Renderer Process

```typescript
// Use in React/Vue component
const handleOpenFile = async () => {
  const result = await window.electronAPI.openFile();
  if (result) {
    console.log('File content:', result.content);
  }
};

const handleSaveFile = async () => {
  await window.electronAPI.saveFile('Hello, World!');
};

const version = await window.electronAPI.getVersion();
```

## Native Features

### File System

```typescript
import fs from 'fs/promises';
import path from 'path';
import { app } from 'electron';

// Read file
const content = await fs.readFile('/path/to/file.txt', 'utf-8');

// Write file
await fs.writeFile('/path/to/file.txt', 'content', 'utf-8');

// Check exists
await fs.access('/path/to/file.txt');

// Get app data directory
const userDataPath = app.getPath('userData');
const tempPath = app.getPath('temp');
const desktopPath = app.getPath('desktop');
const documentsPath = app.getPath('documents');
```

### Clipboard

```typescript
import { clipboard } from 'electron';

// Write text
clipboard.writeText('Hello, World!');

// Read text
const text = clipboard.readText();

// Write image
clipboard.writeImage(nativeImage);

// Clear
clipboard.clear();
```

### Shell

```typescript
import { shell, openExternal } from 'electron';

// Open URL in default browser
await openExternal('https://electronjs.org');

// Open file in default application
await shell.openPath('/path/to/file.txt');

// Show item in folder
shell.showItemInFolder('/path/to/file');

// Open path (asks user to choose app)
shell.openPath('/path/to/file');
```

### Dialog

```typescript
import { dialog } from 'electron';

// Open file dialog
const openResult = await dialog.showOpenDialog({
  title: 'Open File',
  defaultPath: '/home',
  buttonLabel: 'Open',
  filters: [
    { name: 'Images', extensions: ['jpg', 'png', 'gif'] },
    { name: 'All Files', extensions: ['*'] }
  ],
  properties: [
    'openFile',        // Select files
    'multiSelections', // Allow multiple selection
    'showHiddenFiles'  // Show hidden files
  ]
});

// Save file dialog
const saveResult = await dialog.showSaveDialog({
  title: 'Save File',
  defaultPath: 'untitled.txt',
  filters: [
    { name: 'Text Files', extensions: ['txt'] }
  ]
});

// Message box
const result = await dialog.showMessageBox({
  type: 'question',
  buttons: ['Yes', 'No', 'Cancel'],
  defaultId: 0,
  title: 'Confirm',
  message: 'Are you sure?'
});

// Error box
dialog.showErrorBox('Error', 'Something went wrong!');
```

### Notifications

```typescript
import { Notification } from 'electron';

if (Notification.isSupported()) {
  const notification = new Notification({
    title: 'My App',
    body: 'Hello from Electron!',
    icon: '/path/to/icon.png',
    silent: false,
    urgency: 'normal', // normal, critical, low
  });
  
  notification.on('click', () => {
    console.log('Notification clicked');
  });
  
  notification.show();
}
```

### Global Shortcuts

```typescript
import { globalShortcut, app } from 'electron';

// Register shortcut
const registered = globalShortcut.register('CommandOrControl+Shift+G', () => {
  console.log('Shortcut triggered!');
});

// Check if registered
const isRegistered = globalShortcut.isRegistered('CommandOrControl+Shift+G');

// Unregister
globalShortcut.unregister('CommandOrControl+Shift+G');

// Unregister all
globalShortcut.unregisterAll();
```

## Renderer Process (React)

```tsx
// src/renderer/App.tsx
import { useEffect, useState } from 'react';

function App() {
  const [version, setVersion] = useState('');
  
  useEffect(() => {
    // Get app version
    window.electronAPI.getVersion().then(setVersion);
    
    // Listen for events
    window.electronAPI.onFileOpened((path) => {
      console.log('File opened:', path);
    });
  }, []);
  
  return (
    <div>
      <h1>My Electron App</h1>
      <p>Version: {version}</p>
      <p>Platform: {window.electronAPI.getPlatform()}</p>
      
      <button onClick={() => window.electronAPI.minimize()}>
        Minimize
      </button>
      <button onClick={() => window.electronAPI.maximize()}>
        Maximize
      </button>
      <button onClick={() => window.electronAPI.close()}>
        Close
      </button>
    </div>
  );
}

export default App;
```

## Build & Distribution

### Electron Builder Config

```yaml
# electron-builder.yml
appId: com.myapp.desktop
productName: My Electron App
directories:
  output: dist
  buildResources: build
files:
  - "dist/**/*"
  - "package.json"
mac:
  category: public.app-category.productivity
  target:
    - dmg
    - zip
  icon: build/icon.icns
  hardenedRuntime: true
  gatekeeperAssess: false
  entitlements: build/entitlements.mac.plist
  entitlementsInherit: build/entitlements.mac.plist
windows:
  target:
    - nsis
    - portable
  icon: build/icon.ico
  requestedExecutionLevel: asInvoker
linux:
  target:
    - AppImage
    - deb
  category: Utility
  icon: build/icons
asar: true
compression: maximum
```

### Build Commands

```bash
# Development
npm run dev

# Build for current platform
npm run build

# Package (creates unpacked app)
npm run package

# Create distributable (creates installer)
npm run make
```

### Output

- macOS: `.dmg`, `.zip` in `release/`
- Windows: `.exe`, `.portable.exe` in `release/`
- Linux: `.AppImage`, `.deb` in `release/`

## Security Best Practices

### Main Process

```typescript
// Always use contextIsolation and sandbox
webPreferences: {
  contextIsolation: true,
  nodeIntegration: false,
  sandbox: true,
  webSecurity: true,
}

// Validate all IPC input
ipcMain.handle('some:handler', async (event, ...args) => {
  // Validate args
  if (typeof args[0] !== 'string') {
    throw new Error('Invalid argument');
  }
  // Process
});
```

### Preload Script

```typescript
// Only expose what's needed
contextBridge.exposeInMainWorld('api', {
  // Minimal API
});
```

### Content Security Policy

```typescript
// In main.ts
session.webRequest.onHeadersReceived((details, callback) => {
  callback({
    responseHeaders: {
      ...details.responseHeaders,
      'Content-Security-Policy': [
        "default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'"
      ]
    }
  });
});
```

## Troubleshooting

### Performance Issues

- Disable hardware acceleration if needed
- Limit renderer process memory usage
- Use `will-change` sparingly

### Build Errors

```bash
# Clear cache
rm -rf node_modules/.cache
rm -rf release

# Rebuild native modules
npm rebuild

# Update Electron
npm install electron@latest
```

### DevTools Not Working

- Ensure `webPreferences.devTools` is not set to `false`
- Check that window is created before opening DevTools

## Validation

Before release:
1. **Build**: `npm run make`
2. **Test**: Verify all features on target OS
3. **Size**: Check bundle size (~150MB typical)
4. **Signing**: Configure code signing (required for macOS App Store)
5. **Auto-update**: Set up electron-updater if needed

## Resources

- [Electron Documentation](https://www.electronjs.org/docs)
- [Electron Forge](https://www.electronforge.io)
- [Electron API Demos](https://github.com/electron/electron-api-demos)
- [Awesome Electron](https://github.com/sindresorhus/awesome-electron)
