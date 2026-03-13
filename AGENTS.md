# agents.md — SvelteKit + shadcn-svelte Project

## Project Configuration

- **Language**: TypeScript (strict mode)
- **Package Manager**: npm
- **Framework**: SvelteKit (Svelte 5 with runes)
- **Adapter**: `@sveltejs/adapter-static` — **fully static output, NO server-side code**
- **UI Library**: shadcn-svelte (Bits UI primitives + Tailwind CSS v4)
- **Add-ons**: tailwindcss, adapter-static, mdsvex, mcp, better-auth

### ⚠️ Static Adapter Constraints (Critical)

This project uses `adapter-static`. There is **no Node.js server at runtime**. These rules are absolute:

- **No `+server.ts` / API routes** — all data must come from external APIs called client-side
- **No `+page.server.ts` / server load functions** — use `+page.ts` with `ssr: false` or client-side `$effect`
- **No `$env/static/private`** — only `$env/static/public` (PUBLIC_ prefix) is allowed
- **All API calls are made from the browser** — fetch runs in the client, not on a server
- **Form actions do not work** — use client-side form handling (superforms with client adapter)
- Set `export const prerender = true` and `export const ssr = false` in layouts/pages as needed

```typescript
// src/routes/+layout.ts — required for static adapter
export const prerender = true;
export const ssr = false;
```

---

## Project Structure

```
.kiro/
├── skills/
│   ├── frontend-design/         # UI/component design skill
│   ├── seo-audit/               # SEO optimization skill
│   ├── tailwind-design-system/  # Design tokens & theming skill
│   └── web-design-guidelines/   # Accessibility & UX skill
docs/
├── api-backend-docs/            # Backend API endpoint documentation
│   └── *.md                     # Endpoint specs — read before any API call to backend
└── api-relayer-docs/            # External Relayer service API documentation
    └── *.md                     # Endpoint specs — read before any call to relayer
src/
├── lib/
│   ├── components/
│   │   ├── ui/                  # shadcn-svelte components (auto-generated via CLI)
│   │   │   ├── button/
│   │   │   │   ├── index.ts
│   │   │   │   └── button.svelte
│   │   │   ├── card/
│   │   │   ├── dialog/
│   │   │   ├── form/
│   │   │   └── ...
│   │   └── custom/              # Your composite components (use ui/ internally)
│   │       ├── Header.svelte
│   │       ├── Sidebar.svelte
│   │       └── ...
│   ├── hooks/                   # Svelte hooks (use-* pattern)
│   │   └── use-media-query.svelte.ts
│   ├── api/                     # API client modules (all client-side fetch)
│   │   ├── backend.ts           # Calls to api-backend — follow docs/api-backend-docs/
│   │   └── relayer.ts           # Calls to api-relayer — follow docs/api-relayer-docs/
│   ├── utils/                   # Utility functions
│   │   ├── cn.ts                # clsx + tailwind-merge (required by shadcn-svelte)
│   │   └── format.ts
│   ├── stores/                  # Global Svelte 5 $state stores
│   ├── types/                   # Shared TypeScript interfaces
│   └── auth-client.ts           # better-auth client setup
├── routes/
│   ├── +layout.ts               # prerender=true, ssr=false — DO NOT REMOVE
│   ├── +layout.svelte           # Root layout — Toaster/Sonner goes here
│   ├── +page.svelte
│   └── (app)/                   # Authenticated route group
│       ├── +layout.svelte
│       └── dashboard/
│           └── +page.svelte
├── app.css                      # Global CSS — shadcn-svelte CSS vars live here
├── app.d.ts                     # Type declarations
└── app.html
svelte.config.js                 # adapter-static configured here
```

### Key Rules for This Structure

- **Never** manually edit files inside `$lib/components/ui/` — use the CLI or copy-paste from docs.
- **Custom components** go in `$lib/components/custom/` and import from `$lib/components/ui/`.
- **All API calls** go in `$lib/api/` — `backend.ts` for the backend, `relayer.ts` for the relayer service.
- `$lib/utils/cn.ts` must export a `cn()` function (clsx + tailwind-merge) — required by shadcn-svelte.
- All shadcn-svelte CSS variables are declared in `src/app.css` (do not move them).
- **Read `docs/api-backend-docs/` and `docs/api-relayer-docs/` before implementing any API integration.**

