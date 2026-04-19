# Hindia Timur — Project Brief & Design System


---

## 1. Project Overview

**Brand:** Hindia Timur  
**Website:** hindiatimur.com  
**Tagline:** "Elevate Your Sourcing. Taste the Difference."  
**Core mission:** Premium Indonesian agricultural produce for international importers, brands, and distributors.
**GitHub** The files are now hosted on GitHub: https://github.com/DionWicaksono/hindiatimur-html
**Github Pages** Newest Files: https://dionwicaksono.github.io/hindiatimur-html/index.html
## Repo
url: https://github.com/DionWicaksono/hindiatimur-html
branch: main

**Primary audience (B2B focus):** Importers, procurement managers, commodity traders, health & wellness brands, fragrance houses, food manufacturers — based in EU, US, Middle East, East Asia, Australia.

**Secondary audience (B2C):** Regional Southeast Asian consumers seeking premium fresh produce.

**Files built so far: (this is outdated), check the above repo for the most current files**
- `hindiatimur (6).html` — Main B2B landing page (homepage)
- `hindiatimur-products.html` — Full product catalog page (20+ products, filterable, modal detail view)
- 'coffee.html' — Example of individual product page.

---

## 2. Brand Voice & Copy Rules

**Tone:** Authoritative, refined, trustworthy. Not salesy. Like a high-end commodity trading house — confident without being pushy.

**Writing style:**
- Lead with the importer's pain point, not the product feature
- Use dashes ( -- ) not em-dashes for pauses in copy
- No exclamation marks
- No emojis anywhere (use SVG icons instead)
- Italicise key phrases in headings using `<em>` (renders in gold-light or sage)
- Use "we" not "I" — company voice
- Preferred phrases: "export-grade", "farm-to-port", "compliant shipments", "supply chain", "traceable"
- Avoid: "world-class", "best-in-class", "amazing", "delicious"

**Section label pattern:** Short all-caps phrase with gold line prefix, e.g. `Why Partner With Us`, `Our Export Catalog`, `Flexible Solutions`

**Heading pattern:** Main title in Cormorant Garamond light, italic `<em>` on the most important noun/phrase, e.g.:
```
The Sourcing Partner <em>International Importers Trust</em>
20+ Export-Grade <em>Indonesian Products</em>
```

---

## 3. Design Tokens (CSS Variables)

```css
:root {
  --cream:      #F5F0E8;   /* warm off-white, used for cards on dark bg */
  --warm-white: #FAF8F3;   /* page background */
  --forest:     #1C2B1E;   /* primary dark — hero, dark sections, nav CTA */
  --moss:       #2D4A32;   /* secondary dark — compliance section left col */
  --sage:       #4A6741;   /* mid-green — em italic in headings on light bg */
  --gold:       #B8924A;   /* primary accent — labels, borders, CTAs */
  --gold-light: #D4AC6E;   /* secondary accent — stats, em on dark bg, hover */
  --earth:      #6B4E2A;   /* tertiary warm — luxury product tags */
  --text:       #1A1A18;   /* body text */
  --text-mid:   #3D3D38;   /* secondary text, nav links */
  --text-light: #6B6B60;   /* captions, meta, descriptors */
  --border:     rgba(28,43,30,0.12);  /* light-bg dividers */
}
```

**Dark section border:** `rgba(245,240,232,0.10)` (on forest/moss backgrounds)  
**Dark section text:** `rgba(245,240,232,0.65)` for body, `rgba(245,240,232,0.5)` for secondary

---

## 4. Typography

```
Display / Headings:  Cormorant Garamond — weights 300, 400, 600; italic variants used for emphasis
Body:                DM Sans — weights 300, 400, 500
Google Fonts import: https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=DM+Sans:wght@300;400;500&display=swap
```

**Type scale:**
| Element | Font | Size | Weight |
|---|---|---|---|
| H1 (hero) | Cormorant Garamond | clamp(2.8rem, 4.5vw, 4.2rem) | 300 |
| H2 (section) | Cormorant Garamond | clamp(2.2rem, 3.5vw, 3.2rem) | 300 |
| H3 (card title) | Cormorant Garamond | 1.2–1.5rem | 600 |
| Section label | DM Sans | 0.72rem | 500, uppercase, 0.18em spacing |
| Body | DM Sans | 1rem | 300 |
| Small/caption | DM Sans | 0.78–0.82rem | 300–400 |
| Stat number | Cormorant Garamond | 2.2–3rem | 300 |

