# INNORED — Teardown

**URL:** https://www.innored.co.kr/
**Theme:** 03 Cross-Cultural
**Date reviewed:** 2026-07-06

## Why it's a reference
Seoul independent creative agency (Gangnam) — Campaign Asia's No.1 independent agency of the year in Korea 2024, Cannes Lions' most-awarded independent agency in Korea 2022 — and the closest structural comparable to PAULUS in the whole reference set: Korean independent agency, big domestic clients (LG U+, Lotte, Samyang, PepsiCo Korea, Maeil, Paris Croissant), international awards, and a website that must speak to both Korean clients and the global industry at once.

## Stack
- Framework: **Laravel (PHP)** — server-rendered pages (the `/work/list` endpoint returns 419 "Page Expired"/CSRF, Laravel's fingerprint), classic per-page CSS/JS files with version params (`?v=2.1.2`).
- Animation: **GSAP 3.12.5 self-hosted** (`/vendor/gsap-3.12.5/` — core + ScrollTrigger + ScrollToPlugin) + **Lottie 5.12.2**. No Lenis, no smooth-scroll. Vanilla JS, no React/Vue.
- CMS: custom Laravel admin (work items carry `designer_id`, `show_flag`, `order_num`, `status_flag` fields).
- Video: YouTube embeds (their channel @innoredlove) + self-hosted mp4 loops.

## Structure
- Nav pattern: Work / About / People / Contact + "Work with us" CTA; role-split contact emails (campaign / media / recruit / new business). Plus `/change` — their own conference, CHANGE2026 at COEX.
- Homepage flow (section by section):
  1. Hero — "Innovation isn't just a strategy / It's who we are" (English, word-by-word GSAP reveal)
  2. Award headlines — "Campaign Asia, No 1 independent agency of the year in Korea 2024" / "Cannes Lions, Most awarded independent agency in Korea 2022" (English)
  3. Main video + work slider → "View more work"
  4. Client logo strip (11 logos)
  5. Awards section — festival logos: Cannes Lions, Clio, One Show, NY Festivals, London International, Spikes Asia, AdFest, Busan MAD, Korea Ad Awards, YouTube Works, Google Premier Partner Awards
- Work index: 7 category filters + paginated AJAX list (`/work/list`). Data model is **fully bilingual by design** — every item has `project_name_ko/en`, `client_ko/en`, `brand_ko/en`, `brief_ko/en` — but only ~3/30 recent items actually have the English brief filled. Items carry year+month, hashtag arrays (BRANDING, TVC, TIKTOK, POPUP, OOH…), and an `awards_flag`.
- Case study structure (from /work/uplus-firefighter-voice):
  1. Full-width hero image
  2. **Bilingual title with equal visual weight** — "The People Who Fight for Every Second" / "매일 1초와 싸우는 사람들"
  3. Metadata block (Year / Client / Category) + hashtag services
  4. Brief (Korean), then video/imagery
  5. Related works (3 bilingual thumbnails)
- About: manifesto in Korean with English anchor concepts — "Beloved Idea에서 시작해 Beloved Brand로 이어지는 여정" (the journey from Beloved Idea to Beloved Brand); Work scope sections (Campaign, Media & AI Ad-tech, Creative Product, Influencer Creation, Consulting); Awards; History.

## Language strategy (the Theme-03 core)
- **No language toggle — one hybrid page.** English carries positioning/prestige (hero claims, award callouts, section titles like "Work scope"); Korean carries substance (briefs, manifesto, legal). Titles are bilingual with equal weight.
- Festival names rendered in Korean (칸 라이언즈, 클리오 어워즈) — global credentials, localized voice.
- English concepts embedded inside Korean sentences ("Beloved Idea에서 시작해 Beloved Brand로") — the bilingual texture of the Korean ad industry itself.
- The gap: the bilingual CMS exists but EN fields go unfilled (~90% Korean-only briefs) — international visitors hit a wall one level below the surface.

## Standout interaction
Confirmed live (Tiago, 2026-07-06):
- **Entry sequence** — logo animation jumping into the showreel (same staging family as Bürocratik), followed by the one-two copy punch: "Innovation isn't just a strategy, it's who we are." → Campaign Asia No.1 2024 + Cannes Lions most-awarded 2022. The first impression instantly establishes strength both locally AND globally — exactly the dual signal PAULUS needs.
- **"Awards" filter on the Work page** — a project filter dedicated to awarded work puts a spotlight on international recognition beyond Korea/Asia. The Work layout itself isn't the best we've seen, but this filter idea is a keeper.
- **Beloved Idea / Beloved Brand animated diagram** (About) — an abstract animated diagram that genuinely emphasizes their creative global vision; the high point of the About page.
- Case study "I AM NOT KING": very good layout — simple, impactful, big images in a regular grid; right-side service hashtags per project (see What NOT to copy for the missed opportunity).

## How to recreate
- Bilingual content model from day one: every CMS field duplicated ko/en (INNORED's schema is the template — name/client/brand/brief per language), then **enforce EN completion editorially** (their unfilled fields are the cautionary tale). For PAULUS: same discipline, likely with a real toggle.
- Hybrid-language art direction: decide per element class which language leads — EN for claims/navigation/prestige, KO for narrative depth — instead of mirroring whole pages.
- Their stack proves a Korean agency site doesn't need a JS framework: server-rendered Laravel + GSAP + Lottie = fast, indexable (their case pages have full SEO fields — `seo_title`, `seo_desc`).
- Role-split contact routing (campaign/media/recruit/new business) — cheap and instantly useful for a busy agency.
- Hashtag-based capability tags per project (searchable, filterable) rather than rigid categories.
- Hosting their own industry event (CHANGE) as nav-level content — an authority move beyond client work.

## PAULUS applications (Tiago, 2026-07-06)
- **LANGUAGE DECISION: the PAULUS site will be ~95% English** — Korean only for specific concepts/ideas that can't be meaningfully translated. INNORED's mixed Awards section (Korean subtitles + English body) proved the confusion of half-measures; keep sections like Awards fully English.
- **Per-text language toggle idea** — if there's an internal wish to show some project briefs in Korean, add a small KO/EN slider at the top-right of the text block (behaving like a dark/light mode switch) instead of mixing languages inline.
- **Awards filter on the Work page** — adopt: it foregrounds international recognition (PAULUS's Cannes + worldwide press) right where prospects browse.
- **Clickable service hashtags** — INNORED shows per-project service hashtags (#DIGITAL, #TVC…) but they're not clickable; PAULUS should make each tag filter all projects under that service umbrella. Pairs with Watson's capabilities→projects cross-linking.
- **Opening one-two punch** — identity claim then dated, named credentials ("Campaign Asia No.1… 2024 / Cannes Lions… 2022"). Third confirmation of this formula (Collins, Bürocratik) and the best local+global version of it.

## What NOT to copy
From live browsing (Tiago, 2026-07-06):
- **Mixed-language sections confuse** — the Awards section's Korean subtitles over English body text is muddled; pick one language per section (Awards should be fully English since its copy already is).
- **Korean-only brief text, set too small** — on "I AM NOT KING," the award icons and brief are undersized, and the Korean-only brief blocks international readers; should be English (with the optional KO toggle above).
- **Non-clickable hashtags** — service tags that look like filters but do nothing; if it looks interactive, it must be.
- **"Work with us" arrow oversized** — small composition flaw in the footer.
- **Outdated History section layout** on the About page.
- **"People" page without people** — produced photoshoot images that feel superficial, nothing about the actual team. Third data point (after MetaLab's awkward photos and Collins' good art-piece approach): team pages need authentic, team-focused content, not staged production.

From code analysis:
- Bilingual promise, Korean-only delivery — the unfilled `_en` fields undercut the international positioning the homepage claims. Worse than not promising.
- Long Korean-only privacy/legal blocks rendered inside content pages (case study pages end in the full privacy policy).
- Visual design is functional rather than crafted — none of the interaction refinement of Watson/Collins; wins on structure, not on feel.
