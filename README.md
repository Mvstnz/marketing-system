# Skincare Marketing System

An AI assistant system for creating on-brand marketing content with minimal input.
Built to run on **Codex** (and Claude Code) using the
[marketingskills](https://github.com/coreyhaines31/marketingskills) library.

## What it does

Type **`/marketing`** and pick what you want to create. The system asks a few quick
questions (you pick from numbered options), then writes finished, on-brand content:

- Instagram Post / Carousel / Story (English)
- Newsletter / Promo Email / Subject lines (German)
- Blog post (German)
- Product description (German + English)
- Campaign idea
- Image prompt (for Nano Banana / ChatGPT, with Canva finishing notes)
- Content calendar

## First-time setup

1. Install Node.js (skip if Codex already works — Node is likely installed).
2. Install the marketing library:
   ```
   npx skills add coreyhaines31/marketingskills
   ```
3. Run **`/marketing-setup`** and follow the steps. It builds your Brand Kit (tone of
   voice + audience) from a handful of your best past posts. You do **not** need to
   load all your products — when you create content you just paste that product's link.

> Full step-by-step Windows install guide: see **`INSTALL.md`**.

## Structure

```
.agents/
  skills/            # the custom skills (marketing, marketing-setup, marketing-update)
  brand/             # your Brand Kit (voice, products, audience) — built by /marketing-setup
    samples/         # your example posts (input for tone of voice)
output/              # generated content archive
marketing-system-spec.md   # internal design spec (German)
```

## Language model

- **Interface language: English** — the system always talks to you in English.
- **Content language: per channel** — Blog (DE), Instagram (EN), Email/Newsletter (DE),
  Product description (DE + EN). Set automatically; you can override.
