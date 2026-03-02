---
name: tailwindcss
description: Expert guidance for building modern UIs with Tailwind CSS, including configuration, utility classes, responsive design, dark mode, animations, and best practices.
allowed-tools:
  - "Read"
  - "Write"
  - "Bash"
  - "glob"
  - "grep_search"
  - "web_fetch"
---

# Tailwind CSS

You are a styling expert specialized in building modern user interfaces with Tailwind CSS—a utility-first CSS framework that enables rapid UI development.

## Core Concepts

### Utility-First

Tailwind provides **low-level utility classes** that you combine to build custom designs:

```html
<div class="flex items-center justify-between p-4 bg-white rounded-lg shadow-md">
  <h1 class="text-2xl font-bold text-gray-900">Hello</h1>
</div>
```

### Key Benefits

- **No context switching**: Stay in HTML
- **Easy customization**: Config file for design tokens
- **Small bundle**: Purges unused styles
- **Responsive**: Built-in breakpoints
- **Dark mode**: Native support

## Installation

### With Next.js

```bash
npx create-next-app@latest my-app -- --tailwind
```

### Manual Installation

```bash
# Install dependencies
npm install -D tailwindcss postcss autoprefixer

# Initialize config
npx tailwindcss init -p
```

### Configuration

```javascript
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    './src/**/*.{js,ts,jsx,tsx,mdx}',
  ],
  darkMode: 'class', // or 'media' or 'selector'
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#eff6ff',
          100: '#dbeafe',
          500: '#3b82f6',
          600: '#2563eb',
          700: '#1d4ed8',
        },
      },
      fontFamily: {
        sans: ['Inter', 'sans-serif'],
      },
      spacing: {
        '128': '32rem',
      },
    },
  },
  plugins: [],
};
```

```javascript
// postcss.config.js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};
```

```css
/* globals.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Spacing

### Margin & Padding

```html
<!-- Padding -->
<p class="p-4">         <!-- all sides -->
<p class="px-4">         <!-- horizontal -->
<p class="py-4">        <!-- vertical -->
<p class="pt-4 pr-4 pb-4 pl-4"> <!-- individual -->

<!-- Margin -->
<div class="m-4">      <!-- all sides -->
<div class="mx-4">      <!-- horizontal -->
<div class="my-4">      <!-- vertical -->

<!-- Negative margin -->
<div class="-mt-4">    <!-- negative top -->
```

### Spacing Scale

| Class | Value |
|-------|-------|
| `p-0` | 0 |
| `p-1` | 0.25rem (4px) |
| `p-2` | 0.5rem (8px) |
| `p-3` | 0.75rem (12px) |
| `p-4` | 1rem (16px) |
| `p-5` | 1.25rem (20px) |
| `p-6` | 1.5rem (24px) |
| `p-8` | 2rem (32px) |
| `p-10` | 2.5rem (40px) |
| `p-12` | 3rem (48px) |

## Typography

### Font Size

```html
<p class="text-xs">    <!-- 0.75rem -->
<p class="text-sm">    <!-- 0.875rem -->
<p class="text-base">  <!-- 1rem -->
<p class="text-lg">    <!-- 1.125rem -->
<p class="text-xl">    <!-- 1.25rem -->
<p class="text-2xl">   <!-- 1.5rem -->
<p class="text-3xl">   <!-- 1.875rem -->
<p class="text-4xl">   <!-- 2.25rem -->
<p class="text-5xl">   <!-- 3rem -->
```

### Font Weight

```html
<p class="font-thin">        <!-- 100 -->
<p class="font-extralight"> <!-- 200 -->
<p class="font-light">      <!-- 300 -->
<p class="font-normal">      <!-- 400 -->
<p class="font-medium">      <!-- 500 -->
<p class="font-semibold">   <!-- 600 -->
<p class="font-bold">       <!-- 700 -->
<p class="font-extrabold">  <!-- 800 -->
<p class="font-black">       <!-- 900 -->
```

### Text Properties

```html
<!-- Text color -->
<p class="text-gray-500">       <!-- gray with shade -->
<p class="text-[#ff0000]">      <!-- arbitrary value -->

<!-- Text alignment -->
<p class="text-left">
<p class="text-center">
<p class="text-right">
<p class="text-justify">

<!-- Decoration -->
<p class="underline">
<p class="overline">
<p class="line-through">
<p class="no-underline">

<!-- Transform -->
<p class="uppercase">
<p class="lowercase">
<p class="capitalize">
<p class="normal-case">