---

## 5. Layout System

**Page padding:** `8vw` horizontal on all sections  
**Section padding:** `padding: 8rem 8vw` (light sections), same for dark  
**Border radius:** `2px` throughout — never round, never sharp  
**Grid gaps (hairline):** `1px` gap with matching background colour for edge-to-edge grid effect  

**Section background alternation:**
```
Hero          → var(--forest) left / image right
Trust bar     → var(--forest)
Why/Sourcing  → var(--forest)  [dark]
Products      → var(--cream)   [light]
Process       → var(--forest)  [dark]
Compliance    → var(--moss) left / var(--cream) right  [split]
Testimonial   → var(--warm-white)  [light]
CTA/Contact   → var(--forest)  [dark]
Footer        → #111612  [deepest]
```

---

## 6. Component Patterns

### Section Label
```html
<div class="section-label">Label Text</div>
```
- 0.72rem, DM Sans 500, uppercase, 0.18em letter-spacing
- Gold colour with 28px gold line prefix via `::before`
- On dark bg: override to `color: var(--gold-light)` and `::before { background: var(--gold-light) }`

### Section H2
```html
<h2 class="section-h2">Main Title <em>Italic Emphasis</em></h2>
```
- Light bg: `em` = var(--sage)
- Dark bg: override `em` to var(--gold-light) inline or via parent class

### Buttons
```html
<!-- Primary (gold bg) -->
<a href="#" class="btn-primary">Label</a>

<!-- Secondary (transparent, cream border) — for dark bg only -->
<a href="#" class="btn-secondary">Label</a>

<!-- Dark primary (forest bg) — for light bg sections -->
<a href="#" class="btn-primary" style="background:var(--forest); color:var(--cream);">Label</a>
```

### Trust Bar
- Forest background, gold dot separators, uppercase 0.78rem DM Sans
- Items: Phytosanitary Certified · Full Chain of Custody · Flexible MOQ · Custom OEM Labeling · DDP & FOB Shipping · Responsive Account Management

### Product Cards (homepage mini-grid)
- 4-column grid on `var(--cream)` background
- Hover: background flips to `var(--forest)`, gold bottom-border reveals via scaleX
- Tags: `.product-tag` (sage) / `.product-tag.export` (gold)

### Sourcing Cards (5-column dark grid)
- `.sourcing-card` on forest background
- Ghost numeral top-left in Cormorant Garamond, very low opacity gold
- SVG icon in gold-bordered circle
- Gold top-border reveals on hover via scaleX
- CTA link with arrow SVG

### Pillar List (numbered credentials)
- 2-column grid: `3rem` number col + content col
- Number in Cormorant Garamond 1.8rem, gold
- Divider: `var(--border)` on light, `rgba(245,240,232,0.10)` on dark

### Process Steps (5 steps horizontal)
- 5-column grid on forest background
- Circles connected by faint horizontal line via `::before` pseudo-element
- Gold-bordered circles with Cormorant numeral inside

### Fade-up Animation (Progressive Enhancement)
```css
/* Content always visible by default */
.fade-up { opacity: 1; transform: none; }
/* Only animates when JS adds .js-animate to <body> */
.js-animate .fade-up { opacity: 0; transform: translateY(28px); transition: opacity 0.7s ease, transform 0.7s ease; }
.js-animate .fade-up.visible { opacity: 1; transform: translateY(0); }
```
```js
// JS pattern — always add to page
(function() {
  if (!('IntersectionObserver' in window)) return;
  document.body.classList.add('js-animate');
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) { entry.target.classList.add('visible'); observer.unobserve(entry.target); }
    });
  }, { threshold: 0, rootMargin: '0px' });
  document.querySelectorAll('.fade-up').forEach(el => observer.observe(el));
  setTimeout(() => { document.querySelectorAll('.fade-up:not(.visible)').forEach(el => el.classList.add('visible')); }, 800);
})();
```

