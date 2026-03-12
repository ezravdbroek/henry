# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project

**Henry Calligraphy** — Professional one-pager website for calligrapher Isha Henry-Hament. Astro 6.0 static site. Pure Astro — no UI framework integrations, no CSS framework. Requires Node >=22.12.0.

## Brand

- **Name**: Henry Calligraphy by Isha Henry-Hament
- **Colors**: Ivory (`#FAF8F5`) and walnut/brown (`#5C4033`). CSS vars defined in Layout.astro.
- **Fonts**: Cormorant Garamond (headings), Lora (body) via Google Fonts
- **Icons only** — never use emoji anywhere on the site. Use inline SVGs for all iconography.
- **Tone**: Modern, professional, luxury, elegant

## Commands

- `npm run dev` — Start dev server (localhost:4321)
- `npm run build` — Build to `./dist/`
- `npm run preview` — Preview production build locally

## Architecture

- **File-based routing**: `src/pages/index.astro` — single one-pager assembling all components
- **Layout**: `src/layouts/Layout.astro` — HTML shell, Google Fonts, CSS custom properties, language toggle script, scroll animation observer
- **Components**: `src/components/` — Navbar, Hero, About, Services, Calligraphy, Contact, Footer
- **Translations**: `src/data/translations.ts` — EN/NL text content. All translatable elements use `data-i18n` attributes. Client-side JS swaps text via localStorage-persisted language choice.
- **Assets**: `src/assets/` has logo.png and logo.svg; `public/` has foto1-9 (jpg/jpeg), hero.mp4, favicons
- **Styling**: Scoped CSS per component + global vars/resets in Layout. No CSS framework.
- **TypeScript**: Strict mode via Astro's strict preset

## Image Inventory (public/)

- `hero.mp4` — Hero section background video
- `foto1.jpg` (14MB, tools panoramic) — WARNING: very large, needs optimization before use
- `foto2.jpg` — Pen close-up (Calligraphy section)
- `foto3.jpg` — Hand writing calligraphy (About section)
- `foto4.jpg` — Place cards with roses (Services gallery)
- `foto5.jpg` — Gold calligraphy card (Services: Studio Work)
- `foto6.jpg` — Place cards with roses (Services gallery)
- `foto7.jpeg` — Close-up place cards (Services gallery)
- `foto8.jpeg` — Rows of place cards (Services: Live Calligraphy)
- `foto9.jpeg` — Full table of place cards (Services gallery)

## Language Toggle

EN/NL toggle in navbar. All user-facing text is in `src/data/translations.ts`. Elements use `data-i18n="key.path"` attributes. The toggle script in Layout.astro reads these and swaps textContent (or placeholder for inputs). Language persists via `localStorage('henry-lang')`.

## CSS Rules — Avoid These Mistakes

### No fixed/minimum heights on layout containers
- **Problem**: Secties worden onnodig lang en nemen teveel ruimte in.
- **Oorzaak**: `min-height`, `height` of vaste pixel-hoogtes op grid containers/secties forceren een grootte die niet past bij de content. Afbeeldingen met `height: 100%` stretchen dan mee tot de geforceerde hoogte.
- **Oplossing**: Laat content de hoogte bepalen. Gebruik NOOIT `min-height` op sectie-layouts. Gebruik voor afbeeldingen altijd `max-height` met een bovengrens (bijv. `max-height: 480px`) in combinatie met `object-fit: cover`. Stel hoogte alleen in op het `<img>` element zelf, niet op de parent container.
- **Regel**: Bouw altijd eerst ZONDER vaste hoogtes. Test visueel. Voeg pas een `max-height` toe als de afbeelding te groot wordt, nooit een `min-height` op de layout.

### Altijd visueel checken na elke wijziging
- Draai `npm run build` na elke componentwijziging.
- Controleer of secties niet onnodig lang/kort zijn.
- Check uitlijning: elementen binnen een sectie moeten dezelfde `max-width` delen.
