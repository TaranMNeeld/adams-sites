# Master — Website

A clean, accessible, fully static marketing site for Master (Master Corps LLC). No build step or framework required to run it — every page is plain HTML that opens in any browser.

## View it

Open **`index.html`** in a browser. That's the whole requirement.

## Pages

| File | What it is |
|---|---|
| `index.html` | Home — the thesis, the products, the 72-hour cycle |
| `method.html` | The Continuous Flow Model: six phases, the seven judgments, the Concept Passport |
| `studio.html` | **Master Studio** — for founders ($20k–$35k) |
| `metal.html` | **Master Metal** — for enterprise ($75k–$200k) |
| `forge.html` | **Master FORGE** — defense & military (three tiers; scoped individually) |
| `self.html` | **Master Self** — innovation as a service *(in development)* |
| `jiminy.html` | **Jiminy** — the always-on companion *(on the horizon)* |
| `vision.html` | The four-act arc, the Common Memory, the Medical Horizon |
| `manifesto.html` | "Polish the stone." |
| `about.html` | Company, founder, and the ethics underneath |
| `contact.html` | Begin — the early-partner ask |

```
MasterCorps-Website/
├── *.html                 # the 11 pages
├── assets/
│   ├── styles.css         # the entire design system (light + dark, all tokens)
│   ├── site.js            # mobile nav, scroll header, reveal-on-scroll
│   ├── favicon.svg        # the faceted-stone mark
│   └── fonts/             # (optional) drop self-hosted woff2 here — see below
└── README.md
```

## Deploy

It's a static folder. Drag it into any of: Netlify, Vercel, Cloudflare Pages, GitHub Pages, S3 + CloudFront, or any web host. No server, database, or build needed.

## Two things you'll likely want to change

**1. The contact email.** Every "Begin" / "Email" action points to `hello@mastercorps.com`. To change it, find-and-replace that string across the `.html` files (it appears in footers, the About page, and `contact.html`). If you prefer to regenerate instead, edit `EMAIL` at the top of `build_site.py` and re-run it.

**2. The domain in metadata.** Canonical and Open Graph URLs use `https://mastercorps.com`. Update `SITE_URL` in `build_site.py` (or find-and-replace) once the real domain is set.

## Typography

The type is **Source Sans 3** — Adobe's open-source humanist sans, designed as the libre answer to **Myriad Pro** (very close letterforms and proportions). The font-family stack also lists `Myriad Pro` and `Myriad` ahead of the system humanist fallbacks (`-apple-system`/San Francisco, `Segoe UI`), so anyone who already has Myriad installed sees it natively, and everyone else gets a faithful match.

Right now the typeface loads from Google Fonts via a `<link>` in each page's `<head>`. To **self-host** it (no third-party calls — matching the "self-hosted fonts only" principle in your architecture spec):

1. Download the WOFF2 set: <https://github.com/adobe-fonts/source-sans/releases/latest> → the **`WOFF2-source-sans-*.zip`** asset.
2. Copy the weights you want (300/400/600/700 + 400 italic) into `assets/fonts/`.
3. Remove the three Google Fonts `<link>`/`<link rel="preconnect">` lines from each page's `<head>` (or from the `SHELL` template in `build_site.py`).
4. Add this block to the top of `assets/styles.css`:

```css
@font-face{font-family:"Source Sans 3";font-weight:300;font-style:normal;font-display:swap;
  src:url("fonts/SourceSans3-Light.otf.woff2") format("woff2");}
@font-face{font-family:"Source Sans 3";font-weight:400;font-style:normal;font-display:swap;
  src:url("fonts/SourceSans3-Regular.otf.woff2") format("woff2");}
@font-face{font-family:"Source Sans 3";font-weight:400;font-style:italic;font-display:swap;
  src:url("fonts/SourceSans3-It.otf.woff2") format("woff2");}
@font-face{font-family:"Source Sans 3";font-weight:600;font-style:normal;font-display:swap;
  src:url("fonts/SourceSans3-Semibold.otf.woff2") format("woff2");}
@font-face{font-family:"Source Sans 3";font-weight:700;font-style:normal;font-display:swap;
  src:url("fonts/SourceSans3-Bold.otf.woff2") format("woff2");}
```

(Match the filenames to whatever the zip contains.) The fallback stack means nothing breaks during the swap.

## Accessibility (built in)

- Semantic landmarks, one `<h1>` per page, no skipped heading levels.
- "Skip to content" link; visible keyboard focus rings everywhere.
- Mobile menu is a real `<button>` with `aria-expanded` / `aria-controls`, closes on `Esc`, and returns focus.
- **All text meets WCAG 2.1 AA contrast** in both light and dark themes (verified; tightest pair 4.58:1).
- Respects `prefers-color-scheme` (automatic dark mode) and `prefers-reduced-motion` (disables animation).
- Decorative SVG is `aria-hidden`; meaning is never carried by color alone.

## Editing content

Each page is readable, hand-editable HTML — change copy directly. If you'd rather keep the shared header/footer/meta consistent across all 11 pages, edit `build_site.py` (one shell, one nav, one footer; per-page content lives in the `PAGES` dict) and run:

```bash
python3 build_site.py
```

— it rewrites every `.html` file. The generator is a convenience, not a dependency: the site runs without it.

---
© Master Corps LLC · *Master. Make it.* · Virginia, USA
