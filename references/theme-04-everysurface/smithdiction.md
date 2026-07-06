# Smith & Diction — Teardown

**URL:** https://smith-diction.com/
**Theme:** 04 Every Surface
**Date reviewed:** 2026-07-06

## Why it's a reference
A two-person Philadelphia studio (Smith = design, Diction = copywriting; "Thoughtful identities for imaginative clients.") that lands major AI clients — Perplexity, Gamma, Superhuman, Alma — and shows identities deployed across *every physical and digital surface*: packaging, billboards, matchbooks, die-cast pins, motion, UI. The anti-Pentagram: every-surface breadth achieved by a duo with almost zero infrastructure, where the *writing voice* is the differentiator.

## Stack
- Framework: **WordPress 7.0 + Semplice 7** — the off-the-shelf designer-portfolio theme (by Tobias van Schneider). GSAP + Swiper arrive bundled with the theme, not hand-wired.
- Case studies: **hosted on Medium** (medium.com/smith-diction) — the work page links out to articles.
- Shop: **BigCartel** (smithdiction.bigcartel.com). Process documentation: shared **Figma** prototype.
- The entire stack is rented commodity parts — likely <$500/year. Every dollar of impression comes from the work and the words, none from the plumbing. (Server even runs Mod_Security that blocks non-browser user agents — scrapers get 406.)

## Structure
- Nav pattern: Work / Logos / Blog (→ Medium) / Contact / Shop (→ BigCartel). That's it.
- Homepage flow: header image → logo showcase carousels (Perplexity, Ingredient AI, Human Ventures, Rail Park, Living Roots, Two Persons Coffee…) → contact CTA ("Reach out with all project & press inquiries to: mike@smith-diction.com") → Instagram footer.
- Work page: one long page of projects, each = image set + a single crafted sentence + links out (Medium article, live client site). The one-liners carry the every-surface story: "We put their coffee in boxes, not just bags—creating a unique, thoughtful unboxing experience" (Elixr); "Gamma will help you get your ideas out into the universe."
- Case study structure (Medium, from "Branding Perplexity AI" — ~9 min read):
  1. Opens with an anecdote from the client conversation ("We want the brand to feel like a Scandinavian subway system")
  2. Chronological process: symbol → wordmark → typography → color/product → brand elements, with the *reasoning* for each decision
  3. Sketches and dead-ends shown alongside final applications (logo variations, cursor animations, UI mockups, patterns, posters)
  4. Individual contributors credited
- Tone: conversational, irreverent, opinionated — "Uppercase P's are a bitch for kerning," "cough*google*cough." The copywriting half of the studio is fully audible.

## Standout interaction
Confirmed live (Tiago, 2026-07-06): **the Work page grid** — very simple but effective. It quickly shows the different surfaces and mediums their logos/identities successfully landed on, and despite the density of visual information the page *feels light*. The grid and composition are the standout; the message a prospect receives is exactly: "if you hire us, we can produce things in a variety of mediums."

Also: the landing page focuses immediately on their strongest USP — logo development. An impactful, honest start.

**Reviewer's caveat (Tiago):** Smith & Diction isn't the same company profile as PAULUS — it's in the list as an inspiration source for *which images* make impact and communicate multi-medium capability, not as a structural model.

## How to recreate
- **One crafted sentence per project** — the work page proves a single well-written line ("boxes, not just bags") does more than a paragraph of agency-speak. PAULUS: invest copywriting effort in project one-liners; they're the highest-leverage words on the site.
- **Process-narrative case studies with dead-ends included** — the Perplexity article's honesty (sketches, failures, reasoning) builds more trust than polished-only galleries. Pairs with W+K's BTS grids and INNOCEAN's insight pages: show the thinking.
- **Anecdotal openings** — start case studies with the client conversation moment, not the deliverables list.
- **Voice as brand system** — for a studio selling copywriting, every caption proves the product. PAULUS sells creative solutions; the site's own interactions/copy must do the same (consistent with our "site must demonstrate craft" principle).
- Publishing case studies where distribution lives (Medium) is real strategy for a 2-person shop — but rejected for PAULUS (see What NOT to copy); keep everything on-domain, syndicate summaries outward at most.
- **Density-that-feels-light grid** — the Work page shows many mediums at once yet stays light: generous spacing, consistent image treatment, one line of text per project. The reference for PAULUS's deliverables-grid moments (with Watson's color-filter idea as the premium variant).

## What NOT to copy
From live browsing (Tiago, 2026-07-06):
- **Medium as the individual work page — the worst thing about this website.** Definitively against it; the Blog-on-Medium too: avoid completely. (PAULUS: all case studies and articles on-domain.)
- **Logos page composition** — simple and effective idea, but the composition and white spacing could be better.

From code analysis:
- **Off-domain case studies** — the deep content (and its SEO/discovery value) accrues to medium.com, not smith-diction.com; links can rot; no design control over the reading experience. Wrong trade-off for PAULUS.
- Off-the-shelf Semplice look — fine when the portfolio pieces carry everything, but the site itself demonstrates zero web craft; PAULUS needs the site to be evidence.
- Single named contact (mike@) and Instagram-only footer — right scale signals for a duo, wrong for an agency pitching enterprise clients.
- Mod_Security blocking non-browser agents also blocks legitimate crawlers/AI tools — check what PAULUS's host blocks by default.

**[Tiago's observations:]**
