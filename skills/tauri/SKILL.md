---
name: tauri
description: Expert guidance for building cross-platform desktop applications with Tauri v2, including project setup, Rust backend, frontend integration, IPC communication, and native features.
allowed-tools:
  - "Read"
  - "Write"
  - "Bash"
  - "glob"
  - "grep_search"
  - "web_fetch"
---

# Tauri v2 - Desktop Application Framework

You are a desktop application developer specialized in building cross-platform apps with Tauri v2—a framework that combines Rust backend with any frontend framework (React, Vue, Svelte, etc.) to create tiny, fast, and secure desktop applications.

## Core Concepts

Tauri is a **two-part framework**:
1. **Rust Binary**: Creates windows, exposes native APIs
2. **Frontend**: Any framework that produces HTML/CSS/JS

### Why Tauri?

- **Tiny binaries**: ~5-10MB vs ~100MB+ for Electron
- **Native performance**: Rust backend is blazing fast
- **Secure**: No Node.js runtime in final app
- **Cross-platform**: Windows, macOS, Linux, iOS, Android
- **Frontend agnostic**: Use React, Vue, Svelte, vanilla JS

## Prerequisites

### Required Tools

```bash
# Rust (required)
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

# For macOS - Xcode command line tools
xcode-select --install

# For Windows - Visual Studio Build Tools
# Download from https://visualstudio.microsoft.com/visual-cpp-build-tools/

# Node.js (for frontend)
node --version  # v18+

# Package manager
npm --version
```

## Installation

### Create New Project

```bash
# Interactive - choose your framework
npm create tauri-app@latest

# Non-interactive with options
npm create tauri-app@latest my-app -- --template react-ts --manager npm
```

### Available Templates

| Template | Command |
|----------|---------|
| Vanilla JS | `--template vanilla` |
| Vanilla TS | `--template vanilla-ts` |
| React | `--template react` |
| React + TypeScript | `--template react-ts` |
| Vue | `--template vue` |
| Vue + TypeScript | `--template vue-ts` |
| Svelte | `--template svelte` |
| Svelte + TypeScript | `--template svelte-ts` |
| Solid | `--template solid-ts` |
| Next.js | `--template next` |

## Project Structure

```
my-app/
├── src/                    # Frontend source
│   ├── main.tsx
│   ├── App.tsx
│   └── styles.css
├── src-tauri/              # Rust backend
│   ├── src/
│   │   └── main.rs         # Rust entry point
│   ├── Cargo.toml          # Rust dependencies
│   ├── tauri.conf.json     # Tauri configuration
│   ├── capabilities/        # Permission capabilities
│   └── icons/              # App icons
├── package.json
├── vite.config.ts
└── tsconfig.json
```

## Configuration

### tauri.conf.json

```json
{
  "$schema": "https://schema.tauri.app/config/2",
  "productName": "My App",
  "version": "1.0.0",
  "identifier": "com.myapp.desktop",
  "build": {
    "beforeDevCommand": "npm run dev",
    "devUrl": "http://localhost:5173",
    "beforeBuildCommand": "npm run build",
    "frontendDist": "../dist"
  },
  "app": {
    "windows": [
      {
        "title": "My App",
        "width": 800,
        "height": 600,
        "resizable": true,
        "fullscreen": false,
        "minWidth": 400,
        "minHeight": 300
      }
    ],
    "security": {
      "csp": null
    }
  },
  "bundle": {
    "active": true,
    "targets": "all",
    "icon": [
      "icons/32x32.png",
      "icons/128x128.png",
      "icons/128x128@2x.png",
      "icons/icon.icns",
      "icons/icon.ico"
    ]
  }
}
```

## Frontend Integration

### React Example

```tsx
// src/App.tsx
import { useState } from 'react';
import { invoke } from '@tauri-apps/api/core';
import { listen } from '@tauri-apps/api/event';

function App() {
  const [message, setMessage] = useState('');

  // Call Rust command
  const handleClick = async () => {
    try {
      const response = await invoke<string>('greet', { name: 'World' });
      setMessage(response);
    } catch (e) {
      console.error(e);
    }
  };

  // Listen to Rust events
  useState(() => {
    const unlisten = listen('my-event', (event) => {
      console.log('Received:', event.payload);
    });

    return () => {
      unlisten.then(fn => fn());
    };
  }, []);

  return (
    <div>
      <h1>Tauri + React App</h1>
      <button onClick={handleClick}>Greet</button>
      <p>{message}</p>
    </div>
  );
}

export default App;
```

