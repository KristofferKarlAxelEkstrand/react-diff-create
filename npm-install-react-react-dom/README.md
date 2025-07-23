# React Project Manually setup

A React application built with Webpack and Babel.

## Getting Started

### Prerequisites

- Node.js (version 14 or higher)
- npm or yarn

### Installation

1. Install dependencies:
   ```bash
   npm install
   ```

### Available Scripts

- `npm start` - Runs the app in development mode with webpack dev server
- `npm run dev` - Same as start but opens browser automatically
- `npm run build` - Builds the app for production
- `npm run build:dev` - Builds the app in development mode
- `npm test` - Runs tests (currently not configured)

### Development

1. Start the development server:

   ```bash
   npm start
   ```

2. Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

3. The page will reload if you make edits.

### Project Structure

```
├── public/
│   └── index.html          # HTML template
├── src/
│   ├── App.js              # Main App component
│   ├── App.css             # App component styles
│   ├── index.js            # Application entry point
│   └── index.css           # Global styles
├── webpack.config.js       # Webpack configuration
├── babel.config.js         # Babel configuration
└── package.json           # Project dependencies and scripts
```

### Build

To create a production build:

```bash
npm run build
```

This will create a `dist` folder with the optimized production build.

## Package.json Type Field: CommonJS vs ES Modules

### Understanding the `"type"` Field

The `"type"` field in `package.json` determines how Node.js interprets JavaScript files in your
project:

#### When to Use `"type": "commonjs"` (or omit the field)

- **Default behavior** - If you omit the `"type"` field, Node.js assumes CommonJS
- **Legacy projects** using `require()` and `module.exports`
- **Node.js backend projects** that haven't migrated to ES modules
- **Libraries** that need to support older Node.js versions

```javascript
// CommonJS syntax
const React = require('react');
const { createRoot } = require('react-dom/client');

module.exports = MyComponent;
```

#### When to Use `"type": "module"`

- **Modern projects** using ES6 `import`/`export` syntax
- **Pure ES module projects** without build tools
- **Node.js applications** targeting newer Node.js versions (14+)
- **When you want Node.js to natively handle ES modules**

```javascript
// ES Module syntax
import React from 'react';
import { createRoot } from 'react-dom/client';

export default MyComponent;
```

### Our Project Configuration

This React project **omits** the `"type"` field (defaulting to CommonJS for Node.js), but uses:

- **ES6 modules** (`import`/`export`) in source code
- **Webpack + Babel** to transform and bundle the code
- **Babel preset-env** with `modules: false` to let Webpack handle module bundling

#### Why This Works

1. **Webpack** handles the module bundling, not Node.js directly
2. **Babel** transforms JSX and modern JavaScript but leaves modules for Webpack
3. **Source code** uses modern ES6 syntax for better developer experience
4. **Build output** is compatible with browsers

#### Common Issue

If you set `"type": "commonjs"` and use ES6 imports, you'll get this error:

```
Module parse failed: 'import' and 'export' may appear only with 'sourceType: module'
```

**Solution**: Remove the `"type": "commonjs"` field or use `"type": "module"` when using ES6 syntax
with build tools.

### Best Practices

- **Frontend projects with bundlers**: Omit `"type"` field or use `"type": "module"`
- **Backend Node.js projects**: Use `"type": "module"` for modern syntax, `"type": "commonjs"` for
  legacy
- **Libraries**: Consider dual publishing or stick with CommonJS for broader compatibility
- **Gradual migration**: You can use both by naming files `.mjs` (ES modules) or `.cjs` (CommonJS)

## Technologies Used

- React 19
- Webpack 5
- Babel
- CSS Loader
- Style Loader
- HTML Webpack Plugin
