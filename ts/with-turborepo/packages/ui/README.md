# @repo/ui

Shared UI components with shadcn/ui support.

## Installation

```json
{
  "dependencies": {
    "@repo/ui": "workspace:*"
  }
}
```

## Usage

### Main entry imports

```tsx
import { Header, Counter } from "@repo/ui";
```

### Subpath imports

```tsx
import { Header } from "@repo/ui/header";
import { Button } from "@repo/ui/components/ui/button";
import { cn } from "@repo/ui/lib/utils";
```

## Adding shadcn/ui components

1. Follow the [shadcn/ui manual installation guide](https://ui.shadcn.com/docs/installation/manual)
2. Add components to `src/components/ui/`
3. Styles are configured in `packages/tailwind-config/shared-styles.css`
