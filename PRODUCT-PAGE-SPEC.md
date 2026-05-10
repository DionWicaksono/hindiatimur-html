# Hindia Timur — Individual Product Page Specification

> **Reference file:** `sandalwood.html` (verified clean, May 2026)
> Apply this spec to every `/products/[slug].html` page. Do not deviate without updating this document.

---

## Page structure (in order)

```
<nav id="nav">          ← fixed, transparent overlay
<div id="mobileMenu">   ← fullscreen overlay
<div class="page-offset">
  <div class="direct-exporter-bar">   ← gold announcement strip
  <section class="product-hero">      ← split hero: image left, content right
</div>
<div class="trust-bar">              ← 4 trust signals
<section class="specs-section">      ← 2-col: specs+certs left / formats right
<section class="faq-section">        ← 2-col FAQ accordion
<section class="cta-section">        ← 2-col: copy left / quote form right
<footer>
```

---

## 1. Nav

**Type:** Transparent overlay → scroll swap. All product pages use this type (confirmed April 20, 2026 redesign). Never use the fixed light-bar type.

**Behaviour:**
- Default: transparent, `flex-direction: column`, logo centered
- On scroll (>20px): opaque warm-white row, logo image → logotype text
- JS threshold: `window.scrollY > 20`

**Logo sizes:** 130px desktop, 100px mobile (≤768px)

**Link order:** Products | About ▾ | FAQ | Contact | [Request a Quote]

**About dropdown sub-links:**
- Our Story → `about.html`
- How It Works → `index.html#process`
- Compliance → `index.html#compliance`
- For Farmers → `about.html#farmers`

**Link colours:**
| State | Links | Dropdown toggle |
|---|---|---|
| Default (transparent) | `rgba(245,240,232,0.85)` | same |
| Hover (transparent) | `var(--gold-light)` | same |
| Scrolled | `var(--text-mid)` | same |
| Hover (scrolled) | `var(--gold)` | same |

**CTA button `.nav-cta`:**
- Default: ghost — `background: rgba(245,240,232,0.15)`, `border: 1px solid rgba(245,240,232,0.35)`, text cream
- Scrolled: solid `var(--forest)` background, text cream
- Hover (either state): `var(--gold)` background, `var(--forest)` text

**Hamburger bars:** `var(--gold)` on all pages. Never `var(--forest)`, never `rgba(...)`.

**`page-offset` value:** `padding-top: 0` — the hero sits behind the transparent nav, no offset needed.

### Canonical nav CSS block

