# Profile README redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Replace the current terminal/cyber profile README with a concise, public-source-backed editorial portfolio index that works in GitHub light and dark themes.

**Architecture:** Keep the README as linear GitHub-flavored Markdown with a small amount of supported HTML. Use one local hero image selected through `<picture>`, with separate light and dark SVGs so the first view remains legible without JavaScript or external services. Represent projects as numbered editorial entries and derive the practice-area section from those same entries.

**Tech Stack:** GitHub Flavored Markdown, supported HTML (`<div>`, `<picture>`, `<source>`, `<img>`), hand-authored SVG, shell-based XML/link checks.

**Spec:** `docs/superpowers/specs/2026-09-15-profile-readme-design.md`

## Global Constraints

- Use only public information from the `teefloo` GitHub profile and public repositories.
- Do not include private repositories, forks, invented metrics, or unverified claims.
- Do not use JavaScript, iframes, live stats services, counters, trophies, GIFs, or remote widgets.
- Keep all visual assets repository-owned and lightweight.
- Use French copy with sentence-case headings and concrete descriptions.
- Keep the project register linear so long names and links wrap on mobile.
- Preserve the user's existing unrelated worktree changes and do not push or change GitHub settings.

---

### Task 1: Create the theme-aware Atlas hero assets

**Files:**
- Create: `assets/atlas-light.svg`
- Create: `assets/atlas-dark.svg`

**Interfaces:**
- Consumes: the approved Atlas de terrain visual direction and the public identity `Esteban Deloge / teefloo`.
- Produces: two self-contained SVGs with the same `viewBox="0 0 1200 360"`, accessible `<title>` and `<desc>`, and no external references.

- [ ] **Step 1: Set the shared SVG geometry and accessible metadata**

  Use an identical canvas in both files:

  ```xml
  <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 360" role="img" aria-labelledby="atlas-title atlas-desc">
    <title id="atlas-title">Esteban Deloge — Atlas de terrain</title>
    <desc id="atlas-desc">Editorial profile plate for teefloo, showing web products, AI interfaces, automation and developer tooling.</desc>
  ```

- [ ] **Step 2: Draw the light plate**

  Use a paper background around `#F5F0E8`, ink around `#1E2A2D`, muted slate around `#687477`, and oxide red around `#B34A32`. Use thin rules, a small coordinate grid, a compass-like circle, and four labeled nodes: `WEB`, `AI`, `DATA`, and `TOOLS`. Set `ESTEBAN DELOGE` as the largest text, `@teefloo / FRANCE` as metadata, and `automation · products · integrations` as the descriptor. Use system-safe serif and monospace fallbacks only.

- [ ] **Step 3: Draw the dark plate**

  Keep the geometry and wording identical while switching to a charcoal background around `#121819`, warm light ink around `#F1ECE2`, muted sage/slate around `#A5B2AD`, and a brighter oxide accent around `#D56A4D`. Preserve contrast on every label and avoid a neon/cyber treatment.

- [ ] **Step 4: Validate the asset contract**

  Run:

  ```bash
  xmllint --noout assets/atlas-light.svg assets/atlas-dark.svg
  rg -n 'https?://|<script|<iframe|animate|foreignObject' assets/atlas-light.svg assets/atlas-dark.svg
  ```

  Expected: XML validation succeeds and the search returns no external URL, script, iframe, animation, or `foreignObject` line.

### Task 2: Replace the profile README with the editorial project register

**Files:**
- Modify: `README.md`

**Interfaces:**
- Consumes: `assets/atlas-light.svg`, `assets/atlas-dark.svg`, and the verified public project facts in the spec.
- Produces: a README whose first view identifies Esteban, his work areas, and the path to selected projects.

- [ ] **Step 1: Add the theme-aware hero and internal navigation**

  Start the file with a centered `<picture>`:

  ```html
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/atlas-dark.svg">
    <img src="./assets/atlas-light.svg" alt="Esteban Deloge, automation engineer building web products, AI interfaces, automations and integrations" width="100%">
  </picture>
  ```

  Follow it with four plain links: `Projets`, `Terrain`, `Profil`, and `Contact`.

- [ ] **Step 2: Write the short lead paragraph**

  Use concrete French copy that states the role and work without inflated claims:

  ```markdown
  Je suis Esteban Deloge, automation engineer basé en France. Je construis des produits web, des interfaces IA et des outils qui relient données, services et appareils.
  ```

  Add one short pull quote only if it adds meaning; do not add a slogan, counter, or badge row.

