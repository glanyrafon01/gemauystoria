# AGENTS

Guidance for agentic coding in this repository.

## Repo summary
- Hugo static site for Gemau Ystoria (Welsh-first, bilingual).
- Content lives in `content/cy` and `content/en` with shared translation keys.
- Theme is pulled via Hugo modules from `github.com/theNewDynamic/gohugo-theme-ananke/v2`.
- Custom overrides live in `layouts/` and `i18n/`.
- Build output goes to `public/` (ignored); `public-test/` appears to be a committed preview.

## Required tooling
- Hugo (extended) is required for local builds.
- Go is required for Hugo module operations (`hugo mod tidy`).
- GitHub Actions builds and deploys on push to `main`.

## Build, lint, test commands
- Dev server: `hugo server`
- Production build: `hugo --minify`
- Module tidy (CI uses this): `hugo mod tidy`
- Lint: not configured
- Tests: not configured

## Running a single test or page
- There is no test runner; validate a single page by running `hugo server` and opening its URL.
- For a quick rebuild after edits, keep the dev server running and navigate to the specific page.
- If you need a static build of a single language, you can use `hugo --contentDir content/cy` or `hugo --contentDir content/en`.

## CI/CD (from `.github/workflows/deploy.yml`)
- Trigger: push to `main`.
- Steps: `hugo mod tidy` then `hugo --minify`.
- Deploy: `peaceiris/actions-gh-pages` to `gh-pages` from `./public`.
- Do not edit generated files in `public/`.

## Content authoring conventions
- Use YAML front matter delimited by `---` at the top of content files.
- Always set `title` in both languages.
- For translated pairs, use identical `translationKey` values.
- Align URLs across languages (same path) to keep the language switcher consistent.
- Keep filenames meaningful and stable; prefer lowercase with hyphens.

## Bilingual setup
- Welsh content lives in `content/cy/`; English content lives in `content/en/`.
- Update both language files when adding or changing shared pages.
- The default language is Welsh and uses `/cy/` in the URL.
- Interface translations live in `i18n/cy.toml` and `i18n/en.toml`.
- When adding i18n strings, keep keys consistent across languages.

## Hugo template conventions
- Custom layouts in `layouts/` override the theme; avoid editing `_vendor/` theme files.
- Prefer small partials in `layouts/partials/` for repeated markup.
- Use Go template conditionals (`with`, `if`, `default`) to guard optional params.
- Avoid heavy logic in templates; keep content in Markdown and settings in `hugo.toml`.
- Follow existing template formatting when editing `layouts/*.html`.

## Formatting and style
- Keep Markdown paragraphs readable; a blank line separates blocks.
- Use consistent quote style in front matter (double quotes in this repo).
- Maintain trailing newline at end of files.
- Do not introduce non-ASCII characters unless they already exist in the file.
- Do not rewrap existing paragraphs unless needed for clarity.

## Naming and structure
- Content file names: lowercase, hyphenated, language-appropriate.
- `translationKey`: lowercase, stable, and shared between translations.
- `url`: include leading slash for English (`/en/...`) and match across languages.
- New sections should follow the same directory layout as existing content.
- Keep slug/path changes minimal to avoid breaking links.

## Data, assets, and static files
- Use `static/` for images or files that must be copied verbatim to the site root.
- Use `assets/` for pipeline-processed files (if you add any Hugo Pipes usage).
- Do not commit local build output in `public/` or `resources/`.
- `public-test/` appears to be a committed build; do not edit by hand.
- If `public-test/` must be updated, regenerate via Hugo rather than manual edits.

## Error handling and safety
- In templates, prefer `with` blocks to avoid nil access.
- Use `default` to provide fallbacks for optional params.
- Avoid `safeHTML` unless content is trusted and necessary.
- Keep language switcher logic intact; it depends on `.Translations`.

## Imports and dependencies
- There are no code imports in this repo; dependencies are Hugo modules.
- Update module versions in `hugo.toml` only if required.
- Keep `go.mod` in sync with Hugo modules via `hugo mod tidy`.
- Do not edit `_vendor/` unless explicitly asked; it is vendored upstream.

## Generated and vendored content
- `_vendor/` contains the theme sources; treat as read-only.
- `public/` and `resources/` are build outputs and should remain uncommitted.
- `public-test/` is likely a snapshot build; treat as generated.
- `themes/` exists but theme is primarily used as a module.

## Repository files to know
- `hugo.toml` for site configuration and module imports.
- `i18n/*.toml` for interface translations.
- `layouts/` for template overrides.
- `content/` for bilingual content.
- `.github/workflows/deploy.yml` for deployment steps.

## Cursor and Copilot rules
- No `.cursor/rules/` directory found.
- No `.cursorrules` file found.
- No `.github/copilot-instructions.md` found.

## When adding new pages
- Create both language files with matching `translationKey`.
- Keep URLs aligned between languages.
- Update relevant i18n strings if the UI needs new labels.
- Verify locally with `hugo server`.
- Avoid editing generated `public/` artifacts.

## When editing templates
- Prefer edits in `layouts/` over theme internals.
- Keep HTML structure consistent with existing templates.
- Use `partial` for shared elements like headers/footers.
- Test both languages and the language switcher.
- Keep accessibility in mind (heading order, alt text).

## When editing configuration
- Prefer `hugo.toml` for site-level settings.
- Keep language config consistent with the bilingual setup.
- Run `hugo` after config changes to verify build.
- Update docs if behavior changes are user-facing.

## Notes for agents
- Make minimal, focused changes; avoid sweeping rewrites.
- Do not change content tone or language unless explicitly asked.
- Preserve Welsh-first structure and bilingual parity.
- If you add a file, ensure it is linked from navigation or intended usage.
- Keep changes compatible with the deploy workflow.

## Quick reference
- Start dev server: `hugo server`
- Build production output: `hugo --minify`
- Update module deps: `hugo mod tidy`
- Preview Welsh page: `http://localhost:1313/cy/`
- Preview English page: `http://localhost:1313/en/`

## File length note
- This file is intentionally detailed for agentic tools.
- If you update it, keep it around 150 lines.

## TODO markers
- None; follow repository conventions.

## End
- Add new guidance here only when needed.
- Keep instructions aligned with actual repo behavior.