---

## components.json (shadcn-svelte config)

```json
{
  "$schema": "https://shadcn-svelte.com/schema.json",
  "style": "default",
  "tailwind": {
    "config": "",
    "css": "src/app.css",
    "baseColor": "slate"
  },
  "aliases": {
    "components": "$lib/components",
    "utils": "$lib/utils",
    "ui": "$lib/components/ui",
    "hooks": "$lib/hooks",
    "lib": "$lib"
  }
}
```

---

## Build / Development Commands

```bash
npm run dev          # Start development server
npm run build        # Build for production
npm run preview      # Preview production build
npm run check        # Type check (run before every commit)
npm run check:watch  # Watch mode type checking

# shadcn-svelte CLI
npx shadcn-svelte@latest add button       # Add a component
npx shadcn-svelte@latest add card dialog  # Add multiple
npx shadcn-svelte@latest diff             # Sync upstream component changes
```

---

## Code Style Guidelines

### Svelte 5 + shadcn-svelte Patterns

```svelte
<script lang="ts">
  // shadcn-svelte components import from the ui alias
  import { Button } from "$lib/components/ui/button/index.js";
  import { Card, CardHeader, CardContent } from "$lib/components/ui/card/index.js";
  import { cn } from "$lib/utils/cn.js";

  // Svelte 5 runes
  let open = $state(false);
  let { class: className } = $props<{ class?: string }>();
</script>

<!-- Use cn() for conditional classes alongside shadcn components -->
<div class={cn("flex flex-col gap-4", className)}>
  <Card>
    <CardHeader>Title</CardHeader>
    <CardContent>Content</CardContent>
  </Card>
  <Button onclick={() => (open = true)}>Open</Button>
</div>
```

### Import Conventions

```typescript
// External libraries
import { type ClassValue, clsx } from "clsx";
import { twMerge } from "tailwind-merge";

// shadcn-svelte components (always use index.js)
import { Button } from "$lib/components/ui/button/index.js";
import { Input } from "$lib/components/ui/input/index.js";

// Auth
import { PUBLIC_API_URL } from "$env/static/public";
import { authClient } from "$lib/auth-client";

// Local custom components
import Header from "$lib/components/custom/Header.svelte";
```

### Naming Conventions

| Item | Convention | Example |
|---|---|---|
| Svelte components | PascalCase | `UserCard.svelte` |
| shadcn-svelte ui | kebab-case dir | `$lib/components/ui/button/` |
| Custom components | PascalCase dir | `$lib/components/custom/Header.svelte` |
| Utilities | camelCase | `cn.ts`, `formatDate.ts` |
| Hooks | `use-` prefix | `use-media-query.svelte.ts` |
| Constants | SCREAMING_SNAKE_CASE | `MAX_FILE_SIZE` |

### `cn()` Utility (Required)

```typescript
// src/lib/utils/cn.ts
import { type ClassValue, clsx } from "clsx";
import { twMerge } from "tailwind-merge";

export function cn(...inputs: ClassValue[]): string {
  return twMerge(clsx(inputs));
}
```

### Forms with shadcn-svelte (Formsnap + Superforms + Zod)

```svelte
<script lang="ts">
  import { superForm } from "sveltekit-superforms/client";
  import { zodClient } from "sveltekit-superforms/adapters";
  import * as Form from "$lib/components/ui/form/index.js";
  import { Input } from "$lib/components/ui/input/index.js";
  import { z } from "zod";

  const schema = z.object({ email: z.string().email() });
  const { form, errors, enhance } = superForm(data.form, {
    validators: zodClient(schema),
  });
</script>

<form use:enhance>
  <Form.Field {form} name="email">
    <Form.Control>
      {#snippet children({ props })}
        <Form.Label>Email</Form.Label>
        <Input {...props} bind:value={$form.email} />
      {/snippet}
    </Form.Control>
    <Form.FieldErrors />
  </Form.Field>
</form>
```

### TypeScript Guidelines

- Always annotate return types for exported functions
- Prefer `interface` over `type` for object shapes
- Use `unknown` instead of `any`, then narrow
- Wrap all async in try/catch
- Error messages in Spanish (project locale)

### Tailwind CSS v4 Guidelines

