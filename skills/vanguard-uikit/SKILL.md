---
name: vanguard-uikit
description: Expert guidance for building applications with vanguard-uikit - a modern dark-themed UI component library featuring glassmorphism, neuromorphism, and liquid glass aesthetics. Built with React + Tailwind CSS.
allowed-tools:
  - "Read"
  - "Write"
  - "Bash"
  - "glob"
  - "grep_search"
  - "web_fetch"
---

# Vanguard UIKit

You are a frontend engineer specialized in building modern dark-themed interfaces with vanguard-uikit—a React UI component library featuring glassmorphism, neuromorphism, and liquid glass aesthetics built with Tailwind CSS.

## Core Concepts

Vanguard UIKit is a **dark-themed component library** that provides:

- **Glassmorphism**: Multi-layer glass effects with backdrop blur, liquid refraction, holographic gradients
- **Neuromorphism**: Soft shadows, subtle contrasts, tactile surfaces
- **Liquid Glass**: Flowing gradients, refractive light effects, smooth transitions
- **500+ Lucide icons**: Full icon library included
- **Dark theme by default**: Optimized for modern dark interfaces
- **Highly customizable**: Tailwind-based styling

## Installation

### Prerequisites

- React 18+
- Tailwind CSS 3+
- Lucide React 0.200+

### Install Package

```bash
# Using npm
npm install vanguard-uikit

# Using yarn
yarn add vanguard-uikit
```

### Peer Dependencies

```bash
npm install react react-dom lucide-react
```

## Quick Start

```tsx
import React from 'react';
import {
  VanguardButton,
  VanguardCard,
  GlassPanel,
  Icons
} from 'vanguard-uikit';

function App() {
  return (
    <div className="min-h-screen bg-[#0a0a0b] p-8">
      <GlassPanel>
        <VanguardCard
          title="Welcome"
          description="Build amazing interfaces"
          icon={Icons.Zap}
        >
          <VanguardButton variant="accent">
            Get Started
          </VanguardButton>
        </VanguardCard>
      </GlassPanel>
    </div>
  );
}

export default App;
```

## Design Systems

### Glassmorphism

```tsx
// Multi-layer glass effects
<GlassPanel
  className="bg-gradient-to-br from-white/10 via-white/5 to-white/[0.02]"
  backdropBlur="xl"
  border="border border-white/15"
  shadow="[0_8px_32px_rgba(0,0,0,0.3),inset_0_1px_0_rgba(255,255,255,0.1)]"
>
  Content
</GlassPanel>
```

### Neuromorphic Depth

```tsx
// Soft shadows for dimensional feel
<NeuorphicCard
  className="bg-[#0a0a0b]"
  shadow="[8px_8px_16px_rgba(0,0,0,0.4),-8px_-8px_16px_rgba(255,255,255,0.03)]"
  border="border border-white/5"
>
  Content
</NeuorphicCard>
```

### Liquid Glass

```tsx
// Flowing gradient animations
<LiquidPanel
  className="bg-gradient-to-br from-white/[0.08] via-white/[0.02] to-transparent"
  backdropBlur="2xl"
  border="border border-white/10"
  animation="liquid"
>
  Content
</LiquidPanel>
```

## Component Categories

### Buttons

```tsx
import { VanguardButton, Icons } from 'vanguard-uikit';

// Variants
<VanguardButton variant="primary">Primary</VanguardButton>
<VanguardButton variant="accent">Accent</VanguardButton>
<VanguardButton variant="glass">Glass</VanguardButton>
<VanguardButton variant="ghost">Ghost</VanguardButton>
<VanguardButton variant="danger">Danger</VanguardButton>

// With icon
<VanguardButton variant="accent" icon={Icons.ArrowRight}>
  Get Started
</VanguardButton>

// Sizes
<VanguardButton size="sm">Small</VanguardButton>
<VanguardButton size="md">Medium</VanguardButton>
<VanguardButton size="lg">Large</VanguardButton>

// States
<VanguardButton disabled>Disabled</VanguardButton>
<VanguardButton loading>Loading</VanguardButton>
```

### Cards

