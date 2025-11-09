# @repo/tailwind-config

Shared Tailwind CSS configuration with shadcn/ui styles and design tokens.

## Installation

```json
{
  "dependencies": {
    "@repo/tailwind-config": "workspace:*"
  }
}
```

Then follow the [Tailwind CSS Vite guide](https://tailwindcss.com/docs/guides/vite) to install Tailwind in your app.

## Usage

Create `src/style.css`:

```css
@import "tailwindcss";
@import "@repo/tailwind-config";
@source "../../../packages/ui/src/**/*.{ts,tsx}";
```

Import in `src/main.tsx`:

```tsx
import "./style.css";
```

> **Note:** Adjust the `@source` path based on your app's location in the monorepo.