- No `@apply` — use utility classes directly
- Use `cn()` for conditional/merged classes
- shadcn-svelte CSS variables defined in `app.css` — do not override manually
- Theme customization goes in `app.css` under `@layer base`

---

## MCP Tools Usage

MCP config (`.kiro/mcp`):
```json
{
  "mcpServers": {
    "svelte":       { "type": "remote", "url": "https://mcp.svelte.dev/mcp" },
    "better-auth":  { "type": "remote", "url": "https://mcp.inkeep.com/better-auth/mcp" },
    "Context7":     { "type": "stdio", "command": "npx", "args": ["-y", "@upstash/context7-mcp@latest"] },
    "stitch":       { "url": "https://stitch.googleapis.com/mcp", "headers": { "X-Goog-Api-Key": "..." } }
  }
}
```

---

### 1. Svelte MCP (`mcp.svelte.dev`)

Provides Svelte 5 and SvelteKit documentation. **Always run before writing any Svelte/SvelteKit code.**

**Workflow (always follow this order):**
```
1. list-sections        → discover available documentation sections
2. get-documentation    → fetch ALL relevant sections based on use_cases
3. svelte-autofixer     → run on ALL Svelte code before presenting to user
                          keep calling until zero issues are returned
4. playground-link      → only if user explicitly requests it
```

---

### 2. better-auth MCP (`mcp.inkeep.com/better-auth`)

Provides up-to-date better-auth documentation. Use it when:
- Implementing authentication flows (sign in, sign up, sessions, OAuth)
- Configuring `auth-client.ts` or any better-auth plugin
- Handling auth state in Svelte 5 components
- Working with better-auth adapters or middleware

**Rule**: Since this is a static site, better-auth runs **entirely client-side**. Use `createAuthClient()` from `better-auth/svelte` — there is no server session. Always query the MCP before implementing auth logic; do NOT rely on training data.

---

### 3. Context7 MCP (`@upstash/context7-mcp`)

Provides up-to-date documentation for **Semaphore Protocol** and other fast-evolving libraries. Use it when:
- Implementing Semaphore Protocol integration (identity, groups, proofs, signals)
- Working with ZK proof primitives or on-chain verification
- Resolving SDK ambiguity for any library not covered by the other MCPs

**Workflow:**
```
1. resolve-library-id   → find the library ID (e.g. "@semaphore-protocol/core")
2. get-library-docs     → fetch current docs with topic filter
```

Always use Context7 before writing Semaphore-related code. Do NOT rely on training data — the protocol changes frequently.

---

### 4. Stitch MCP (`stitch.googleapis.com`)

Google Stitch MCP — provides access to Google APIs and data services. Use it when:
- Integrating with any Google service (Sheets, Drive, BigQuery, etc.)
- Reading or writing structured data to Google-hosted sources
- The user requests any Google Cloud or Workspace data operation

**Rule**: All Stitch calls are made client-side (no server). Handle API key via `import.meta.env.PUBLIC_STITCH_API_KEY` — never hardcode the key in source.

---

### 5. shadcn-svelte Documentation (web fetch)

Not an MCP — fetch docs directly from the web before implementing any component:

```
LLMs index:  https://www.shadcn-svelte.com/llms.txt
Component:   https://shadcn-svelte.com/docs/components/<name>.md
Theming:     https://shadcn-svelte.com/docs/theming.md
Tailwind v4: https://shadcn-svelte.com/docs/migration/tailwind-v4.md
```

**Rule**: Fetch the `.md` doc before implementing. Do NOT rely on memory.

---

## API Integration (Client-Side Only)

Since this is a static site, **all API calls are made client-side from the browser**. Never use server load functions or server routes.

### Backend API (`docs/api-backend-docs/`)

```typescript
// src/lib/api/backend.ts
const BASE_URL = import.meta.env.PUBLIC_BACKEND_URL;

export async function fetchResource(id: string) {
  const res = await fetch(`${BASE_URL}/resource/${id}`, {
    headers: { Authorization: `Bearer ${token}` },
  });
  if (!res.ok) throw new Error(`Error: ${res.status}`);
  return res.json();
}
```

**Rule**: Always read `docs/api-backend-docs/` before implementing a backend call. The docs contain the exact endpoint paths, request shapes, and response types.