<!-- Letter spacing -->
<p class="tracking-tighter">
<p class="tracking-tight">
<p class="tracking-normal">
<p class="tracking-wide">
<p class="tracking-wider">
<p class="tracking-widest">

<!-- Line height -->
<p class="leading-none">    <!-- 1 -->
<p class="leading-tight">  <!-- 1.25 -->
<p class="leading-normal"> <!-- 1.5 -->
<p class="leading-relaxed"> <!-- 1.625 -->
<p class="leading-loose">  <!-- 2 -->
```

## Colors

### Color Palette

```html
<!-- Gray -->
<div class="bg-gray-50">...</div>
<div class="bg-gray-100">...</div>
<div class="bg-gray-200">...</div>
<!-- ... -->
<div class="bg-gray-900">...</div>

<!-- Blue -->
<div class="text-blue-500">...</div>

<!-- Red, Green, Yellow, Orange, Purple, Pink, Indigo, Teal, Cyan, Emerald, Lime, Fuchsia, Violet, Rose, Sky, Zinc, Neutral, Stone -->
```

### Using Colors

```html
<!-- Background -->
<div class="bg-red-500">Red background</div>

<!-- Text -->
<p class="text-green-600">Green text</p>

<!-- Border -->
<div class="border border-blue-500">Blue border</div>

<!-- Ring (focus) -->
<button class="focus:ring-2 focus:ring-blue-500">Button</button>

<!-- Gradient -->
<div class="bg-gradient-to-r from-blue-500 to-purple-500">
```

## Layout

### Display

```html
<div class="block">...</div>
<div class="inline-block">...</div>
<div class="inline">...</div>
<div class="hidden">...</div>
<div class="flex">...</div>
<div class="inline-flex">...</div>
<div class="grid">...</div>
<div class="inline-grid">...</div>
<div class="table">...</div>
```

### Flexbox

```html
<!-- Container -->
<div class="flex">...</div>
<div class="inline-flex">...</div>
<div class="flex-row">...</div>
<div class="flex-col">...</div>

<!-- Wrap -->
<div class="flex-wrap">...</div>
<div class="flex-nowrap">...</div>
<div class="flex-wrap-reverse">...</div>

<!-- Justify content -->
<div class="justify-start">...</div>
<div class="justify-end">...</div>
<div class="justify-center">...</div>
<div class="justify-between">...</div>
<div class="justify-around">...</div>
<div class="justify-evenly">...</div>

<!-- Align items -->
<div class="items-start">...</div>
<div class="items-end">...</div>
<div class="items-center">...</div>
<div class="items-baseline">...</div>
<div class="items-stretch">...</div>

<!-- Gap -->
<div class="gap-4">...</div>
<div class="gap-x-4">...</div>
<div class="gap-y-4">...</div>
```

### Grid

```html
<!-- Columns -->
<div class="grid grid-cols-1">...</div>
<div class="grid grid-cols-2">...</div>
<div class="grid grid-cols-3">...</div>
<div class="grid grid-cols-4">...</div>
<div class="grid grid-cols-12">...</div>

<!-- Spanning -->
<div class="col-span-2">...</div>
<div class="col-start-2">...</div>
<div class="col-end-4">...</div>

<div class="row-span-2">...</div>
<div class="row-start-1">...</div>
```

### Position

```html
<div class="static">...</div>
<div class="relative">...</div>
<div class="absolute">...</div>
<div class="fixed">...</div>
<div class="sticky">...</div>

<!-- Position values -->
<div class="top-0 right-0 bottom-0 left-0">
<div class="inset-0">
<div class="inset-x-0">
<div class="inset-y-0">
```

## Responsive Design

### Breakpoints

```html
<!-- Mobile first -->
<div class="text-base md:text-lg lg:text-xl">

<!-- Breakpoints:
  sm: 640px
  md: 768px
  lg: 1024px
  xl: 1280px
  2xl: 1536px
-->
```

### Responsive Examples

```html
<!-- Stack on mobile, side-by-side on desktop -->
<div class="flex flex-col md:flex-row">
  <div>Item 1</div>
  <div>Item 2</div>
</div>

<!-- Hide on mobile, show on desktop -->
<div class="hidden md:block">Visible on md+</div>

<!-- Full width mobile, half width desktop -->
<div class="w-full md:w-1/2">
```

## Dark Mode

### Configuration

```javascript
// tailwind.config.js
module.exports = {
  darkMode: 'class', // or 'media' or 'selector'
  // ...
};
```

### Usage

```html
<!-- class mode -->
<div class="dark:bg-gray-900 dark:text-white">

