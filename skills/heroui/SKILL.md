---
name: heroui
description: Expert guidance for building beautiful, accessible UIs with HeroUI - a React UI library featuring modern components, theming, and comprehensive accessibility.
allowed-tools:
  - "Read"
  - "Write"
  - "Bash"
  - "glob"
  - "grep_search"
  - "web_fetch"
---

# HeroUI - React UI Library

You are a frontend expert specialized in building beautiful, accessible user interfaces with HeroUI—a React UI library built on top of Tailwind CSS and React Aria.

## Core Concepts

### What is HeroUI?

- **Component Library**: Pre-built React components
- **Tailwind CSS**: Styling with Tailwind utilities
- **React Aria**: Accessible primitives
- **Themeable**: Light/dark mode, custom themes
- **TypeScript**: Full type support

### Why HeroUI?

- **Accessible**: WCAG compliant out of the box
- **Customizable**: Full Tailwind control
- **Modern**: Newest features, regular updates
- **Dark mode**: Native support

## Installation

### Prerequisites

- React 18+
- Tailwind CSS 3+
- TypeScript (recommended)

### Install

```bash
# Core package
npm install @heroui/react

# Install dependencies
npm install framer-motion tailwindcss postcss autoprefixer
```

### Setup

```tsx
// src/providers/heroui-provider.tsx
'use client';

import { HeroUIProvider } from '@heroui/react';

export function Providers({ children }: { children: React.ReactNode }) {
  return (
    <HeroUIProvider>
      {children}
    </HeroUIProvider>
  );
}
```

```tsx
// src/app/layout.tsx
import { Providers } from '@/providers/heroui-provider';

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" className="dark">
      <body>
        <Providers>{children}</Providers>
      </body>
    </html>
  );
}
```

### Tailwind Config

```javascript
// tailwind.config.js
const { heroui } = require('@heroui/react');

/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './src/**/*.{js,ts,jsx,tsx}',
    './node_modules/@heroui/theme/src/**/*.{js,ts,jsx,tsx}',
  ],
  theme: {
    extend: {},
  },
  darkMode: 'class',
  plugins: [heroui({
    themes: {
      light: {},
      dark: {},
    },
  })],
};
```

## Components

### Button

```tsx
import { Button } from '@heroui/react';

// Variants
<Button color="default">Default</Button>
<Button color="primary">Primary</Button>
<Button color="secondary">Secondary</Button>
<Button color="success">Success</Button>
<Button color="warning">Warning</Button>
<Button color="danger">Danger</Button>

// Variants style
<Button variant="solid">Solid</Button>
<Button variant="faded">Faded</Button>
<Button variant="bordered">Bordered</Button>
<Button variant="light">Light</Button>
<Button variant="flat">Flat</Button>
<Button variant="ghost">Ghost</Button>
<Button variant="shadow">Shadow</Button>

// Sizes
<Button size="sm">Small</Button>
<Button size="md">Medium</Button>
<Button size="lg">Large</Button>

// States
<Button isLoading>Loading</Button>
<Button isDisabled>Disabled</Button>

// With icon
<Button startContent={<Icon />}>Start Icon</Button>
<Button endContent={<Icon />}>End Icon</Button>
```

### Input

```tsx
import { Input } from '@heroui/react';

// Basic
<Input />                                   // Empty
<Input placeholder="Enter text" />          // Placeholder
<Input label="Email" />                     // With label
<Input label="Email" placeholder="Enter email" />

// Variants
<Input variant="flat" />
<Input variant="faded" />
<Input variant="bordered" />
<Input variant="underlined" />

// With description/error
<Input 
  label="Email" 
  description="We'll never share your email" 
/>
<Input 
  label="Email" 
  errorMessage="Invalid email" 
  isInvalid 
/>

// With icons
<Input 
  startContent={<MailIcon />} 
  endContent={<Icon />}
/>

// Types
<Input type="email" />
<Input type="password" />
<Input type="search" />
<Input type="number" />
<Input type="tel" />
<Input type="url" />
```

### Select

