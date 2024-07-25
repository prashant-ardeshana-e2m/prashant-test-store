## How to Set Up Shopify Vite with Tailwind CSS

Follow these steps to set up Shopify with Vite and Tailwind CSS for a modern development workflow.

### Step 1: Clone the Dawn Repository

First, clone the Dawn theme repository from Shopify using the following command:

```bash
git clone https://github.com/Shopify/dawn
```

### Step 2: Check Software Versions

Ensure you have the required software versions by checking:

```bash
npm -v
node -v
shopify version
```

### Step 3: Install Tailwind CSS and PostCSS

Install Vite, Tailwind CSS, and PostCSS using the following command:

```bash
npm install vite tailwindcss postcss autoprefixer --save-dev
```

Additionally, install `npm-run-all` to manage multiple npm scripts concurrently:

```bash
npm install npm-run-all --save-dev
```

You can also use a combined installation command:

```bash
npm install autoprefixer npm-run-all postcss tailwindcss vite vite-plugin-shopify --save-dev
```

### Step 4: Create Frontend Entry Points

Create the `frontend/entrypoints` folder and add two files: `main.css` and `main.js`.

#### **main.css**

Add the following code:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

#### **main.js**

Add the following code:

```javascript
import 'vite/modulepreload-polyfill';
```

### Step 5: Create Configuration Files

In the root directory, create the following files using these commands:

```bash
touch tailwind.config.cjs
touch postcss.config.cjs
touch vite.config.js
touch .shopifyignore
touch jsconfig.json
```

### Step 6: Configure Tailwind

Add the following code to `tailwind.config.cjs`:

```javascript
/** @type {import('tailwindcss').Config} */

let plugin = require('tailwindcss/plugin');

module.exports = {
  content: ['./**/*.liquid', './frontend/**/*.{js,ts,jsx,tsx}'],
  safelist: [],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

### Step 7: Update .shopifyignore

Add the following entries to `.shopifyignore`:

```
package.json
jsconfig.json
package-lock.json
frontend/
vite.config.js
tailwind.config.cjs
postcss.config.cjs
.gitignore
.prettierignore
.prettierrc.json
.theme-check.yml
.vscode/
*.md
translation.yml
node_modules
.git/
.github/
```

### Step 8: Update .gitignore

Add the following entries to `.gitignore`:

```
node_modules
.ruby-version
```

### Step 9: Configure PostCSS

Add the following code to `postcss.config.cjs`:

```javascript
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};
```

### Step 10: Configure Vite

Add the following code to `vite.config.js`:

```javascript
// vite.config.js
import { defineConfig } from 'vite';
import shopify from 'vite-plugin-shopify';

export default defineConfig({
  plugins: [shopify()],
  build: {
    emptyOutDir: false,
  },
});
```

### Step 11: Update package.json

Add or modify the following code in `package.json`:

```json
"name": "BFT",
"version": "0.1.0",
"license": "MIT",
"keywords": [],
"type": "module",
"scripts": {
  "dev": "run-p -sr \"shopify:dev -- {@}\" \"vite:dev\" --",
  "deploy": "run-s \"vite:build\" \"shopify:push -- {@}\" --",
  "shopify:dev": "shopify theme dev",
  "shopify:push": "shopify theme push",
  "vite:dev": "vite",
  "vite:build": "vite build"
},
```

### Step 12: Configure JavaScript Paths

Add the following code to `jsconfig.json`:

```json
{
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["frontend/*"],
      "~/*": ["frontend/*"]
    }
  }
}
```

### Step 13: Update Liquid Templates

Add the following snippet before the `content_for_header` in your Liquid templates:

```liquid
{%- liquid
      render 'vite-tag' with 'main.css'
      render 'vite-tag' with 'main.js'
    -%}
```

### Step 14: Run Development Server

Install dependencies and start the development server with hot-reload:

```bash
npm install
npm run dev -- --store store-name --live-reload hot-reload
```

### Step 15: Deploy to Shopify

Deploy your theme to Shopify:

```bash
npm run deploy -- --store store-name
```

### Step 16: Target a Specific Theme by ID

To target a specific theme by its ID during deployment, use the following command:

```bash
npm run deploy -- --store store-name -t138234462371
```

---

### Summary

This guide covers the necessary steps to set up a Shopify theme using Vite and Tailwind CSS. By following these instructions, you'll benefit from a modern development workflow with faster builds, live reloading, and an improved developer experience.

**Key Points:**
- Clone the Shopify Dawn theme.
- Check necessary software versions.
- Install Vite, Tailwind CSS, and related packages.
- Configure the project with essential files and settings.
- Set up scripts for development and deployment.
- Ensure your Shopify theme is linked with Vite for better performance.

By implementing these steps, you'll be ready to develop and deploy a Shopify theme with Vite and Tailwind CSS efficiently.
