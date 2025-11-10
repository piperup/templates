# Copilot Instructions for piper-templates

## Repository Overview

This is a **template collection** repository containing reusable project scaffolds, AI prompts, and GitHub/VS Code automation. Not a single application—each directory is an independent, copy-paste starting point.

**Structure:**

- `ts/with-turborepo/` - Complete Turborepo monorepo template (Vite + React 19 + TypeScript + shadcn/ui)
- `.github/` - GitHub issue/PR templates (auto-populate forms)
- `.vscode/` - VS Code snippets and settings

## Turborepo Monorepo Architecture

### Package Manager & Workspace

- **pnpm** v8.15.6 with workspaces (`pnpm-workspace.yaml` defines `apps/*` and `packages/*`)
- All internal packages use `workspace:*` protocol for dependencies
- Turborepo v2.6.0 orchestrates tasks with caching (see `turbo.json`)

### Monorepo Structure

```
ts/with-turborepo/
├── apps/with-vite-react/      # React 19 + Vite app (consumes shared packages)
└── packages/
    ├── ui/                     # Shared React components (shadcn/ui + custom)
    ├── eslint-config/          # ESLint v9 flat configs
    ├── typescript-config/      # TypeScript configs (base, react-library, vite)
    └── tailwind-config/        # Tailwind v4 + shadcn design tokens
```

### Critical Workflows

**Build:**

```bash
pnpm build  # Runs `turbo run build` - respects ^build dependencies
```

- Turborepo executes packages in topological order
- Outputs: `dist/**` (configured in `turbo.json`)
- Apps typecheck + build (e.g., `tsc && vite build`)

**Dev:**

```bash
pnpm dev    # Starts all dev servers (persistent, no cache)
```

- Apps run on Vite dev server (`--clearScreen false` to reduce noise)
- Changes to `@repo/*` packages hot-reload via Vite's HMR

**Lint/Typecheck:**

```bash
pnpm lint       # ESLint v9 flat config across workspace
pnpm typecheck  # TypeScript with project references
```

### Shared Package Conventions

#### `@repo/ui` - Component Library

- **Exports:** Granular subpath exports (`package.json` exports field)
  - Main: `import { Header, Counter } from "@repo/ui"`
  - Subpath: `import { Button } from "@repo/ui/components/ui/button"`
- **shadcn/ui integration:** Components in `src/components/ui/` follow manual installation pattern
- **Styling:** Uses `cn()` utility (`@repo/ui/lib/utils`) for conditional classes (clsx + tailwind-merge)

#### `@repo/eslint-config` - ESLint v9 Flat Configs

- **Key pattern:** Export composable config arrays from `.js` files
  - `base.js` - TypeScript + Prettier + turbo plugin
  - `react-internal.js` - Adds React/React Hooks rules
- **Usage:** `import baseConfig from "@repo/eslint-config/base"` then spread in `eslint.config.js`
- **Plugin:** `eslint-plugin-turbo` enforces undeclared env vars

#### `@repo/typescript-config` - TypeScript Presets

- **Strict by default:** `strict: true`, ESNext modules, Bundler resolution
- **Configs:**
  - `base.json` - Core strict settings
  - `react-library.json` - Extends base + `jsx: "react-jsx"`
  - `vite.json` - Extends base + DOM types, `noEmit: true`
- **Usage:** `"extends": "@repo/typescript-config/vite.json"` in app `tsconfig.json`

#### `@repo/tailwind-config` - Design System

- **Tailwind v4** with `@tailwindcss/vite` plugin
- **Critical pattern:** Apps import `shared-styles.css` which defines:
  - CSS custom properties for shadcn/ui tokens (light/dark themes via OKLCH)
  - `@source` directive pointing to `../../../packages/ui/src/**/*.{ts,tsx}` for cross-package class scanning
- **Dark mode:** Custom variant `@custom-variant dark (&:is(.dark *))` in CSS

### Adding New Components

**shadcn/ui components:**

1. Add to `packages/ui/src/components/ui/` (manual installation, no CLI)
2. Import primitives (@radix-ui) + `class-variance-authority` for variants
3. Use `cn()` utility for conditional classes
4. Export via `packages/ui/src/components/index.ts` or subpath
5. Styles auto-scanned via `@source` in consuming apps' CSS

**Custom components:**

- Use React 19 patterns (no legacy FC types, prefer `React.ComponentProps<typeof X>`)
- Example: `Counter` wraps `Button` with state (`useState`)

### Configuration Conventions

**ESLint (v9 flat config):**

- Root `eslint.config.js` imports shared config and exports directly
- Ignores: `dist/**` in all packages

**TypeScript:**

- Project references NOT used (Turborepo handles build order)
- `include: ["src"]` in most packages
- `noEmit: true` in apps (Vite handles bundling)

**Vite:**

- React plugin + Tailwind v4 Vite plugin
- Imports `style.css` from `src/main.tsx` (contains `@import "@repo/tailwind-config"`)

## AI Prompt Templates (Manual Use)

Located in `ai/github/templates/` - these are NOT automated. Copy, fill placeholders (`<language>`, `<files>`), paste into AI tools:

- `pull_request_prompt.md` - Generate PR descriptions
- `code_review_prompt.md` - AI-assisted reviews
- `refactor_prompt.md` - Refactoring requests
- `test_generation_prompt.md` - Generate tests

## Key Decision Rationale

1. **ESLint v9 flat config:** Modern approach, no cascading `.eslintrc` files
2. **Tailwind v4:** Uses native CSS layers, no PostCSS config needed
3. **pnpm workspaces:** Fast, efficient with Turborepo
4. **Subpath exports:** Granular imports reduce bundle size (tree-shaking friendly)
5. **OKLCH color space:** Better perceptual uniformity for design tokens
6. **React 19:** Early adoption for testing new features

## Common Pitfalls

- **Tailwind scanning:** Apps must adjust `@source` path in CSS based on monorepo depth (e.g., `../../../packages/ui/src/**`)
- **ESLint imports:** Use `workspace:*` protocol, not relative paths, for shared configs
- **Turborepo caching:** `dev` task has `cache: false` and `persistent: true` - don't cache long-running servers
- **TypeScript paths:** No path aliases configured - rely on package names (`@repo/ui`)

## License & Attribution

MIT License - templates meant for copy/modification. Based on Turborepo community example `with-vite-react` v2.6.0.