```tsx
import { Select, SelectItem } from '@heroui/react';

<Select
  label="Favorite Animal"
  placeholder="Select an animal"
>
  <SelectItem key="dog">Dog</SelectItem>
  <SelectItem key="cat">Cat</SelectItem>
  <SelectItem key="rabbit">Rabbit</SelectItem>
</Select>

// With description
<Select
  label="Role"
  description="Select your role in the company"
>
  <SelectItem key="admin">Administrator</SelectItem>
  <SelectItem key="user">User</SelectItem>
</Select>

// Multiple selection
<Select
  label="Colors"
  selectionMode="multiple"
>
  <SelectItem key="red">Red</SelectItem>
  <SelectItem key="blue">Blue</SelectItem>
</Select>
```

### Checkbox

```tsx
import { Checkbox, CheckboxGroup } from '@heroui/react';

<Checkbox>Remember me</Checkbox>

// Group
<CheckboxGroup label="Select options">
  <Checkbox value="option1">Option 1</Checkbox>
  <Checkbox value="option2">Option 2</Checkbox>
  <Checkbox value="option3">Option 3</Checkbox>
</CheckboxGroup>

// With colors
<Checkbox color="success">Success</Checkbox>
<Checkbox color="warning">Warning</Checkbox>
<Checkbox color="danger">Danger</Checkbox>
```

### Radio

```tsx
import { Radio, RadioGroup } from '@heroui/react';

<RadioGroup label="Delivery method">
  <Radio value="standard">Standard</Radio>
  <Radio value="express">Express</Radio>
  <Radio value="overnight">Overnight</Radio>
</RadioGroup>
```

### Switch

```tsx
import { Switch } from '@heroui/react';

<Switch>Enable notifications</Switch>

// With colors
<Switch color="primary">Primary</Switch>
<Switch color="secondary">Secondary</Switch>
<Switch color="success">Success</Switch>
<Switch color="warning">Warning</Switch>
<Switch color="danger">Danger</Switch>

// Controlled
const [isSelected, setIsSelected] = useState(false);
<Switch 
  isSelected={isSelected} 
  onValueChange={setIsSelected}
>
  Controlled Switch
</Switch>
```

### Textarea

```tsx
import { Textarea } from '@heroui/react';

<Textarea
  label="Description"
  placeholder="Enter your description"
/>

<Textarea
  label="Bio"
  minRows={3}
  maxRows={6}
/>
```

### Card

```tsx
import { Card, CardBody, CardHeader, CardFooter } from '@heroui/react';

<Card>
  <CardHeader>
    <h3>Card Title</h3>
  </CardHeader>
  <CardBody>
    <p>Card content goes here.</p>
  </CardBody>
  <CardFooter>
    <Button>Action</Button>
  </CardFooter>
</Card>

// Variants
<Card isHoverable>Hoverable</Card>
<Card isPressable>Pressable</Card>
<Card variant="bordered">Bordered</Card>
<Card variant="shadowed">Shadowed</Card>
```

### Modal

```tsx
import { Modal, ModalContent, ModalHeader, ModalBody, ModalFooter, Button, useDisclosure } from '@heroui/react';

const { isOpen, onOpen, onClose } = useDisclosure();

<>
  <Button onPress={onOpen}>Open Modal</Button>
  
  <Modal isOpen={isOpen} onClose={onClose}>
    <ModalContent>
      <ModalHeader className="flex flex-col gap-1">
        Modal Title
      </ModalHeader>
      <ModalBody>
        <p>Modal content here.</p>
      </ModalBody>
      <ModalFooter>
        <Button color="danger" variant="flat" onPress={onClose}>
          Close
        </Button>
        <Button color="primary" onPress={onClose}>
          Confirm
        </Button>
      </ModalFooter>
    </ModalContent>
  </Modal>
</>
```

### Dropdown

```tsx
import { Dropdown, DropdownTrigger, DropdownMenu, DropdownItem, Button } from '@heroui/react';

<Dropdown>
  <DropdownTrigger>
    <Button>Actions</Button>
  </DropdownTrigger>
  <DropdownMenu aria-label="Actions">
    <DropdownItem key="edit">Edit</DropdownItem>
    <DropdownItem key="delete" color="danger">Delete</DropdownItem>
  </DropdownMenu>
</Dropdown>
```

### Avatar