```tsx
import { VanguardCard, GlassPanel, StatCard } from 'vanguard-uikit';

// Basic glass card
<VanguardCard
  title="Feature"
  description="Description here"
  icon={Icons.Zap}
  tag="New"
  hoverable
/>

// Stat card with metrics
<StatCard
  title="Revenue"
  value="$10,000"
  change="+12%"
  trend="up"
  icon={Icons.Wallet}
/>

// Glass panel container
<GlassPanel>
  <VanguardCard title="Content" />
</GlassPanel>
```

### Form Elements

```tsx
import { 
  Input, 
  SearchInput, 
  Textarea, 
  Select, 
  Toggle, 
  Switch, 
  Checkbox, 
  RadioGroup,
  Slider 
} from 'vanguard-uikit';

// Text inputs
<Input icon={Icons.Search} placeholder="Search..." />
<SearchInput placeholder="Search..." />
<Textarea placeholder="Enter description..." rows={3} />

// Select dropdown
<Select
  options={[{ label: 'Option 1', value: '1' }]}
  value={value}
  onChange={setValue}
  placeholder="Choose option..."
/>

// Toggle & Switch
<Toggle checked={checked} onChange={setChecked} label="Enable" />
<Switch checked={checked} onChange={setChecked} label="Dark mode" />

// Checkbox & Radio
<Checkbox checked={checked} onChange={setChecked} label="Accept terms" />
<RadioGroup options={options} value={value} onChange={setValue} />

// Slider
<Slider value={value} onChange={setValue} min={0} max={100} />
```

### Navigation

```tsx
import { Navbar, NavTab, Tabs, Accordion } from 'vanguard-uikit';

// Navbar
<Navbar scrolled={scrolled}>
  <Logo />
  <NavTab active>Home</NavTab>
  <NavTab>About</NavTab>
  <NavTab>Contact</NavTab>
</Navbar>

// Tabs
<Tabs 
  tabs={tabs} 
  activeTab={activeTab} 
  onChange={setActiveTab} 
/>

// Accordion
<Accordion
  items={[
    { id: '1', title: 'Question?', content: 'Answer!' }
  ]}
  allowMultiple
/>
```

### Feedback Components

```tsx
import { 
  Modal, 
  ConfirmDialog, 
  ToastProvider, 
  useToast 
} from 'vanguard-uikit';

// Toast notifications
<ToastProvider>
  <YourComponent />
</ToastProvider>

// In YourComponent:
const { addToast } = useToast();
addToast({ title: 'Success!', variant: 'success' });

// Modal
<Modal 
  isOpen={isOpen} 
  onClose={setIsOpen} 
  title="Modal Title"
>
  Content here
</Modal>

// Confirmation dialog
<ConfirmDialog
  isOpen={isOpen}
  onClose={setIsOpen}
  onConfirm={handleConfirm}
  title="Confirm"
  message="Are you sure?"
/>
```

### Data Display

```tsx
import { Table, Pagination, ProjectRow, Badge, StatusBadge } from 'vanguard-uikit';

// Data table
<Table
  columns={[{ header: 'Name', accessor: 'name' }]}
  data={[{ name: 'John' }]}
/>

// Pagination
<Pagination
  currentPage={1}
  totalPages={10}
  onPageChange={setPage}
/>

// Project row
<ProjectRow
  name="Project Name"
  status="Active"
  progress={75}
  category="Development"
/>

// Badges
<Badge>Default</Badge>
<Badge variant="blue">New</Badge>
<Badge variant="emerald">Active</Badge>
<Badge variant="rose">Error</Badge>

<StatusBadge variant="blue">Live</StatusBadge>
<StatusBadge variant="emerald">Online</StatusBadge>
```

### Progress Components

```tsx
import { ProgressBar, CircularProgress } from 'vanguard-uikit';

// Linear progress
<ProgressBar value={75} showLabel variant="blue" />
<ProgressBar value={50} variant="emerald" />
<ProgressBar value={25} variant="rose" />

// Circular progress
<CircularProgress value={60} variant="emerald" size={80} />
<CircularProgress value={75} size={100} showLabel />
```

## Icons

### Using Icons