---

## 7. Page Architecture — hindiatimur.html (Homepage)

| Order | Section | Class/ID | Background |
|---|---|---|---|
| 1 | Fixed Nav | `nav` | warm-white, frosted |
| 2 | Hero | `.hero` | forest (left) + image (right) |
| 3 | Trust Bar | `.trust-bar` | forest |
| 4 | Why + Sourcing Models (merged) | `.sourcing-section` | forest |
| 5 | Products mini-grid | `.products-section #products` | cream |
| 6 | How It Works (Process) | `.process-section #process` | forest |
| 7 | Compliance + Markets | `.compliance-section #compliance` | moss/cream split |
| 8 | Testimonial | `.testimonial-section` | warm-white |
| 9 | CTA + Contact Form | `.cta-section #contact` | forest |
| 10 | Footer | `footer` | #111612 |

---

## 8. Page Architecture — hindiatimur-products.html (Catalog)

| Order | Section | Notes |
|---|---|---|
| 1 | Fixed Nav | Same pattern as homepage |
| 2 | Page Header | Dark hero header, breadcrumb, stats bar |
| 3 | Sticky Filter Bar | Category tabs + count + grid/list toggle |
| 4 | Products Grid | 4-col, filterable, click opens modal |
| 5 | Product Detail Modal | Image + 6-spec grid + cert badges + CTA |
| 6 | CTA Strip | Forest bg, "Custom Sourcing" offer |
| 7 | Footer | Simplified single-row footer |

**Product categories (filter tabs):** All · Superfoods · Fragrance & Oils · Food & Sweeteners · Industrial · Luxury

**Products (20):** Specialty Coffee, Moringa Powder, Vanilla Beans, Agarwood (Oud), Sandalwood, Patchouli Oil, Raw Forest Honey, Cacao & Chocolate, Gula Aren, Porang/Konjac Flour, Tapioca Starch, Premium Avocado, Premium Spices, Charcoal Briquettes, Natural Indigo Paste, Cashew, Red Beans, Sorghum, Corncob, Kratom (Export Only)

---

## 9. Compliance & Certification Reference

Always-available certifications to reference in copy:
- Phytosanitary Certificate (BKP / Ministry of Agriculture)
- Certificate of Origin (SKTM / Trade Ministry)
- Certificate of Analysis (ISO 17025-accredited labs)
- CITES Appendix II (Agarwood, Sandalwood)
- Halal (MUI) — on request
- Organic (IMO / USDA NOP) — select products
- EU Timber Regulation (EUTR)
- GC/MS Analysis (essential oils)

**Export markets served:** EU (Germany, Netherlands, France, Belgium), USA, Middle East (UAE, Saudi, Qatar), East Asia (Japan, Korea, China), South Asia (India, Sri Lanka), Australia & NZ

**Incoterms offered:** FOB, CIF, DDP

---

## 10. The 5 Partnership Models

These must always be presented in this order with these exact titles:

| # | Title | One-line summary |
|---|---|---|
| 01 | Direct Exporter | Own harvests — Coffee, Moringa, Vanilla. No middlemen, best price. |
| 02 | Full Sourcing Agent | End-to-end: find, vet, manage, ship across Indonesia. |
| 03 | QC + Compliance Only | Buyer has supplier — we add inspection + paperwork. |
| 04 | Trading & Spot Supply | Ready stock, stable pricing, fast dispatch. |
| 05 | Private Label / OEM | Their product, buyer's brand + packaging + certs. |

---

## 11. Key Stats & Proof Points

Always use these numbers consistently:
- **20+** export product lines
- **15+** export destination markets
- **100%** phytosanitary compliant shipments
- **24h** quote turnaround
- **17,000+** islands of biodiversity (Indonesia)
- **3 years** — reference tenure for testimonial partner

---

## 12. Testimonial

> "Hindia Timur has been our trusted supplier for over three years. Their consistency in quality and reliability in delivery is unmatched. The phytosanitary compliance documentation is always impeccable -- customs clearance has never been smoother."
>
> **Ahmad Wijaya** — Procurement Manager, PT Global Exports

