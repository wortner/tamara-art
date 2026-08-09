# Repository Guidelines

## Project Structure & Module Organization

This is a bilingual Hugo portfolio: Czech is the default language and English pages use the `.en.md` suffix. Page content lives in `content/`; gallery artwork and captions live in `assets/images/<gallery>/`. Pair each image with language-specific captions such as `01-drawing.cs.md` and `01-drawing.en.md`. Gallery order is derived from the first four-digit year in each caption (newest first), with the filename breaking ties.

The custom theme is under `themes/tamara/`: layouts and partials are in `layouts/`, while the hand-written stylesheet is `static/css/style.css`. Site settings and menus are in `hugo.toml`. Files in `static/` are copied unchanged. Do not edit generated `public/` or `resources/_gen/` content.

## Build, Test, and Development Commands

Use Hugo Extended 0.156.0, matching `.github/workflows/hugo.yml`.

- `hugo server` starts the live-reload site at `http://localhost:1313/`.
- `hugo --gc --minify` creates the production build in `public/` and mirrors CI.

There is no npm, Make, or separate test command. A successful production build is the required baseline check.

## Coding Style & Naming Conventions

Follow existing formatting: two-space indentation in HTML templates, CSS, TOML, and YAML; lowercase kebab-case for content slugs; and numbered, descriptive image names such as `02-painting.jpg`. Keep Czech/English page pairs structurally aligned. Use Hugo template whitespace and pipelines consistently with nearby files. No formatter or linter is configured, so keep diffs focused and avoid unrelated reformatting.

## Testing Guidelines

Run `hugo --gc --minify` before submitting. In the local server, inspect both `/` and `/en/`, affected navigation, responsive layouts, image captions, lightbox behavior, and image loading. For exhibitions, verify frontmatter paths (`poster`, optional `photos`) resolve under `assets/images/exhibitions/`.

## Commit & Pull Request Guidelines

Recent history uses short, direct subjects such as `adding exhibitions` and `fixing SEO`. Prefer a concise imperative subject that identifies the change, for example `add Ledax exhibition photos`. Keep each commit scoped to one logical update.

Pull requests should summarize visible and content changes, list validation performed, and link any relevant issue. Include desktop and mobile screenshots for layout or styling changes. Call out bilingual omissions, new large image assets, or changes to `hugo.toml`, SEO metadata, `static/CNAME`, or deployment configuration.
