# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
npm run dev       # Start dev server at localhost:4321
npm run build     # Build production site to ./dist/
npm run preview   # Preview production build locally
```

## Architecture

**Predy Clicker** is a mobile-first idle/clicker game built with Astro 5, TypeScript (strict), and Tailwind CSS 4.

### Key pages
- [src/pages/index.astro](src/pages/index.astro) — Login (hardcoded credentials: `Predy` / `Master`)
- [src/pages/clicker.astro](src/pages/clicker.astro) — Main game: click mechanics, rank system, XP bar
- [src/pages/register.astro](src/pages/register.astro) — Registration form with Flatpickr date picker (Spanish locale)
- [src/pages/profile/[id].astro](src/pages/profile/[id].astro) — Dynamic profile routes generated from `src/data/users.ts`

### Components
- [src/layouts/Layout.astro](src/layouts/Layout.astro) — Shared HTML wrapper; all pages use this. Sets dark theme, Outfit font, max-w-xl constraint.
- [src/components/UserProfile.astro](src/components/UserProfile.astro) — Complex profile view (settings overlay, user grid, avatar with glow, ownership hierarchy).
- [src/components/Footer.astro](src/components/Footer.astro) — Fixed bottom nav with 4 tabs; Social and Shop are disabled (`#` links).
- [src/components/ui/Button.astro](src/components/ui/Button.astro) — Variants: `primary` (yellow), `secondary`, `outline`, `ghost`.
- [src/components/ui/Input.astro](src/components/ui/Input.astro) — Supports password toggle; uses debounced listener to handle Astro page transitions.

### Data
- [src/data/users.ts](src/data/users.ts) — Static array of 10 `User` objects. No backend — all data is hardcoded. User IDs follow `"0000-XXXX"` format.

### Game logic (clicker.astro)
- Balance drives rank: 13 ranks (INDIGENTE → MULTIBILLONARIO) with thresholds at `[4,6,8,10,...,26]`.
- Level system: 3 difficulty levels with XP requirements `[3, 6, 9]`; XP bar hides at max rank.
- Each click increments balance by 1 and spawns a floating "+1" label (`coinFloat` CSS animation).
- "Multiplicar click" upgrade button exists in the UI but is not yet implemented.

### Conventions
- All UI text is in Spanish.
- Tailwind CSS 4 is loaded via the `@tailwindcss/vite` plugin (no `tailwind.config` file).
- No persistence layer — state is in-memory only (resets on page refresh).
- `configuration.astro` is an empty placeholder page.