```css
nav#nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 200;
  display: flex; flex-direction: column; align-items: center;
  padding: 18px 5vw 12px;
  background: transparent;
  backdrop-filter: none;
  transition: background 0.35s, box-shadow 0.35s, padding 0.35s;
}
nav#nav.scrolled {
  flex-direction: row; justify-content: space-between; align-items: center;
  padding: 0 5vw; height: 64px;
  background: rgba(245,239,228,0.97);
  backdrop-filter: blur(14px);
  box-shadow: 0 1px 12px rgba(0,0,0,0.09);
}

.nav-logo { display: block; text-decoration: none; line-height: 0; margin-bottom: 10px; }
nav#nav.scrolled .nav-logo { margin-bottom: 0; }
.nav-logo-img-main {
  display: block; width: 130px; height: auto;
  transition: opacity 0.25s, width 0.25s;
}
nav#nav.scrolled .nav-logo-img-main { width: 0; opacity: 0; pointer-events: none; overflow: hidden; }
.nav-logo-img-scrolled {
  display: block; font-family: 'Cormorant Garamond', serif;
  font-size: 1.55rem; font-weight: 600; color: var(--forest);
  white-space: nowrap; line-height: 1;
  width: 0; opacity: 0; overflow: hidden;
  transition: opacity 0.25s, width 0.25s; pointer-events: none;
}
.nav-logo-img-scrolled span { color: var(--gold); }
nav#nav.scrolled .nav-logo-img-scrolled { width: auto; opacity: 1; pointer-events: auto; overflow: visible; }

.nav-links {
  display: flex; gap: 2rem; list-style: none; align-items: center;
  font-size: 0.78rem; font-weight: 500; letter-spacing: 0.12em; text-transform: uppercase;
}
.nav-links a { text-decoration: none; color: rgba(245,240,232,0.85); transition: color 0.2s; }
.nav-links a:hover { color: var(--gold-light); }
.nav-links a.active { color: var(--cream); }
nav#nav.scrolled .nav-links a { color: var(--text-mid); }
nav#nav.scrolled .nav-links a:hover { color: var(--gold); }
nav#nav.scrolled .nav-links a.active { color: var(--forest); }
.nav-cta {
  background: rgba(245,240,232,0.15) !important; color: var(--cream) !important;
  border: 1px solid rgba(245,240,232,0.35);
  padding: 0.4rem 1.1rem; border-radius: 2px;
  transition: background 0.2s, border-color 0.2s !important;
}
.nav-cta:hover { background: var(--gold) !important; border-color: var(--gold) !important; color: var(--forest) !important; }
nav#nav.scrolled .nav-cta { background: var(--forest) !important; border-color: var(--forest) !important; color: var(--cream) !important; }
nav#nav.scrolled .nav-cta:hover { background: var(--gold) !important; border-color: var(--gold) !important; color: var(--forest) !important; }

.nav-dropdown { position: relative; }
.nav-dropdown-toggle {
  display: flex; align-items: center; gap: 0.3rem; cursor: pointer;
  background: none; border: none; padding: 0;
  font-size: 0.78rem; font-weight: 500; letter-spacing: 0.12em; text-transform: uppercase;
  color: rgba(245,240,232,0.85); transition: color 0.2s;
}
.nav-dropdown-toggle:hover { color: var(--gold-light); }
nav#nav.scrolled .nav-dropdown-toggle { color: var(--text-mid); }
nav#nav.scrolled .nav-dropdown-toggle:hover { color: var(--gold); }
.dropdown-chevron { width: 10px; height: 6px; transition: transform 0.2s; flex-shrink: 0; }
.nav-dropdown:hover .dropdown-chevron,
.nav-dropdown:focus-within .dropdown-chevron { transform: rotate(180deg); }
.nav-dropdown-menu {
  display: none; list-style: none; padding: 0.5rem 0;
  position: absolute; top: calc(100% + 1rem); left: 50%;
  transform: translateX(-50%);
  min-width: 175px; background: var(--forest);
  border: 1px solid rgba(245,240,232,0.1); border-radius: 2px;
  box-shadow: 0 8px 32px rgba(0,0,0,0.3); z-index: 201;
}
.nav-dropdown:hover .nav-dropdown-menu,
.nav-dropdown:focus-within .nav-dropdown-menu { display: block; }
.nav-dropdown-menu li a {
  display: block; padding: 0.55rem 1.2rem;
  font-size: 0.72rem; letter-spacing: 0.1em; text-transform: uppercase;
  color: rgba(245,240,232,0.7) !important; white-space: nowrap;
  transition: color 0.2s, background 0.2s; text-decoration: none;
}
.nav-dropdown-menu li a:hover { color: var(--gold-light) !important; background: rgba(245,240,232,0.05); }

.nav-hamburger {
  display: none;
  flex-direction: column; justify-content: center; align-items: center;
  gap: 5px; width: 40px; height: 40px;
  background: none; border: none; cursor: pointer; padding: 4px; z-index: 301;
}
.nav-hamburger span {
  display: block; width: 22px; height: 1.5px;
  background: var(--gold); border-radius: 2px;
  transition: transform 0.35s cubic-bezier(0.23,1,0.32,1), opacity 0.25s, width 0.3s;
  transform-origin: center;
}
.nav-hamburger.open span:nth-child(1) { transform: translateY(6.5px) rotate(45deg); }
.nav-hamburger.open span:nth-child(2) { opacity: 0; width: 0; }
.nav-hamburger.open span:nth-child(3) { transform: translateY(-6.5px) rotate(-45deg); }
```

### Mobile media query additions (≤768px)

```css
@media (max-width: 768px) {
  .nav-links { display: none !important; }
  .nav-hamburger { display: flex; }
  .mobile-menu { display: flex; }
  .nav-logo-img-main { width: 100px; }
}
```