```tsx
import { Icons } from 'vanguard-uikit';

// All Lucide icons available
<Icons.Zap />
<Icons.Box />
<Icons.Settings />
<Icons.User />
<Icons.ArrowRight />
<Icons.Mail />
<Icons.Search />
<Icons.Loader />
<Icons.CheckCircle />
// ... 500+ more
```

### Icon Sizes

```tsx
<Icons.Zap size={16} />  // Small
<Icons.Zap size={24} />  // Medium (default)
<Icons.Zap size={32} />  // Large

// With color
<Icons.Zap className="text-blue-500" />
```

## Animation Variants

```tsx
// Available animation speeds
<VanguardButton animation="fast">Quick</VanguardButton>
<VanguardButton animation="normal">Normal</VanguardButton>
<VanguardButton animation="slow">Smooth</VanguardButton>
<VanguardButton animation="liquid">Liquid Flow</VanguardButton>
```

## Color Variants

Available for badges, progress bars, alerts, and buttons:

| Variant | Use Case |
|---------|-----------|
| **blue** | Default, information |
| **emerald** | Success, positive |
| **rose** | Danger, error |
| **amber** | Warning, caution |
| **purple** | Premium, special |

## Theme Configuration

### Tailwind Classes Used

```css
/* Glassmorphism base */
bg-gradient-to-br
from-white/10 
via-white/5 
to-white/[0.02]
backdrop-blur-xl
border-white/15

/* Neuromorphism base */
bg-[#0a0a0b]
shadow-[8px_8px_16px_rgba(0,0,0,0.4),-8px_-8px_16px_rgba(255,255,255,0.03)]
border-white/5

/* Liquid Glass base */
bg-gradient-to-br 
from-white/[0.08] 
via-white/[0.02] 
to-transparent
backdrop-blur-2xl
border-white/10
```

## Common Patterns

### 1. Login Form

```tsx
import { GlassPanel, VanguardCard, Input, VanguardButton, Checkbox } from 'vanguard-uikit';
import { Icons } from 'vanguard-uikit';

function LoginForm() {
  return (
    <div className="min-h-screen bg-[#0a0a0b] flex items-center justify-center p-4">
      <GlassPanel className="max-w-md w-full p-6">
        <VanguardCard
          title="Welcome Back"
          description="Sign in to your account"
          icon={Icons.Lock}
          className="mb-6"
        />
        
        <form className="space-y-4">
          <Input 
            icon={Icons.Mail} 
            type="email" 
            placeholder="Email address" 
          />
          <Input 
            icon={Icons.Lock} 
            type="password" 
            placeholder="Password" 
          />
          
          <div className="flex items-center justify-between">
            <Checkbox label="Remember me" />
            <a href="#" className="text-sm text-blue-400">Forgot password?</a>
          </div>
          
          <VanguardButton variant="accent" block>
            Sign In
          </VanguardButton>
        </form>
      </GlassPanel>
    </div>
  );
}
```

### 2. Dashboard Card

```tsx
import { StatCard, GlassPanel, ProgressBar } from 'vanguard-uikit';
import { Icons } from 'vanguard-uikit';

function DashboardStats() {
  return (
    <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
      <GlassPanel>
        <StatCard
          title="Total Users"
          value="12,345"
          change="+8.2%"
          trend="up"
          icon={Icons.Users}
        />
      </GlassPanel>
      
      <GlassPanel>
        <StatCard
          title="Revenue"
          value="$45,678"
          change="+12.5%"
          trend="up"
          icon={Icons.Wallet}
        />
      </GlassPanel>
      
      <GlassPanel>
        <StatCard
          title="Active Sessions"
          value="1,234"
          change="-2.1%"
          trend="down"
          icon={Icons.Activity}
        />
      </GlassPanel>
    </div>
  );
}
```

### 3. Settings Panel

