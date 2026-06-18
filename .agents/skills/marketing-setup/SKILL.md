---
name: marketing-setup
description: Use ONCE to build (or rebuild) the Brand Kit for the skincare marketing system. Reads a Shopify product CSV export and a folder of example posts, then writes the brand voice, product catalog, and audience files that every other marketing skill relies on. Trigger with "/marketing-setup", "set up the brand kit", "set up marketing", or the first time the marketing system is used.
metadata:
  version: 0.1.0
---

# Marketing Setup — Build the Brand Kit

You are setting up the foundation that every other marketing skill depends on.
Your job: turn the user's raw material (Shopify product export + a few example posts)
into a clean, reusable **Brand Kit** under `.agents/brand/`.

## Golden rules

- **Always talk to the user in English.** She speaks only English. (The *content* you
  later generate follows a per-channel language matrix — but setup conversation is English.)
- **Quality over quantity** for tone of voice. A handful of great example posts beats a
  big pile of mediocre ones.
- **Never invent product facts.** Only use what is in the CSV / files the user provides.
- Produce **drafts**, then have the user review the voice files once before locking them in.

## Step 1 — Locate the source material

The brand has hundreds of products, so **do NOT try to build a full product catalog.**
Setup focuses on the durable, reusable brand knowledge: **tone of voice + audience.**
Individual products are pulled on-demand from a link each time content is created
(in `/marketing`). The required material is:

1. **Example posts** — placed in `.agents/brand/samples/`. Ideally:
   - 10–20 typical Instagram captions (English)
   - 2–3 newsletters / emails (German)
   - 1–2 blog posts (German), if available
2. **Audience notes** — a few words on who buys (age, skin concerns, segments).
   Ask for these if not provided.

If this material is missing, tell the user **in English** exactly what to add and where
(e.g. "Please drop 10–20 of your best Instagram captions as text files into
`.agents/brand/samples/`, and tell me in a sentence who your typical customers are").

## Step 2 — Products are optional (no upfront catalog)

`.agents/brand/products.md` is just an **optional cache** of products the user has
already worked on. **Skip it during setup** unless the user explicitly wants a few
bestsellers saved. The normal flow is: in `/marketing`, the user pastes a product link
and the system fetches that product's data on the spot (and can save it to
`products.md` for reuse). Never invent product facts.

## Step 3 — Derive the tone of voice → `voice-de.md` and `voice-en.md`

Read the example posts. Build **two** voice files because tone does not translate 1:1:

- `.agents/brand/voice-en.md` — from the **English** Instagram captions.
- `.agents/brand/voice-de.md` — from the **German** newsletters / blog posts.

For each, capture **robust, model-independent rules** (this must work on OpenAI models
in Codex, not just Claude) — describe the voice as concrete instructions, never as
"sound like X model":

- Overall personality (e.g. warm / playful / luxurious / clinical)
- Sentence length & rhythm
- Vocabulary: words the brand uses / words it avoids
- Emoji & punctuation habits
- How it addresses the reader (du/Sie, first person, etc.)
- 3–5 short verbatim example lines that capture the voice
- A "this is off-brand" example for contrast

## Step 4 — Audience → `.agents/brand/audience.md`

Write the audience segments (e.g. younger skin / anti-aging / sensitive skin), each with:
who they are, their main skin concern, what motivates them to buy, tone notes.

## Step 5 — Review gate

Show the user a **summary in English** of what you built, then ask her to read the two
voice files once and correct anything that sounds off. Apply her corrections.
Only after her confirmation is the Brand Kit considered "locked".

## Step 6 — Done

Tell the user (in English) that setup is complete and she can now run **`/marketing`**
to create content. Mention she can re-run `/marketing-update` whenever products or
style change.

---

## Templates

If the brand files don't exist yet, base them on the template files already in
`.agents/brand/` (`voice-de.md`, `voice-en.md`, `products.md`, `audience.md`), replacing
the placeholder sections with real, derived content.