### Canonical nav JS (one block, no duplicates)

```js
const nav = document.getElementById('nav');
window.addEventListener('scroll', () => nav.classList.toggle('scrolled', window.scrollY > 20), { passive: true });

(function() {
  var btn  = document.getElementById('navHamburger');
  var menu = document.getElementById('mobileMenu');
  if (!btn || !menu) return;
  function openMenu() {
    btn.classList.add('open'); menu.classList.add('open');
    btn.setAttribute('aria-expanded', 'true');
    document.body.style.overflow = 'hidden';
  }
  function closeMenu() {
    btn.classList.remove('open'); menu.classList.remove('open');
    btn.setAttribute('aria-expanded', 'false');
    document.body.style.overflow = '';
  }
  btn.addEventListener('click', function() {
    menu.classList.contains('open') ? closeMenu() : openMenu();
  });
  menu.querySelectorAll('a').forEach(function(a) { a.addEventListener('click', closeMenu); });
  var closeBtn = document.getElementById('mobileMenuClose');
  if (closeBtn) closeBtn.addEventListener('click', closeMenu);
  document.addEventListener('keydown', function(e) { if (e.key === 'Escape') closeMenu(); });

  menu.querySelectorAll('.mobile-dropdown-toggle').forEach(function(toggle) {
    toggle.addEventListener('click', function(e) {
      e.preventDefault(); e.stopPropagation();
      var submenu = toggle.parentElement.querySelector('.mobile-dropdown-menu');
      if (!submenu) return;
      var isOpen = submenu.classList.contains('open');
      menu.querySelectorAll('.mobile-dropdown-menu').forEach(function(m) { m.classList.remove('open'); });
      menu.querySelectorAll('.mobile-dropdown-toggle').forEach(function(t) { t.setAttribute('aria-expanded', 'false'); });
      if (!isOpen) { submenu.classList.add('open'); toggle.setAttribute('aria-expanded', 'true'); }
    });
  });
})();
```

---

## 2. Direct exporter bar

Gold `#B8924A` strip immediately below the hero (but inside `page-offset`). Text and icon in `var(--forest)`. Customise the message per product — e.g. CITES for sandalwood/agarwood, organic for moringa.

```html
<div class="direct-exporter-bar">
  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><!-- icon --></svg>
  PRODUCT-SPECIFIC compliance message here.
</div>
```

---

## 3. Product hero

Two-column grid (`1fr 1fr`), min-height `calc(90vh - 36px)` on desktop.

### Left panel — hero image

- Full-bleed image with `object-fit: cover`
- Dark gradient overlay (corner + bottom)
- Two stacked badges bottom-left: **origin badge** (cream bg) + **certification badge** (gold bg)

**Badge sizing — canonical values:**
```css
.origin-badge, .score-badge {
  font-size: 0.62rem;
  padding: 0.4rem 0.75rem;
  letter-spacing: 0.12em;
  border-radius: 2px;
}
.origin-badge svg { width: 10px; height: 10px; }   /* pin icon */
```

For the certification badge, if using a star icon: set explicit `width="10" height="10"` on the SVG and use `fill="currentColor" stroke="none"` so it renders solid at small size. Do not use stroked star — it looks oversized.

```html
<!-- origin badge -->
<div class="origin-badge">
  <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
    <path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7z"/>
  </svg>
  Region &middot; Region
</div>

<!-- certification badge -->
<div class="score-badge">
  <svg width="10" height="10" viewBox="0 0 24 24" fill="currentColor" stroke="none">
    <path d="M12 2l2 7h7l-5.5 4 2 7L12 16l-5.5 4 2-7L3 9h7z"/>
  </svg>
  Certification Label
</div>
```

**Region in origin badge must match the specs table.** Do not default to Kalimantan/Sumatra. Double-check per product.

### Right panel — hero content

Dark `var(--forest)` background with radial gradient accent. Contains:
- Breadcrumb: Home / Products / Product Name
- Eyebrow label (product category)
- `<h1>` in Cormorant Garamond
- Tagline (italic, Cormorant)
- Description paragraph
- Two CTA buttons