```tsx
import { Avatar, AvatarGroup } from '@heroui/react';

<Avatar src="https://image.url/avatar.jpg" />

// Sizes
<Avatar size="sm" />
<Avatar size="md" />
<Avatar size="lg" />

// With fallback
<Avatar name="John Doe" />

// Group
<AvatarGroup>
  <Avatar src="1.jpg" />
  <Avatar src="2.jpg" />
  <Avatar src="3.jpg" />
</AvatarGroup>
```

### Badge

```tsx
import { Badge } from '@heroui/react';

<Badge color="default">Default</Badge>
<Badge color="primary">Primary</Badge>
<Badge color="secondary">Secondary</Badge>
<Badge color="success">Success</Badge>
<Badge color="warning">Warning</Badge>
<Badge color="danger">Danger</Badge>

// With dot
<Badge color="danger" isDot>Nebula</Badge>

// With size
<Badge size="sm">Small</Badge>
<Badge size="md">Medium</Badge>
<Badge size="lg">Large</Badge>
```

### Chip

```tsx
import { Chip } from '@heroui/react';

<Chip>Chip</Chip>

// Variants
<Chip variant="solid">Solid</Chip>
<Chip variant="bordered">Bordered</Chip>
<Chip variant="light">Light</Chip>
<Chip variant="flat">Flat</Chip>

// Colors
<Chip color="primary">Primary</Chip>
<Chip color="success">Success</Chip>
<Chip color="warning">Warning</Chip>
<Chip color="danger">Danger</Chip>

// Removable
<Chip onClose={() => {}}>Removable</Chip>

// Avatars
<Chip 
  avatar={<Avatar src="image.jpg" name="JS" />}
>
  With Avatar
</Chip>
```

### Tabs

```tsx
import { Tabs, Tab } from '@heroui/react';

<Tabs aria-label="Options">
  <Tab key="photos" title="Photos">
    <p>Photos content</p>
  </Tab>
  <Tab key="music" title="Music">
    <p>Music content</p>
  </Tab>
  <Tab key="videos" title="Videos">
    <p>Videos content</p>
  </Tab>
</Tabs>

// Variants
<Tabs variant="solid" />
<Tabs variant="underlined" />
<Tabs variant="bordered" />
<Tabs variant="light" />
```

### Table

```tsx
import { Table, TableHeader, TableBody, TableColumn, TableRow, TableCell } from '@heroui/react';

<Table aria-label="Example table">
  <TableHeader>
    <TableColumn>NAME</TableColumn>
    <TableColumn>ROLE</TableColumn>
    <TableColumn>STATUS</TableColumn>
  </TableHeader>
  <TableBody>
    <TableRow key="1">
      <TableCell>Tony Reichert</TableCell>
      <TableCell>CEO</TableCell>
      <TableCell>Active</TableCell>
    </TableRow>
  </TableBody>
</Table>
```

### Progress

```tsx
import { Progress } from '@heroui/react';

<Progress value={50} />

// With label
<Progress value={75} label="Loading..." />

// Sizes
<Progress size="sm" value={50} />
<Progress size="md" value={50} />
<Progress size="lg" value={50} />

// Colors
<Progress color="default" value={50} />
<Progress color="primary" value={50} />
<Progress color="success" value={50} />
<Progress color="warning" value={50} />
<Progress color="danger" value={50} />
```

### Skeleton

```tsx
import { Skeleton } from '@heroui/react';

<Skeleton className="rounded-lg" isLoaded={false}>
  <div className="h-4 bg-gray-200 rounded-lg w-3/5"></div>
</Skeleton>
```

### Spinner

```tsx
import { Spinner } from '@heroui/react';

<Spinner />

// Sizes
<Spinner size="sm" />
<Spinner size="md" />
<Spinner size="lg" />

// Colors
<Spinner color="primary" />
<Spinner color="success" />
```

### Tooltip

```tsx
import { Tooltip, Button } from '@heroui/react';

<Tooltip content="Add to cart">
  <Button isIconOnly><PlusIcon /></Button>
</Tooltip>
```

### Popover

```tsx
import { Popover, PopoverTrigger, PopoverContent, Button } from '@heroui/react';

<Popover placement="right">
  <PopoverTrigger>
    <Button>Toggle Popover</Button>
  </PopoverTrigger>
  <PopoverContent>
    <div className="px-1 py-2">
      <p>Popover content here.</p>
    </div>
  </PopoverContent>
</Popover>
```

