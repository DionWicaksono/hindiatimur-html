# Hindia Timur — Project Brief, Design System & Session Log

> **Last updated: April 23, 2026**
> For nav-specific rules and bug history see `NAV-SPEC.md`.
> For a full session-by-session change log see `CHANGES.md`.

---

## 1. Project Overview

**Brand:** Hindia Timur
**Website:** hindiatimur.com
**Tagline:** "Elevate Your Sourcing. Taste the Difference."
**Core mission:** Premium Indonesian agricultural produce for international importers, brands, and distributors.

**Repo:** https://github.com/DionWicaksono/hindiatimur-html
**Branch:** main
**GitHub Pages (preview):** https://dionwicaksono.github.io/hindiatimur-html/

**Primary audience (B2B):** Importers, procurement managers, commodity traders, health & wellness brands, fragrance houses, food manufacturers — EU, US, Middle East, East Asia, Australia.
**Secondary audience (B2C):** Regional Southeast Asian consumers seeking premium fresh produce.

---

## 2. Current File Inventory

| File | Type | Nav default | Formspree | Notes |
|---|---|---|---|---|
| `index.html` | Homepage | Transparent → scroll swap | `mdawjowa` | 4-field contact form + phone/country field |
| `products.html` | Product catalog | Transparent → scroll swap | — | Filterable grid, modal detail view |
| `about.html` | About / story | Transparent → scroll swap | `xreydgrv` | Farmer partnership form |
| `exporter-quote.html` | Quote form | Transparent → scroll swap | `xwvrzkaz` | Multi-field B2B quote form |
| `coffee.html` | Product page | Transparent → scroll swap | — | Arabica/Robusta variety switcher; `padding-top: 0px` on `.product-hero` |
| `moringa.html` | Product page | Transparent → scroll swap | — | Static nutritional profile panel |
| `fruit-chips.html` | Product page | Transparent → scroll swap | — | 5-variety switcher (Jackfruit/Banana/Pineapple/Coconut/Mixed); white-bar fix applied |
| `cashew.html` | Product page | **Cream fixed → scroll swap** | — | W-grade switcher (W240/W320/W450/Splits); nav starts cream |
| `faq.html` | FAQ | Transparent → scroll swap | — | Accordion FAQ |
| `blog.html` | Blog index | Transparent → scroll swap | — | Card grid |
| `blog-coffee-heritage-volcanic.html` | Blog post | Transparent → scroll swap | — | |
| `blog-organic-certification-fair-trade.html` | Blog post | Transparent → scroll swap | — | |
| `blog-seasonal-availability-guide.html` | Blog post | Transparent → scroll swap | — | |
| `blog-vanilla-sourcing-journey.html` | Blog post | Transparent → scroll swap | — | |
| `blog-water-conservation-tropical.html` | Blog post | Transparent → scroll swap | — | |
| `blog-sustainable-coconut-farming.html` | Blog post | Transparent → scroll swap | — | |

**Assets:**
- `hindia-timur-logo.webp` — primary logo (all pages). `.png` kept as fallback only — do not reference in HTML.

---

## 3. Brand Voice & Copy Rules

**Tone:** Authoritative, refined, trustworthy. Not salesy. Like a high-end commodity trading house.

- Lead with the importer's pain point, not the product feature
- Use dashes ( -- ) not em-dashes for pauses in copy
- No exclamation marks anywhere
- No emojis — SVG icons only
- Italicise key phrases in headings with `<em>` (gold-light on dark bg, sage on light bg)
- Use "we" not "I" — company voice
- Preferred: "export-grade", "farm-to-port", "compliant shipments", "supply chain", "traceable"
- Avoid: "world-class", "best-in-class", "amazing", "delicious"

**Section label pattern:** `<div class="section-label">Short All-Caps Label</div>` — gold line prefix via `::before`

**Heading pattern:** Cormorant Garamond light, `<em>` on key noun:
```html
The Sourcing Partner <em>International Importers Trust</em>
```

---

## 4. Design Tokens

Copy verbatim on every page — must be identical everywhere.

```css
:root {
  --cream:         #F5F0E8;
  --warm-white:    #FAF8F3;
  --forest:        #1C2B1E;
  --moss:          #2D4A32;
  --sage:          #4A6741;
  --gold:          #B8924A;
  --gold-light:    #D4AC6E;
  --earth:         #6B4E2A;
  --text:          #1A1A18;
  --text-mid:      #3D3D38;
  --text-light:    #6B6B60;
  --border:        rgba(28,43,30,0.12);
  --border-strong: rgba(28,43,30,0.18);
}
```

