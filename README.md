# tamara-art.cz

Personal portfolio website for Tamara Wortnerová — artist, physiotherapist and craniosacral therapist.

## SEO Setup

### Google Search Console

1. Go to [search.google.com/search-console](https://search.google.com/search-console)
2. Add `tamara-art.cz` as a property
3. Verify ownership via DNS TXT record (add it in Wedos DNS settings)
4. Submit sitemap: `https://tamara-art.cz/sitemap.xml` under Sitemaps section

### What was implemented

- Meta descriptions on all pages (CS + EN)
- Open Graph tags for social media previews (Facebook, Instagram)
- Twitter Card tags
- Canonical URLs to prevent duplicate content
- Hreflang tags linking Czech and English language variants
- JSON-LD structured data (Person schema on homepage, CollectionPage on galleries)
- `robots.txt` allowing all crawlers and pointing to sitemap
- `lastmod` dates in content frontmatter for freshness signals
- Descriptive image alt text generated from captions
- Author meta tag

### What still can be done

- Create a favicon (from hero image or custom design)
- Register on Google Search Console and submit sitemap
- Add backlinks from social media profiles (Facebook, Instagram bio)
- Register on Czech art directories (artlist.cz, artmap.cz)
- Ask galleries (ESSE Gallery, Café Kampus) to link back to tamara-art.cz
- Create a Google Business Profile if Tamara has a physical practice

## Tech Stack

- **Static site generator:** [Hugo](https://gohugo.io/)
- **Hosting:** GitHub Pages
- **Domain:** tamara-art.cz (registered at Wedos)
- **Theme:** Custom theme in `themes/tamara/`

## DNS Configuration

### Apex domain (tamara-art.cz) — A records
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

### www subdomain — CNAME record
```
www  300  CNAME  wortner.github.io
```

## Local Development

```bash
hugo server
```

Site available at http://localhost:1313/

## Content Structure

- `content/drawings/` — Kresba/Akvarel gallery
- `content/paintings/` — Malba gallery
- `content/water-cycle/` — Cyklus o vode gallery
- `content/silhouettes/` — Cyklus siluety (coming soon)
- `content/about/` — About page
- `content/contacts/` — Contacts page

Each gallery's images are in `assets/images/<folder>/` with caption files (`NN-name.cs.md`, `NN-name.en.md`).