**Button sizing — canonical values:**
```css
.btn-primary {
  font-size: 0.72rem;
  padding: 0.65rem 1.2rem;
  gap: 0.4rem;
}
.btn-primary svg { width: 13px; height: 13px; }

.btn-secondary {
  font-size: 0.72rem;
  padding: 0.65rem 1.2rem;
}
```

Do not use `font-size: 0.78rem` or `padding: 0.8rem 1.5rem` — these are the oversized values from the original template.

---

## 4. Trust bar

Four items separated by 1px dividers. Always 4 items on product pages. Customise labels per product (e.g. "CITES Permit Included" for sandalwood, "Organic Certified" for moringa).

---

## 5. Specs section

Two-column grid (`1fr 1fr`, `gap: 6rem`). `align-items: start` — columns are independently top-aligned.

### Left column — specs + certs

**HTML nesting rule (critical):** The `certs-title` and `certs-list` divs must be **inside** the same `<div>` as the `specs-grid`. The original template had a misplaced closing `</div>` that broke this — the column closed before the certs, making them span full width on desktop.

Correct structure:
```html
<section class="specs-section">
  <div>                              ← LEFT COLUMN OPENS
    <div class="section-label">...</div>
    <h2 class="section-h2">...</h2>
    <p class="section-lead">...</p>
    <div class="specs-grid">
      <!-- spec-item rows -->
    </div>
    <div class="certs-title">Certifications &amp; Documentation</div>
    <div class="certs-list">
      <span class="cert-tag">...</span>
    </div>
  </div>                             ← LEFT COLUMN CLOSES HERE

  <div>                              ← RIGHT COLUMN
    ...supply formats...
  </div>
</section>
```

**Specs grid** is `grid-template-columns: 1fr 1fr` (collapses to `1fr` on mobile ≤768px).

### Right column — supply formats

Stacked list of format items (powder / chips / oil / etc.), each with a small icon, name, and description. Ends with a `btn-primary` CTA.

---

## 6. FAQ section

2-column accordion grid (collapses to 1-col on ≤1024px). Minimum 4 FAQs, maximum 6. Each product should have at least 2 product-specific questions; the last 2-3 can be generic (MOQ, packaging, quote turnaround).

---

## 7. CTA section (quote form)

Two-column: copy/checklist left, inline form right.

**Form rules:**
- Must be wrapped in `<form>` tag with `onsubmit="handleSubmit(event)"` — not a bare `<div>`
- Every input/select/textarea must have a `name=` attribute or Formspree will not receive the data
- Submit button: `<button type="submit" id="[product]SubmitBtn">`
- Use **real async Formspree fetch** — never `setTimeout` fake submission

**Formspree endpoint:** Use `xwvrzkaz` (exporter-quote endpoint) unless a dedicated endpoint is created per product.

**Canonical form submit handler:**
```js
async function handleSubmit(e) {
  e.preventDefault();
  var btn = document.getElementById('[product]SubmitBtn');
  var original = btn.textContent;
  btn.textContent = 'Sending…'; btn.disabled = true;
  try {
    var response = await fetch('https://formspree.io/f/xwvrzkaz', {
      method: 'POST',
      body: new FormData(e.target),
      headers: { 'Accept': 'application/json' }
    });
    if (response.ok) {
      btn.textContent = '✓ Inquiry Sent';
      btn.style.background = 'var(--sage)';
      e.target.reset();
    } else {
      btn.textContent = 'Error — Try Again';
      btn.style.background = '#c0392b';
    }
    setTimeout(function() {
      btn.textContent = original; btn.disabled = false; btn.style.background = '';
    }, 3000);
  } catch(err) {
    btn.textContent = 'Error — Try Again'; btn.style.background = '#c0392b';
    setTimeout(function() {
      btn.textContent = original; btn.disabled = false; btn.style.background = '';
    }, 3000);
  }
}
```

---

## 8. Footer

4-column grid (`2fr 1fr 1fr 1fr`). Canonical column content:

