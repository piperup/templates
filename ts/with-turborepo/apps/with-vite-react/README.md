# with-vite-react

A Vite + React + TypeScript application configured with Turborepo monorepo tooling.

## What's inside

This app is configured with:

- **React 19** with TypeScript
- **Vite** for fast development and building
- **Tailwind CSS** with shared configuration from `@repo/tailwind-config`
- **shadcn/ui** components from `@repo/ui`
- **ESLint** with React configuration from `@repo/eslint-config`
- **TypeScript** configuration from `@repo/typescript-config`

## Development

### Install dependencies

From the root of the monorepo:

```sh
pnpm install
```

### Run the development server

```sh
pnpm dev
```

The app will be available at `http://localhost:5173`

### Build for production

```sh
pnpm build
```

### Preview production build

```sh
pnpm preview
```

## Using monorepo packages

### Importing UI components

Import components from the shared UI package:

```tsx
import { Header, Counter } from "@repo/ui";
import { Button } from "@repo/ui/components/ui/button";

export default function App() {
  return (
    <div>
      <Header />
      <Counter />
      <Button>Click me</Button>
    </div>
  );
}
```

### Using shared styles

The app imports shared Tailwind CSS configuration in `src/style.css`:

```css
@import "tailwindcss";
@import "@repo/tailwind-config";
@source "../../../packages/ui/src/**/*.{ts,tsx}";
```

### TypeScript configuration

The app extends the shared Vite TypeScript configuration:

```json
{
  "extends": "@repo/typescript-config/vite.json"
}
```

### ESLint configuration

The app uses the shared React ESLint configuration:

```js
import reactConfig from "@repo/eslint-config/react-internal";

export default reactConfig;
```

## Resources

- [Vite Documentation](https://vitejs.dev)
- [React Documentation](https://react.dev)
- [Turborepo Documentation](https://turbo.build/repo)