Dark section text: `rgba(245,240,232,0.65)` body · `rgba(245,240,232,0.5)` secondary
Dark section borders: `rgba(245,240,232,0.10)`

---

## 5. Typography

```
Display/Headings: Cormorant Garamond — 300, 400, 600; italic for <em>
Body:             DM Sans — 300, 400, 500
```

Google Fonts import (use on every page):
```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
```

| Element | Font | Size | Weight |
|---|---|---|---|
| H1 hero | Cormorant Garamond | clamp(2.4rem, 3.8vw, 3.8rem) | 300 |
| H2 section | Cormorant Garamond | clamp(1.8rem, 2.8vw, 2.6rem) | 300 |
| Section label | DM Sans | 0.68–0.72rem | 500, uppercase, 0.18em spacing |
| Body | DM Sans | 0.9–1rem | 300 |
| Caption/meta | DM Sans | 0.68–0.82rem | 300–500 |

---

## 6. Layout

- **Horizontal padding:** `8vw` on all sections
- **Section padding:** `7rem 8vw` (product pages consistently use `7rem`, not `8rem`)
- **Border radius:** `2px` everywhere
- **Hairline grids:** `gap: 1px` on parent + matching background colour — creates thin-line grid without per-cell borders

**Section background order (product pages):**
```
Hero (2-col)     → forest (content) + image
Trust bar        → var(--cream)
Specs (2-col)    → var(--warm-white)
Varieties/Grades → var(--forest)
Process          → var(--warm-white)
FAQ              → var(--cream)
CTA + Form       → var(--forest)
Footer           → #111612
```

---

## 7. Nav System

See `NAV-SPEC.md` for full canonical CSS/HTML/JS. Summary:

**Two nav types:**

| Type | Pages | Default bg |
|---|---|---|
| Transparent → scroll swap | All except `cashew.html` | `transparent` |
| Cream fixed → scroll swap | `cashew.html` | `rgba(245,239,228,0.97)` |

Both use the same scroll JS (`.scrolled` at `scrollY > 40`), same logo→logotype swap CSS, same hamburger system.

**Nav link structure (all pages):**
```
Logo | Products | About ▾ | FAQ | Contact | [Request a Quote]
```

About dropdown: Our Story · How It Works · Compliance · For Farmers

**Hamburger bars:** `var(--gold)` on all pages — uniform, visible on both dark and light backgrounds.

**To try a different nav background on `cashew.html`:** find the line marked `← NAV BG` in the CSS and swap the `rgba` value:
- Cream (current): `rgba(245,239,228,0.97)`
- Forest: `rgba(28,43,30,0.97)`
- Moss: `rgba(45,74,50,0.97)`
- Transparent: `transparent`

If switching to a dark background, also update the four lines marked `← LINK COLOUR` to `rgba(245,240,232,0.9)` and the hamburger bars line to `var(--gold)`.

---

## 8. Product Page Architecture

Canonical section order:

| # | Section | Class | Bg |
|---|---|---|---|
| 1 | Hero (2-col split) | `.product-hero` | Forest + image |
| 2 | Trust bar | `.trust-bar` | `var(--cream)` |
| 3 | Specs (2-col) | `.specs-section` | `var(--warm-white)` |
| 4 | Varieties / Grades | `.varieties-section` / `.grades-section` | `var(--forest)` |
| 5 | Process (5 steps) | `.process-section` | `var(--warm-white)` |
| 6 | FAQ accordion | `.faq-section` | `var(--cream)` |
| 7 | CTA + Quote form | `.cta-section#contact` | `var(--forest)` |
| 8 | Footer | `footer` | `#111612` |

**Hero white-bar rule:** Never apply `padding-top` to `.product-hero` (the grid) when nav is transparent — it exposes the body background. Instead apply `padding-top` to `.hero-content` only. When nav is cream/opaque (cashew.html), `padding-top: 72px` on `.product-hero` is safe.