---

## 13. Contact / CTA Copy Patterns

**Primary CTA label:** `Request a Quote`  
**Secondary CTA label:** `View Product Catalog` or `Browse Products`  
**Form promise bullets:**
- Free product samples for qualified importers
- Response within 24 business hours
- Full compliance documentation before commitment
- Dedicated account manager assigned from day one

**Direct contact:**
- Email: info@hindiatimur.com
- WhatsApp: +62 (XXX) XXX-XXXX

---

## 14. Image Style Guide

All images from Unsplash. Filter applied: `saturate(0.85–0.9)` to keep natural, non-oversaturated look. Overlay gradients used on all hero/section images to integrate with forest green palette.

**Hero image:** Tropical Indonesian landscape — `https://images.unsplash.com/photo-1530062845289-9109b2c9c868`  
**Why/Sourcing image:** Indonesian farmland/soil — `https://images.unsplash.com/photo-1596040033229-a9821ebd058d`

---

## 15. Pages Still To Build (Backlog)

| Page | URL | Priority | Notes |
|---|---|---|---|
| Individual product pages | `/products/[slug]` | High | 20 pages, reuse modal content as template |
| Exporter quote form | `/exporter-quote` | High | Multi-step form, product selector |
| About / Story | `/about` | Medium | Founders, mission, Indonesia origin story |
| For Farmers | `/join-as-farmer` | Medium | Supply side acquisition |
| Blog | `/blog` | Low | SEO, thought leadership |
| FAQ | `/faq` | Low | Compliance & process questions |
| Contact | `/contact` | Low | Simple form + map |

---

## 16. Coding Conventions

- **Single-file HTML** — all CSS in `<style>`, JS in `<script>` at bottom of body
- **No frameworks** — vanilla HTML/CSS/JS only
- **Border radius:** always `2px`, never more
- **Transitions:** `0.2s–0.35s` for hovers, `0.7s` for scroll animations
- **Hover pattern on dark cards:** background lightens slightly (`rgba(245,240,232,0.06)`), gold top-border reveals via `scaleX(0 → 1)`
- **Hover pattern on light cards:** background flips to `var(--forest)`, text to `var(--cream)`
- **No inline styles** except for one-off overrides (margin, colour context-switches)
- **SVG icons** preferred over emoji or icon fonts — always `stroke="currentColor"` so colour inherits
- **Responsive breakpoints:** 1024px (3-col grids), 768px (stack + hide hero image), 480px (1-col)
- **Font loading:** always `preconnect` to fonts.googleapis.com and fonts.gstatic.com

# Hindia Timur — Project Log

---

## Session: Link Restructure & Mobile Nav

### Canonical File Map

| Old filename | Canonical filename |
|---|---|
| `hindiatimur__6_.html` | `index.html` |
| `hindiatimur-products.html` | `products.html` |
| `coffee.html` | `coffee.html` ✓ |
| `about.html` | `about.html` ✓ |
| `exporter-quote.html` | `exporter-quote.html` ✓ |
| `blog.html` | `blog.html` ✓ |
| `blog-coffee-heritage-volcanic.html` | `blog-coffee-heritage-volcanic.html` ✓ |
| `blog-organic-certification-fair-trade.html` | `blog-organic-certification-fair-trade.html` ✓ |
| `blog-seasonal-availability-guide.html` | `blog-seasonal-availability-guide.html` ✓ |

---

### Link Fixes Applied (all 5 main pages)

- All `hindiatimur-products.html` references → `products.html`
- All `hindiatimur__6_.html` references → `index.html`
- All `index.html#contact` CTA links → `exporter-quote.html`
- All `href="#"` company footer links resolved:
  - About Hindia Timur → `about.html`
  - For Farmers → `about.html#farmers`
  - Request a Quote / Contact Us → `exporter-quote.html`
  - Request Samples / OEM & Private Label → `exporter-quote.html`
- **Blog & Insights**, **FAQ**, **WhatsApp/LinkedIn** left as `href="#"` (no page yet)

### Nav Structure (consistent across all pages)

