# MetaLab — Teardown

**URL:** https://www.metalab.com/
**Theme:** 01 Guardian
**Date reviewed:** 2026-07-06

## Why it's a reference
Product design/development firm (est. 2006) with the most confident three-word positioning in the industry — "We make interfaces" — and the strongest example of *packaging client work inside the agency's own visual language*: every project, even Midjourney or Calvin Klein, is presented in MetaLab's uniform composition system, making the work unmistakably theirs. Work is organized by industry category (Finance, SaaS, Media, Ecommerce…), each fronted by one flagship case study, so the portfolio reads as "pick your industry, see the proof."

## Stack
- Framework: **Next.js** (Pages Router — `__NEXT_DATA__`, `/_next/` chunks)
- Animation: **The full toolkit** — GSAP + ScrollTrigger, Lenis smooth scroll, Framer Motion (internals in bundle), Swiper for carousels. Opposite philosophy to Collins' zero-library approach; `_app` bundle is 1.5 MB.
- CMS: **Sanity** (project `nuxb3jim`; public dataset holds ~75 portfolio items, but flagship case studies like Robinhood resolve from a separate/private source at runtime)
- Video: **Vimeo** + self-hosted MP4 loops from Sanity CDN (hero is a `videoLoopDesktop` file with 40% dark overlay)

## Structure
- Nav pattern: Work (by category) / What We Do / About / Blog ("Latest") / Careers / Contact. Footer lists office city airport codes (YYZ, LDN, CDG, NYC, SFO, SYD, CPT…) — a compact worldwide-presence signal.
- Homepage flow (section by section):
  1. Hero — "We make / interfaces" in two lines over fullscreen video loop, dark theme + subtitle "Since 2006, we've helped the most innovative startups and reputable brands design, build, and ship products worth talking about."
  2. "HoverDrag" work showcase — a draggable/hoverable carousel numbered 1–24 (the site's signature module)
  3. Work by category — Product/Finance → Robinhood, SaaS → Uber, Full Build → Suno, Health & Wellness → Ro, Media → The Atlantic, Ecommerce → Calvin Klein…
  4. Blog/Latest teasers ("Our Windsurf case study", "2025 Recap")
  5. Contact prompt — "How can we help?"
- Case study structure (from /work/robinhood):
  1. Full-bleed hero image
  2. Metadata block — Project Type / Stage (e.g. "Leader") / Deliverables — classifies the engagement up front
  3. Narrative + media sections (client-rendered from CMS; alternating text and full-bleed visuals with generous spacer sections between)
  - URL pattern: flat `/work/<client>` — no category in path, so recategorizing never breaks links.

## Standout interaction
Confirmed live (Tiago, 2026-07-06): **the homepage doesn't scroll** — very unusual for a creative agency. Instead, an **overlay project menu** replaces scrolling entirely, and it's the most special thing on the site (this is the "HoverDrag" 1–24 module seen in code). Every project is packaged the same way — same composition system, slightly varied per project, different imagery — but always inside MetaLab's own visual language. Even huge clients like Midjourney and Calvin Klein feel like *MetaLab's* work; they reclaim ownership of the vision. **This is the site's most "guardian of the vision" quality and the core Theme-01 lesson.**

Other live observations:
- **"Phone App" feel** to the whole site: dark/light mode toggle at the top, plus live clocks showing multiple timezones around the world (pairs with the airport-code office list).
- Case study pages that exist are really well designed — strong typographic hierarchy and white space.

## How to recreate
- HoverDrag-style carousel: drag container (Swiper free-mode, or GSAP Draggable + `inertia`) + per-card hover state that swaps static image → video loop. The numbering is just an index overlay — cheap, but makes it feel curated.
- Their smooth-scroll feel = Lenis + GSAP ScrollTrigger (`scrollerProxy` wiring) — the standard premium-agency combo, and the counterpoint to Collins: MetaLab buys the feel with ~1.5 MB of JS.
- Case study metadata block (Type / Stage / Deliverables) = 3 CMS fields rendered as a spec sheet — instantly tells a prospect "this is what an engagement looks like." Trivial to implement, high clarity payoff.
- "Category → one flagship case study" portfolio model: each service/industry category leads with its single best proof instead of a wall of thumbnails.
- Office city airport codes in footer + live timezone clocks: two small text elements = global footprint signal. PAULUS could do SEL + partner cities.
- **Uniform project packaging system:** design ONE flexible case-study composition template (cover typography, image placement rules, color handling) and pour every client into it. The consistency itself communicates "our vision governs the work" — the guardian move worth recreating for PAULUS.
- Scroll-triggered video lesson (from The Atlantic page): never let two heavy videos autoplay from the same scroll region. Stagger triggers, lazy-load with `IntersectionObserver`, use poster-first loading, and prefer one hero video per viewport.

## What NOT to copy
From live browsing (Tiago, 2026-07-06):
- **"All Work" list page is the site's weakest moment** — a text-list "Sample of Our Work" with no visual previews. For a creative agency this kills the hook for prospective clients. Many projects lack a sample image or an individual case study page, so the archive feels incomplete and unattractive. The overlay menu only surfaces recent work, forcing users into this weak page for anything older. → PAULUS: every listed project needs a visual preview, even in archive views.
- **Scroll-triggered performance debt** — on The Atlantic case study, two heavy video animations fire at nearly the same scroll position ("Wanting to protect the core editorial brand…") and the page visibly slows. Avoid on the PAULUS site (see mitigation notes in How to recreate).
- **Text squeezed between images** in case studies when they go deep on process. Collins' pattern is the fix: show only the summarized hook inline, let the user expand ("Read the Full Story") for depth.
- **"Who we are" over-indexes on personal photos** of team and CEO — comes off a bit awkward. Prefer Collins' team approach (art pieces + profiles).
- **"What we do" hover animation** scroll-flashes many images at once — dilutes the impact of an otherwise good process list. One strong image beats ten flickering ones.
- **Menu navigation is disorienting** — opening the Menu gives no clear way back to where you were, forcing a decision to jump somewhere unrelated. Keep an obvious "close/return" affordance on any overlay nav.
- **"Latest News" thumbnails inside the menu** — unlabeled small thumbnails on the right side; users can't tell what the section is without stopping to read. Overkill; cut or label clearly.

From code analysis:
- 1.5 MB `_app` bundle with four animation libraries — heavier and slower than Collins; PAULUS should pick ONE animation approach, not stack them.
- Content is invisible without JS (sections hydrate client-side from Sanity) — bad for SEO/AI-crawlers compared to Collins' fully-SSR'd HTML.
- Blog buried as "Latest" with sparse cadence — don't add a blog section unless there's a publishing habit to back it.
