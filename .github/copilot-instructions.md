<!-- .github/copilot-instructions.md for AI coding agents -->

This repository is a small Astro (v4) static website with minimal structure. Below are concise, actionable notes that help an AI coding agent be immediately productive in this codebase.

- **Project type:** Astro static site (see `package.json` dependency `astro`).
- **Key scripts:**
  - `npm run dev` — start local dev server (`astro dev`).
  - `npm run build` — build static site (`astro build`).
  - `npm run preview` — preview built site (`astro preview`).

- **Important files / folders**
  - `astro.config.mjs` — site configuration (currently `site: 'https://example.com'`).
  - `src/layouts/BaseLayout.astro` — main layout, implements language handling and navigation.
  - `src/pages/*.astro` — page components (e.g. `index.astro`, `about.astro`, `services.astro`, `contact.astro`).
  - `src/content/text.js` — all user-facing text / translations (default language `zh` with `zh` and `ja` entries). Edit here to change copy or add languages.
  - `public/styles/global.css` — global styling.

- **Architecture & conventions (what to know)**
  - Language selection is done via a `lang` query parameter (not path or subdomain). The layout reads `Astro.url.searchParams.get('lang') ?? defaultLang` in `BaseLayout.astro`.
  - All pages use the same `BaseLayout.astro` to obtain `t` (translations). When adding content, follow the pattern: import `Layout` and `text` as in `src/pages/index.astro`.
  - Navigation links are generated with helper functions in the layout: `link(path)` and `switchLink(targetLang)` so edits to links should respect these helpers to preserve `lang` parameter behavior.

- **Editing content / translations**
  - To update copy, modify `src/content/text.js`. Add a new language by adding a key (e.g. `en`) and updating `defaultLang` if needed.
  - When you add new text keys, update templates to reference `t.<path>` (example: `t.home.heroTitle` used in `index.astro`).

- **Adding a page**
  - Create `src/pages/yourpage.astro`.
  - Use the existing layout pattern:
    - `import Layout from "../layouts/BaseLayout.astro";`
    - Read `lang` from `Astro.url.searchParams` and use `t = text[lang]` if you need translations.

- **Build / deploy notes**
  - `astro.config.mjs` contains a comment in Chinese mentioning GitHub Pages — if deploying to GitHub Pages, update the `site` field and follow Astro's GH Pages deployment docs.
  - No tests or CI configured in the repo — changes should be validated locally with `npm run dev` and `npm run build` + `npm run preview`.

- **Patterns to preserve / avoid**
  - Preserve the query-parameter based i18n approach. Replacing it with a path-based i18n requires updating `BaseLayout.astro` link helpers and all page links.
  - Keep copy centralized in `src/content/text.js`. Avoid scattering literal strings across pages unless they're page-specific and non-translatable.

- **Quick examples**
  - Change site title: edit `text.zh.brand` and `text.ja.brand` in `src/content/text.js`.
  - Add a feature card: update `home.features` array in `src/content/text.js` (both languages if required).

- **Local commands**
  - Install dependencies (if missing): `npm install`
  - Dev server: `npm run dev`
  - Build: `npm run build`
  - Preview build: `npm run preview`

If any part of the codebase is unclear or you want the instructions to be more/less prescriptive (for example, to add CI steps or a different i18n approach), tell me which area to expand and I'll iterate.