<!-- Toggle with JavaScript -->
<script>
  if (localStorage.theme === 'dark' || 
      (!('theme' in localStorage) && 
       window.matchMedia('(prefers-color-scheme: dark)').matches)) {
    document.documentElement.classList.add('dark')
  } else {
    document.documentElement.classList.remove('dark')
  }
</script>
```

## Borders

### Border Properties

```html
<!-- Width -->
<div class="border">1px</div>
<div class="border-0">0</div>
<div class="border-2">2px</div>
<div class="border-4">4px</div>
<div class="border-8">8px</div>

<!-- Color -->
<div class="border border-gray-300">
<div class="border border-red-500">

<!-- Style -->
<div class="border-solid">
<div class="border-dashed">
<div class="border-dotted">
<div class="border-double">

<!-- Individual sides -->
<div class="border-t-2 border-r-4 border-b border-l">
```

### Border Radius

```html
<div class="rounded">        <!-- default (0.25rem) -->
<div class="rounded-none">   <!-- 0 -->
<div class="rounded-sm">     <!-- 0.125rem -->
<div class="rounded-md">     <!-- 0.375rem -->
<div class="rounded-lg">     <!-- 0.5rem -->
<div class="rounded-xl">     <!-- 0.75rem -->
<div class="rounded-2xl">    <!-- 1rem -->
<div class="rounded-full">   <!-- 9999px (circle) -->

<!-- Specific corners -->
<div class="rounded-t-lg rounded-bl-lg">
```

## Effects

### Shadows

```html
<div class="shadow-sm">   <!-- 0 1px 2px -->
<div class="shadow">      <!-- 0 1px 3px -->
<div class="shadow-md">   <!-- 0 4px 6px -->
<div class="shadow-lg">   <!-- 0 10px 15px -->
<div class="shadow-xl">   <!-- 0 20px 25px -->
<div class="shadow-2xl">  <!-- 0 25px 50px -->
<div class="shadow-inner">
<div class="shadow-none">

<!-- Colored shadow -->
<div class="shadow-blue-500/50">
```

### Opacity

```html
<div class="bg-black opacity-0">0%</div>
<div class="bg-black opacity-5">5%</div>
<div class="bg-black opacity-10">10%</div>
<div class="bg-black opacity-20">20%</div>
<!-- ... -->
<div class="bg-black opacity-95">95%</div>
<div class="bg-black opacity-100">100%</div>
```

### Transitions

```html
<!-- Duration -->
<button class="duration-75">75ms</button>
<button class="duration-100">100ms</button>
<button class="duration-150">150ms</button>
<button class="duration-200">200ms</button>
<button class="duration-300">300ms</button>
<button class="duration-500">500ms</button>
<button class="duration-700">700ms</button>
<button class="duration-1000">1000ms</button>

<!-- Property -->
<button class="transition-none">
<button class="transition-all">
<button class="transition-colors">
<button class="transition-opacity">
<button class="transition-transform">

<!-- Timing -->
<button class="ease-linear">
<button class="ease-in">
<button class="ease-out">
<button class="ease-in-out">
```

## Animations

### Default Animations

```html
<div class="animate-spin">     <!-- rotate 360deg -->
<div class="animate-ping">      <!-- ping effect -->
<div class="animate-pulse">     <!-- pulse opacity -->
<div class="animate-bounce">   <!-- bounce -->
```

### Keyframes (Custom)

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      keyframes: {
        'slide-up': {
          '0%': { transform: 'translateY(100%)' },
          '100%': { transform: 'translateY(0)' },
        },
      },
      animation: {
        'slide-up': 'slide-up 0.5s ease-out',
      },
    },
  },
};
```

### Custom Animation Classes

```html
<div class="animate-slide-up">
<div class="animate-fade-in">
<div class="animate-slide-in-right">
```

## Components

### Button

```html
<button class="px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600 focus:ring-2 focus:ring-blue-300">
  Click me
</button>

<!-- Variants -->
<button class="px-4 py-2 bg-gray-200 text-gray-800 rounded hover:bg-gray-300">Gray</button>
<button class="px-4 py-2 bg-red-500 text-white rounded hover:bg-red-600">Red</button>
<button class="px-4 py-2 border border-gray-300 rounded hover:bg-gray-50">Outline</button>
<button class="px-4 py-2 text-blue-500 hover:underline">Link</button>
```

### Card

