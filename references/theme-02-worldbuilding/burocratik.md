# Bürocratik — Teardown

**URL:** https://www.burocratik.com/
**Theme:** 02 Worldbuilding
**Date reviewed:** 2026-07-06

## Why it's a reference
Portuguese studio (Coimbra + Porto) ranked Europe's #1 digital studio by the ED Awards agencies league (2021–2025) that turns its own history into a world: a "7.340 days" live counter, a team timeline of every Büro member through the years (departed members marked †), 303 awards, and a manifesto of principles — the studio itself is the world being built. First reference in our set with real WebGL craft.

## Stack
- Framework: **Nuxt 3** (Vue — `/_nuxt/` chunks, `_payload.json` per route)
- Animation: **The premium full stack, done lean** — GSAP + ScrollTrigger + SplitText + CustomEase, Lenis smooth scroll, and a **custom raw-WebGL "image mesh"** (hand-written, not Three.js: `precision highp float` texture shader, WebGL2 with WebGL1 iPhone fallback, logs "No WebGL support. Image mesh will…" and degrades gracefully). Total JS ~1.2 MB across 12 chunks.
- CMS: **Sanity** (project `zksivtxz`; rich typed schema: `caseStudy`, `project`, `award`, `testimonial`, `studio`, `naming`, `biography`, `self`…)
- Video: self-hosted via **DigitalOcean** files (`digital-ocean-files.media` type) + some Vimeo

## Structure
- Nav pattern: Homepage / Studios / Recognition / Work (Branding, Naming) / "18 Years of Büro" + "Let's talk?" CTA. Footer: offices with GPS coordinates, socials, newsletter.
- Homepage flow (section by section):
  1. Hero — repeated brand name + "Let's talk?"
  2. Tagline — "We're a fearless 🤟 digital studio with two decades of craft…" (emojis in body copy) + "Apply now" + **"7.340 days" counter**
  3. **Team timeline** — "Every Büro, through the years": 37+ names, deceased marked with †
  4. Awards — 303 awards + 4 ED Awards league badges
  5. Seven principles — manifesto statements ("You never get a second chance to make a memorable first impression")
  6. Featured work carousel — Clear Street, TUU, Floema, Jeton, Keikku, Phive, Remote, MultiversX, Kozowood, Grab&Go
  7. Services — 4 categories (Branding, Digital Branding, Experience, Business Design) with sub-services
  8. Testimonials — 6 client quotes (Clear Street, Unilever, Remote.com…)
  9. Contact CTA — "Say no more. It's a match ↓"
- Case study structure (from Keikku's Sanity document — modular section types):
  `caseStudy_header` → `caseStudy_heroVideo` → `caseStudy_textWithMediaGallery` (×4) → `caseStudy_fullscreenMedia` (×4) → `caseStudy_mediaGallery` → `caseStudy_heading` (×2) → `caseStudy_testimonial`
  - ~11 videos + 12 images in ONE case study — motion-first storytelling
  - Copy is compact and flavorful (e.g. "Did you know that in Finnish, Keikku means 'toy'?")
  - Fully client-rendered (raw HTML shows only "Loading…" — SEO cost)

## Standout interaction
Confirmed live (Tiago, 2026-07-06):
- **Opening sequence** — "We are Büro" appears alone in a small font, then the showreel arrives. Lovely staging (though the showreel cuts too fast and gets hectic — fixable purely through content choice).
- **Team rewind timeline** — days-since-founding counter + casual team photos with names through the years. Acknowledges people as creative partners *even after they left*. Hovering cascades the person's photos — a bit hectic, but it fits this studio's personality.
- **Bottom-locked menu** — the nav sits locked at the bottom within the scroll, phone-app-like. Very creative, and it makes the pages look cleaner. (Second "app-feel" win after MetaLab.)
- **Case studies pop up like a newspaper article** — the page opens as an overlay with editorial typography, great font/size/composition/white-space hierarchy; genuinely enjoyable to scroll despite the length.

From code (verify the feel live): the custom WebGL image mesh distorting images on scroll/hover, and SplitText + CustomEase typography reveals.

## How to recreate
- WebGL image mesh: don't need Three.js — a small hand-rolled WebGL layer (or OGL/curtains.js) that syncs `<img>` positions to GPU planes, with Lenis scroll velocity driving vertex distortion. Their fallback pattern is the model: detect WebGL2 → WebGL1 (iPhone) → plain images, never break.
- GSAP SplitText + CustomEase for typography moments: buy Club GSAP once, define 2–3 house easing curves, use them everywhere for a consistent motion identity.
- Studio-as-world content: `award`, `testimonial`, `biography`, `self` as first-class CMS types — the agency's own story gets the same CMS rigor as client work. PAULUS equivalents: prize archive, press archive, team history.
- Modular case study sections (header / heroVideo / textWithMediaGallery / fullscreenMedia / mediaGallery / testimonial) — same lesson as W+K's layout blocks, confirmed by a second top studio.
- Days-since-founding counter: trivial JS (`Date.now() - founding`) — a small worldbuilding signal that says "we endure."

## PAULUS applications (Tiago, 2026-07-06)
- **"Fearless studio… ranked… awarded" opening formula** — the tagline structure (identity claim → ranking → awards) maps directly to PAULUS (top-5 Korea, Cannes).
- **Alumni-inclusive team timeline** — PAULUS has many professionals who left to freelance but still join projects when we need their expertise. A through-the-years team section shows how connected we stay and how we appreciate previous professionals. Strong cultural fit.
- **Awards count in big impactful type** — pairs with the planned accolades strip.
- **Bottom-locked app-style menu** — candidate nav pattern for PAULUS: cleaner pages, and consistent with the app-feel Tiago liked on MetaLab.
- **Newspaper-article case study overlay** — combine Bürocratik's editorial pop-up presentation with Collins' brief-first + expand model: open as an editorial overlay, but keep it concise with "full version" opt-in.
- **Testimonials belong on project pages** — tie each quote to its specific project rather than pooling them near the homepage footer.

## What NOT to copy
From live browsing (Tiago, 2026-07-06):
- **Eyes-emoji cursor (👀)** — very outdated, definitely not PAULUS voice and tone. (Third cursor-gimmick strike across reviews: MetaLab's image flashes, W+K's PLAY cursor, this.)
- **Undated projects right after the timeline** — Clear Street and TUU thumbnails carry no dates, so the user can't tell recent from prioritized. Same critique as W+K: date or explicitly order the work.
- **"Our Accolades" runs too long** — 3–4 bullet points maximum would be more impactful than the full list.
- **Testimonials pooled near the footer** — disconnected from the work they praise; move them onto individual project pages.
- **Showreel cut too fast** — hectic first impression; pace the reel calmly.
- **Case studies too long with no summary option** — well-designed but should be more concise, with an opt-in "see the full version." (Fourth site confirming brief-first.)

From code analysis:
- Fully client-rendered case studies (raw HTML = "Loading…") — terrible for SEO/link previews/AI crawlers. PAULUS must SSR case study content.
- ~1.2 MB JS + WebGL + 11 videos per case study — needs careful lazy-loading discipline PAULUS should design in from day one.
- Emojis inside the manifesto copy (🤟💫) — charming for a fearless Portuguese studio, likely off-brand for PAULUS's premium positioning.
- Team timeline marking deceased members with † — moving for a 20-year studio, but only works with that history.