```
Logo | Products | Compliance | Process | About | [Request a Quote]
```

- `Products` → `products.html`
- `Compliance` → `index.html#compliance`
- `Process` → `index.html#process`
- `About` → `about.html`
- `Request a Quote` → `exporter-quote.html` (styled as `.nav-cta`)
- Active page gets `class="active"` on its own nav link

---

### Mobile Nav — Hamburger Menu

Added to all 5 pages (`index.html`, `coffee.html`, `products.html`, `exporter-quote.html`, `about.html`).

**Behaviour**
- Breakpoint: `≤ 768px` — `.nav-links` hidden, hamburger shown
- Menu opens fullscreen (`position: fixed; inset: 0`) over `var(--forest)` background
- 3-bar icon animates to × on open; bars turn `var(--cream)` against dark bg
- Links stagger in with `transition-delay` cascade (0.06s increments)
- "Request a Quote" styled italic in `var(--gold-light)` to stand out
- Closes on: link click, Escape key, button re-click
- `body overflow: hidden` while open

**HTML added inside `<nav>`**
```html
<button class="nav-hamburger" id="navHamburger" aria-label="Open menu" aria-expanded="false">
  <span></span><span></span><span></span>
</button>
```

**HTML added after `</nav>`**
```html
<div class="mobile-menu" id="mobileMenu" role="dialog" aria-modal="true" aria-label="Navigation">
  <ul>
    <!-- same links as desktop nav, active class preserved per page -->
  </ul>
  <span class="mobile-menu-footer">Hindia Timur &mdash; Indonesia</span>
</div>
```

**Key CSS classes**
- `.nav-hamburger` — hidden by default, `display: flex` at ≤768px, `z-index: 301`
- `.mobile-menu` — `display: none` by default, `display: flex` at ≤768px, `z-index: 300`
- `.mobile-menu.open` — triggers opacity + translateY transition to show
- `.nav-hamburger.open` — triggers bar-to-× animation

**JS pattern (added before last `</script>`)**
```js
(function() {
  var btn = document.getElementById('navHamburger');
  var menu = document.getElementById('mobileMenu');
  // toggle open/close, lock body scroll, close on link click + Escape
})();
```

---

### New Pages — Checklist

When creating any new page, ensure:

- [ ] Use canonical filenames (see map above)
- [ ] Copy `:root` CSS variables block from any existing page
- [ ] Import Cormorant Garamond + DM Sans from Google Fonts
- [ ] Nav includes: Logo → `index.html`, Products, Compliance, Process, About, Request a Quote CTA — with `class="active"` on current page
- [ ] Add hamburger button HTML inside `<nav>` (after `.nav-links`)
- [ ] Add `.mobile-menu` div immediately after `</nav>` with matching links
- [ ] Add hamburger CSS block (`.nav-hamburger`, `.mobile-menu`) before `</style>`
- [ ] Add hamburger JS block before last `</script>`
- [ ] Footer: 4-column grid — Products, For Importers, Company, (Connect or Insights)
- [ ] Footer company links: `about.html`, `about.html#farmers`, `exporter-quote.html`
- [ ] No `href="#"` except: Blog, FAQ, WhatsApp, LinkedIn (not yet built)

## Session Log — April 12, 2026

### index.html
- **BUG FIX**: Removed Cloudflare-injected `<script data-cfasync="false" src="/cdn-cgi/...">` wrapper
  that silently swallowed all inline hamburger-menu JS (browsers ignore inline content in external script tags).
- **BUG FIX**: Restored truncated script — file was cut off at `btn.textConten`, missing scroll listener
  and `handleSubmit` completion.
- **FIX**: Replaced obfuscated Cloudflare email (`[email protected]`) with plain `hello@hindiatimur.com`.
- Combined all page JS into one clean `<script>` block: hamburger menu, sticky nav scroll, fade-up animations, form submit handler.

### Pending (next session)
- Uniform nav + footer across all 8 pages
- SEO meta tags + JSON-LD on all pages
- sitemap.xml
- faq.html

