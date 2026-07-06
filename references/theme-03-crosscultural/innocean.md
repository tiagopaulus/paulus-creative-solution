# INNOCEAN — Teardown

**URL:** https://www.innocean.com/ww-en
**Theme:** 03 Cross-Cultural
**Date reviewed:** 2026-07-06

## Why it's a reference
The Hyundai-affiliated global agency network (est. 2005): 22 countries, 32 networks, 207 clients, listed company. The opposite pole from INNORED on the Korean-agency spectrum — where INNORED is one independent shop speaking two languages on one page, INNOCEAN is a **hub-and-spokes architecture**: a central worldwide site (`/ww-en` + `/ww-ko`) with regional subsidiaries on entirely separate domains (innoceanusa.com, innocean.com.br, innocean.ca…). Instructive for PAULUS mostly as a map of what corporate scale does to a creative site.

## Stack
- Framework: **Nuxt 3 SSR** (`data-ssr="true"`, `data-capo` head optimization) + **Tailwind CSS** (utility classes with `md:` breakpoints, `!delay-[400ms]`)
- Animation: **Swiper only.** No GSAP, no Lenis, no Lottie — CSS transitions (`main--transition` classes with staggered delays). The most conservative animation stack in the reference set.
- CMS: custom backend at `mng.innocean.com:8080` proxied through Nuxt (`/api/banner`, `/api/client`, `/api/kv`, `/api/networks`, `/api/search`, `/api/works/highlight`)
- Video: YouTube embeds

## Structure
- Nav pattern: Work (Recent / Highlight / Awards) · Expertise (Business Solutions / Network / Our Clients) · About (Our Story / Careers / Press / **IR** / Magazine) · Values (**ESG** / Speak up) · Contact + KOR/ENG toggle + region selector. IR and ESG in the main nav = listed-company DNA.
- Homepage flow:
  1. Hero — featured work carousel
  2. Business Solutions — "We Craft Innovative Brand Experiences, Driven By The Latest Technology And Data"
  3. **Company Information — financials on the homepage** (2025 Gross Profit ₩990.2B, Operating Income ₩163.3B, Net Income ₩109.4B)
  4. Global stats — 22 countries / 32 networks
  5. Global Network — "Global Network, Powerful Impact"
  6. Contact — "We Can Build Something Greater, Together"
- Network page: 5 regions (Korea / Americas / Europe / APAC / China / India+MEA) in expandable tabs, offices labeled HQ/RHQ, each linking out to its own domain. Korea lists specialist sub-studios (D-Plan360, D.Purple, INNOCEAN-S, Studio abit, Studio Lennon).
- Work detail (from /ww-en/work/recent/1053 "Summer of gamtan"): title + client, YouTube video as primary media, metadata (Date / Service / Industry / Country), hashtags, "You Might Also Like" related projects.

## Language strategy (the Theme-03 core)
- **Path-based locales** (`/ww-en`, `/ww-ko`) with a real KOR/ENG toggle — architecturally the "right" way (vs INNORED's single hybrid page)…
- **…but the content doesn't keep the promise.** On the English site: work descriptions come from the API in Korean only, client categories are Korean (모빌리티), case study pages show *no English description at all*, hashtags mix Korean and romanized forms (감탄/gamtan). Same disease as INNORED — bilingual shell, monolingual content — at a company 50× the size.
- No `hreflang` tags despite the dual-locale structure — SEO owns none of the language mapping.
- Regional model: separate domains per country rather than localized pages — full autonomy for subsidiaries, zero shared design system visible across them.

## Standout interaction
Confirmed live (Tiago, 2026-07-06):
- **Scroll-expanding showreel** — unique in our set: the reel starts small at the top-right and grows with the scroll until it fills the full div; only when it reaches full width does the "View Our All Work" button appear. The scroll gesture itself builds the hierarchy — very intuitive.
- **Awards page with stacked trophies** — a visual animation piling the awards on top of each other, breaking the seriousness of the subject with play. Fun where every other agency is solemn.
- **Business Solutions → Insight hot-page** — showcases their internal process with sketch-like content and straight-to-the-point text; process transparency without wall-of-text.
- Footer CTA — "We Can Build Something Greater, Together" + a "Get on Board" button, possibly a subtle nod to the "ocean" in their name without bending the brand voice.

## How to recreate
- Path-based locale architecture (`/en`, `/ko`) with a toggle is the correct skeleton for a bilingual site — but pair it with `hreflang` tags and an editorial rule that NO content ships until both locales exist (or the page explicitly falls back).
- Nuxt SSR + Tailwind + Swiper-only is the "corporate-safe" stack: fast, indexable, cheap to maintain — proof that a 22-country site can run on almost no animation code. (PAULUS wants more craft than this, but it's the reliability baseline.)
- Metadata block on work pages (Date / Service / Industry / **Country**) — the Country field is a nice touch for a cross-market agency; PAULUS could tag market (Korea / Global / client-region) per project.
- Related-works recommendations ("You Might Also Like") keep visitors inside the work section.
- Scroll-expanding hero reel: pin the section (ScrollTrigger or CSS `position: sticky`), interpolate the video container from a corner rect to full-bleed as scroll progresses, reveal the CTA at progress=1. High impact, one section, no library beyond the scroll driver.

## PAULUS applications (Tiago, 2026-07-06)
- **Find PAULUS's "surprising data point."** INNOCEAN shows gross profit — risky, unique, memorable. PAULUS can't share financials, but the lesson stands: lead with one stat that genuinely surprises a future client (candidates to explore: cumulative content views, campaign engagement records, years of top-5 ranking, number of markets shipped to).
- **Scroll-expanding showreel** — candidate hero pattern: reel grows with scroll, work CTA appears only at full size. Solves the "showreel blocks navigation" problem (Bürocratik, W+K) by making the reel scroll-driven instead of time-driven.
- **Work in 3 categories — Recent / Highlight / Awards — but as filters, not pages.** Great categorization; implement as in-place filters so users don't bounce between pages. Merges with INNORED's Awards-filter idea.
- **Playful awards presentation** — stacked-trophy animation direction for the PAULUS awards section: celebrate without solemnity.
- **Process-transparency hot-page** — sketch-like internal process content, concise text (their business-solutions > insight). Matches W+K's BTS-grid lesson: craft shown, not claimed — but at the *methodology* level rather than production level.
- **Real-presence storytelling** — offices/operations shown as a world map of actual capability, not partner logos. PAULUS should be precise about what's real presence vs. collaboration network (honesty reads stronger).

## What NOT to copy
From live browsing (Tiago, 2026-07-06):
- **Press page very outdated and hard to navigate** — the one section that clearly missed the redesign. (PAULUS's logo-led press section plan already avoids this.)
- **Work split across 3 separate pages** — Recent/Highlight/Awards categories are great but should be filters, not page navigation.
- Business Solutions page: concise and well designed but font hierarchy is one notch flat — with stronger type hierarchy it would be perfect.
- Gross profit disclosure: works as a surprise for a listed giant, but it's not transferable — PAULUS needs its own surprising stat, not financials (see PAULUS applications).

From code analysis:
- The bilingual-shell/monolingual-content failure (second Korean agency in a row) — for PAULUS the ~95% English decision (see INNORED teardown) sidesteps this trap entirely.
- Separate uncoordinated domains per region — fragments brand and SEO authority; irrelevant at PAULUS's scale anyway.
- Swiper-only conservatism — safe but characterless outside the hero moment; interaction rarely expresses the brand.
- No hreflang tags despite dual locales.
