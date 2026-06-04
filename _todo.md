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

- [ ] **10. Table overflow on mobile**
  The Presentations table has 7 columns with long conference names. Will wrap badly on small screens. Consider collapsing Date and Location into one column, or dropping Location entirely.

- [ ] **11. Emojis in section headings** *(likely stale — re-confirm)*
  🏆, 🎤, 📰 — personal call. As of the 2026-06-03 review, the Professional Activity headings no longer contain emojis; the only emoji left on the site is `➡️` before "View Projects" on the homepage. Decide whether to keep that one and close this item.

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

- [ ] **H. No social-share preview (Open Graph / Twitter Cards)**
  When the site is shared on LinkedIn, Slack, or iMessage, no preview card renders (no title, description, or image). For a portfolio that lives or dies on how it looks when a hiring manager pastes the link, this is the single highest-value fix. Add `og:title`, `og:description`, `og:image`, `og:url`, `og:type`, and `twitter:card` tags to `_layouts/default.html`. Reuse `uong_logo.png` or create a 1200×630 share image. Simplest path: enable the `jekyll-seo-tag` plugin (supported on GitHub Pages) and add `{% seo %}` to `<head>`.

- [ ] **I. Every page emits the same `<meta name="description">`**
  `default.html` hard-codes `{{ site.description }}` for all pages, so Home, About, Projects, and Professional Activity share one generic description. Add a `description:` key to each page's front matter and fall back to `site.description` (`{{ page.description | default: site.description }}`), or let `jekyll-seo-tag` handle it.

- [ ] **J. No sitemap or robots.txt**
  Add the `jekyll-sitemap` plugin (GitHub Pages-supported) to generate `sitemap.xml`, and a small `robots.txt` pointing to it. Improves crawlability and indexing for the custom domain.

- [ ] **K. Add JSON-LD `Person` structured data**
  A `Person` schema block on the homepage (name, jobTitle, worksFor: University of Florida, sameAs: LinkedIn) gives search engines and AI assistants a clean machine-readable identity. Low effort, good for a name-based search ("Joe Uong UF data").

### Accessibility

- [ ] **L. No skip-to-content link**
  Keyboard and screen-reader users must tab through the full nav on every page. Add a visually-hidden "Skip to content" link that targets the `<main>` element.

- [ ] **M. Verify low-contrast text against WCAG AA**
  Footer text is `#555` on `#141414` (≈2.8:1 — below the 4.5:1 AA threshold). Muted `small`/tagline text uses `#999`. Audit these and bump the dim colors until they pass AA, or accept them deliberately.

### Mobile / CSS

- [ ] **N. Make wide tables horizontally scrollable (addresses open item #10)**
  Rather than restructuring the 7-column Presentations table by hand, add a global rule that lets any overflowing table scroll within its container (e.g. wrap tables or apply `display: block; overflow-x: auto;` on `table` under the mobile breakpoint). One CSS change fixes every current and future table. Item #10 can then be closed.

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
