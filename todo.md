# Portfolio TODO

## Technical (fix these first)

- [ ] **1. Missing `baseurl` and `url` in `_config.yml`**
  The site lives at `joeufl.github.io/portfolio/` but `_config.yml` has no `baseurl: "/portfolio"`. Without it, the `relative_url` filter generates paths like `/projects` instead of `/portfolio/projects` — nav links and CSS may be broken on the live site right now.

- [ ] **2. `index.md` "View Projects" link uses `projects.md`**
  Should be `/projects` (a URL, not a file path). Jekyll may resolve it, but it's fragile.

---

## Content Gaps

- [ ] **3. No contact information anywhere**
  A visitor who wants to reach you has no path forward. LinkedIn, email, or GitHub — even one is enough. Could go in the footer of `default.html` or on the homepage.

- [ ] **4. No institutional context on the homepage**
  The homepage doesn't mention UF. A visitor with no prior context doesn't know the scale of the institution (50,000+ students, top-10 public university) or that the work operates at that level. One sentence would do it.

- [ ] **5. Two strong projects missing from the Projects page**
  Both have public URLs and real outcomes:
  - **CLAS Analytics of Registration Dashboard** — live at [advising.ufl.edu/headcount/](https://www.advising.ufl.edu/headcount/), used for leadership decisions, key metrics over time
  - **Unique Waitlist Demand Reporting** — built custom logic to count unique students across sections, adopted by Enterprise Reports for campus-wide use. That adoption is a meaningful signal.

- [ ] **6. C2Grad / Close2Grad is portfolio-worthy**
  Got a Ytori magazine feature and a dean-level quote. The story — finding discontinued students with few requirements left and getting them to graduation — is compelling and human. Cross-functional (Joe + Becca Sandbach Woods). Not in projects at all.

- [ ] **7. `writing.md` is an empty dead-end**
  Has a permalink but no content and isn't in the nav. Either fill it or delete it. If there's any published writing beyond the 2017 journal article, this is the place.

---

## Homepage Voice

- [ ] **8. The opening line is generic**
  "I design analytics systems that help organizations make better decisions" could describe any data analyst anywhere. The actual differentiator is the combination of technical depth (Snowflake stored procedures, AI prompt engineering) *and* institutional navigation (getting things approved, being the first to go first). That's unusual and worth naming.

- [ ] **9. Bullet list is lowercase, inconsistent**
  `- Snowflake data pipelines` vs. `- Python automation` — minor, but easy fix. Capitalize all items.

---

## Professional Activity Page

- [ ] **10. Table likely overflows on mobile**
  The Presentations table has 7 columns with long conference names. The conference name and title columns especially will wrap badly on smaller screens. Consider collapsing Date and Location into one column, or dropping Location.

- [ ] **11. Emojis in section headings**
  🏆, 🎤, 📰 — personal call. They read fine on the light minima theme but can feel out of place on a professional dark theme. Worth checking how they render live.

---

## Layout / Navigation

- [ ] **12. Site title in nav h1 is "Joe Uong Portfolio"**
  With the midnight theme, the h1 in the sidebar acts as your name/brand. "Joe Uong Portfolio" is redundant — the whole site is the portfolio. "Joe Uong" alone is cleaner.

- [ ] **13. No About page**
  Common for portfolios and useful here — the background arc (community college student affairs → registrar → data analyst) says something about how institutional problems get approached that the projects page doesn't surface.

---

## Priority Order
1. Item 1 (baseurl)
2. Item 2 (View Projects link)
3. Item 3 (contact info)
4. Item 4 (UF context on homepage)
5. Item 12 (nav title)
6. Item 5 or 6 (new projects)
7. Item 8 (homepage voice)
8. Item 10 (table overflow)
9. Item 13 (about page)