- CHANGES.md
## exporter-quote.html
- Nav: centered image logo (hindia-timur-logo.png), scrolls to logotype
- Nav links: Products, Compliance, About, Request a Quote
- Mobile: hamburger menu
- Footer: image logo
FAQ.html done

# Session Log — April 14, 2026

---

## Tasks Completed

### 1. Mobile Nav — Added to Missing Blog Posts
**Files:** `blog-vanilla-sourcing-journey.html`, `blog-water-conservation-tropical.html`, `blog-sustainable-coconut-farming.html`

These three blog posts were missing the hamburger menu entirely. Added:
- Full hamburger CSS block (`.nav-hamburger`, `.mobile-menu`, stagger animations)
- Hamburger button HTML inside `<nav>`
- `.mobile-menu` overlay div with matching links
- Hamburger open/close JS (toggle, Escape key, body scroll lock)

---

### 2. Stale Filename References — Fixed Across All Pages
**Files:** All 12 HTML pages

Replaced 34 stale references:
- `hindiatimur__6_.html` → `index.html`
- `hindiatimur-products.html` → `products.html`

---

### 3. Formspree Endpoints — Wired to All Three Forms
Real `async fetch()` submission replacing previous fake `setTimeout` simulations.

| File | Form | Endpoint |
|---|---|---|
| `exporter-quote.html` | Exporter Quote Form | `xwvrzkaz` |
| `about.html` | Farmer Partnership Application | `xreydgrv` |
| `index.html` | Contact Form | `mdawjowa` |

**`about.html` additional work:** The farmer form had no `<form>` tag — inputs were in a plain `<div>`. Wrapped in `<form action="...">`, added `name=` attributes to all inputs/selects/textarea, replaced truncated `handleSubmit` JS with real fetch + success/error states.

**`exporter-quote.html` additional work:** Form tag already existed but the submit listener called `e.preventDefault()` and used a fake `setTimeout`. Replaced with real `fetch()` to Formspree with error handling.

---

### 4. index.html Contact Form — Simplified
Replaced the complex 8-field quote form in the CTA section with a clean 4-field contact form:
- Name, Business Email, Company, Message
- Wired to Formspree endpoint `mdawjowa` via `async fetch()`
- Fixed Cloudflare-obfuscated email (`[email protected]`) → `hello@hindiatimur.com`

---

### 5. Logo — PNG → WebP Across All Pages
**Files:** 12 HTML pages

Replaced all `src="hindia-timur-logo.png"` references with `hindia-timur-logo.webp`, including JSON-LD absolute URLs in `<script type="application/ld+json">` blocks.

---

### 6. Phone / WhatsApp Field — Added to index.html Contact Form
Added an inline country code dropdown (`+1` through `+974`, covering all primary export markets) paired with a tel input. `exporter-quote.html` and `about.html` already had phone fields.

---

### 7. Mobile Nav Style Leak — Fixed on Blog Posts
**Files:** `blog-vanilla-sourcing-journey.html`, `blog-water-conservation-tropical.html`, `blog-sustainable-coconut-farming.html`

**Root cause:** The original `@media (max-width: 768px)` block in these pages contained `nav { justify-content: center !important }` and `.nav-logo { margin: 0 auto !important }` — declarations that fought the hamburger CSS added in the previous task. Removed the two conflicting nav declarations from the old media query, retaining layout-only rules (`.post-hero`, `.hero-image`, `.footer-top`).

---

### 8. Oversized Logo — Fixed on Blog Posts
**Files:** `blog-vanilla-sourcing-journey.html`, `blog-water-conservation-tropical.html`, `blog-sustainable-coconut-farming.html`

**Root cause:** When the hamburger nav was added, only the `<img class="nav-logo-img-main">` HTML was injected — but the CSS rules that control it were never carried over from `blog.html`.

Missing rules added:
- `.nav-logo-img-main { display: block; width: 110px; ... }`
- `nav#nav.scrolled .nav-logo-img-main { width: 0; opacity: 0; ... }`
- `.nav-logo-img-scrolled` (hidden by default)
- `nav#nav.scrolled .nav-logo-img-scrolled` (visible on scroll)

---

### 9. Nav Scroll Transform, Logo Centering, Post-Nav/Footer Overlap — Fixed All Blog Posts
**Files:** All 6 blog post pages