**Hero switcher panels:**
- `coffee.html` — `.variety-btn` / `.variety-content` — Arabica / Robusta
- `moringa.html` — static `.nutrition-panel`, no switcher
- `fruit-chips.html` — `.variety-btn` / `.variety-content` — Jackfruit / Banana / Pineapple / Coconut / Mixed
- `cashew.html` — `.grade-btn` / `.grade-content` — W240 / W320 / W450 / Splits

---

## 9. Component Quick Reference

### Section label
```css
.section-label {
  font-size: 0.68rem; font-weight: 500; letter-spacing: 0.18em; text-transform: uppercase;
  color: var(--gold); display: flex; align-items: center; gap: 0.7rem; margin-bottom: 1.2rem;
}
.section-label::before { content: ''; display: block; width: 24px; height: 1px; background: var(--gold); }
/* On dark bg: color: var(--gold-light) — ::before background stays var(--gold) */
```

### Buttons
```html
<a class="btn-primary" href="#">Gold button</a>               <!-- dark bg -->
<a class="btn-primary" style="background:var(--forest);color:var(--cream);" href="#">Forest button</a>  <!-- light bg -->
<a class="btn-secondary" href="#">Ghost button</a>            <!-- dark bg only -->
```

### Dark grid cards (varieties / grades / origins)
- Parent: `gap: 1px; background: rgba(245,240,232,0.07);`
- Card hover: `rgba(245,240,232,0.04)` + gold bottom-border via `::after { scaleX(0→1) }`
- Ghost number: Cormorant Garamond 3rem, `rgba(184,146,74,0.2)`

### Specs grid
- `gap: 1px; background: var(--border);` on grid, `background: var(--warm-white)` on cells
- `.spec-key` 0.6rem uppercase `var(--text-light)` · `.spec-val` Cormorant 1.05rem `var(--forest)`

### Process steps
- 5-col grid, horizontal connector via `::before` on `.process-steps`
- Step circle: 56px, `border: 1px solid var(--border)`, numeral in `var(--gold)`

### FAQ accordion
- `.faq-item.open .faq-a { max-height: 300px; }` — height transition
- Chevron: `transform: rotate(180deg)` on open

### Footer
- `grid-template-columns: 2fr 1fr 1fr 1fr` — collapses to 2-col at 1024px, 1-col at 480px
- Background `#111612`, link colour `rgba(245,240,232,0.35)` → hover `var(--gold-light)`

---

## 10. Fade-up Animation

```css
.fade-up { opacity: 1; transform: none; }
.js-animate .fade-up { opacity: 0; transform: translateY(28px); transition: opacity 0.7s ease, transform 0.7s ease; }
.js-animate .fade-up.visible { opacity: 1; transform: translateY(0); }
```

```js
(function() {
  if (!('IntersectionObserver' in window)) {
    document.body.classList.add('js-animate');
    document.querySelectorAll('.fade-up').forEach(function(el) { el.classList.add('visible'); });
    return;
  }
  document.body.classList.add('js-animate');
  var observer = new IntersectionObserver(function(entries) {
    entries.forEach(function(entry) {
      if (entry.isIntersecting) { entry.target.classList.add('visible'); observer.unobserve(entry.target); }
    });
  }, { threshold: 0, rootMargin: '0px 0px -40px 0px' });
  document.querySelectorAll('.fade-up').forEach(function(el) { observer.observe(el); });
  setTimeout(function() {
    document.querySelectorAll('.fade-up:not(.visible)').forEach(function(el) { el.classList.add('visible'); });
  }, 800);
})();
```

---

## 11. Formspree Endpoints

| Form | File | Endpoint | Status |
|---|---|---|---|
| Contact | `index.html` | `mdawjowa` | Live |
| Farmer partnership | `about.html` | `xreydgrv` | Live |
| Exporter quote | `exporter-quote.html` | `xwvrzkaz` | Live |
| Coffee quote | `coffee.html` | — | Fake setTimeout — wire when ready |
| Moringa quote | `moringa.html` | — | Fake setTimeout — wire when ready |
| Fruit chips quote | `fruit-chips.html` | — | Fake setTimeout — wire when ready |
| Cashew quote | `cashew.html` | — | Fake setTimeout — wire when ready |

---

## 12. Contact Info

- **Email:** hello@hindiatimur.com
- **WhatsApp:** +62 (XXX) XXX-XXXX ← **placeholder — replace sitewide when number is confirmed**

---

## 13. Coding Conventions

