# Wieden+Kennedy — Teardown

**URL:** https://www.wk.com/
**Theme:** 01 Guardian
**Date reviewed:** 2026-07-06

## Why it's a reference
The world's most famous independent creative network ("Just Do It", "Dilly Dilly") whose site leads with attitude, not polish: "We were founded as an ad agency that didn't like advertising." The homepage is a living feed of work and culture posts tagged by office (+PDX, +LDN, +NYC), positioning the network as one creative organism across 9+ cities — identity carried by voice and work, not by web-tech spectacle.

## Stack
- Framework: **Gatsby** (React, static-generated — `page-data.json` per route, webpack chunks)
- Animation: **None detected** — no GSAP, Lenis, Framer Motion, or Swiper in any bundle (all grep hits were base64 false positives). CSS + React only. Like Collins, proof that a top-tier creative brand doesn't need an animation stack.
- CMS: **Contentful** (assets on `ctfassets.net`; typed models: `ContentfulWork`, `ContentfulNews`, offices, brands, "wiedensims")
- Video: self-hosted MP4s via Contentful (`videos.ctfassets.net`, e.g. "Netflix_Reel_Preview-10mb.mp4" — pre-compressed ~10 MB loops) + Vimeo/YouTube embeds

## Structure
- Nav pattern: brutally simple — Work / About / Jobs / Contact + search. Footer = full office directory with addresses (Portland, Amsterdam, NYC, Tokyo, London, Shanghai, São Paulo, Mexico City, Sydney).
- Homepage flow (section by section):
  1. Featured slides — "What We've Been Up To" video reel + top campaigns
  2. Mixed feed — work (Absolut Tabasco, McDonald's: Minecraft, YETI, Nike: So Win, Ford, DoorDash…) interleaved with news/culture posts (HBCU relationships, scholarships, "The Case For Chaos"), every item tagged with its office (+PDX, +LDN, +AMS)
  3. About blurb — the 40-years manifesto
  4. Office directory footer
- Case study structure (from /work/mcdonalds-minecraft data model):
  - Fields: hero (`fullscreenHeader` option), `videoFull` (the actual film — the work IS the content), `shortDescription` (one markdown paragraph of context), `longform` (modular blocks), `brand` + `office` tags, `relatedByBrand`
  - `longform` blocks are CMS-configurable layouts: `layout`, `mediasLayout`, `imagesPerRow` (e.g. 4), `darkBackground`, `narrowTextColumn`, `fullWidthImagesContainer` — an editorial grid system, not a fixed template
  - Work cards have `mainImageHover` + `videoPreview` fields → static image swaps to alternate image/video on hover

## Standout interaction
Confirmed live (Tiago, 2026-07-06): **the behind-the-scenes Instagram-like photo grid** on some project pages (e.g. Absolut Tabasco) is the best thing on the site. A grid of candid BTS/craft shots makes their attention to detail and *guardianship of the project* easily readable at a glance — the guardian value expressed visually instead of claimed in copy. This is the pattern to steal for PAULUS.

Also good live:
- The opening showreel titled "What We've Been Up To" — casual yet respectful, concise tone. (Caveat: it makes initial navigation slow — avoid that cost on the PAULUS site.)
- Scroll-triggered animations on the main page use **static images only**, which keeps navigation direct and un-hectic — a deliberate calm compared to video-heavy feeds.

(Where the CMS "wiedensims" surface: they're the provocative footer sentences — see What NOT to copy.)

## How to recreate
- Ad-agency model: the case study page centers on `videoFull` — the film itself — with one paragraph of setup. When the work is video, don't bury it under process narrative.
- CMS-driven layout blocks: instead of hard-coded case study templates, give each content block layout knobs (images per row, narrow/wide text, dark background). One schema, endless editorial layouts — how they keep hundreds of case studies fresh. Sanity/Contentful both handle this well.
- Office-tagging every piece of content (+SEL-style) makes a multi-city network feel unified; for PAULUS this could tag Seoul HQ vs. partner/worldwide work.
- Mixed work + culture feed: news, scholarships, and POV pieces sit beside client work — the agency's values are content, not an About-page afterthought.
- Card hover swap = two CMS fields (`mainImageHover`, `videoPreview`) + CSS opacity/`<video>` play on `mouseenter`. Cheap, effective.
- **BTS photo grid (the keeper):** a CMS gallery field of candid production shots rendered as a tight Instagram-style grid on the case study page. Shows craft/ownership without a word of copy. For PAULUS: shoot BTS on every project and make this a standard case-study module.
- Static-image scroll reveals on listing pages (save video for the case study itself) — calmer navigation, better performance.

## What NOT to copy
From live browsing (Tiago, 2026-07-06):
- **Broken storytelling hierarchy on the homepage** — "What We've Been Up To" is followed by projects (Absolut Tabasco, YETI) that aren't in the showreel and carry no dates, so "recent" is unverifiable; then it jumps back 40 years to the founding paragraph, then back to undated projects. → PAULUS: keep one narrative direction per page, and date (or explicitly order) the work.
- **Inconsistent work-card system** — some projects full-width, some square thumbnails; squares show Location + Project Name + "View Work" but full-width ones drop the "View Work" label; thumbnail sizes don't follow a regular grid, so the white space feels polluted and unintentional. → uniform card grammar: same metadata, same affordance, intentional grid.
- **Footer maxims feel like an afterthought** — "Independence is Everything", "Shut up when someone's talking" (the CMS "wiedensims") break the nice casual-respectful tone the showreel established. Values need staging, not a dumping ground.
- **Multiple world clocks in the footer feel very outdated** — note: the same element felt app-like and charming on MetaLab; execution and context decide, not the feature.
- **Cursor becomes a "PLAY" text over videos** — reads as an old HTML blog, not a premium agency. Skip text-cursor gimmicks.
- **Wall-of-text project pages** — good font and size hierarchy, but no summarized version exists; the text gets lost in full-text form. Third site in a row confirming the Collins brief-first + expand pattern as the PAULUS standard.
- Showreel autoplay slows initial navigation — if PAULUS opens with a reel, lazy-load/stream it so it never blocks first interaction.

From code analysis:
- Feed-first homepage assumes the visitor already knows W+K — weak wayfinding for a prospect evaluating agencies (no services/programs entry point at all). PAULUS needs clearer "what we can do for you" paths.
- No case study index filtering beyond search; discovery relies on scrolling the feed.
- ~10 MB preview videos on the homepage — heavy; PAULUS should use adaptive streaming (Mux) or tighter compression for loops.
