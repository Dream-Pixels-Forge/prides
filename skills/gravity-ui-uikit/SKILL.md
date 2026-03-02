---
name: gravity-ui-uikit
description: Expert guidance for building applications with @gravity-ui/uikit - Yandex's React UI library featuring components, charts, theming, and design system integration.
allowed-tools:
  - "Read"
  - "Write"
  - "Bash"
  - "glob"
  - "grep_search"
  - "web_fetch"
---

# Gravity UIKit

You are a frontend engineer specialized in building applications with @gravity-ui/uikit—Yandex's React component library and design system that provides accessible, customizable UI components.

## Core Concepts

@gravity-ui/uikit is a **component library** from Yandex that offers:
- **Production-ready components**: Battle-tested at Yandex scale
- **TypeScript support**: Full type definitions included
- **Accessibility**: WCAG compliant components
- **Theming**: Customizable via CSS variables
- **Storybook**: Interactive component documentation

## Installation

### Prerequisites

- React 18+
- TypeScript 4.7+
- Node.js 18+

### Install Package

```bash
# Using npm
npm install @gravity-ui/uikit

# Using yarn
yarn add @gravity-ui/uikit
```

### Required Peer Dependencies

```bash
npm install react react-dom
```

## Quick Start

### Basic Setup

```tsx
import { Button, Card, Input } from '@gravity-ui/uikit';
import '@gravity-ui/uikit/styles/css/uikit.css';

function App() {
  return (
    <div>
      <Button view="action">Click me</Button>
      <Card>
        <Input placeholder="Enter text" />
      </Card>
    </div>
  );
}
```

### With Theme Provider

```tsx
import { ThemeProvider, Button } from '@gravity-ui/uikit';

function ThemedApp() {
  return (
    <ThemeProvider theme="light">
      <Button view="action">Themed Button</Button>
    </ThemeProvider>
  );
}
```

## Component Categories

### Basic Components

| Component | Description |
|-----------|-------------|
| **Button** | Clickable button with multiple variants |
| **Icon** | Scalable SVG icons |
| **Text** | Text with typography control |
| **Link** | Hyperlink with styles |
| **Avatar** | User avatar display |
| **Badge** | Status indicator |

### Form Components

| Component | Description |
|-----------|-------------|
| **Input** | Text input field |
| **Textarea** | Multi-line text input |
| **Select** | Dropdown selector |
| **Checkbox** | Checkbox input |
| **RadioButton** | Radio button input |
| **Switch** | Toggle switch |
| **Slider** | Range slider |
| **DateInput** | Date picker input |
| **FileUpload** | File upload component |

### Layout Components

| Component | Description |
|-----------|-------------|
| **Card** | Content container |
| **Block** | Section container |
| **Grid** | CSS Grid layout |
| **FlexLayout** | Flexbox layout |
| **Spinner** | Loading indicator |
| **Skeleton** | Content placeholder |

### Overlay Components

| Component | Description |
|-----------|-------------|
| **Modal** | Dialog/modal window |
| **Popup** | Popover/tooltip |
| **Toast** | Notification message |
| **Alert** | Alert banner |
| **Tooltip** | Hover tooltip |

### Navigation Components

| Component | Description |
|-----------|-------------|
| **Tabs** | Tab navigation |
| **Menu** | Dropdown menu |
| **Breadcrumbs** | Navigation breadcrumbs |
| **Pagination** | Page navigation |

## Component Usage

### Button

```tsx
import { Button } from '@gravity-ui/uikit';

// Variants
<Button view="normal">Normal</Button>
<Button view="action">Action</Button>
<Button view="flat">Flat</Button>
<Button view="outlined">Outlined</Button>

// Sizes
<Button size="xs">Extra Small</Button>
<Button size="s">Small</Button>
<Button size="m">Medium</Button>
<Button size="l">Large</Button>

// States
<Button disabled>Disabled</Button>
<Button loading>Loading</Button>

// With icon
<Button leftIcon={<Icon />}>With Icon</Button>
```

### Input

```tsx
import { Input } from '@gravity-ui/uikit';

function FormInput() {
  const [value, setValue] = useState('');
  
  return (
    <Input
      value={value}
      onUpdate={setValue}
      placeholder="Enter text"
      labelText="Label"
      error={value.length < 3 ? 'Min 3 characters' : undefined}
      disabled={false}
      size="m"
    />
  );
}
```

### Select