### Vue Example

```vue
// src/App.vue
<script setup lang="ts">
import { ref } from 'vue';
import { invoke } from '@tauri-apps/api/core';

const message = ref('');

async function handleClick() {
  try {
    message.value = await invoke<string>('greet', { name: 'World' });
  } catch (e) {
    console.error(e);
  }
}
</script>

<template>
  <h1>Tauri + Vue App</h1>
  <button @click="handleClick">Greet</button>
  <p>{{ message }}</p>
</template>
```

## Rust Backend (src-tauri)

### Basic Commands

```rust
// src-tauri/src/main.rs
#![cfg_attr(not(debug_assertions), windows_subsystem = "windows")]

use tauri::Manager;

fn main() {
    tauri::Builder::default()
        .invoke_handler(tauri::generate_handler![greet])
        .setup(|app| {
            // App initialization
            println!("App starting up!");
            Ok(())
        })
        .run(tauri::generate_context!())
        .expect("error while running tauri application");
}

#[tauri::command]
fn greet(name: &str) -> String {
    format!("Hello, {}!", name)
}
```

### Commands with State

```rust
use std::sync::Mutex;

struct AppState {
    counter: Mutex<i32>,
}

#[tauri::command]
fn increment(state: tauri::State<AppState>) -> i32 {
    let mut counter = state.counter.lock().unwrap();
    *counter += 1;
    *counter
}

fn main() {
    tauri::Builder::default()
        .manage(AppState {
            counter: Mutex::new(0),
        })
        .invoke_handler(tauri::generate_handler![increment])
        .run(tauri::generate_context!())
        .expect("error while running tauri application");
}
```

### Async Commands

```rust
use tauri::command;

#[command]
async fn fetch_data(url: String) -> Result<String, String> {
    let response = reqwest::get(&url)
        .await
        .map_err(|e| e.to_string())?;
    
    let body = response.text()
        .await
        .map_err(|e| e.to_string())?;
    
    Ok(body)
}
```

## IPC Communication

### Frontend → Rust (Commands)

```typescript
import { invoke } from '@tauri-apps/api/core';

// Sync call
const result = await invoke<ReturnType>('command_name', { param: value });

// Async call
const result = await invoke<Promise<ReturnType>>('async_command', { param: value });
```

### Rust → Frontend (Events)

```rust
use tauri::{AppHandle, Emitter};

// Emit to frontend
app.emit("event-name", payload)?;
```

### Frontend Listening

```typescript
import { listen } from '@tauri-apps/api/event';

const unlisten = await listen<string>('event-name', (event) => {
  console.log('Received:', event.payload);
});

// Clean up
unlisten();
```

## Native Features

### File System

```typescript
import { 
  readTextFile, 
  writeTextFile, 
  exists,
  mkdir,
  readDir
} from '@tauri-apps/plugin-fs';

// Read file
const content = await readTextFile('path/to/file.txt');

// Write file
await writeTextFile('path/to/file.txt', 'Content');

// Check if exists
const exists = await exists('path/to/file.txt');
```

### Dialog

```typescript
import { 
  open, 
  save, 
  message, 
  ask, 
  confirm 
} from '@tauri-apps/plugin-dialog';

// Open file dialog
const file = await open({
  multiple: false,
  filters: [{ name: 'Images', extensions: ['png', 'jpg'] }]
});

// Save file dialog
const path = await save({
  filters: [{ name: 'Text', extensions: ['txt'] }],
  defaultPath: 'document.txt'
});

// Show message
await message('Operation completed!', { title: 'Success', kind: 'info' });

// Ask confirmation
const confirmed = await ask('Are you sure?', { title: 'Confirm' });
```

### Shell

```typescript
import { open as shellOpen, Command } from '@tauri-apps/plugin-shell';

// Open URL in default browser
await shellOpen('https://tauri.app');

// Execute command
const output = await Command.create('ls', ['-la']).execute();
```

### Window Management

```typescript
import { 
  getCurrentWindow,
  Window 
} from '@tauri-apps/api/window';

const appWindow = getCurrentWindow();

// Minimize
await appWindow.minimize();

// Maximize/unmaximize
await appWindow.toggleMaximize();

// Close
await appWindow.close();

// Set title
await appWindow.setTitle('New Title');

// Set size
await appWindow.setSize({ width: 800, height: 600 });
```

### System Tray

