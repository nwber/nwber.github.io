# nwber.blog

Personal blog built with [Astro](https://astro.build) and deployed to GitHub Pages at [blog.nbergeron.dev](https://blog.nbergeron.dev).

## Prerequisites

- Node 22 (via nvm). Run `nvm use` from the repo root.

## Local development

```sh
npm install
npm run dev
```

## Build

```sh
npm run build
```

Static output goes to `dist/`.

## Deployment

A GitHub Actions workflow (`.github/workflows/deploy.yml`) builds the site with `npm run build` and publishes `dist/` to GitHub Pages on every push to `master`.

## Setup required (GitHub UI, one time)

- **Settings > Pages > Source = "GitHub Actions"** (replaces the legacy Jekyll build).
- Keep the custom domain `blog.nbergeron.dev` configured in Settings > Pages. The DNS record (CNAME `blog` -> `nwber.github.io`) must still resolve, and GitHub re-verifies HTTPS enforcement after the switch.

## Analytics

PostHog is loaded when `PUBLIC_POSTHOG_KEY` is set at build time (see `.env.example` for local use, copy it to `.env`).

For CI deploys, add repo **Actions variables** (Settings > Secrets and variables > Actions > Variables):
- `PUBLIC_POSTHOG_KEY`: the project API key (`phc_...`) from app.posthog.com
- `PUBLIC_POSTHOG_HOST`: optional; defaults to `https://us.i.posthog.com` (EU cloud: `https://eu.i.posthog.com`)
