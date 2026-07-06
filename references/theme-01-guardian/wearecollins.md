# COLLINS — Teardown

**URL:** https://wearecollins.com/
**Theme:** 01 Guardian
**Date reviewed:** 2026-07-06

## Why it's a reference
Brand strategy/design agency (8x AdAge Agency of the Year, 2019–2026) that sells transformation as a product — services are packaged as named "Programs" (Brand Refresh, Reposition, Expansion, Turnaround) instead of a generic capabilities list. Confident, declarative copywriting ("Rewrite your worth", "Don't Become the Best. Become the Only") that treats the agency's POV as the product.

## Stack
- Framework: **Nuxt 3** (Vue, SSR — `__NUXT_DATA__` payload, `/_nuxt/` chunks)
- Animation: **No GSAP, no Lenis, no Framer Motion** — scanned all 40 JS chunks. Everything is CSS transitions + Vue transitions + custom `requestAnimationFrame`. Proof that restraint + native tech can feel premium.
- CMS: **Sanity** (`cdn.sanity.io/images/fmzd4n68`)
- Video: **Mux** (custom `MuxVideoPlayer` component; video used heavily in cards and case study heroes)

## Structure
- Nav pattern: Minimal top nav — Programs / Case Studies / Arts & Culture / "Work with us". Footer: Team, Careers, Press, socials.
- Homepage flow (section by section):
  1. Logo + headline "Rewrite your worth"
  2. Accolades strip (8x Agency of the Year — social proof immediately after the claim)
  3. Programs — 4 named offerings with sharp one-line descriptors
  4. Case study grid — 12 featured (Bose, Robinhood, Target up&up, Arcane, SF Symphony, YouTube Gaming…), video thumbnails via Mux
  5. Secondary stories — Arts & Culture initiatives ("The House of Belonging", "Hope as Defiance")
- Case study structure (from /case-studies/robinhood):
  1. Hero — full-width video/image gallery
  2. Headline ("Elevating an app into an ecosystem") + short context narrative
  3. ~3 body paragraphs: problem → insight → solution, media interleaved throughout
  4. "Augments" module — 4 named design-system components with imagery
  5. Impact metrics — 6 big stats, no elaboration
  6. Credits by discipline + press mentions
  - Index page is a plain grid: name + thumbnail, no filters, ~50 studies.

## Standout interaction
Three confirmed from live browsing (Tiago, 2026-07-06):

1. **"Window-into-a-new-world" image reveal** — on scroll, images expand sideways from the center, like a window opening onto the project. The signature scroll moment of the site.
2. **Dark-mode switch at Case Studies** — as the user scrolls into the projects area, the whole site flips to dark mode. Shifts contrast from text to imagery exactly when imagery becomes the point. Very effective, cheap to build, high perceived craft.
3. **Overlay "hot-pages" for depth on demand** — case studies show the brief version first; buttons like "Read the Full Story" and "Explore Augments" open overlay pages with process/behind-the-scenes detail. The user chooses what to go deeper on instead of being forced through everything.

Also: UP & UP case study has an intuitive right-to-left horizontal image gallery with an option to expand into the full gallery.

## How to recreate
- Nuxt/Vue equivalent in our stack: video-thumbnail cards = `<video muted loop playsinline>` with poster, play on hover/in-view — Mux handles streaming + thumbnails (`image.mux.com` for posters).
- Their animation lesson: no scroll-jacking, no smooth-scroll library. Native scroll + CSS transitions + IntersectionObserver reveals. Site loads fast and lets you scroll immediately — minimal first paint is part of the design.
- **Center-out image reveal:** wrapper with `overflow: hidden`, animate `clip-path: inset(0 50% 0 50%)` → `inset(0 0 0 0)` (or scaleX on a mask) triggered by IntersectionObserver.
- **Section-scoped dark mode:** IntersectionObserver on the Case Studies section toggles a `data-theme="dark"` class on `<html>`/`<body>`; all colors are CSS custom properties so the flip is one transition.
- **Overlay hot-pages:** route-based modals (Nuxt/Next parallel routes) — overlay opens with its own URL, main page state preserved underneath, closes back to scroll position.
- Case study formula worth copying: problem → insight → solution in 3 paragraphs, then named deliverable modules, then raw stats. Copy stays 15–150 words per section. Brief-first with opt-in depth.

## PAULUS applications (Tiago, 2026-07-06)
- **Accolades strip after the headline** — PAULUS has been ranked ~top 5 agencies in Korea for the past 5 years + diverse prizes incl. Cannes. Mirror the "strong claim → immediate proof" sequence.
- **Impact section** — big-typography stats, instantly scannable. PAULUS often lacks hard impact data → use views/engagement metrics for content work, plus sales-improvement data when clients provide it.
- **Press section** — Collins leads with the logos of publications, not article text. PAULUS has been featured in many articles in Korea and worldwide; add a logo-led press section.
- **Programs page** — break down Creative Solution's many capabilities into clear named offerings for future clients, AND use those programs as internal categories to organize the project portfolio.
- **Team page** — Collins asked each member to choose a piece of art that represents them (great connector). PAULUS version: add a brief profile with keywords describing each teammate's creative profile + main responsibilities/USPs.

## What NOT to copy
- Case study index is a bare grid with zero filtering/categorization — fine at their brand strength, but weaker wayfinding than PAULUS needs.
- No detectable playfulness in tech — if a signature WebGL/canvas moment is part of PAULUS's identity, this site won't show how.