This resolved multiple distinct symptoms with two root causes.

#### Root Cause A — Conflicting `nav` base rule
All blog posts had a minified `nav { height:72px; background:rgba(250,248,243,0.94) }` rule (the original light-bar style) alongside the newer `nav#nav { column layout, transparent }` block added for the scroll-transform effect. Because the tag selector `nav` matches `nav#nav` with equal or higher specificity in some cascade positions, it was overriding the scroll state.

**Fix by group:**
- `blog-coffee-heritage-volcanic.html`, `blog-organic-certification-fair-trade.html`, `blog-seasonal-availability-guide.html` — Removed the conflicting minified `nav` rule. The `nav#nav` block was already present and correct.
- `blog-vanilla-sourcing-journey.html`, `blog-water-conservation-tropical.html` — Removed minified `nav` rule + associated simple `.nav-logo`/`.nav-links`/`.nav-cta` rules. Inserted full canonical `nav#nav` block (default state was missing entirely).
- `blog-sustainable-coconut-farming.html` — Replaced expanded old nav block with canonical `nav#nav` block.

**Canonical nav#nav structure (all 6 files now identical):**
```
Default:  transparent overlay, flex-direction: column, logo centred large
Scrolled: flex-direction: row, light bg, logotype swap, links visible
```

#### Root Cause B — `<nav class="post-nav">` tag inheritance
The Previous/Next post bar used a `<nav>` tag. It was inheriting all `nav` tag CSS (`position: fixed`, `z-index: 200`, `flex-direction: column`, etc.), causing it to float, overlap the footer, and render incorrectly.

**Fix:** Changed `<nav class="post-nav">` → `<div class="post-nav">` on all 6 blog post pages. Eliminates tag-level inheritance entirely — no CSS reset required.

#### Cleanup
Removed orphaned standalone `.nav-logo-img-main` CSS blocks from `blog-vanilla`, `blog-water`, and `blog-coconut` that had been inserted in a prior session and were now duplicated inside the canonical `nav#nav` block.

---

## Canonical File State (Post-Session)

| File | Nav Type | Hamburger | Formspree | Logo |
|---|---|---|---|---|
| `index.html` | Fixed light bar | ✓ | `mdawjowa` | `.webp` |
| `products.html` | Fixed light bar | ✓ | — | `.webp` |
| `about.html` | Fixed light bar | ✓ | `xreydgrv` | `.webp` |
| `exporter-quote.html` | Fixed light bar | ✓ | `xwvrzkaz` | `.webp` |
| `coffee.html` | Fixed light bar | ✓ | — | `.webp` |
| `faq.html` | Fixed light bar | ✓ | — | `.webp` |
| `blog.html` | Fixed light bar | ✓ | — | `.webp` |
| `blog-coffee-heritage-volcanic.html` | Transparent overlay → scroll swap | ✓ | — | `.webp` |
| `blog-organic-certification-fair-trade.html` | Transparent overlay → scroll swap | ✓ | — | `.webp` |
| `blog-seasonal-availability-guide.html` | Transparent overlay → scroll swap | ✓ | — | `.webp` |
| `blog-vanilla-sourcing-journey.html` | Transparent overlay → scroll swap | ✓ | — | `.webp` |
| `blog-water-conservation-tropical.html` | Transparent overlay → scroll swap | ✓ | — | `.webp` |
| `blog-sustainable-coconut-farming.html` | Transparent overlay → scroll swap | ✓ | — | `.webp` |

---

## Known Remaining Issues / Next Session

- Individual product pages (`/products/[slug]`) — 20 pages, high priority
- Exporter quote form — consider adding product multi-select back to index.html contact if conversion data warrants it
- Blog nav "active" state — all blog post pages mark Blog as active but do not differentiate individual posts
- `faq.html` — verify nav/footer structure matches canonical pattern
- WhatsApp number placeholder (`+62 (XXX) XXX-XXXX`) still needs real number inserted
- Sitemap URLs should be updated from `dionwicaksono.github.io/hindiatimur-html/` to `hindiatimur.com/` before or at domain switch