| Col | Title | Links |
|---|---|---|
| 1 | — | Logo + tagline |
| 2 | Source | Specialty Coffee · Full Product Catalog · Request a Quote |
| 3 | Company | About Hindia Timur · How It Works · For Farmers · FAQ |
| 4 | Connect | hello@hindiatimur.com · WhatsApp · Blog & Insights · Contact Us |

No `href="#"` except WhatsApp (real number still pending sitewide). Do not add product-specific links like `vanilla.html` to the footer until those pages exist.

---

## 9. Script block — closing tag rule

The script block must always close correctly. Last four lines of the file must be:

```
  })();
</script>
</body>
</html>
```

An unclosed `</script>` silently swallows everything after it including the footer. If the footer is missing or truncated, this is the first thing to check.

---

## 10. Hero text / nav overlap

**Why this happens:** `page-offset` is `padding-top: 0` on product pages because the transparent nav floats over the hero image. On desktop this is fine — the hero is a side-by-side split and the nav overlaps only the image panel (left), not the content panel (right). But on tablet/mobile (≤1024px) the hero stacks to a single column: image on top, content panel below. The content panel's top padding alone (`4rem` at ≤1024px, `3rem` at ≤480px) is not enough to guarantee the first line of text — breadcrumb or eyebrow — clears the fixed nav bar (64px).

**Rule:** Always add `padding-top` to the first text element inside `.hero-content` — whichever appears first in the HTML, breadcrumb or eyebrow. Do not rely on `.hero-content`'s own padding alone.

**Canonical values:**

```css
/* Desktop: hero is side-by-side, nav overlaps image panel only.
   Extra top padding on content panel is not needed but harmless. */
.breadcrumb,
.product-eyebrow:first-child {
  padding-top: 5rem;   /* matches .hero-content top padding on desktop */
}

/* Tablet: hero stacks, content panel sits below image.
   Nav is fixed at 64px — content needs clearance. */
@media (max-width: 1024px) {
  .breadcrumb,
  .product-eyebrow:first-child {
    padding-top: 5.5rem;   /* 64px nav + comfortable breathing room */
  }
}

/* Mobile */
@media (max-width: 768px) {
  .breadcrumb,
  .product-eyebrow:first-child {
    padding-top: 5rem;
  }
}
```

**Implementation note:** Only one of `.breadcrumb` or `.product-eyebrow` will be the first element — check the HTML. If the page opens with a breadcrumb, apply `padding-top` to `.breadcrumb`. If it opens directly with the eyebrow (no breadcrumb), apply it to `.product-eyebrow`. Do not apply to both — that doubles the gap.

**Quick visual test:** Scroll back to top on a mobile viewport. The breadcrumb or eyebrow text should be fully visible below the nav bar with a small gap, never hidden behind it.

---

## Quick audit checklist

When reviewing a new product page before shipping, check every item:

- [ ] Nav type: transparent overlay (not fixed light bar)
- [ ] Logo: 130px desktop, 100px mobile
- [ ] Scroll JS threshold: `window.scrollY > 20`
- [ ] Nav link colors correct for transparent + scrolled states (see table in §1)
- [ ] Hamburger spans: `var(--gold)`
- [ ] `page-offset`: `padding-top: 0`
- [ ] Origin badge region matches specs table
- [ ] Certification badge icon: solid fill, explicit `width="10" height="10"`
- [ ] Button sizing: `font-size: 0.72rem`, `padding: 0.65rem 1.2rem`
- [ ] Badge sizing: `font-size: 0.62rem`, `padding: 0.4rem 0.75rem`
- [ ] `certs-title` / `certs-list` inside the left column `<div>` (not after it)
- [ ] First hero text element (breadcrumb or eyebrow) has `padding-top` to clear the nav — test at mobile viewport
- [ ] Form wrapped in `<form>` tag, all inputs have `name=` attributes
- [ ] Form uses real `fetch()` to Formspree, not `setTimeout`
- [ ] Footer uses canonical 4-column structure
- [ ] No stale links to unbuilt pages (e.g. `vanilla.html`)
- [ ] `</script>` present before `</body>`
- [ ] One JS hamburger IIFE only — no duplicates
