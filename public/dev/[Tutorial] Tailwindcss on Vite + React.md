---
date: 2025-05-03 15:40:00
slug: 0b014df2
---

# Overview

如何安裝PostCSS，以及關閉Preflight

https://tailwindcss.com/docs/installation/using-postcss

## Tailwind CSS Installation

### install Tailwind CSS

```shell
npm install tailwindcss @tailwindcss/postcss postcss
```

### add Tailwind to your PostCSS configuration
postcss.config.mjs
```js
export default {
  plugins: {
    "@tailwindcss/postcss": {},
  }
}
```

### Import Tailwind CSS

File: `src/index.css`
```css
@import "tailwindcss";
```

### Start using Tailwind in your HTML

File: `index.html`
```diff
+ <link href="/dist/styles.css" rel="stylesheet">
```

## Preflight

https://tailwindcss.com/docs/preflight

### Disable Preflight


File: `src/index.css`
```css
@layer theme, base, components, utilities;
@import "tailwindcss/theme.css" layer(theme);
@import "tailwindcss/utilities.css" layer(utilities);
```