# Portfolio TODO

## Completed

- [x] **1. `baseurl` and `url` in `_config.yml`** — Custom domain `portfolio.joeuong.com` configured; `baseurl: ""` correct for subdomain root.
- [x] **2. "View Projects" link** — Fixed to `/projects`.
- [x] **3. Contact information** — LinkedIn added to footer.
- [x] **4. Institutional context on homepage** — UF, CLAS, 60,000+ students, top-10 public university.
- [x] **5. Two missing projects** — CLAS Registration Dashboard and Unique Waitlist Demand Reporting added to projects page and homepage.
- [x] **6. Close2Grad** — Added to projects page (#3) and homepage.
- [x] **7. `writing.md` dead-end** — Deleted.
- [x] **8. Generic opening line** — Homepage intro rewritten with technical depth + institutional navigation angle.
- [x] **9. Bullet list capitalization** — Fixed.
- [x] **12. Nav title** — Changed to "Joe Uong".
- [x] **13. About page** — Created with corrected career arc (UF Registrar → COMPASS → BI Analyst → CLAS). Added to nav.

---

## Open

### Layout / Navigation

- [x] **A. About page nav position** — Moved to second: Home → About → Projects → Professional Activity.

### Professional Activity Page

- [x] **10. Table overflow on mobile** — Resolved via item N: tables now scroll horizontally on small screens (`display: block; overflow-x: auto; white-space: nowrap` under the mobile breakpoint), so the 7-column Presentations table no longer breaks the layout. No content restructuring needed.

- [x] **11. Emojis** — Closed. Professional Activity headings already had no emojis; the last emoji on the site (`➡️` before "View Projects") was replaced with a styled `.cta` button whose `→` arrow is a CSS pseudo-element (accent-blue pill, arrow nudges right on hover). The site is now emoji-free.

---

## New Items

### Repo Hygiene

- [x] **B. `Joe_Accomplishments.md` is publicly accessible** — Renamed to `_Joe_Accomplishments.md`; Jekyll will ignore it.

- [x] **C. Orphaned files cleaned up** — Deleted `projects/advising-analytics.md`, `projects/project_template.md`, and `archive/presentations.md`.

### Content

- [x] **D. CLAS Instructor Workload — strong quote not yet used**
  Added Trysh Travis quote to homepage: *"This would not have been possible without Joe Uong's swift and clever buildout of the data."*

- [ ] **E. Internal web apps not yet in portfolio**
  Three live tools co-built with Dan Shields (he handled front-end):
  - Cancel Non-Pay web app — tracks re-enrollment after cancellation
  - CLAS Foreign Language Courses app — custom display supplementing UF registration
  - CLAS Advising Candidate Evaluation portal — collects hiring evaluations online
  These demonstrate full-stack thinking even if backend-focused. Worth a brief mention or a grouped "Internal Tools" entry on the projects page.

- [x] **F. Leadership roles not surfaced anywhere**
  Added Service & Leadership section to Professional Activity page: UAC Finance Committee Chair/Steering Committee, CLAS Staff Council, SAM workgroup, Data@UF, AOTW.

- [x] **G. About page — published paper** — Added note to education section: doctoral coursework produced a peer-reviewed publication in the *Community College Journal of Research and Practice* (2017). Framed as research output, not a community college specialization.

---

## Suggested (Portfolio Review — 2026-06-03)

New items from a full review of the site source. Ordered roughly by impact-to-effort.

### SEO & Discoverability (highest leverage — this is a portfolio meant to be shared)

- [x] **H. Social-share preview (Open Graph / Twitter Cards)** — Done. Added Open Graph (`og:type/site_name/title/description/url/image`) and Twitter card meta tags to `_layouts/default.html`, so a preview card now renders when the link is shared on LinkedIn, Slack, iMessage, etc. Titles/descriptions are per-page (`page.description | default: site.description`); the meta description now uses the same fallback, which also covers item I. Works alongside `noindex` — social scrapers read these tags regardless of search indexing.
  - **Follow-up — done:** added a branded 1200×630 share image (`assets/images/og-share.png`, dark theme + name/tagline/URL + logo) and switched the card to `summary_large_image` with `og:image:width/height` set. Links now render a full-width banner preview.

- [ ] **I. Every page emits the same `<meta name="description">`**
  `default.html` hard-codes `{{ site.description }}` for all pages, so Home, About, Projects, and Professional Activity share one generic description. Add a `description:` key to each page's front matter and fall back to `site.description` (`{{ page.description | default: site.description }}`), or let `jekyll-seo-tag` handle it.

- [x] **J. Search-engine visibility** — Decided *against* a sitemap. Goal reversed to keeping the site out of search results: added a site-wide `<meta name="robots" content="noindex, nofollow">` to `_layouts/default.html`. Note: this hides the site from search engines but does **not** make it private — the custom domain remains publicly accessible to anyone with the URL. Crawling is intentionally left unblocked (no `robots.txt` disallow) so crawlers can read the `noindex` and actually drop the pages.

- [ ] **K. Add JSON-LD `Person` structured data**
  A `Person` schema block on the homepage (name, jobTitle, worksFor: University of Florida, sameAs: LinkedIn) gives search engines and AI assistants a clean machine-readable identity. Low effort, good for a name-based search ("Joe Uong UF data").

### Accessibility

- [ ] **L. No skip-to-content link**
  Keyboard and screen-reader users must tab through the full nav on every page. Add a visually-hidden "Skip to content" link that targets the `<main>` element.

- [ ] **M. Verify low-contrast text against WCAG AA**
  Footer text is `#555` on `#141414` (≈2.8:1 — below the 4.5:1 AA threshold). Muted `small`/tagline text uses `#999`. Audit these and bump the dim colors until they pass AA, or accept them deliberately.

### Mobile / CSS

- [x] **N. Make wide tables horizontally scrollable (addresses open item #10)** — Done. Added a rule under the `max-width: 700px` breakpoint in `style.scss` making tables `display: block; overflow-x: auto; white-space: nowrap`, so any overflowing table scrolls horizontally rather than collapsing. Fixes every current and future table; closed item #10.

### Content

- [ ] **O. Add a downloadable résumé / CV (PDF)**
  Standard expectation for a portfolio and currently absent. Drop a PDF in `assets/` and link it from the nav or About page header.

- [ ] **P. Add a direct contact method**
  The only contact channel is the LinkedIn nav link. Consider a `mailto:` (or a simple contact line on About) so a visitor who isn't on LinkedIn can still reach out.

- [ ] **Q. Homepage quote block leans on a single source**
  All four homepage testimonials are drawn from the UF HR Superior Accomplishment nomination packet. They're strong, but varying the sourcing (e.g. surface one from a peer/partner office) would read as broader endorsement and reduce repetition of the same parenthetical attribution.

- [ ] **E. (still open) Internal web apps not yet in portfolio** — see "Content" above; carry over the Cancel Non-Pay, Foreign Language Courses, and Advising Candidate Evaluation tools as a grouped "Internal Tools" entry.

### Repo Hygiene / Developer Experience

- [ ] **R. No `README.md`**
  Add a short README documenting what the site is, the page/layout structure, how to build locally, and the deploy path (GitHub Pages → `portfolio.joeuong.com` via CNAME). Helps future-you and anyone reviewing the repo.

- [ ] **S. No `Gemfile`**
  Pin the `github-pages` gem in a `Gemfile` for reproducible local builds (`bundle exec jekyll serve`) that match the GitHub Pages build environment.

- [ ] **T. Doc drift on completed item #3**
  Item #3 reads "LinkedIn added to footer," but LinkedIn currently lives in the nav and the footer shows only the copyright line. Reword #3 (or add the LinkedIn link to the footer too) so the record matches the site.