```tsx
import { GlassPanel, VanguardCard, Switch, Slider, Select } from 'vanguard-uikit';
import { Icons } from 'vanguard-uikit';

function SettingsPanel() {
  return (
    <GlassPanel className="max-w-2xl">
      <VanguardCard
        title="Settings"
        description="Manage your preferences"
        icon={Icons.Settings}
      />
      
      <div className="space-y-6 mt-6">
        <div className="flex items-center justify-between">
          <div>
            <p className="font-medium">Dark Mode</p>
            <p className="text-sm text-gray-400">Enable dark theme</p>
          </div>
          <Switch checked={true} onChange={() => {}} />
        </div>
        
        <div className="flex items-center justify-between">
          <div>
            <p className="font-medium">Notifications</p>
            <p className="text-sm text-gray-400">Receive push notifications</p>
          </div>
          <Switch checked={false} onChange={() => {}} />
        </div>
        
        <div>
          <p className="font-medium mb-2">Volume</p>
          <Slider value={75} onChange={() => {}} />
        </div>
        
        <div>
          <p className="font-medium mb-2">Language</p>
          <Select
            options={[
              { value: 'en', label: 'English' },
              { value: 'es', label: 'Spanish' },
              { value: 'fr', label: 'French' },
            ]}
            placeholder="Select language"
          />
        </div>
      </div>
    </GlassPanel>
  );
}
```

### 4. Toast Notifications

```tsx
import { ToastProvider, useToast, VanguardButton } from 'vanguard-uikit';
import { Icons } from 'vanguard-uikit';

function NotificationDemo() {
  const { addToast } = useToast();
  
  const showToast = (variant) => {
    addToast({
      title: variant === 'success' ? 'Success!' : 'Error',
      message: variant === 'success' 
        ? 'Operation completed successfully' 
        : 'Something went wrong',
      variant
    });
  };
  
  return (
    <div className="space-x-4">
      <VanguardButton 
        variant="emerald"
        onClick={() => showToast('success')}
      >
        Show Success
      </VanguardButton>
      
      <VanguardButton 
        variant="rose"
        onClick={() => showToast('error')}
      >
        Show Error
      </VanguardButton>
    </div>
  );
}

// Wrap your app
function App() {
  return (
    <ToastProvider>
      <NotificationDemo />
    </ToastProvider>
  );
}
```

## File Structure

```
src/
├── components/
│   ├── Button/
│   │   ├── VanguardButton.tsx
│   │   └── index.ts
│   ├── Card/
│   │   ├── VanguardCard.tsx
│   │   ├── GlassPanel.tsx
│   │   ├── StatCard.tsx
│   │   └── index.ts
│   ├── Form/
│   │   ├── Input.tsx
│   │   ├── Select.tsx
│   │   └── index.ts
│   └── index.ts
├── styles/
│   └── theme.css
└── App.tsx
```

## Tailwind Configuration

Add the library to your Tailwind config:

```js
// tailwind.config.js
module.exports = {
  content: [
    './node_modules/vanguard-uikit/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {
      colors: {
        // Custom colors if needed
      },
    },
  },
  plugins: [],
}
```

## Troubleshooting

### Style Not Applying

- Ensure Tailwind is configured to scan vanguard-uikit in content
- Check that you imported the CSS if required
- Verify peer dependencies are installed

### Icons Not Showing

- Make sure `lucide-react` is installed
- Check icon import: `import { Icons } from 'vanguard-uikit'`
- Icons should be used as `<Icons.Zap />` not `<Icons.Zap />`

### Glass Effect Not Working

- Ensure element has a background behind it
- Glassmorphism requires content behind the glass panel
- Check backdrop-filter support in browsers

### Animation Issues

- Use animation variants: `fast`, `slow`, `liquid`
- Liquid animations may need longer transition times

## Validation and Quality

Before committing:

1. **Type check**: Run `tsc --noEmit`
2. **Build**: Verify production build works
3. **Test**: Verify components render correctly
4. **Visual QA**: Test glassmorphism effects
5. **Responsive**: Test at different breakpoints

## Resources

- [npm Package](https://www.npmjs.com/package/vanguard-uikit)
- [Demo Website](https://dream-pixels-forge.github.io/vanguard-uikit/)
- [GitHub Repository](https://github.com/Dream-Pixels-Forge/vanguard-uikit)
- [Lucide Icons](https://lucide.dev/icons/)
