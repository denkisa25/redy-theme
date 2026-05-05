# First Claude Code Session — Copy-paste this prompt

This is the **exact prompt** to paste into Claude Code at the start of your very first session. It's been carefully scoped to get you a plan before any code touches the theme. Don't skip the planning step — it saves hours later.

---

## Step 1 — Open Claude Code in the project root

```bash
cd /path/to/redy-shopify-theme
claude
```

## Step 2 — Paste this as your first message

> I have the Ella multipurpose Shopify theme in this directory. I'm reskinning it for a Bulgarian brand called **Redy** (redy.one) — a curated first-menstruation box for girls aged 9–13.
>
> Before you touch any code, I need you to do **discovery and planning only**. Specifically:
>
> 1. Read `CLAUDE.md` in full. Confirm you understand the brand rules, file locations, and operating principles.
> 2. Read `reference/redy-website-vision.html` end to end. This is the target design.
> 3. Read `reference/redy-brand-guidelines.html` for the visual system.
> 4. Look at `reference/box-photo.png` to understand the actual product (the real Redy box laid out on grass with all 8 items visible).
> 5. Map the Ella theme's structure: list the contents of `sections/`, `templates/`, `snippets/`, `layout/`, `config/`, `locales/`. Identify which existing Ella sections we'll reuse, which we'll modify, and which we'll need to build new.
> 6. Identify the schema settings file (`config/settings_schema.json`) — tell me what color tokens and font settings already exist so we know what to override vs add.
> 7. Check `assets/` for the main CSS/SCSS file and report its size and structure.
> 8. Verify `shopify` CLI is installed and that I can run `shopify theme dev` against this folder. If anything is missing for setup, list it.
>
> When you're done, give me **one document** with these sections:
>
> - **Discovery summary** (what's in the theme, key files)
> - **Phase 1 plan** (just the tokens phase — colors, fonts, type scale wiring)
> - **Risks and gotchas** specific to this Ella version
> - **Three questions for me** before we start writing code
>
> Do not modify any files in this session. The output should be a markdown plan only.

---

## Step 3 — Review the plan

Read what Claude Code produces carefully. Look for:

- Does it correctly identify Ella's section files? (Ella usually has 50+ sections — Claude should list them, not invent names.)
- Does the Phase 1 plan respect Ella's existing schema (i.e. it's adding to settings, not replacing them)?
- Are the risks specific (e.g. "Ella's color settings use SCSS variables in `assets/theme.scss.liquid` which is compiled at theme save") or vague?
- The three questions should be substantive. If they're trivial ("what colors do you want?" — those are in CLAUDE.md), push back.

## Step 4 — Then commit and start Phase 1

Once the plan looks right:

```
> Looks good. Commit a baseline snapshot with message "Ella original baseline" before any changes. Then proceed with Phase 1 — wire the brand colors and typography into Ella's theme settings. Stop after Phase 1 so I can preview before we move on.
```

---

## Tips for the rest of the project

**Phase boundaries are commit boundaries.** End every phase with: tested in browser → screenshot → Git commit → update `PROGRESS.md`. If a phase is taking more than ~3 hours, break it down further.

**When something breaks, revert, don't debug.** Git is your safety net. `git reset --hard HEAD` wipes the bad state. Then rephrase the task more narrowly.

**Use the Shopify theme editor as a sanity check.** After every Liquid change, open `https://your-dev-store.myshopify.com/admin/themes` → Customize → see if the theme editor still loads cleanly. If a schema field broke, you'll know immediately.

**For the infographic section specifically:** The SVG is ~400 lines. Ask Claude Code to extract it as a snippet (`snippets/redy-box-infographic.svg.liquid`) so the section file stays readable. Each text label and product description should be a schema field so you can edit copy from the admin.

**When you reach the product page (Phase 5):** Don't try to convert the whole page at once. Identify the 3–4 elements that differ from Ella's default (price typography, CTA button, "what's inside" accordion, donation messaging) and only touch those.

**Don't customize what you're not using.** Ella has wishlists, quick view, currency switchers, country selectors, product comparison. None of these matter for Redy v1. Disable them in theme settings, don't try to delete them from code.
