---
name: react-three-uikit
description: Expert guidance for building 3D user interfaces with @react-three/uikit for React Three Fiber, including layouts, components, interactivity, and XR/VR applications.
allowed-tools:
  - "Read"
  - "Write"
  - "Bash"
  - "glob"
  - "grep_search"
  - "web_fetch"
---

# React Three UIKit

You are a 3D frontend engineer specialized in building performant user interfaces with @react-three/uikit—a library for creating 3D user interfaces using React Three Fiber and Yoga layout engine.

## Core Concepts

@react-three/uikit is a **3D UI library** that brings web-like layouts to Three.js:
- **Flexbox for 3D**: Use familiar flexbox properties in 3D space
- **React Three Fiber**: Native React integration
- **Yoga Layout**: Facebook's layout engine (same as React Native)
- **XR Ready**: Perfect for VR/AR applications
- **Performant**: Optimized for 60fps in 3D

## Installation

### Prerequisites

- React 18+
- Three.js / @react-three/fiber
- Node.js 18+

### Install Package

```bash
# Core package
npm install @react-three/uikit

# For default shadcn-style components
npm install @react-three/uikit-default
npm install @pmndrs/uikit-default
```

## Quick Start

### Basic 3D Layout

```tsx
import { createRoot } from 'react-dom/client';
import { Canvas } from '@react-three/fiber';
import { Fullscreen, Container } from '@react-three/uikit';

function App() {
  return (
    <Canvas>
      <Fullscreen
        flexDirection="row"
        padding={10}
        gap={10}
      >
        <Container
          flexGrow={1}
          opacity={0.5}
          hover={{ opacity: 1 }}
          backgroundColor="red"
        />
        <Container
          flexGrow={1}
          opacity={0.5}
          hover={{ opacity: 1 }}
          backgroundColor="blue"
        />
      </Fullscreen>
    </Canvas>
  );
}
```

### Fullscreen with Theme

```tsx
import { Fullscreen, Container, Text } from '@react-three/uikit';
import { themes } from '@react-three/uikit-default';

function ThemedApp() {
  return (
    <Canvas>
      <Fullscreen theme={themes.default}>
        <Container>
          <Text>Hello 3D World!</Text>
        </Container>
      </Fullscreen>
    </Canvas>
  );
}
```

## Core Components

### Layout Components

| Component | Description |
|-----------|-------------|
| **Fullscreen** | Root container that fills the viewport |
| **Container** | Generic flexbox container |
| **Text** | 3D text with typography support |
| **Image** | 3D image display |
| **Scroll** | Scrollable container |

### Available Components

| Component | Category | Description |
|-----------|----------|-------------|
| **Button** | Interactive | Clickable button |
| **Input** | Forms | Text input field |
| **Checkbox** | Forms | Toggle checkbox |
| **Switch** | Forms | On/off switch |
| **Select** | Forms | Dropdown selector |
| **Slider** | Forms | Range slider |
| **Avatar** | Display | User avatar |
| **Badge** | Display | Status badge |
| **Card** | Display | Content card |
| **Accordion** | Layout | Collapsible sections |
| **Tabs** | Navigation | Tab navigation |

## Layout System

### Flexbox Properties

All standard flexbox properties work in 3D:

```tsx
<Container
  // Flex container
  display="flex"
  flexDirection="row"        // row, column, row-reverse, column-reverse
  flexWrap="wrap"           // wrap, nowrap, wrap-reverse
  
  // Alignment
  justifyContent="center"   // flex-start, flex-end, center, space-between, space-around
  alignItems="center"       // flex-start, flex-end, center, stretch, baseline
  alignContent="center"     // flex-start, flex-end, center, space-between, space-around
  
  // Sizing
  width={200}
  height={100}
  padding={20}
  margin={10}
  gap={15}
  
  // Position
  position="absolute"
  left={0}
  top={0}
>
  {/* Children */}
</Container>
```

### 3D-Specific Properties

```tsx
<Container
  // 3D positioning
  position={[0, 1, 0]}
  rotation={[0, Math.PI, 0]}
  scale={[1, 1, 1]}
  
  // 3D appearance
  backgroundColor="#ff0000"
  opacity={0.8}
  transparent={true}
  side="double"  // front, back, double
  
  // Border
  borderWidth={2}
  borderRadius={10}
  borderColor="#000000"
>
```

## Interactivity

### Hover States

```tsx
<Container
  opacity={0.5}
  hover={{
    opacity: 1,
    scale: 1.1,
    backgroundColor: '#ff0000'
  }}
>
  {/* Content */}
</Container>
```

### Press/Click States

```tsx
<Container
  onClick={() => console.log('clicked')}
  onPointerDown={() => console.log('pressed')}
  onPointerUp={() => console.log('released')}
  onPointerOver={() => console.log('entered')}
  onPointerOut={() => console.log('left')}
>
```

### Gestures

```tsx
import { useGesture } from '@use-gesture/react';

function DraggableContainer() {
  const bind = useGesture({
    onDrag: ({ offset: [x, y] }) => {
      // Handle drag
    }
  });
  
  return <Container {...bind()} />;
}
```

## Typography

### Text Component

```tsx
import { Text } from '@react-three/uikit';

<Text
  // Typography
  fontSize={16}
  lineHeight={1.5}
  fontWeight="bold"
  fontStyle="italic"
  
  // Text properties
  textAlign="center"        // left, center, right
  verticalAlign="middle"    // top, middle, bottom
  
  // Color
  color="#ffffff"
  backgroundColor="#000000"
  padding={10}
>
  Hello World
</Text>
```

### Custom Fonts