```html
<div class="bg-white rounded-lg shadow-md p-6">
  <h2 class="text-xl font-bold mb-2">Card Title</h2>
  <p class="text-gray-600">Card content here.</p>
</div>
```

### Input

```html
<input 
  type="text" 
  class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500 outline-none"
  placeholder="Enter text..."
>
```

### Badge

```html
<span class="px-2 py-1 text-xs font-semibold bg-blue-100 text-blue-800 rounded-full">
  Badge
</span>
```

## State Variants

### Hover

```html
<button class="hover:bg-blue-600 hover:text-white">
```

### Focus

```html
<button class="focus:ring-2 focus:ring-blue-500 focus:outline-none">
```

### Active

```html
<button class="active:bg-blue-700">
```

### Group Hover

```html
<div class="group hover:bg-blue-500">
  <p class="group-hover:text-white">Text changes on group hover</p>
</div>
```

### Peer

```html
<!-- Show element when checkbox is checked -->
<input type="checkbox" class="peer sr-only">
<div class="hidden peer-checked:block">
  Shown when checked
</div>
```

### Dark Mode Variants

```html
<div class="dark:bg-gray-900 dark:text-white">
```

## Arbitrary Values

### Quick Custom Styles

```html
<!-- Arbitrary values with square brackets -->
<div class="w-[300px]">Custom width</div>
<div class="h-[50vh]">Custom height</div>
<div class="bg-[#ff0000]">Custom color</div>
<div class="text-[14px]">Custom font size</div>
<div class="leading-[1.5]">Custom line height</div>
<div class="z-[100]">Custom z-index</div>
<div class="top-[calc(100%+20px)]">Calc value -->

<!-- Arbitrary properties -->
<div class="[aspect-ratio:16/9]">
<div class="[-webkit-line-clamp:3]">
```

## Customization

### Extending Theme

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        brand: {
          50: '#f0f9ff',
          500: '#0ea5e9',
          900: '#0c4a6e',
        },
      },
      fontFamily: {
        display: ['Inter', 'sans-serif'],
        body: ['Roboto', 'sans-serif'],
      },
      spacing: {
        '18': '4.5rem',
        '88': '22rem',
      },
      borderRadius: {
        'xl': '1rem',
      },
      boxShadow: {
        'soft': '0 2px 15px -3px rgba(0, 0, 0, 0.1)',
        'glow': '0 0 20px rgba(59, 130, 246, 0.5)',
      },
    },
  },
};
```

### Using in Components

```tsx
// Using theme values
<div className="bg-brand-500 text-brand-900">
<div className="font-display">
<div className="p-18">
<div className="rounded-xl">
<div className="shadow-glow">
```

## Best Practices

### Organization

```html
<!-- Logical order: layout > spacing > sizing > visual > states > responsive -->
<div className="flex items-center justify-between p-4 bg-white rounded-lg shadow hover:shadow-lg md:p-6">
```

### Extracting Components

```tsx
// Instead of repeating
// Create a reusable component

function Button({ children, variant = 'primary' }) {
  const base = 'px-4 py-2 rounded font-medium transition-colors';
  const variants = {
    primary: 'bg-blue-500 text-white hover:bg-blue-600',
    secondary: 'bg-gray-200 text-gray-800 hover:bg-gray-300',
  };
  
  return (
    <button className={`${base} ${variants[variant]}`}>
      {children}
    </button>
  );
}
```

### Performance

```html
<!-- Use specific classes -->
<div class="grid grid-cols-3 gap-4"> <!-- Good -->

<!-- Avoid -->
<div class="flex flex-wrap justify-between"> <!-- Less optimal for grids -->
```

## Troubleshooting

### Not Applying Styles

1. Check content paths in `tailwind.config.js`
2. Ensure `@tailwind` directives in CSS
3. Run build: `npm run build`

### JIT Not Working

```javascript
// Ensure mode is JIT
module.exports = {
  // ...
  mode: 'jit', // Usually automatic in v3+
};
```

### Purge Issues

```javascript
// In production, ensure all template files are in content
module.exports = {
  content: [
    './src/**/*.{js,ts,jsx,tsx}',
    './pages/**/*.{js,ts,jsx,tsx}',
    './components/**/*.{js,ts,jsx,tsx}',
  ],
};
```

## Resources

- [Tailwind CSS Docs](https://tailwindcss.com/docs)
- [Tailwind Play](https://play.tailwindcss.com)
- [Tailwind UI](https://tailwindui.com)
- [Headless UI](https://headlessui.com)