### Relayer API (`docs/api-relayer-docs/`)

```typescript
// src/lib/api/relayer.ts
const RELAYER_URL = import.meta.env.PUBLIC_RELAYER_URL;

export async function relayTransaction(payload: RelayPayload) {
  const res = await fetch(`${RELAYER_URL}/relay`, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(payload),
  });
  if (!res.ok) throw new Error(`Relayer error: ${res.status}`);
  return res.json();
}
```

**Rule**: Always read `docs/api-relayer-docs/` before implementing a relayer call. The relayer is an external service — its API contract must be followed exactly.

### Calling APIs from Svelte 5 Components

```svelte
<script lang="ts">
  import { fetchResource } from "$lib/api/backend.js";

  let data = $state<Resource | null>(null);
  let error = $state<string | null>(null);
  let loading = $state(false);

  $effect(() => {
    loading = true;
    fetchResource("123")
      .then((r) => (data = r))
      .catch((e) => (error = e.message))
      .finally(() => (loading = false));
  });
</script>
```

---

## Skills Usage

This project has access to the following skills. Read the relevant SKILL.md **before** starting any task in that domain. Skills compound — use multiple when appropriate.

### `.kiro/skills/frontend-design`
Use when building any UI component, page, or layout. Commit to a bold, intentional aesthetic. Avoid generic AI aesthetics (no Inter/Roboto, no purple gradients). Design should be distinctive, memorable, and production-grade.

### `.kiro/skills/seo-audit`
Use when creating or modifying pages, metadata, or content. Since this is a static site, SEO is handled entirely at build time. Apply when:
- Writing `<svelte:head>` meta tags (title, description, og:*, canonical)
- Structuring headings (`h1`→`h2`→`h3` hierarchy)
- Adding structured data / JSON-LD
- Optimizing images (`alt`, `loading="lazy"`, dimensions)
- Generating sitemap or robots.txt

### `.kiro/skills/tailwind-design-system`
Use when defining or extending the design system — colors, spacing, typography tokens, and CSS variable conventions for shadcn-svelte theming.

### `.kiro/skills/web-design-guidelines`
Use for accessibility, semantic HTML, responsive layout decisions, and general UX patterns.

**Rule**: Read SKILL.md before the task, not after. Multiple skills can and should be combined (e.g., `frontend-design` + `seo-audit` + `tailwind-design-system` when building a new page).

---

## Theming (shadcn-svelte + Tailwind v4)

CSS variables are declared in `src/app.css`. To customize the theme:

```css
/* src/app.css */
@import "tailwindcss";

@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 222.2 84% 4.9%;
    --primary: 221.2 83.2% 53.3%;
    --primary-foreground: 210 40% 98%;
    /* ... other shadcn-svelte tokens */
  }
  .dark {
    --background: 222.2 84% 4.9%;
    --foreground: 210 40% 98%;
    /* ... */
  }
}
```

Use the [shadcn-svelte theming docs](https://shadcn-svelte.com/docs/theming.md) to customize colors.

---

## Accessibility

- Use semantic HTML (`<button>`, `<nav>`, `<main>`, `<dialog>`)
- shadcn-svelte components are accessible by default (Bits UI primitives) — don't break ARIA by overriding roles
- Ensure `aria-label` on icon-only buttons
- All interactive elements keyboard-navigable

---

## Quick Reference

| Task | Command / Resource |
|---|---|
| Dev server | `npm run dev` |
| Type check | `npm run check` |
| Build (static) | `npm run build` |
| Add UI component | `npx shadcn-svelte@latest add <name>` |
| Sync component updates | `npx shadcn-svelte@latest diff` |
| shadcn-svelte component docs | `https://shadcn-svelte.com/docs/components/<name>.md` |
| shadcn-svelte full index | `https://www.shadcn-svelte.com/llms.txt` |
| Svelte 5 docs | MCP: `list-sections` -> `get-documentation` -> `svelte-autofixer` |
| Semaphore Protocol docs | MCP Context7: `resolve-library-id` -> `get-library-docs` |
| Backend API spec | `docs/api-backend-docs/` |
| Relayer API spec | `docs/api-relayer-docs/` |
| better-auth docs | MCP `better-auth` — query before any auth implementation |
| Google/Stitch data | MCP `stitch` — query for any Google API integration |