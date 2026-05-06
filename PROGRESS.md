# Redy — Build Progress

## Phase 5 — Product page (2026-05-07)

### Changed
- **`templates/product.json`**: switched main section from `scheme-6` (white/generic) to `scheme-1` (cream bg + Redy red buttons)
- **Block cleanup**: removed vendor/SKU/barcode block, product countdown, hot stock indicator, size chart/colour comparison/ask-an-expert perks, customization option — all noise for a single-SKU brand
- **Donate note**: added text block under price — "Купи едно — даряваш едно на нуждаещо се момиче."
- **Product tabs**: renamed "Description" → "За кутията", "Shipping & Return" → "Доставка"; removed unused Additional Information and Custom Tab tabs
- **Section order**: removed recently-viewed-products and product-recommendations sections (single-product store)
- **`assets/redy-tokens.css`**: added Phase 5 rules — Fraunces weight-300 product title, red pill ATC button, Fraunces price display, red tab active indicator, sticky ATC cream bg, variant pill red selected state

### Next
- Phase 6 — Polish: mobile QA, performance, SEO meta, OG images, legal pages (GDPR, privacy, terms, returns)

## Phase 6 — Polish (2026-05-07)

### Changed
- **`sections/faq-redy.liquid`** (new): native `<details>` accordion, 6 Bulgarian FAQ items, 2-col grid matching reference design, red +/× toggle icon
- **`templates/index.json`**: disabled all 10 Ella default homepage sections (slideshow, collection lists, lookbook, marquee, media gallery); added `faq_redy_main` between donation CTA and the disabled sections
- **`assets/redy-tokens.css`**: Phase 6 FAQ styles — cream background, Fraunces heading, border-top accordion list, animated red icon on open state; mobile 1-col at 900px
- **SEO**: Ella's `meta-tags.liquid` already outputs correct OG/Twitter tags — store name, description, and OG image to be configured in Shopify Admin > Online Store > Preferences
- **Product page upload fixes**: restored all block IDs to block_order (Shopify requires every block in `blocks` to also appear in `block_order`); hid unwanted blocks via CSS `display:none`

### Next
- Phase 7 — Launch prep: Еконт shipping app, BGN currency, payment gateway, test checkout end-to-end
- Admin tasks: set store name to "Redy", set SEO description, upload OG social sharing image (1200×630px)

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