### Alert

```tsx
import { Alert } from '@heroui/react';

<Alert 
  title="Success" 
  description="Your changes have been saved."
  color="success"
/>

// Colors
<Alert color="default" />
<Alert color="primary" />
<Alert color="secondary" />
<Alert color="success" />
<Alert color="warning" />
<Alert color="danger" />
```

### Accordion

```tsx
import { Accordion, AccordionItem } from '@heroui/react';

<Accordion>
  <AccordionItem key="1" aria-label="Accordion 1" title="Accordion 1">
    <p>Content for accordion 1.</p>
  </AccordionItem>
  <AccordionItem key="2" aria-label="Accordion 2" title="Accordion 2">
    <p>Content for accordion 2.</p>
  </AccordionItem>
</Accordion>
```

### Divider

```tsx
import { Divider } from '@heroui/react';

<Divider />

// With label
<Divider>Or</Divider>

// Orientations
<Divider orientation="horizontal" />
<Divider orientation="vertical" />
```

## Form Integration

### With React Hook Form

```tsx
import { useForm } from 'react-hook-form';
import { Input, Button, Form } from '@heroui/react';

type Inputs = {
  email: string;
  password: string;
};

export default function LoginForm() {
  const { register, handleSubmit, formState: { errors } } = useForm<Inputs>();
  
  const onSubmit = (data: Inputs) => {
    console.log(data);
  };
  
  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-4">
      <FormField
        errorMessage={errors.email?.message}
        isInvalid={!!errors.email}
      >
        <Input
          {...register('email', { required: 'Email is required' })}
          label="Email"
          type="email"
        />
      </FormField>
      
      <FormField
        errorMessage={errors.password?.message}
        isInvalid={!!errors.password}
      >
        <Input
          {...register('password', { required: 'Password is required' })}
          label="Password"
          type="password"
        />
      </FormField>
      
      <Button type="submit" color="primary">
        Submit
      </Button>
    </form>
  );
}
```

## Theming

### Dark Mode

```tsx
// Automatic based on system
<HeroUIProvider>
  <App />
</HeroUIProvider>

// Force dark mode
<HeroUIProvider defaultTheme="dark">
  <App />
</HeroUIProvider>
```

### Custom Theme

```tsx
// tailwind.config.js
const { heroui } = require('@heroui/react');

module.exports = {
  plugins: [heroui({
    themes: {
      mytheme: {
        colors: {
          primary: {
            50: '...',
            100: '...',
            // ...
          },
        },
      },
    },
  })],
};
```

## Layout Components

### Grid

```tsx
import { Grid, GridItem } from '@heroui/react';

<Grid>
  <GridItem>Item 1</GridItem>
  <GridItem>Item 2</GridItem>
</Grid>
```

### Container

```tsx
import { Container, Row, Column } from '@heroui/react';

<Container>
  <Row>
    <Column>Left</Column>
    <Column>Right</Column>
  </Row>
</Container>
```

## Utilities

### Pagination

```tsx
import { Pagination } from '@heroui/react';

<Pagination 
  total={10} 
  initialPage={1} 
  onChange={(page) => console.log(page)} 
/>
```

### Kbd

```tsx
import { Kbd } from '@heroui/react';

<Kbd keys={['command']}>K</Kbd>
<Kbd keys={['command', 'shift']}>P</Kbd>
```

### Link

```tsx
import { Link } from '@heroui/react';

<Link href="#" isExternal>External Link</Link>
<Link href="#" showAnchorIcon>Link with icon</Link>
```

## Troubleshooting

### Styles Not Applying

1. Ensure HeroUI is in tailwind config content
2. Check that providers wrap your app
3. Run build again after config changes

### Dark Mode Issues

1. Add `dark` class to html element
2. Use `HeroUIProvider` correctly
3. Check tailwind darkMode setting

## Resources

- [HeroUI Documentation](https://heroui.com)
- [HeroUI GitHub](https://github.com/heroui-inc/heroui)
- [React Aria](https://react-spectrum.adobe.com/react-aria)