```rust
use tauri::{
    menu::{Menu, MenuItem},
    tray::{TrayIconBuilder, TrayIconEvent},
    Manager,
};

fn main() {
    tauri::Builder::default()
        .setup(|app| {
            let quit = MenuItem::with_id(app, "quit", "Quit", true, None::<&str>)?;
            let show = MenuItem::with_id(app, "show", "Show", true, None::<&str>)?;
            let menu = Menu::with_items(app, &[&show, &quit])?;

            let _tray = TrayIconBuilder::new()
                .menu(&menu)
                .tooltip("My App")
                .on_menu_event(|app, event| {
                    match event.id.as_ref() {
                        "quit" => {
                            app.exit(0);
                        }
                        "show" => {
                            if let Some(window) = app.get_webview_window("main") {
                                let _ = window.show();
                                let _ = window.set_focus();
                            }
                        }
                        _ => {}
                    }
                })
                .build(app)?;

            Ok(())
        })
        .run(tauri::generate_context!())
        .expect("error while running tauri application");
}
```

### Clipboard

```typescript
import { writeText, readText } from '@tauri-apps/plugin-clipboard-manager';

// Write to clipboard
await writeText('Hello, World!');

// Read from clipboard
const text = await readText();
```

### Notifications

```typescript
import { isPermissionGranted, requestPermission, sendNotification } from '@tauri-apps/plugin-notification';

// Check permission
let permission = await isPermissionGranted();

// Request permission
if (!permission) {
  const result = await requestPermission();
  permission = result === 'granted';
}

// Send notification
if (permission) {
  sendNotification({
    title: 'My App',
    body: 'Hello from Tauri!'
  });
}
```

## Capabilities (Permissions)

### Defining Capabilities

```json
// src-tauri/capabilities/main.json
{
  "$schema": "https://schema.tauri.app/config/2/capability",
  "identifier": "main-capability",
  "description": "Main window capability",
  "windows": ["main"],
  "permissions": [
    "core:default",
    "fs:default",
    "dialog:default",
    "shell:default",
    {
      "identifier": "fs:allow-read-text-file",
      "allow": [{ "path": "$APPDATA/**" }]
    }
  ]
}
```

### Common Permissions

| Permission | Description |
|------------|-------------|
| `core:default` | Core APIs |
| `fs:default` | File system |
| `dialog:default` | Native dialogs |
| `shell:default` | Shell execution |
| `window:default` | Window management |
| `notification:default` | Notifications |
| `clipboard-manager:default` | Clipboard |

## Build & Distribution

### Development

```bash
# Start dev server
npm run tauri dev

# Or just
npm run dev
# Then in another terminal:
cd src-tauri && cargo run
```

### Production Build

```bash
# Build for current platform
npm run tauri build

# Build for specific platforms
npm run tauri build -- --target x86_64-pc-windows-msvc
npm run tauri build -- --target x86_64-unknown-linux-gnu
npm run tauri build -- --target aarch64-apple-darwin
```

### Output

Build output in:
- Windows: `src-tauri/target/release/bundle/nsis/`
- macOS: `src-tauri/target/release/bundle/dmg/`
- Linux: `src-tauri/target/release/bundle/deb/`

## Logging

### Rust Logging

```rust
use log::{info, error};

fn main() {
    // Initialize logging
    env_logger::Builder::from_env(env_logger::Env::default().default_filter_or("info"))
        .init();

    info!("Application starting");
    error!("Something went wrong");

    tauri::Builder::default()
        .run(tauri::generate_context!())
        .expect("error");
}
```

### Frontend Logging

```typescript
import { info, error, warn, debug } from '@tauri-apps/plugin-log';

info('Info message');
error('Error message');
warn('Warning message');
debug('Debug message');
```

## Troubleshooting

### Build Errors

```bash
# Update Rust
rustup update

# Clean build
cd src-tauri && cargo clean

# Rebuild
cd .. && npm run tauri build
```

### Permission Denied

- Check capabilities configuration
- Ensure proper permissions in `capabilities/`

### DevTools Not Working

Add to `tauri.conf.json`:
```json
{
  "build": {
    "devtools": true
  }
}
```

## Validation

Before release:
1. **Build**: `npm run tauri build`
2. **Test**: Verify all features work
3. **Size**: Check bundle size
4. **Signing**: Configure code signing (optional)

## Resources

- [Tauri Documentation](https://tauri.app)
- [Tauri GitHub](https://github.com/tauri-apps/tauri)
- [Tauri Discord](https://discord.gg/tauri)
- [Awesome Tauri](https://github.com/tauri-apps/awesome-tauri)
