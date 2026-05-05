# Pre-Session Setup Checklist

Do these steps **before** opening Claude Code. They're tedious but each one removes a class of problem you'd otherwise hit mid-session. Estimated time: **45–60 minutes.**

## ✅ 1. Install required tools

### Node.js (18 or higher)
```bash
node --version    # should print v18.x.x or higher
```
If missing → install from nodejs.org or via `nvm install 20`.

### Shopify CLI
```bash
npm install -g @shopify/cli @shopify/theme
shopify version    # should print version 3.x or higher
```

### Git
```bash
git --version
```

### Claude Code
```bash
npm install -g @anthropic-ai/claude-code
claude --version
```
Then run `claude` once and follow auth prompts.

## ✅ 2. Create a Shopify development store

1. Go to https://partners.shopify.com (free account)
2. Stores → Add store → **Development store**
3. Name it something like `redy-dev` — you'll get a URL like `redy-dev.myshopify.com`
4. **Important:** when asked about purpose, choose "Build a new store for a client" or "Start a business" — NOT "Test an app". Test stores can't process real orders later.

Note the store URL. You'll need it.

## ✅ 3. Get the Ella theme files

1. Download Ella from ThemeForest (the `.zip` you bought)
2. Unzip it. You'll see something like an `ella` folder containing `sections/`, `assets/`, `templates/`, etc.
3. Move that folder somewhere sensible:
   ```
   ~/projects/redy-shopify-theme/
   ```
4. **Important:** if the zip contains multiple theme variants (Ella ships with several presets), pick **one** to start with. Ask the support docs which preset is closest to "minimal feminine" or "wellness/beauty" — that'll need the least visual surgery.

## ✅ 4. Initialize Git

```bash
cd ~/projects/redy-shopify-theme
git init
git add -A
git commit -m "Ella theme — baseline (untouched)"
```

This is your **safety net**. Every time something breaks, `git reset --hard HEAD` wipes it back to working state.

## ✅ 5. Upload Ella to your dev store

The first time, you push the unmodified theme as a starting point:

```bash
shopify theme push --unpublished --store=redy-dev
```

Replace `redy-dev` with your actual store name. The CLI will open a browser for auth on first run. After it finishes, you'll have Ella as an unpublished theme in your store admin.

**Don't publish it yet.** We'll work against it as a "development theme" via `shopify theme dev`.

## ✅ 6. Create the reference folder

Inside your theme directory:
```bash
mkdir reference
```

Drop the following files into `reference/`:
- `redy-website-vision.html` — the design mockup (from outputs in this conversation)
- `redy-brand-guidelines.html` — the brand bible
- `redy-box-infographic.png` — the rendered infographic for visual reference
- `box-photo.png` — rename your real box photo (`IMG_1220.png`) to this for clarity
- `redy-pitch-deck.pdf` — optional, but useful context if Claude Code asks

## ✅ 7. Drop CLAUDE.md into the project root

Copy the provided `CLAUDE.md` file into the root of your theme directory (same level as `sections/` and `assets/`). Claude Code reads this automatically on every session.

## ✅ 8. Make a backup of Ella original

```bash
cp -r . ../redy-shopify-theme-backup
```

This is paranoia, but cheap. If everything goes catastrophically wrong, you have a clean copy. (Yes, Git also does this — but a separate folder protects you against `rm -rf` accidents.)

## ✅ 9. Test the dev server before involving Claude Code

```bash
shopify theme dev --store=redy-dev
```

You should see:
- A localhost URL (something like `http://127.0.0.1:9292`)
- Your Ella theme rendering in the browser, unmodified

If this doesn't work, **fix it before starting Claude Code.** Common issues:
- Wrong Node version → switch to 18+
- Auth expired → `shopify auth logout && shopify theme dev` again
- Wrong store name → check it matches `redy-dev.myshopify.com` (without `.myshopify.com` suffix)

When dev server runs cleanly, Ctrl+C to stop it. You'll restart it inside the Claude Code session.

## ✅ 10. Final folder structure check

Your project folder should now look roughly like this:

```
redy-shopify-theme/
├── CLAUDE.md                    ← project rules (read every session)
├── FIRST_SESSION.md             ← starter prompt
├── HANDOFF_CHECKLIST.md         ← this file
├── PROGRESS.md                  ← Claude Code will create/update this
├── assets/
├── config/
├── layout/
├── locales/
├── sections/
├── snippets/
├── templates/
└── reference/
    ├── redy-website-vision.html
    ├── redy-brand-guidelines.html
    ├── redy-box-infographic.png
    ├── box-photo.png
    └── redy-pitch-deck.pdf
```

If yours looks like this, you're ready.

## ✅ 11. Open Claude Code

```bash
cd ~/projects/redy-shopify-theme
claude
```

Then paste the first session prompt from `FIRST_SESSION.md`.

---

## What if I get stuck?

**During setup:**
- Shopify CLI errors → https://shopify.dev/docs/storefronts/themes/tools/cli
- Theme push fails → check your dev store has a Shopify Plan tier compatible with custom themes (development stores do by default)

**During Claude Code session:**
- Claude proposes deleting something you don't understand → say no, ask for explanation first
- Theme editor breaks after a change → `git reset --hard HEAD` and try a smaller change
- Dev server stops live-reloading → restart it (`Ctrl+C`, then re-run)

**General:**
- Save the conversation transcript at the end of each session for context. Claude Code can resume context but a saved transcript is your record.

## When to step away from Claude Code and call a human

You should hire a Shopify dev for a few hours if:
- You hit Liquid template compilation errors that don't resolve in 2 attempts
- The theme editor admin page itself becomes broken (white screen, JS errors)
- You need to do payment gateway setup, Stripe/Borica integration, or tax configuration — those are merchant-of-record decisions, not theme work
- You're at Phase 7 (launch prep) and want a senior pair of eyes before you publish

A 2-hour consultation with a Shopify dev at this stage is worth more than 10 hours of Claude Code grinding on the same bug.
