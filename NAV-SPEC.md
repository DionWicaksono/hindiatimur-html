# Hindia Timur — Nav Header Specification

> **Status: Closed.** All 13 pages verified clean as of April 18, 2026.  
> Do not re-open nav header issues without consulting this document first.

---

## What the nav does (the full contract)

### 1. Centered logo — default state
- Nav sits in `flex-direction: column`, `align-items: center`
- Logo image (`hindia-timur-logo.webp`) is centered, `width: 110px` desktop / `80px` mobile
- Nav links are hidden by default on transparent-overlay pages; always visible on light-bar pages

### 2. Logo → logotype transform on scroll
- JS adds `.scrolled` class to `<nav id="nav">` when `window.scrollY > 20`
- On `.scrolled`: nav switches to `flex-direction: row`, `justify-content: space-between`
- `.nav-logo-img-main` collapses: `width: 0; opacity: 0`
- `.nav-logo-img-scrolled` expands: `width: auto; opacity: 1`
- Logotype text: `Hindia <span>Timur</span>` — "Timur" in `var(--gold)`

### 3. Hamburger — mobile (≤768px)
- `.nav-links` hidden with `display: none !important`
- Hamburger button shown: 3 bars → animates to × on open
- Fullscreen overlay opens: `var(--forest)` bg, opacity/transform transition (NOT display toggle)
- Overlay contains: logo image → × close button → nav links → footer tagline
- Closes on: × button click, any link click, Escape key, hamburger re-click

---

## Two nav types in use

| Type | Pages | Default state |
|---|---|---|
| **Light fixed bar** | `index.html`, `about.html`, `exporter-quote.html`, `coffee.html`, `faq.html`, `blog.html` | Always opaque warm-white, `height: 64–72px` |
| **Transparent overlay → scroll swap** | All 6 blog posts, `products.html` | Transparent over hero image, transforms to light bar on scroll |

Both types use the same scroll JS, same logo swap CSS, same hamburger system.

---

## Canonical HTML (inside `<nav id="nav">`)

```html
<nav id="nav">
  <a href="index.html" class="nav-logo">
    <img class="nav-logo-img-main" src="hindia-timur-logo.webp" alt="Hindia Timur">
    <span class="nav-logo-img-scrolled">Hindia <span>Timur</span></span>
  </a>
  <ul class="nav-links">
    <li><a href="products.html">Products</a></li>
    <li><a href="index.html#compliance">Compliance</a></li>
    <li><a href="about.html">About</a></li>
    <li><a href="blog.html">Blog</a></li>
    <li><a href="exporter-quote.html" class="nav-cta">Request a Quote</a></li>
  </ul>
  <button class="nav-hamburger" id="navHamburger" aria-label="Open menu" aria-expanded="false">
    <span></span><span></span><span></span>
  </button>
</nav>

<div class="mobile-menu" id="mobileMenu" role="dialog" aria-modal="true" aria-label="Navigation">
  <div class="mobile-menu-logo-wrap">
    <img src="hindia-timur-logo.webp" alt="Hindia Timur">
  </div>
  <button class="mobile-menu-close" id="mobileMenuClose" aria-label="Close menu">&times;</button>
  <ul>
    <!-- same links as desktop nav, active class on current page -->
  </ul>
  <span class="mobile-menu-footer">Hindia Timur &mdash; Indonesia</span>
</div>
```

---

## Canonical CSS (minimum required, light-bar variant)