```tsx
import { Select } from '@gravity-ui/uikit';

const options = [
  { value: '1', content: 'Option 1' },
  { value: '2', content: 'Option 2' },
  { value: '3', content: 'Option 3' },
];

function MySelect() {
  const [selected, setSelected] = useState(null);
  
  return (
    <Select
      value={selected}
      onUpdate={setSelected}
      options={options}
      placeholder="Select option"
    />
  );
}
```

### Modal

```tsx
import { useState } from 'react';
import { Modal, Button } from '@gravity-ui/uikit';

function ModalExample() {
  const [open, setOpen] = useState(false);
  
  return (
    <>
      <Button onClick={() => setOpen(true)}>Open Modal</Button>
      <Modal
        open={open}
        onClose={() => setOpen(false)}
        title="Modal Title"
      >
        <p>Modal content goes here</p>
        <Button onClick={() => setOpen(false)}>Close</Button>
      </Modal>
    </>
  );
}
```

## Theming

### CSS Variables

```css
:root {
  /* Colors */
  --g-color-base-background: #ffffff;
  --g-color-base-text: #000000;
  --g-color-base-text-secondary: #666666;
  
  /* Primary colors */
  --g-color-primary: #0077ff;
  --g-color-primary-hover: #0066dd;
  --g-color-primary-active: #0055bb;
  
  /* Typography */
  --g-font-family: 'YS Text', 'Helvetica Neue', sans-serif;
  --g-font-size-xs: 10px;
  --g-font-size-s: 12px;
  --g-font-size-m: 14px;
  --g-font-size-l: 16px;
  --g-font-size-xl: 18px;
  
  /* Spacing */
  --g-spacing-1: 4px;
  --g-spacing-2: 8px;
  --g-spacing-3: 12px;
  --g-spacing-4: 16px;
  --g-spacing-5: 20px;
  --g-spacing-6: 24px;
  
  /* Border radius */
  --g-border-radius-s: 4px;
  --g-border-radius-m: 8px;
  --g-border-radius-l: 12px;
  
  /* Shadows */
  --g-shadow-color: rgba(0, 0, 0, 0.1);
}
```

### Dark Theme

```tsx
import { ThemeProvider } from '@gravity-ui/uikit';

function DarkApp() {
  return (
    <ThemeProvider theme="dark">
      <AppContent />
    </ThemeProvider>
  );
}
```

### Custom Theme

```tsx
import { ThemeProvider } from '@gravity-ui/uikit';

const customTheme = {
  light: {
    primary: '#ff6b6b',
    secondary: '#4ecdc4',
  },
  dark: {
    primary: '#ff8787',
    secondary: '#63e6be',
  },
};

<ThemeProvider theme="light" customTheme={customTheme}>
  <App />
</ThemeProvider>
```

## File Structure

```
src/
├── components/
│   ├── Button/
│   │   ├── Button.tsx
│   │   └── Button.stories.tsx
│   ├── Input/
│   │   └── Input.tsx
│   └── AppLayout.tsx
├── styles/
│   └── theme.css
└── App.tsx
```

## Form Integration

### With react-hook-form

```tsx
import { useForm } from 'react-hook-form';
import { Input, Button, FormRow } from '@gravity-ui/uikit';

interface FormData {
  email: string;
  password: string;
}

function LoginForm() {
  const { register, handleSubmit, formState: { errors } } = useForm<FormData>();
  
  const onSubmit = (data: FormData) => {
    console.log('Submit:', data);
  };
  
  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <FormRow label="Email">
        <Input
          {...register('email', { required: true })}
          error={errors.email ? 'Email is required' : undefined}
        />
      </FormRow>
      <FormRow label="Password">
        <Input
          type="password"
          {...register('password', { required: true, minLength: 8 })}
          error={errors.password ? 'Password must be 8+ chars' : undefined}
        />
      </FormRow>
      <Button type="submit" view="action">Login</Button>
    </form>
  );
}
```

### With FormBuilder

```tsx
import { FormBuilder, useForm } from '@gravity-ui/uikit';

const schema = {
  fields: {
    name: {
      type: 'text',
      label: 'Name',
      required: true,
    },
    email: {
      type: 'text',
      label: 'Email',
      validation: { pattern: /@/ },
    },
    age: {
      type: 'number',
      label: 'Age',
    },
  },
};

function MyForm() {
  const form = useForm();
  
  return (
    <FormBuilder
      form={form}
      schema={schema}
      onSubmit={(data) => console.log(data)}
    />
  );
}
```

## Accessibility

### ARIA Support

All components include proper ARIA attributes:

```tsx
// Button has proper roles and states
<Button 
  aria-label="Close dialog"
  aria-describedby="dialog-description"
>
  ×
</Button>
```

### Keyboard Navigation

- Tab order follows visual order
- Focus indicators are visible
- Escape closes modals/popups
- Arrow keys work in selects/menus

### Screen Reader

- Form labels are associated
- Error messages are announced
- Status updates use live regions

## Common Patterns

### 1. Login Form

```tsx
import { useState } from 'react';
import { Input, Button, Card, FormRow } from '@gravity-ui/uikit';

function LoginForm() {
  const [loading, setLoading] = useState(false);
  
  const handleSubmit = async (e: React.FormEvent) => {
    e.preventDefault();
    setLoading(true);
    // Login logic
    setLoading(false);
  };
  
  return (
    <Card style={{ maxWidth: 400, padding: 24 }}>
      <form onSubmit={handleSubmit}>
        <FormRow label="Email">
          <Input placeholder="email@example.com" />
        </FormRow>
        <FormRow label="Password">
          <Input type="password" placeholder="Password" />
        </FormRow>
        <Button
          type="submit"
          view="action"
          width="max"
          loading={loading}
        >
          Sign In
        </Button>
      </form>
    </Card>
  );
}
```

### 2. Data Table

```tsx
import { Table, TableBody, TableHead, TableRow, TableCell } from '@gravity-ui/uikit';

function DataTable({ data }) {
  return (
    <Table>
      <TableHead>
        <TableRow>
          <TableCell>Name</TableCell>
          <TableCell>Status</TableCell>
          <TableCell>Actions</TableCell>
        </TableRow>
      </TableHead>
      <TableBody>
        {data.map(item => (
          <TableRow key={item.id}>
            <TableCell>{item.name}</TableCell>
            <TableCell>
              <Badge theme={item.active ? 'success' : 'warning'}>
                {item.active ? 'Active' : 'Pending'}
              </Badge>
            </TableCell>
            <TableCell>
              <Button size="s" view="flat">Edit</Button>
            </TableCell>
          </TableRow>
        ))}
      </TableBody>
    </Table>
  );
}
```

### 3. Notifications

```tsx
import { Toast, Button } from '@gravity-ui/uikit';

function NotificationExample() {
  const notify = (type) => {
    Toast.add({
      name: 'notification',
      type, // 'success' | 'warning' | 'error' | 'info'
      title: 'Notification Title',
      content: 'Notification message',
      actions: [
        { label: 'Action', onClick: () => {} }
      ],
    });
  };
  
  return (
    <>
      <Button onClick={() => notify('success')}>Success</Button>
      <Button onClick={() => notify('error')}>Error</Button>
    </>
  );
}
```

## Icons

### Using Icons

```tsx
import { Icon } from '@gravity-ui/uikit';
import { Xmark, Checkmark, ArrowRight } from '@gravity-ui/icons';

function IconExample() {
  return (
    <>
      <Icon data={Xmark} size={16} />
      <Icon data={Checkmark} size={24} />
      <Icon data={ArrowRight} size="m" />
    </>
  );
}
```

### Icon Sizes

```tsx
// Predefined sizes
<Icon data={IconComponent} size="xs" />  // 12px
<Icon data={IconComponent} size="s" />   // 14px
<Icon data={IconComponent} size="m" />   // 16px
<Icon data={IconComponent} size="l" />   // 20px
<Icon data={IconComponent} size="xl" />  // 24px

// Custom size
<Icon data={IconComponent} size={32} />
```

## Troubleshooting

### Style Issues

- Import CSS: `import '@gravity-ui/uikit/styles/css/uikit.css';`
- Check CSS variables are defined
- Verify theme provider wraps your app

### TypeScript Errors

- Ensure TypeScript 4.7+
- Check @gravity-ui/uikit types are installed
- Restart TypeScript server

### Performance Issues

- Use `React.memo()` for custom components
- Implement virtualization for large lists
- Lazy load components with `React.lazy()`

## Validation and Quality

Before committing:
1. **Type check**: Run `tsc --noEmit`
2. **Lint**: Run linter to catch issues
3. **Test**: Verify component interactions
4. **A11y**: Test with screen reader
5. **Responsive**: Test at different breakpoints

## Resources

- [Gravity UI Website](https://gravity-ui.com)
- [Component Library](https://gravity-ui.com/components/uikit)
- [Storybook](https://preview.gravity-ui.com)
- [GitHub](https://github.com/gravity-ui/uikit)
- [Figma Design System](https://www.figma.com/community/file/1271150067798118027)
