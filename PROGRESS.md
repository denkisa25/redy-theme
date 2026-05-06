# Redy — Build Progress

## Phase 2 iteration 2 — Header & Hero refinement (2026-05-07)

### Changed
- **Hero background**: switched from `--redy-cream` to `--redy-pink-soft` to match reference design
- **Hero blobs**: replaced blurred-circle blobs with solid organic shapes (ellipses, rotated) in brand colors — matching the reference's bold, graphic feel; added 7th blob in center-right position
- **Hero title**: weight 300 → light editorial style, `clamp(48px, 7vw, 96px)`, `line-height: 0.95`, `letter-spacing: -0.025em`
- **Hero eyebrow**: pill background (`rgba(255,255,255,0.7)`) + pulsing animated red dot via CSS `::before`
- **Ghost button**: changed from bordered pill to underlined text link style (matching reference)
- **Primary button**: hover now lifts with `translateY(-2px)` + red shadow
- **Product card**: `aspect-ratio: 4/5`, flex column layout, stronger red shadow (`0 40px 80px -20px rgba(200,16,46,0.25)`), pink-soft `::before` blob decoration
- **Product card visual**: pink-soft background, `flex: 1` to fill space, inner product box with dashed red border
- **Product card name**: 44px weight 300 (light Fraunces)
- **Product price**: 40px weight 300
- **Nav CTA button**: injected "Поръчай" red pill button into `header-functions.liquid` before cart icon (desktop only)
- **Nav links**: forced lowercase via CSS

### Next
- Phase 3 complete — move to Phase 4: custom sections (box contents, infographic, founder story, donation CTA, FAQ)
- Start with `box-contents.liquid` — 7-card grid of what's inside the box
