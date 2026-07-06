# Watson — Teardown

**URL:** https://watson.la/
**Theme:** 02 Worldbuilding
**Date reviewed:** 2026-07-06

## Why it's a reference
LA brand & entertainment creative studio (Watson Design Group, est. 2005, independent, minority-owned) working with A24, Amazon, Disney, FX, Mattel, WB, Neon, Focus Features. Positioning: "A brand & entertainment creative studio led by craft — in search of conversation." Their site is the purest *experience-as-world* build in our set — a fully custom WebGL engine in black & white, developed with Aristide Benoist (one of the top creative developers working today). Awwwards Site of the Day (Sep 2024, 7.58 — Design 7.98).

## Stack
- Framework: **None — 100% hand-rolled vanilla JS.** No Next/Nuxt/React/Vue. A tiny inline bootstrap detects device and loads a device-specific bundle (`/static/js/d.js` desktop / `m.js` mobile) + matching CSS. Custom router (`_A` global with route table), counter preloader ("0 → 100"), versioned assets (`?175600`).
- Animation/3D: **Three.js bundled into a custom engine** (~670 KB total — less than half of MetaLab's bundle, WITH a 3D engine inside). Custom shaders everywhere: displacement (103 refs), refraction (30+), blur, masks, GPU instancing. **Draco-compressed glTF 3D models loaded per page** (`/static/gltf/<page>/<file>/0.gltf`). No GSAP, no Lenis — everything custom rAF.
- CMS: none detectable — content baked/fetched via versioned static assets.
- Fonts: self-hosted woff2 with obfuscated 2-letter names (`ba`, `bu`, `ca`), aggressive CSS reset inlined in `<head>`.
- Palette: pure black & white (#000/#FFF) per Awwwards data.

## Structure
(From live browsing — Tiago, 2026-07-06; raw HTML contains only a preloader, so all structure was documented live.)
- Nav pattern: pages named **"Partnerships" / "Capabilities" / "Conversations" / About** — the naming alone builds the world and makes the tone unique. Nothing generic ("Work", "Services", "Blog") survives.
- Homepage: simple and graphic — communicates a lot with very few elements; excellent font hierarchy and composition. Footer is dedicated to their most recent achievements — concise, straight to the point.
- **Partnerships page** (the reason it's in this list): projects presented as *Watson × Partner* (Watson x Disney, Watson x Amazon…) under one umbrella of concise style — the studio's personality and creative world expressed while flagship clients rotate through it. Scroll animation transitions between partners very smoothly.
- Individual project pages:
  1. **Title = the creative challenge**, not the client — e.g. "Marketing a Goliath through a David Mentality" (Amazon). Metaphorical yet precise; in a few words you see how they think AND what the project was.
  2. Quick introduction, including stylized references (likely developed post-project).
  3. **Irregular deliverables grid** — all surfaces/mediums shown, but thumbnails are first filtered through the studio's main colors so the wall of work never looks crowded.
  4. Click a thumbnail → **hot page** with the specific videos/images, then an extensive yet smooth scrolling list of more thumbnails from the same project. Prolific production without a cramped or heavy feel.
- Capabilities page: amazing hierarchy, very clear — each core capability links to projects that exemplify it.
- Conversations page: creative discussions and diverse media explorations, related to but separate from project work — shows the team's social/cultural engagement. Great first impression for clients.
- About: casual team pictures, very straight to the point — also a good first impression.
- Note: `<noscript>` shows "Please enable javascript to view this website"; robots see nothing beyond the meta tags. The most extreme SEO trade-off in our reference set.

## Standout interaction
Confirmed live (Tiago, 2026-07-06): the **Partnerships scroll transition** — scrolling changes the partner (Watson x Disney → Watson x Amazon → …) with a very smooth morph, presenting diverse projects under one consistent stylistic umbrella. The single best expression of "the studio's world absorbs its clients" in our reference set. (Under the hood this is the custom WebGL engine: displacement/refraction shaders + per-page glTF scenes.)

Runner-up: the **color-filtered deliverables grid → hot page** flow on project pages — thumbnails unified by the studio's palette until clicked, then a dedicated overlay reveals the real media. Volume without clutter, ownership without hiding the work.

## How to recreate
- The lesson isn't "hand-roll everything" — it's **budget discipline in service of a world**: one 670 KB device-specific bundle replaces framework + animation libs + 3D lib. Device-split bundles (`d.js`/`m.js`) mean mobile never downloads desktop shader complexity.
- Draco-compressed glTF per page = heavy 3D worlds at small transfer sizes (Draco typically cuts mesh size 90%+). Three.js `DRACOLoader` + `GLTFLoader`, models lazy-loaded per route.
- Displacement/refraction on images: standard technique — image as texture on a plane, shader distorts UVs by scroll velocity/cursor; a "mask" uniform reveals on scroll. curtains.js or OGL gets PAULUS there without a custom engine.
- B&W-only palette makes WebGL effects read as *craft* rather than decoration — restraint elsewhere buys license for spectacle.
- If PAULUS wants one "world" moment (e.g. hero), this proves it can be done at sane bundle sizes — but hire/allocate a dedicated creative developer; this level is a specialist discipline.

## PAULUS applications (Tiago, 2026-07-06)
- **Challenge-as-title case studies** — name each project by its creative challenge ("Marketing a Goliath through a David Mentality"), not just the client. Shows how PAULUS thinks and what the project was, in one line.
- **PAULUS × Client framing** — a Partnerships-style presentation (PAULUS x Samsung, PAULUS x …) that keeps every collaboration inside PAULUS's visual world. Pairs with MetaLab's uniform-packaging lesson but with a smoother, more editorial expression.
- **Color-filtered deliverables grid + hot pages** — the answer to "how do we show prolific production without crowding": unify thumbnails under brand colors, put real media one click deeper. Directly relevant to PAULUS's high-volume content output.
- **Capabilities → example projects cross-linking** — each capability links to the projects that prove it; same instinct as Collins' Programs, executed with cleaner hierarchy.
- **A "Conversations"-style section** — home for Creative Solution's media explorations and creative discussions that relate to, but shouldn't mix with, project work. Also signals social/cultural engagement — a good client first impression.
- **Named-world navigation** — invest in page names that carry tone (not "Work/Services/Blog"). Precision naming = cheap worldbuilding.
- **Concise achievements footer** — recent awards/recognition in the footer, short and to the point; complements the accolades strip without repeating it.

## What NOT to copy
- **Zero content without JS** — no nav, no text, no work in the HTML. Terrible SEO/social-preview/AI-crawler visibility; only viable for a studio whose clients arrive by referral. PAULUS must keep content indexable (SSR).
- Usability scored lowest of their Awwwards marks (7.23) — experience sites tax wayfinding; jury flagged accessibility.
- No CMS — every content change is a developer deploy. Wrong trade-off for an agency updating its portfolio regularly.
- Blocking preloader (0→100 counter) before ANY content — the anti-pattern to Collins' instant-scroll opening; violates our performance-as-design principle.

(Tiago's live review was entirely positive on design/UX — the only cautions on this site are the technical trade-offs above.)

---
Sources: [watson.la](https://watson.la/) · [Awwwards SOTD](https://www.awwwards.com/sites/watson) · [Watson DG LinkedIn](https://www.linkedin.com/company/watson-dg) · [Behance](https://www.behance.net/watsondg)
