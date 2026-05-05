# Redy Shopify Theme — Project Context

This file is read by Claude Code at the start of every session. It establishes the project context, brand rules, and operating principles. **Read this entire file before making any changes.**

## What we're building

I'm reskinning the **Ella multipurpose Shopify theme** to become the storefront for **Redy** — a Bulgarian brand selling a curated first-menstruation box for girls aged 9–13. The site is **redy.one** and is **Bulgarian-first** (no English fallback needed for v1).

The destination is a Shopify dev store. The current theme is a stock Ella install. My target design is a custom HTML mockup at `reference/redy-website-vision.html` and a brand guidelines doc at `reference/redy-brand-guidelines.html`.

This is a **reskin, not a rebuild.** Ella's e-commerce engine, cart, checkout, product page logic, and section architecture stay. We replace visual identity (colors, typography, hero content, custom sections) on top of that foundation.

## The brand in one paragraph

Redy is *„Когато моментът дойде, тя е Redy."* — when the moment comes, she's Redy. Created by a mother for mothers. The voice is **gentle but not babyish, supportive not dramatic, informed not clinical**. Three pillars in priority order: майчина топлина (mother's warmth), социална смелост (social courage), еко грижа (eco care). Pilot is 50 hand-packed boxes at 49 лв. Social model: buy one, donate one.

## Brand tokens — single source of truth

Use these everywhere. Do not invent new colors or fonts.

### Colors
```
--redy-red:       #C8102E   /* primary, CTAs, accents */
--redy-red-deep:  #9B0E22   /* hover states, depth */
--redy-pink:      #FF8FB5   /* logo bubble, secondary */
--redy-pink-soft: #FFE4ED   /* soft backgrounds */
--redy-blush:     #FBE9EC   /* alternating sections */
--redy-cream:     #FFF5EE   /* primary background */
--redy-peach:     #F5B384   /* tertiary accent */
--redy-lavender:  #B5A4D4   /* tertiary accent */
--redy-ink:       #2A1418   /* body text, headings */
--redy-charcoal:  #4A2A30   /* secondary text */
```

### Typography
- **Display (headings, emphasis):** Fraunces — serif with character. Always italic for *accented* words inside otherwise-roman headings.
- **Body:** DM Sans — clean, readable
- **Script (logo, small handwritten accents):** Caveat — used sparingly

Load all three from Google Fonts. Variable weights preferred.

### Tone for any UI copy you write
- Bulgarian only
- Lowercase first words after dashes work fine ("— създаден от майка")
- Use „български кавички" not "ascii quotes"
- Em-dash (—) between thoughts, not hyphens
- Italic on emotional emphasis, never bold-as-shouting

## File locations

- **Theme code:** the root of this directory (Ella installation)
- **Reference design:** `reference/redy-website-vision.html` — the target visual
- **Brand guidelines:** `reference/redy-brand-guidelines.html`
- **Infographic SVG:** `reference/redy-box-infographic.svg` (extract from website-vision.html, the `#infographic` section)
- **Real product photo:** `reference/box-photo.png` — use this for inspiration, not as a literal product image
- **Original Ella backup:** `_ella-original/` — never modify, only read for diffing

## Operating principles for this project

### Always
1. **Read before writing.** Before modifying any Liquid file, view it in full, understand its schema, and check what other sections include it via `{% render %}` or `{% section %}`.
2. **Preserve schema integrity.** Never delete schema fields from existing Ella sections. If a field is unused, leave it. Removing fields can corrupt the theme editor for merchants.
3. **Commit before each significant change.** This project is on Git. After every working state, commit with a descriptive message. If something breaks, we revert, we don't debug forward.
4. **Test in `shopify theme dev` before committing.** Visual regressions are easier to catch when watching the browser refresh. If the dev server is running, screenshots welcomed.
5. **Match the reference design's intent, not its literal CSS.** The reference HTML uses custom utility classes. Ella has its own. Translate the *design decision* (e.g. "warm cream background with red accent") into Ella's existing patterns.
6. **Bulgarian by default.** Every new string goes into `locales/bg.json` first, with an `en.default.json` mirror only if Ella enforces it.

### Never
1. **Never edit a published theme directly.** Always work against a duplicate or development theme.
2. **Never invent new color tokens** outside the brand palette above.
3. **Never use emoji in production copy.** Decorative ✿ in headings is fine sparingly. ☺️ 😊 etc. are out.
4. **Never reproduce children's bodies, period blood imagery, or clinical medical illustrations.** The brand uses organic blob shapes, soft backgrounds, and warm photography only.
5. **Never auto-update Ella from the admin** while this project is mid-customization. Theme updates overwrite custom changes.
6. **Never publish to the live store** without explicit confirmation in the chat. Working theme = development theme only.

## Section mapping — what becomes what

When converting the reference HTML to Ella sections, expect roughly this mapping. The exact Ella section names depend on the version installed; check `sections/` directory.

| Reference HTML block | Likely Ella section |
|---|---|
| Sticky nav with `redy.one` + Поръчай CTA | `header.liquid` or `header-search.liquid` |
| Hero with product card (49 лв) | Replace `slideshow.liquid` or build new `hero-redy.liquid` |
| „Какво има вътре" 7-card grid | New custom section: `box-contents.liquid` |
| Box infographic (the SVG illustration) | New custom section: `box-infographic.liquid` |
| Founder story (Анна Г.) | Adapt `image-with-text.liquid` or build `founder-story.liquid` |
| FAQ accordion | Ella likely has `faq.liquid` already — restyle it |
| „Купи една — даряваш една" CTA | New section: `donation-cta.liquid` |
| Footer 4-column | `footer.liquid` |

## Order of operations (recommended)

Do these phases in order. Don't skip ahead — global tokens first, then layout, then content.

1. **Phase 0 — Setup.** Verify dev server runs. Take baseline screenshot. Initial Git commit.
2. **Phase 1 — Tokens.** Wire brand colors into Ella's settings (theme settings → Colors). Load Fraunces/DM Sans/Caveat. Set type scale.
3. **Phase 2 — Header & Footer.** Get nav and footer matching the reference. These appear on every page.
4. **Phase 3 — Homepage hero.** Build the hero section with the 49 лв product card.
5. **Phase 4 — Custom sections.** Box contents, infographic, founder story, donation CTA, FAQ.
6. **Phase 5 — Product page.** Adapt Ella's product template to match Redy aesthetic.
7. **Phase 6 — Polish.** Mobile QA, performance, SEO meta, OG images, legal pages (GDPR, privacy, terms, returns).
8. **Phase 7 — Launch prep.** Еконт shipping app, BGN currency, payment gateway, test checkout end-to-end.

## What good progress looks like

Each session should end with:
- A working `shopify theme dev` preview
- A clean Git commit
- A short note in `PROGRESS.md` (in this directory) listing what changed and what's next
- No console errors, no broken admin editor

## Out of scope for v1

Don't go down these rabbit holes:
- Multi-language (English version) — Bulgarian only for v1
- Customer accounts / loyalty — guest checkout fine for pilot
- Subscription billing — boxes are one-off purchases for now
- Multi-currency — BGN only for Bulgarian market
- Blog — maybe in v2
- Multi-product collections — Redy has one product at launch
- Mega menu — single product means single nav