- Single-file HTML — all CSS in `<style>`, all JS in one `<script>` at bottom of `<body>`
- No frameworks — vanilla HTML/CSS/JS only
- Border radius: `2px` only
- Transitions: `0.2s–0.35s` hover · `0.7s` scroll animations
- SVG icons: `stroke="currentColor"` so colour inherits
- No inline styles except one-off colour overrides

**Critical: Script closing rule**
```
    })();
  </script>
  </body>
  </html>
```
Never `})();` directly before `</body>` — unclosed `<script>` silently swallows all following HTML including the footer.

**Critical: Post-nav bar on blog posts must be `<div>`, not `<nav>`**
Using `<nav class="post-nav">` causes it to inherit `position: fixed` and float over the footer.

---

## 14. Pages Still To Build

| Page | Priority | Notes |
|---|---|---|
| `vanilla.html` | High | Direct exporter product — same template as coffee.html |
| `cacao.html` | High | — |
| `honey.html` | Medium | Raw forest honey |
| `agarwood.html` | Medium | CITES Appendix II — requires compliance note |
| `gula-aren.html` | Medium | Palm sugar |
| Remaining 11 product slugs | Lower | See products.html catalog for full list |
| Sitemap domain update | Medium | Change `dionwicaksono.github.io/hindiatimur-html/` → `hindiatimur.com/` at domain switch |

---

## 15. Known Issues / Tech Debt

| Issue | Files | Priority |
|---|---|---|
| WhatsApp number placeholder | All pages | High — replace `+62 (XXX) XXX-XXXX` sitewide |
| Formspree not wired on product pages | `coffee.html`, `moringa.html`, `fruit-chips.html`, `cashew.html` | Medium |
| Hero `padding-top` inconsistency | All product pages | Low — works correctly but pattern differs per page, standardise next time each file is edited |
| `faq.html` nav | `faq.html` | Low — transparent nav with no hero image may look odd on load |
| Sitemap domain | `sitemap.xml` | Medium — update at domain switch |
| Blog active state | All blog posts | Low — all mark "Blog" active, no differentiation per post |

---

## 16. Session History Summary

### Pre-Claude sessions (early April 2026)
Initial build: `index.html`, `products.html`, `coffee.html`, `about.html`, `exporter-quote.html`, 6 blog posts.

### April 12, 2026
- Fixed Cloudflare-broken JS on `index.html` (swallowed inline scripts)
- Restored truncated `handleSubmit`; fixed Cloudflare-obfuscated email
- Hamburger nav added to all 5 main pages

### April 14, 2026
- Hamburger nav added to 3 missing blog posts
- Stale filename refs replaced sitewide (`hindiatimur__6_.html` → `index.html` etc.)
- Formspree wired to 3 forms: index, about, exporter-quote
- Logo `.png` → `.webp` sitewide including JSON-LD blocks
- Blog post nav scroll transform fixed (conflicting `nav` vs `nav#nav` selectors)
- `<nav class="post-nav">` → `<div class="post-nav">` on all 6 blog posts
- Mobile nav style leak fixed on 3 blog posts

### April 18, 2026
- Missing `</script>` closing tag fixed on 3 blog posts (was swallowing footer HTML)
- Mismatched `</nav>` → `</div>` on post-nav bar (vanilla + coconut blog posts)
- Nav selector standardised sitewide: all plain `nav` blocks replaced with `nav#nav`
- Hamburger bar colour unified to `var(--gold)` on all 13 pages
- Nav redesign: new uniform link structure (Products | About ▾ | FAQ | Contact | CTA)
- About dropdown added to all pages (desktop hover + mobile tap-expand)
- Footer standardised to 4-column layout sitewide

### April 2026 — Current session
- `moringa.html` — Moringa Powder product page created
- `fruit-chips.html` — Fruit Chips product page created; 7 varieties (Jackfruit, Banana, Pineapple, Coconut, Mango, Salak, Mixed); white-bar fix applied correctly (padding-top on `.hero-content` not `.product-hero`)
- Coconut chips added to `fruit-chips.html` (hero switcher, profile panel, variety card, spec list, form dropdown)
- `cashew.html` — Cashew Nuts product page created; cream fixed nav (experimental — `← NAV BG` comment left in CSS for easy swapping); W-grade switcher; 6-grade reference section; HACCP and aflatoxin compliance content
- `PROJECTS.md` fully rewritten to reflect current state
