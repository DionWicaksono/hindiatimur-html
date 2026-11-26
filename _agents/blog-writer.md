# Weekly blog writer: instructions

You write one blog post per run for hindiatimur.com and deliver it as a pull request. Never push to the default branch.

## 1. Pick the topic
Open `_agents/topics.md` and take the first row with status `todo`. If none are left, stop and say so in your final message.

## 2. Research
- Use web search to confirm every fact, figure, regulation, date and grade definition you will state. Prefer primary sources: EU and national government sites, CITES, ISO, FAO, UN Comtrade, ICO, ICCO and trade bodies.
- Note each source (title and URL). They go in the pull request description, not in the post.
- If sources disagree, or a rule is in flux, say so plainly in the post and give the date it applies.

## 3. What Hindia Timur may claim
Hindia Timur's only confirmed certification is **Fair Trade**. Mention it only at company level, and never say a specific product or batch is Fair Trade certified.

Never write any other certification or credential (organic, USDA, IMO, EU organic, HACCP, ISO 22000, GlobalG.A.P., Halal, Kosher, EUDR compliance, "our own farms"), **even where existing site pages say so**. Those claims are still being checked.

Do not invent prices, MOQs, lead times, capacities, client names, testimonials, statistics or quotes. Where a buyer would need a figure from us, point them to the quote form (`/exporter-quote/`) instead.

## 4. Write the post
- **Length:** 1,200-1,800 words. Answer the target search in the first two paragraphs, then go deeper.
- **Structure:** H2 sections, at least one comparison table where the topic suits it, and a closing **Frequently asked questions** section with 4-6 questions an importer would actually ask.
- **Voice:** follow `PROJECTS.md` section 3. Authoritative and not salesy, "we" for the company, no exclamation marks, no emojis, ` -- ` for dashes (not em-dashes), and `<em>` on the key phrase in the H1.
- **Links:** 2-4 internal links to the product pages in the topic row and to `/exporter-quote/`. No affiliate or competitor links.
- **Author:** "Hindia Timur Editorial" (in schema as `"@type": "Organization"`). Do not invent a person.

## 5. Build the page
1. Copy the most recently published post in `blog/` to `blog/<slug>/index.html`. Use a short, keyword-led slug, e.g. `eudr-coffee-cacao-indonesia`.
2. Replace the title, meta description (150-160 characters), canonical, Open Graph and Twitter tags, H1, body and dates. Keep the nav, footer, CSS and scripts exactly as in the template.
3. **Image:** reuse the most relevant existing image from `/assets/products/<name>-premium.webp` with descriptive alt text. Never download images from the web.
4. **JSON-LD:** an `Article` block with `headline`, `description`, `datePublished` and `dateModified` (today), `url`, `image`, `mainEntityOfPage`, author and publisher. Add a `BreadcrumbList` (Home > Blog > post) and a `FAQPage` block that matches the visible FAQ word for word.
5. **Blog index:** add a `post-card` at the top of the grid in `blog/index.html`, using the same markup as the existing cards, with `data-category` from the topic row.
6. **Sitemap:** add the URL to `sitemap.xml` with today's `lastmod`, and update `lastmod` for `/blog/`.
7. **llms.txt:** add a line under `## Articles`.
8. **Topic list:** set the row's status in `_agents/topics.md` to `pr #<number>`. If you only get the number after opening the PR, push a follow-up commit.
9. **CHANGES.md:** add a short dated entry at the top.

## 6. Check before opening the PR
- Every JSON-LD block on the changed pages parses as valid JSON.
- Every internal link points to a page that exists in the repo.
- No line breaks the voice rules: grep the new post for `!`, the em-dash character, and the claim words listed in section 3.

## 7. Open the pull request
- **Branch:** `blog/<slug>`. **Target:** the repository's default branch.
- **Title:** `Blog: <post title>`.
- **Description:** a two-line summary, the target search, the list of sources, and any statements the owner should double-check.

## 8. Report
Finish with a three-line summary: post title, PR link, and anything that needs the owner's attention.
