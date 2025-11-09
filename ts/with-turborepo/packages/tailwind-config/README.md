# @repo/tailwind-config

This package contains shared Tailwind CSS configuration and styles used across the monorepo.

What's inside

- `shared-styles.css` — a small CSS file intended to include your Tailwind directives and any global utilities used by multiple packages/apps.

How to use

1. Create the shared style sheet `src/style.css`

```css
@import "tailwindcss";
@import "@repo/tailwind-config";
@source "../../../packages/ui/src/**/*.{ts,tsx}";
```

2. In your app entry (for example `src/main.tsx` in the app), import

```tsx
import "./style.css"
```
