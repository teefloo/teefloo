# Profile README redesign

## Goal

Replace the existing terminal/cyber profile README with a compact public-facing portfolio index that answers three questions immediately:

1. Who is Esteban Deloge professionally?
2. What kinds of systems does he build?
3. Which public projects are worth opening next?

The result must be native to GitHub Markdown. It cannot depend on JavaScript, live stats services, external counters, remote widgets, or hidden interactive behavior.

## Direction

Use the approved **Atlas de terrain** concept.

- Visual language: editorial luxury, with paper/ink/oxide-red tones and a restrained technical annotation layer.
- Hero: one repo-owned SVG plate, supplied in light and dark variants through `<picture>`.
- Layout: a short internal index followed by an editorial project register. The Markdown remains linear so it reads cleanly on narrow screens.
- Voice: precise, French, human, and evidence-led. No generic enthusiasm, invented metrics, or claims that cannot be tied to a public profile or repository.
- Motion: none required. Static SVG keeps the README legible when GitHub sanitizes or proxies image content.

## Public content set

The account is `teefloo`, named Esteban Deloge, located in France, with the public bio “Automation Engineer | PHP/JS Plugin Creator | n8n Workflows Expert ...”, public website `https://teeflo.me/`, public LinkedIn link `https://www.linkedin.com/in/esteban-deloge/`, and public email `contact@teeflo.me` currently present in the profile README.

The selected public projects are:

- **Lunidex**: active open-source Pokémon workspace with Pokédex, TCG collection, team-building, battle tools, quizzes, progress tracking, and the public product URL `https://lunidex.app`.
- **ComparPrix**: discount-price comparison product with live scraping, PostgreSQL persistence, Next.js, Playwright, and the public product URL `https://comparprix.vercel.app/`.
- **PolyChat AI**: browser chat studio that compares up to three language-model conversations, with a public product URL `https://polychat-ai-xi.vercel.app`.
- **AsusWRT MCP**: public Python MCP server for controlled AsusWRT administration over SSH, with allowlisted operations, dry-run support, and explicit mutation confirmation.
- **MyImpots**: French tax-information product with simulators, declaration-box explanations, fiscal calendar, document checklist, and public product URL `https://myimpots.vercel.app`.

These are all public repositories. Forks, private repositories, unverified client work, and project metrics are excluded. The README should link to the repository for each entry and link to the product only where the public homepage is verified.

## README structure

1. Theme-aware hero with name, role, location, and a one-sentence description.
2. Four compact anchor links: `projets`, `terrain`, `profil`, `contact`.
3. “Projets choisis” register with five numbered entries. Each entry has a short description, an evidence line, and GitHub/product links.
4. “Ce qui relie ces projets” with four concrete practice areas: products web, interfaces IA, automatisation/data, and integrations/outillage.
5. “Profil public” with the source-backed role and the public website/LinkedIn/GitHub links.
6. “Contact” as a minimal closing line.

Avoid tables for the project register so long names and links wrap naturally on mobile. Avoid shields, stats cards, trophies, counters, GIFs, and a generic technology wall.

## Files

- Replace `README.md` completely.
- Add `assets/atlas-light.svg` and `assets/atlas-dark.svg` as small, self-contained local hero assets.
- Remove the old terminal, system-panel, workflow-rail, and divider SVGs once no README reference remains.
- Do not add remote assets or a build dependency.

## Verification

- Check the README for missing local assets, malformed Markdown/HTML, duplicate sections, unsupported script/iframe usage, and links that no longer match public sources.
- Validate both SVG files as XML and inspect their dimensions and text content.
- Check all external URLs with an HTTP request where network access permits.
- Render the README in a small local HTML wrapper for desktop and mobile-width visual review when tools permit.
- Confirm the working-tree diff contains only the intended README, new assets, removed obsolete assets, and this design note.
