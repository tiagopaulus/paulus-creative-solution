# Pentagram — Teardown

**URL:** https://www.pentagram.com/
**Theme:** 04 Every Surface
**Date reviewed:** 2026-07-06

## Why it's a reference
The world's largest independent design consultancy (est. 1972, 23 partners working "independently and collaboratively") and the definitional Theme-04 site: **"We design everything for everyone."** The whole architecture exists to prove one idea — a single firm credibly delivering across 14 disciplines × 16+ sectors, from typefaces to buildings to data experiences — and to let any prospect slice that universe along their own axis.

## Stack
- Framework: **server-rendered HTML (~1 MB per page, fully indexable) + Vite-built JS layer.** No React/Vue/Next in the page — classic SSR enhanced by a single module bundle.
- Animation: **GSAP + ScrollTrigger + Barba.js + Swiper** (~520 KB bundle). Barba.js = smooth page-to-page transitions over server-rendered pages — SPA feel without SPA architecture. The pragmatic middle path between Collins (nothing) and Watson (custom engine).
- CMS: custom/headless (not fingerprintable — no Craft/WP/Django markers). Images via **imgix** (`pentagram-production.imgix.net`, 1900+ refs with on-the-fly transforms). CloudFront + nginx.
- Video: **Vimeo** embeds.

## Structure
- Nav pattern: Work / About / News / Contact / Archive / Search — plus the real navigation: **the discipline × sector taxonomy**. 14 disciplines (Brand Identity, Typefaces, Exhibitions, Data Driven Experiences, Industrial/Product Design, Motion, Naming, Packaging, Signage & Environmental…) × 16+ sectors (Arts & Culture, Finance, Technology, Climate & Sustainability…), every project tagged with both. Sector pages live at root level (`/arts-culture`, `/finance`).
- Homepage flow:
  1. Rotating featured projects hero (Isomorphic Labs, National Building Museum…)
  2. "We design everything for everyone" + filterable discipline/sector tags
  3. **Curated editorial sets** — not a feed: "Our Future is the Ultimate Project" (climate), "Retrospective: Saturday Night Live" (30-year partnership), "Type Has Spirit" (typography), "Here is New York" (office identity), each with 4–8 projects
  4. Partner quotes woven through ("Words have meaning. Type has spirit" — Paula Scher)
  5. News; footer with 4 offices (London, New York, Austin, Berlin)
- Case study structure (from /work/isomorphic-labs):
  1. Title + one-line thesis ("Beautiful Symmetry: … a new visual language for digital biology")
  2. Discipline + sector tags upfront
  3. Long-form narrative: brand idea → visual language → typography → grid systems → 3D language → UI → voice/tone — **the story of a SYSTEM, then its deployment across surfaces** (site, business cards, on-screen graphics, social, launch campaign)
  4. Full-bleed media interleaved with narrative; Vimeo players for motion
  5. Credits: Client / Sector / Discipline / **Office / Partners by name** / full team / collaborators
  6. "Next Project" navigation + related content
- Archive: dedicated section for 50+ years of legacy work — history as a first-class feature.

## Standout interaction
Confirmed live (Tiago, 2026-07-06) — **the reason this site made the list**: the transparent, ever-present dropdown/header that reads "We Design Everything, For Everyone" and **rewrites itself contextually** as you scroll, open a project, or view media: "We Design Brand Identity, For Finance." / "We Design Campaigns, For Beauty." The two-axis taxonomy performed live — versatility shown super creatively and intuitively rather than claimed. Only con: it changes too fast; a PAULUS version should be smoother and slower.

Also strong live:
- **The Archive** — keyword search over 50+ years of visual references and projects; visitors can mine it for inspiration. Communicates both creative diversity and generosity: sharing knowledge freely with anyone who visits.
- Obama Presidential Center case study — simple (Vimeo + images), a bit heavy, but impactful composition with the right amount of text and the right amount of behind-the-scenes information.

## How to recreate
- **Two-axis taxonomy (discipline × sector)** — the mechanism that makes "every surface" navigable. For PAULUS: service/medium as one axis (Video, Branding, Digital, Popup, OOH…), industry/market as the other; every project tagged with both; tags clickable everywhere (fixes INNORED's dead hashtags at scale).
- **Curated sets over feeds** — homepage groups work into named editorial ideas (retrospectives, themes, office identities) instead of chronological grids. A CMS "collection" type: title + thesis sentence + 4–8 projects. Directly answers W+K's broken-hierarchy feed.
- **Case study = system story, then surface deployment** — narrate the identity system once (idea → language → type → grid), then show it landing on each surface. This is THE Theme-04 storytelling template.
- **Barba.js over SSR** — full server-rendered pages (SEO-perfect, 1 MB of indexable HTML) + client-side transition layer for continuity. Strong pattern for PAULUS: SSR everything, animate between.
- **Named partner attribution** on every project — people as first-class data (Office / Partners / Team). Feeds a future PAULUS team-page ↔ project cross-linking.
- imgix (or equivalent: Cloudinary, Next/Image) for one-master-image → all-crops delivery.
- **Dynamic contextual tagline**: sentence template `We Design {discipline}, For {sector}` bound to the current scroll section/page's tags; crossfade or slide per word on change (GSAP or CSS transitions). PAULUS version: slower, smoother easing than Pentagram's — let each combination breathe before the next.

## PAULUS applications (Tiago, 2026-07-06)
- **Adapt the dynamic tagline** — a live "We Create {service}, For {industry}" element driven by PAULUS's own two-axis tags. The single best "every surface" device seen; tune the pacing down.
- **An Archive/reference-search feature** — searchable visual archive open to visitors. Positions PAULUS as generous with knowledge, and showcases diversity beyond the curated portfolio. (Long-term: pairs with the internal Programs taxonomy for organizing legacy work.)
- **Work thumbnails must carry metadata** — year + industry or program/service on every thumbnail (Pentagram's are bare). Consolidates the dated-work rule from W+K/Bürocratik reviews.
- **Curated theme sets as hooks, kept short** — adopt the "contemporary themes" grouping but cap the landing page length; the hook loses impact when the page runs too long.
- **Team profiles: name + creative personality only** — Pentagram's photo-plus-mini-CV profiles feel corporate and lack personality; PAULUS will also avoid exposing much personal info about members. Exact profile format to be defined later.

## What NOT to copy
From live browsing (Tiago, 2026-07-06):
- **Landing page runs too long** — the curated-theme hook works, then dilutes as sets keep stacking; and the footer adds *more* news on top, which is overkill.
- **Bare work thumbnails** — no year, no industry, no service; weakest work-index metadata among the references.
- **About-page partner profiles** — personal photos + mini-CVs feel too corporate and lack personality; also over-shares personal information. PAULUS: name + creative personality, details TBD.
- **News page is messy** — avoid anything similar.
- Dynamic tagline transition speed — right idea, too fast.
- (Case study note: unlike W+K/Bürocratik, Pentagram's long-form got the balance right — "the right amount of text and behind-the-scenes"; pages can be a bit heavy, but composition carries them.)

From code analysis:
- The model requires Pentagram's volume — 14×16 taxonomy with thin cells looks worse than no taxonomy. PAULUS should launch with fewer axes-values, every cell populated (3+ projects), grow from there.
- Visually quiet presentation: the site is a container, the work is the color. Right for a 23-partner collective; PAULUS's site must itself demonstrate craft (closer to Watson) because PAULUS IS the creative product.
- html5shiv still shipped in 2026 — legacy cruft; audit dependencies.
