---
name: postcss
description: Expert guidance for using PostCSS - a tool for transforming CSS with JavaScript plugins, including autoprefixer, nesting, Tailwind, and custom transformations.
allowed-tools:
  - "Read"
  - "Write"
  - "Bash"
  - "glob"
  - "grep_search"
  - "web_fetch"
---

# PostCSS

You are a CSS tooling expert specialized in PostCSS—a JavaScript tool for transforming CSS with plugins for vendor prefixing, nesting, linting, and more.

## Core Concepts

### What is PostCSS?

- **CSS Processor**: Transforms CSS with JavaScript
- **Plugin-Based**: Modular plugins for different tasks
- **Fast**: Written in JavaScript, no native deps
- **Extensible**: Write custom plugins

### Common Workflow

```
CSS → [PostCSS Plugins] → Transformed CSS
```

## Installation

### Basic Setup

```bash
# Install PostCSS CLI
npm install -D postcss postcss-cli

# Or with all common plugins
npm install -D postcss postcss-cli autoprefixer postcss-nesting postcss-custom-properties
```

### With Framework

```bash
# Next.js (includes PostCSS)
# Already configured in create-next-app

# Vite
npm install -D postcss autoprefixer

# Rollup
npm install -D rollup-plugin-postcss
```

## Configuration

### postcss.config.js

```javascript
module.exports = {
  plugins: [
    require('autoprefixer'),
    require('postcss-nesting'),
    require('cssnano')({
      preset: 'default',
    }),
  ],
};
```

### With Different Environments

```javascript
// postcss.config.js
module.exports = (ctx) => ({
  plugins: [
    require('autoprefixer'),
    ctx.env === 'production' && require('cssnano')({ preset: 'default' }),
  ].filter(Boolean),
});
```

### package.json Scripts

```json
{
  "scripts": {
    "build:css": "postcss src/styles.css -o dist/styles.css",
    "watch:css": "postcss src/styles.css -o dist/styles.css -w",
    "build:all": "npm run build:css && npm run build:js"
  }
}
```

## Popular Plugins

### Autoprefixer

Adds vendor prefixes automatically:

```javascript
// postcss.config.js
module.exports = {
  plugins: {
    autoprefixer: {},
  },
};
```

```css
/* Input */
.container {
  display: flex;
  user-select: none;
}

/* Output */
.container {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
```

### PostCSS Nesting

Enables nested CSS rules:

```css
/* Input */
.card {
  background: white;
  
  &:hover {
    background: gray;
  }
  
  & .title {
    font-size: 1.5rem;
    
    &:hover {
      color: blue;
    }
  }
}

/* Output */
.card {
  background: white;
}

.card:hover {
  background: gray;
}

.card .title {
  font-size: 1.5rem;
}

.card .title:hover {
  color: blue;
}
```

### PostCSS Preset Env

Transforms modern CSS for older browsers:

```javascript
// postcss.config.js
module.exports = {
  plugins: {
    'postcss-preset-env': {
      stage: 3,
      features: {
        'nesting-rules': true,
        'custom-properties': false,
      },
    },
  },
};
```

Features:
- Custom selectors
- custom-properties
- environment-variables
- focus-visible
- focus-within
- initial
- inset
- logical-properties
- matches-pseudo-class
- not-pseudo-class
- nth-child-pseudo
- optional-pseudo
- overflow-property
- placeholder
- place-properties
- prefers-color-scheme
- pseudo-elements
- read-only-pseudo
- relative-color-syntax
- shadow
- string-not
- trigonometric-functions

### PostCSS Custom Properties

Enables CSS variables:

```css
/* Input */
:root {
  --color-primary: #0066ff;
}

.container {
  color: var(--color-primary);
}

/* Output */
.container {
  color: #0066ff;
  color: var(--color-primary);
}
```

### PostCSS Modules

```javascript
// postcss.config.js
module.exports = {
  modules: {
    generateScopedName: '[name]__[local]',
  },
  plugins: {
    'postcss-modules': {},
  },
};
```

```css
/* component.css */
.title {
  font-size: 2rem;
}
```

```javascript
// Component.jsx
import styles from './component.css';

export function Title() {
  return <h1 className={styles.title}>Hello</h1>;
}
```

### CSSNano

Minifies CSS for production:

```javascript
// postcss.config.js
module.exports = {
  plugins: {
    cssnano: {
      preset: 'default',
      // Or 'advanced' for more aggressive minification
    },
  },
};
```

Presets:
- `default`: Safe optimizations
- `advanced`: Aggressive (may break some CSS)

Options:
```javascript
cssnano: {
  preset: ['default', {
    discardComments: { removeAll: true },
    normalizeWhitespace: true,
    minifyFontValues: true,
    minifyGradients: true,
  }],
}
```

### StyleLint

Lints CSS for errors:

```javascript
// postcss.config.js
module.exports = {
  plugins: {
    stylelint: {
      rules: {
        'color-no-invalid-hex': true,
        'declaration-block-no-duplicate-properties': true,
      },
    },
  },
};
```

