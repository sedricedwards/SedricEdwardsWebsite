# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev        # Vite dev server (http://localhost:5173)
npm run build      # Production build to build/ (static SPA)
npm run preview    # Serve the production build locally
npm run check      # svelte-kit sync + svelte-check type check (the only "lint/test")
npm run check:watch
```

There is no test runner and no ESLint. `npm run check` (svelte-check against `jsconfig.json`) is the sole automated verification.

## Stack & Build Model

- **SvelteKit + Svelte 5**, Vite 6, Tailwind CSS v3, GSAP 3 (with ScrollTrigger), `lucide-svelte` icons.
- Ships as a **static SPA**, not SSR. `svelte.config.js` uses `adapter-static` with `fallback: 'index.html'`. `src/routes/+layout.js` sets `ssr = false` and `prerender = true`. Pages also set `ssr = false` in their own `+page.js` (e.g. `src/routes/+page.js`) so all rendering and GSAP/canvas animation runs client-side in `onMount`. Do not introduce server-only code (`+page.server.js`, form actions, `+server.js`) — there is no server at runtime.

## Design System — "Midnight Luxe"

Keep all new UI consistent with this preset.

- **Palette** (defined in both `tailwind.config.js` and as CSS vars in `src/app.css`): `obsidian #0D0D12` (bg), `champagne #C9A84C` (accent), `ivory #FAF8F5` (text), `slate #2A2A35`.
- **Fonts** loaded via Google Fonts `<link>` in `src/app.html`: `Inter` (sans/headings), `Playfair Display` (drama serif, used italic), `JetBrains Mono` (data/labels). Use the `.font-drama` and `.font-mono-custom` helper classes (or Tailwind `font-sans`/`font-drama`/`font-mono`).
- **Shared utilities live in `src/app.css`**, not in components — reuse them rather than re-rolling: `.btn-magnetic` + `.btn-primary`/`.btn-outline` (with a nested `.btn-slide` span for the hover wipe), `.section-container` (max-w-1280 centered), `.nav-link`, `.card-lift`, `.pulse-dot`, `.cursor-blink`, `.protocol-card` (sticky-stacking), `.page-fade`. A global SVG film-grain noise overlay is applied via `html::before`.

## Architecture

`src/routes/+layout.svelte` wraps every page with `Navbar` → `<slot/>` (the page) → `Footer`. Routes:

- `/` (`+page.svelte`) — the landing page: composes `Hero`, the three service cards, `Philosophy`, `Protocol`.
- `/work`, `/services`, `/contact` — secondary pages.

Components in `src/lib/components/` (imported via the `$lib` alias):

- **Three "interactive artifact" service cards** — each is a self-contained micro-UI, not a static card: `MixingShufflerCard` (cycling stack), `WebDesignTypewriterCard` (typewriter feed), `PlanningSchedulerCard` (animated scheduler cursor).
- **`Protocol.svelte`** — sticky-stacking scroll section; each step renders one of the canvas animation components `GeometricCanvas`, `LaserGridCanvas`, `EKGCanvas`.
- `Hero`, `Philosophy`, `Pricing`, `Navbar`, `Footer`.

### Animation conventions (follow these)

- Register plugins once at module scope: `gsap.registerPlugin(ScrollTrigger)`.
- Run all GSAP setup inside `onMount` wrapped in `gsap.context(() => { ... })`, and **return `() => ctx.revert()`** from `onMount` for cleanup. See `src/routes/+page.svelte` for the canonical pattern.
- Entrance easing `power3.out`, stagger `~0.08` for text / `~0.15` for cards, `fade-up` = `{ y: 40, opacity: 0 } → { y: 0, opacity: 1 }`, triggered on scroll via `scrollTrigger: { trigger, start: "top 85%" }`.
- Buttons/links use the magnetic-hover + sliding-fill pattern (`.btn-magnetic`/`.btn-slide`); preserve it rather than adding plain buttons.