- [ ] **Step 3: Add the five verified project entries**

  Use numbered headings and one compact paragraph per project. Include only these links and facts:

  ```markdown
  01 — [Lunidex](https://github.com/teefloo/Lunidex) · [ouvrir l'app](https://lunidex.app)
  02 — [ComparPrix](https://github.com/teefloo/comparateur-prix-discount) · [ouvrir le produit](https://comparprix.vercel.app/)
  03 — [PolyChat AI](https://github.com/teefloo/PolyChat-AI) · [ouvrir l'app](https://polychat-ai-xi.vercel.app)
  04 — [AsusWRT MCP](https://github.com/teefloo/asuswrt-mcp)
  05 — [MyImpots](https://github.com/teefloo/MyImpots) · [ouvrir le produit](https://myimpots.vercel.app)
  ```

  Describe each with the facts from the spec, and close with a short inline evidence line such as `TypeScript · Next.js · React · Expo`. Do not add stars, user counts, years, or claims copied from marketing copy that are not needed to identify the project.

- [ ] **Step 4: Add the terrain, profile, and contact sections**

  Map the selected projects to four concrete areas: produits web, interfaces IA, automatisation et données, intégrations et outillage. Use a two-column Markdown table only for this compact mapping if it improves scanning. In the profile section, include France and the public GitHub, website, and LinkedIn links. In the contact section, include the existing public email as a mailto link.

- [ ] **Step 5: Check the README structure before cleanup**

  Run:

  ```bash
  rg -n '<picture|<source|<img|<script|<iframe|shields.io|github-readme-stats|trophy|counter|GIF|###|## ' README.md
  ```

  Expected: the file contains the local `<picture>` hero, the five project headings, the four intended sections, and no banned widget/service references.

### Task 3: Remove obsolete visual assets

**Files:**
- Delete: `assets/hero.svg`
- Delete: `assets/terminal-hero.svg`
- Delete: `assets/system-panel.svg`
- Delete: `assets/workflow-rail.svg`
- Delete: `assets/divider.svg`

**Interfaces:**
- Consumes: the new README references from Task 2.
- Produces: an asset directory containing only the two Atlas hero variants.

- [ ] **Step 1: Confirm no README or repository text still references the old assets**

  Run:

  ```bash
  rg -n 'hero\.svg|terminal-hero|system-panel|workflow-rail|divider\.svg' . --glob '!docs/superpowers/**'
  ```

  Expected: no matches after the README replacement.

- [ ] **Step 2: Remove only the obsolete SVG files**

  Delete the five named files after the reference check. Do not remove the two Atlas files or unrelated user files.

- [ ] **Step 3: Confirm the asset directory is intentional**

  Run:

  ```bash
  rg --files assets | sort
  ```

  Expected output contains exactly `assets/atlas-dark.svg` and `assets/atlas-light.svg`.

### Task 4: Verify GitHub compatibility and presentation

**Files:**
- Verify: `README.md`
- Verify: `assets/atlas-light.svg`
- Verify: `assets/atlas-dark.svg`

**Interfaces:**
- Consumes: the completed README and local assets from Tasks 1–3.
- Produces: evidence for links, local paths, SVG validity, Markdown safety, and visual review at desktop/mobile widths.

- [ ] **Step 1: Check local paths and Markdown safety**

  Run:

  ```bash
  rg -o 'src="\./assets/[^" ]+"' README.md | sed 's/src="//; s/"$//' | while read -r path; do test -f "$path" || exit 1; done
  rg -n '<script|<iframe|javascript:|data:text/html|onload=|onclick=' README.md assets/atlas-light.svg assets/atlas-dark.svg
  ```

  Expected: the path loop exits successfully and the unsafe-markup search returns no matches.

- [ ] **Step 2: Check external URLs**

  Run a read-only status check for every external URL used in the README:

  ```bash
  rg -o 'https?://[^)" ]+' README.md | sort -u | while read -r url; do curl -L -sS -o /dev/null -w '%{http_code}\t%{url_effective}\n' --max-time 20 "$url"; done
  ```

  Expected: GitHub, product, website, LinkedIn, and mailto links resolve or return an expected redirect/status. Record any network limitation rather than replacing a valid URL with an invented one.

- [ ] **Step 3: Render at desktop and mobile widths**

  Build a temporary local HTML wrapper that places the README-equivalent hero and content in a `1200px` viewport and a `390px` viewport. Inspect the result with the available browser/image tooling. Confirm the hero remains legible, the project links wrap without horizontal scrolling, and no content relies on side-by-side layout.

- [ ] **Step 4: Review the final diff and content truth**

  Run:

  ```bash
  git diff --check
  git status --short
  git diff --stat
  ```

  Re-read every sentence against the public profile/repository facts and confirm that no private repository, fork, metric, client, role, technology, result, or link was invented. Note that the environment may prevent committing because `.git` is read-only; do not push or alter remotes.
