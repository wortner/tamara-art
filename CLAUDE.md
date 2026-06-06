# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Bilingual (Czech default / English) Hugo static site — a portfolio for artist Tamara Wortnerová. Custom theme in `themes/tamara/`. Deployed to GitHub Pages on every push to `main` via `.github/workflows/hugo.yml`.

## Commands

```bash
hugo server          # local dev at http://localhost:1313/ (live reload)
hugo --gc --minify   # production build into ./public (mirrors CI)
```

Requires **Hugo extended** (CI pins `0.156.0`). The extended edition is mandatory — the theme uses `images.AutoOrient`, `.Resize`, and WebP encoding, which the standard edition cannot do.

There are no tests, linters, or npm/build tooling — Hugo is the entire toolchain.

## Architecture

### Galleries are image-driven, not content-driven
Each gallery section (`drawings`, `paintings`, `water-cycle`, `silhouettes`) has a `content/<section>/_index.md` + `_index.en.md` that hold **only the title/description/intro text**. The actual images come from `assets/images/<folder>/`, scanned at build time by `themes/tamara/layouts/partials/gallery.html` via `resources.Match`. **To add/remove artwork you add/remove image files in `assets/images/`, not markdown in `content/`.**

- Images render sorted by filename, so the `NN-` numeric prefix (`01-drawing.jpg`) controls gallery order.
- Each image may have sibling caption files `NN-name.cs.md` and `NN-name.en.md` in the same folder. The gallery partial picks the one matching the page language; caption text also becomes the image `alt`. Caption files are often empty — that's fine.
- The partial generates a responsive WebP thumbnail (`1400x`) + full-size (`2400x`) and wires a lightbox.

### Section → image-folder mapping has a naming mismatch
Each section gets its own layout `themes/tamara/layouts/<section>/list.html`, which calls the gallery partial with an explicit folder name. **Note `water-cycle` (URL/section) maps to the `water_cycle` (underscore) image folder.** When adding a section, create both the content dir and a matching `layouts/<section>/list.html` passing the correct `folder`.

### Bilingual content
Configured in `hugo.toml` under `[languages]` with per-language menus. Default language `cs` serves at the root (no `/cs/` prefix); English files use the `.en.md` suffix convention. Both languages share the same image assets and galleries.

### SEO lives in one place
`themes/tamara/layouts/partials/head.html` centralizes all meta tags, Open Graph, Twitter cards, canonical URLs, hreflang alternates, and JSON-LD (`Person` schema on the homepage, `CollectionPage` on gallery sections). Per-page `description` in frontmatter overrides the site default. See `README.md` for the wider SEO checklist and DNS/Search Console setup.

### Layout chain
`baseof.html` (shell + inline lightbox/menu JS) → `partials/head.html` + `partials/sidebar.html` (nav from `.Site.Menus.main`, social links, language switch) → section `list.html` or `index.html`. Styling is a single hand-written stylesheet at `themes/tamara/static/css/style.css`. Goldmark is configured with `unsafe = true` (raw HTML in markdown is allowed); inline gallery markdown images go through `layouts/_default/_markup/render-image.html` for automatic resizing.

## Deployment notes
- `static/CNAME` (`tamara-art.cz`) and `static/robots.txt` are copied verbatim to the site root; don't relocate them.
- `public/` and `resources/_gen/` are git-ignored build artifacts — never edit by hand.
