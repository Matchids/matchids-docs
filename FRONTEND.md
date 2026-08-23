# Frontend (matchids-web)

Next.js 14 App Router, TypeScript, Tailwind (via `@matchids/design-system`'s
preset). Mobile-first, one route folder per page under `src/app/`.

## Key conventions

- **No direct data access.** Every network call goes through
  `src/lib/api.ts`, which talks to `matchids-backend` over HTTP. No
  Prisma, no payment SDK, no database credentials anywhere in this repo.
- **Demo content lives in `src/data/`**, clearly marked
  `isDemoContent: true`, used as local-dev fallback so the site is
  browsable without a running backend — never shipped as if it were real
  catalog data.
- **Components are grouped by feature** (`components/books`,
  `components/home`) plus shared primitives imported from
  `@matchids/design-system`.

## Rendering strategy

Mostly static/server-rendered pages (book listings, marketing pages) with
client components only where interactivity is required (checkout,
donations, the mobile nav). See individual `page.tsx` files for the
`"use client"` boundary.

## SEO & accessibility

`sitemap.ts` and `robots.ts` generate the standard files; every page sets
its own `metadata` export. Accessibility baseline: semantic HTML, visible
focus states (global in `styles/globals.css`), a skip-to-content link in
the root layout, alt text on every meaningful image.
