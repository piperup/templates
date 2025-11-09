# @repo/ui — UI components

This package exports shared UI components used by the example app.

What this package provides

- A place to add shadcn/ui components and shared UI primitives.

Using `shadcn/ui`

This monorepo doesn't automatically scaffold shadcn components for you. To add shadcn/ui components into this package:

1. Follow the shadcn manual installation guide: [Manual Installation](https://ui.shadcn.com/docs/installation/manual)
2. Add any generated/global styles into the shared Tailwind CSS file at `packages/tailwind-config/shared-styles.css`.
3. Ensure `packages/ui` can resolve the shared styles and aliases:
   - Add `baseUrl`/`paths` to `packages/ui/tsconfig.json` if needed.
   - Use the alias `@repo/ui` in consuming apps (this repo already wires the package with workspaces).

Example usage in an app:

```tsx
import React from "react";
import { Header } from "@repo/ui";

export default function Page() {
  return (
    <div>
      <Header />
    </div>
  );
}
```