```css
nav#nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 200;
  display: flex; flex-direction: column; align-items: center;
  padding: 18px 5vw 12px;
  transition: background 0.35s, box-shadow 0.35s, padding 0.35s;
  background: rgba(245,239,228,0.97);
  backdrop-filter: blur(14px);
}
nav#nav.scrolled {
  flex-direction: row; justify-content: space-between; align-items: center;
  padding: 0 5vw; height: 64px;
}

/* Logo image — visible by default, hides on scroll */
.nav-logo { display: block; text-decoration: none; line-height: 0; margin-bottom: 10px; }
nav#nav.scrolled .nav-logo { margin-bottom: 0; }
.nav-logo-img-main {
  display: block; width: 110px; height: auto;
  transition: opacity 0.25s, width 0.25s;
}
nav#nav.scrolled .nav-logo-img-main { width: 0; opacity: 0; pointer-events: none; overflow: hidden; }

/* Logotype text — hidden by default, reveals on scroll */
.nav-logo-img-scrolled {
  display: block; font-family: 'Cormorant Garamond', serif;
  font-size: 1.55rem; font-weight: 600; color: var(--forest);
  width: 0; opacity: 0; overflow: hidden;
  transition: opacity 0.25s, width 0.25s; pointer-events: none;
}
.nav-logo-img-scrolled span { color: var(--gold); }
nav#nav.scrolled .nav-logo-img-scrolled { width: auto; opacity: 1; pointer-events: auto; overflow: visible; }

/* Mobile menu overlay */
.mobile-menu {
  display: none; position: fixed; inset: 0; z-index: 300;
  background: var(--forest); flex-direction: column;
  justify-content: center; align-items: center;
  opacity: 0; transform: translateY(-12px);
  transition: opacity 0.35s cubic-bezier(0.23,1,0.32,1), transform 0.35s cubic-bezier(0.23,1,0.32,1);
  pointer-events: none;
}
/* IMPORTANT: .open uses opacity, NOT display:flex — JS relies on this */
.mobile-menu.open { opacity: 1; transform: translateY(0); pointer-events: all; }

/* Logo inside overlay */
.mobile-menu-logo-wrap { margin-bottom: 2rem; }
.mobile-menu-logo-wrap img {
  display: block; width: 90px; height: auto;
  filter: drop-shadow(0 2px 10px rgba(0,0,0,0.35)); opacity: 0.92;
}

/* × close button */
.mobile-menu-close {
  display: block; margin-bottom: 2rem;
  background: none; border: none; cursor: pointer; padding: 0;
  color: var(--gold-light); font-size: 2rem; line-height: 1;
  opacity: 0.85; transition: opacity 0.2s, transform 0.2s;
}

@media (max-width: 768px) {
  .nav-links { display: none !important; }
  .nav-hamburger { display: flex; }
  .mobile-menu { display: flex; }
}
```

---

## Canonical JS

```js
// Scroll transform
const nav = document.getElementById('nav');
window.addEventListener('scroll', () => nav.classList.toggle('scrolled', window.scrollY > 20), { passive: true });

// Hamburger open/close — ONE block only, no duplicates
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
})();
```

---

## Rules for new pages

- [ ] Copy the canonical HTML block above verbatim
- [ ] Choose nav type (light-bar or transparent-overlay) and use the matching CSS base
- [ ] `.mobile-menu.open` must use `opacity` / `pointer-events` — **never** `display: flex`
- [ ] **One CSS hamburger block only** — do not add a second
- [ ] **One JS hamburger IIFE only** — do not add a second `<script>` block for it
- [ ] Span bar colour: `var(--forest)` on light-bar pages, `rgba(245,240,232,0.9)` on transparent-overlay pages
- [ ] Always include `.mobile-menu-logo-wrap img { width: 90px; }` CSS — logo is unsized without it

---

## Known remaining nav work

- WhatsApp number placeholder `+62 (XXX) XXX-XXXX` needs real number sitewide
- Blog nav "active" state marks Blog on all blog post pages but does not differentiate individual posts (low priority)
- Individual product pages (`/products/[slug]`) not yet built — use transparent-overlay nav type when created

---

## Post-fix note — April 18, 2026

### Root cause of "half footer / no scroll transform" on blog posts

Three blog posts (`blog-coffee-heritage-volcanic.html`, `blog-organic-certification-fair-trade.html`, `blog-seasonal-availability-guide.html`) were missing the closing `</script>` tag on the last script block.

**What happens:** The browser encounters an unclosed `<script>` block and treats everything after it — including footer HTML — as JavaScript. The footer is silently swallowed. The scroll JS inside that block also never executes, so the logo transform never fires.

**Symptom pattern:**
- Footer renders truncated or missing → unclosed `</script>` before `</body>`
- Logo does not transform on scroll → scroll JS is inside the unclosed block
- These two symptoms always appear together for this reason

**Fix:** Added `</script>` before `</body>` on all three files.

**Rule for new pages and edits:** The last `<script>` block must always end with:
```
  })();
</script>
</body>
</html>
```
Never `})();` directly followed by `</body>` — that is always a bug.

---

## Post-fix note — April 18, 2026 (footer split on vanilla + coconut)

**Root cause:** `blog-vanilla-sourcing-journey.html` and `blog-sustainable-coconut-farming.html` had `<div class="post-nav">` opened but closed with `</nav>` instead of `</div>`. The browser parsed the mismatched tag, broke the box model, and rendered the footer split or displaced.

**Fix:** `</nav>` → `</div>` on the post-nav container in both files.

**Rule:** The Previous/Next post bar must always be a `<div>`, never a `<nav>`:
```html
<div class="post-nav">
  <a class="post-nav-item prev" href="...">...</a>
  <a class="post-nav-item next" href="...">...</a>
</div>   ← must be </div>, never </nav>
```
Using `<nav>` causes the element to inherit all `nav` tag CSS (`position: fixed`, `z-index: 200`, `flex-direction: column`, etc.) and float over the footer.