```tsx
import { Text } from '@react-three/uikit';
import myFont from './fonts/custom-font.woff';

<Text
  font={myFont}
  fontSize={24}
>
  Custom Font Text
</Text>
```

## Theming

### Using Built-in Themes

```tsx
import { themes } from '@react-three/uikit-default';
import { Fullscreen } from '@react-three/uikit';

// Shadcn-style theme
<Fullscreen theme={themes.default}>

// Other available themes
// themes.horizon - Horizon OS style
</Fullscreen>
```

### Custom Theme

```tsx
const myTheme = {
  colors: {
    primary: '#6366f1',
    secondary: '#8b5cf6',
    background: '#ffffff',
    text: '#1f2937',
  },
  fonts: {
    body: 'Inter',
    mono: 'Fira Code',
  },
  shadows: {
    sm: '0 1px 2px rgba(0,0,0,0.1)',
    md: '0 4px 6px rgba(0,0,0,0.1)',
  },
};

<Fullscreen theme={myTheme}>
```

## File Structure

```
src/
├── components/
│   ├── 3DLayout.tsx       # 3D layout components
│   ├── Card3D.tsx         # Card with 3D effects
│   └── UI3D.tsx           # Main UI component
├── App.tsx
└── main.tsx
```

## Common Patterns

### 1. Card with Hover Effect

```tsx
import { Container, Text, Image } from '@react-three/uikit';

function ProductCard({ imageUrl, title, price }) {
  return (
    <Container
      width={200}
      height={300}
      backgroundColor="white"
      borderRadius={12}
      shadow
      hover={{
        scale: 1.05,
        shadow: { blur: 20, color: 'rgba(0,0,0,0.3)' }
      }}
      transition={{ duration: 0.3 }}
    >
      <Image
        width="100%"
        height={150}
        objectFit="cover"
        src={imageUrl}
      />
      <Container padding={16}>
        <Text fontSize={18} fontWeight="bold">{title}</Text>
        <Text fontSize={14} color="gray">{price}</Text>
      </Container>
    </Container>
  );
}
```

### 2. Form Input

```tsx
import { Input, Text } from '@react-three/uikit';

function LoginInput() {
  return (
    <Container flexDirection="column" gap={10}>
      <Text fontSize={14} fontWeight="medium">Email</Text>
      <Input
        width="100%"
        height={40}
        placeholder="Enter your email"
        padding={12}
        borderWidth={1}
        borderColor="gray"
        focus={{
          borderColor: 'blue',
          borderWidth: 2
        }}
      />
    </Container>
  );
}
```

### 3. Tab Navigation

```tsx
import { Tabs, Tab } from '@react-three/uikit';

function TabNavigation() {
  const [activeTab, setActiveTab] = useState(0);
  
  return (
    <Tabs value={activeTab} onChange={setActiveTab}>
      <Tab value={0} label="Home" />
      <Tab value={1} label="Settings" />
      <Tab value={2} label="Profile" />
    </Tabs>
  );
}
```

## VR/XR Support

### Setting up for VR

```tsx
import { VRButton } from '@react-three/xr';
import { Fullscreen, Container, Text } from '@react-three/uikit';

function VRApp() {
  return (
    <>
      <VRButton />
      <XR>
        <Controllers />
        <Hands />
        <Fullscreen>
          <Container>
            <Text>Welcome to VR!</Text>
          </Container>
        </Fullscreen>
      </XR>
    </>
  );
}
```

### VR Interaction

```tsx
import { useXR } from '@react-three/xr';

function VRButton3D() {
  const { isPresenting } = useXR();
  
  return (
    <Container
      width={0.2}
      height={0.05}
      backgroundColor={isPresenting ? '#4ade80' : '#3b82f6'}
      onClick={() => console.log('VR clicked')}
      hover={isPresenting ? {
        scale: 1.1,
        backgroundColor: '#22c55e'
      } : undefined}
    >
      <Text fontSize={0.02} color="white">Click Me</Text>
    </Container>
  );
}
```

## Performance Optimization

### Best Practices

```tsx
// Good: Use instances for repeated elements
function ListItem({ items }) {
  return (
    <Container>
      {items.map(item => (
        <Container key={item.id} /* ... */ />
      ))}
    </Container>
  );
}

// Good: Lazy load components
const Heavy3DComponent = React.lazy(() => import('./HeavyComponent'));

// Good: Use memo for stable references
const MemoizedContainer = React.memo(Container);
```

### Performance Tips

- Use `dpr={[1, 2]}` to limit pixel ratio
- Implement `frameloop="demand"` for static content
- Use `instances` for repeated geometries
- Limit shadow casting
- Use `gl={{ powerPreference: 'high-performance' }}`

## Troubleshooting

### Layout Issues

- Check that parent has defined dimensions
- Verify flex direction is set correctly
- Ensure `display: flex` is set on container

### Rendering Issues

- Verify all required dependencies are installed
- Check that Canvas has sufficient size
- Ensure materials support transparency

### Interaction Issues

- Add `pointerEvents="auto"` to interactive elements
- Check that raycaster can reach the object
- Verify z-index/order of elements

## Validation and Quality

Before committing:
1. **Type check**: Run `tsc --noEmit`
2. **Build**: Verify production build works
3. **Test**: Verify 3D interactions work
4. **Performance**: Check frame rate (60fps target)
5. **VR Test**: If XR feature, test in headset

## Resources

- [UIKit Documentation](https://docs.pmnd.rs/uikit)
- [GitHub Repository](https://github.com/pmndrs/uikit)
- [Examples](https://docs.pmnd.rs/uikit/getting-started/examples)
- [PMNDRS Discord](https://discord.gg/ZZjjNvJ)