## CSS-in-JS Integration

### Styled Components

```javascript
// postcss.config.js
module.exports = {
  plugins: [
    'postcss-styled-syntax',
  ],
};
```

### Emotion

```javascript
// postcss.config.js
module.exports = {
  plugins: [
    '@emotion/postcss-styled',
  ],
};
```

## Advanced Usage

### Multiple Config Files

```bash
# Use specific config
postcss src/app.css -c postcss.app.config.js
postcss src/admin.css -c postcss.admin.config.js
```

### CLI Options

```bash
# Watch mode
postcss src/app.css -o dist/app.css -w

# Source maps
postcss src/app.css -o dist/app.css --map

# Glob
postcss 'src/**/*.css' -d dist

# Using config
postcss src/app.css -o dist/app.css -c postcss.config.js
```

### Programmatic Usage

```javascript
import postcss from 'postcss';
import autoprefixer from 'autoprefixer';
import nesting from 'postcss-nesting';

const css = `
.card {
  &:hover {
    background: blue;
  }
}
`;

const result = await postcss([autoprefixer, nesting]).process(css, {
  from: 'input.css',
  to: 'output.css',
});

console.log(result.css);
```

## Writing Custom Plugins

### Simple Plugin

```javascript
// my-plugin.js
module.exports = (opts = {}) => {
  return {
    postcssPlugin: 'my-custom-plugin',
    Declaration(decl) {
      if (decl.prop === 'font-size') {
        decl.value = decl.value.replace(/(\d+)px/, (_, num) => `${num / 16}rem`);
      }
    },
  };
};
```

```javascript
// postcss.config.js
module.exports = {
  plugins: {
    './my-plugin.js': { option: 'value' },
  },
};
```

### Complex Plugin

```javascript
module.exports = (opts = {}) => {
  return {
    postcssPlugin: 'my-plugin',
    
    // Run once at start
    Once(root, { result }) {
      // Process root
    },
    
    // For each rule
    Rule(rule, { result }) {
      // Process rule
    },
    
    // For each declaration
    Declaration(decl, { result }) {
      // Process declaration
    },
    
    // For each at-rule
    AtRule(atRule, { result }) {
      // Process at-rule
    },
  };
};
```

## Tailwind Integration

### With Tailwind

PostCSS is built into Tailwind:

```javascript
// postcss.config.js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};
```

### Custom Tailwind Config

```javascript
// tailwind.config.js
module.exports = {
  content: ['./src/**/*.{html,js,jsx,ts,tsx}'],
  theme: {
    extend: {
      colors: {
        brand: '#0066ff',
      },
    },
  },
  plugins: [],
};
```

```css
/* styles.css */
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer components {
  .btn-primary {
    @apply bg-brand text-white px-4 py-2 rounded;
  }
}
```

## Performance Tips

### Speed Up Builds

```javascript
// postcss.config.js
module.exports = {
  fast: {
    // Cache results
    log: function() {
      console.log.apply(console, arguments);
    },
  },
  plugins: [
    // Order matters - put fastest first
    autoprefixer,
    postcss-nesting,
    // Processing last
    require('cssnano')({
      preset: 'default',
    }),
  ].filter(Boolean),
};
```

### Parallel Processing

```javascript
// For large projects, use postcss-load-config with async
module.exports = async () => ({
  plugins: [
    await import('autoprefixer'),
    await import('postcss-nesting'),
  ],
});
```

## Troubleshooting

### Plugin Not Found

```bash
# Install missing plugin
npm install -D postcss-plugin-name
```

### Config Not Loading

- Ensure file is named `postcss.config.js`
- Check file is in project root
- Try specifying config path explicitly

### Source Maps Not Working

```bash
# CLI
postcss src.css -o dist.css --map

# Config
module.exports = {
  map: true,
  plugins: [/* plugins */],
};
```

## Common Configurations

### Production Build

```javascript
// postcss.config.js
module.exports = {
  plugins: [
    require('tailwindcss'),
    require('autoprefixer'),
    require('cssnano')({
      preset: 'default',
    }),
  ],
};
```

### Development

```javascript
// postcss.config.js
module.exports = {
  plugins: [
    require('tailwindcss'),
    require('autoprefixer'),
  ],
};
```

### With PostCSS Nesting

```javascript
// postcss.config.js
module.exports = {
  plugins: [
    require('postcss-nesting'),
    require('postcss-preset-env')({
      stage: 3,
    }),
    require('autoprefixer'),
  ],
};
```

## Resources

- [PostCSS Documentation](https://postcss.org)
- [PostCSS GitHub](https://github.com/postcss/postcss)
- [Autoprefixer](https://github.com/postcss/autoprefixer)
- [PostCSS Nesting](https://github.com/csstools/postcss-nesting)
- [CSSNano](https://cssnano.co)
- [PostCSS Preset Env](https://preset-env.cssdb.org)
