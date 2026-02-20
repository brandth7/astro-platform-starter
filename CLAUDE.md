# CLAUDE.md - Project Guide for Claude Code

## Project Overview

Astro + Netlify Platform Starter — a full-stack web app built with Astro.js showcasing Netlify platform features (SSR, Edge Functions, Blob Store, Image CDN, cache revalidation). Includes an **Infinite Banking Calculator** page for whole life policy cash value projections and IBC financing vs. traditional loan comparisons.

## Tech Stack

- **Framework**: Astro ^4.6.2 (hybrid output mode — mixed SSR + static)
- **UI**: React ^18.2.0 (via @astrojs/react), Tailwind CSS ^3.4.3, daisyUI ^4.10.2
- **Hosting**: Netlify (adapter: @astrojs/netlify)
- **Storage**: Netlify Blob Store (@netlify/blobs)
- **Language**: TypeScript (React JSX mode)

## Commands

- `npm run dev` — Start local dev server (use `netlify dev` for full Netlify feature support)
- `npm run build` — Production build
- `npm run preview` — Preview production build locally

## Project Structure

```
src/
├── pages/                    # Routes (file-based routing)
│   ├── index.astro           # Home page
│   ├── infinite-banking.astro # IBC Calculator (whole life policy projections + loan comparisons)
│   ├── revalidation.astro    # Cache revalidation demo
│   ├── image-cdn.astro       # Netlify Image CDN demo
│   ├── edge/                 # Edge function geolocation routing demo
│   ├── blobs/                # Blob store interactive demo (React components)
│   │   └── _components/      # React components: NewShape, ShapeEditor, ShapePreview, StoredShapes
│   └── api/                  # API endpoints (non-prerendered, dynamic SSR)
│       ├── blob.ts           # GET single blob by key
│       ├── blobs.ts          # Blob management CRUD
│       └── revalidate.ts     # Cache revalidation endpoint
├── components/               # Reusable Astro components
│   ├── Header.astro          # Navigation (6 pages)
│   ├── Footer.astro
│   ├── Card.astro
│   ├── ContextAlert.astro    # Netlify context/environment display
│   └── ...
├── layouts/
│   └── Layout.astro          # Master layout (takes `title` prop)
├── styles/
│   └── globals.css           # Tailwind directives + custom styles
├── types.ts                  # BlobParameterProps, BlobProps
└── utils.ts                  # Blob generation, caching helpers, unique naming
netlify/
└── edge-functions/
    └── rewrite.js            # Geolocation-based routing (AU vs non-AU)
```

## Key Files

- `src/pages/infinite-banking.astro` — IBC Calculator: policy details inputs, scenario comparisons (car, real estate, business, emergency, debt), cash value projection table, loan amortization with interest recapture calculations. All logic is client-side `<script>` with TypeScript.
- `src/components/Header.astro` — Navigation menu (edit here to add/remove pages)
- `src/layouts/Layout.astro` — Wraps all pages with head, header, footer
- `astro.config.mjs` — Astro config: hybrid output, Netlify adapter, React + Tailwind integrations
- `tailwind.config.mjs` — Custom theme: Inter font, daisyUI lofi theme, primary colors #F67280/#C06C84

## Code Conventions

- **Formatting**: Prettier — 4-space indentation, single quotes, 160 char line width
- **Styling**: Tailwind utility classes + daisyUI component classes. Custom styles via `<style>` blocks in `.astro` files.
- **Pages**: Astro components with frontmatter (`---`) for imports/server logic, HTML template below, optional `<style>` and `<script>` blocks
- **API routes**: TypeScript files in `src/pages/api/` exporting HTTP method handlers
- **React components**: Only used in `src/pages/blobs/_components/` for interactive blob editor
- **Environment variables**: `PUBLIC_DISABLE_UPLOADS` flag controls blob upload availability
