---
name: marketing
description: The single entry point for creating any marketing asset for the skincare brand — Instagram post/carousel/story, newsletter, promo email, blog post, product description, campaign idea, image prompt, or content calendar. Trigger with "/marketing", "create marketing content", "write me a post", "I need a newsletter", etc. Always reads the Brand Kit in .agents/brand/ first.
metadata:
  version: 0.3.0
---

# Marketing — Create on-brand content

The single entry point. The user picks what to create, gives minimal input, and gets
finished, on-brand content.

## Golden rules (read every time)

- **Talk to the user in English at all times.** She speaks only English.
- **Generate the CONTENT in the channel's language** (see matrix below) — but explain
  what you're doing in English.
- **Read the Brand Kit FIRST**, every run:
  `.agents/brand/voice-de.md`, `.agents/brand/voice-en.md`,
  `.agents/brand/products.md`, `.agents/brand/audience.md`.
  - If `products.md` still contains the "_(not filled in yet)_" placeholder, stop and
    tell her **in English** to run `/marketing-setup` first.
- **Ask only what you cannot infer.** Set content language automatically. Turn every
  required question into **numbered options** generated from the Brand Kit — she types a
  number, she doesn't write prose. Mark anything you assumed as `Assumption: …` so she
  can override.
- **Never invent product facts.** Use only what's in `products.md`.
- **Orchestrate the library for quality, don't hand off control.** Apply the frameworks
  from the installed `coreyhaines31/marketingskills` skills (e.g. `social`, `copywriting`)
  using the Brand Kit as context — but do NOT re-run their long questionnaires; you have
  already gathered the inputs here.

## Channel → content language
| Asset | Content language |
|---|---|
| Blog post | German |
| Instagram (post / carousel / story) | English |
| Newsletter / promo email / subject lines | German |
| Product description | German + English |

## Step 1 — Main menu

Show this menu and ask her to type a number:

```
What would you like to create?
 1) Instagram post           (English)
 2) Instagram carousel       (English)
 3) Instagram story          (English)
 4) Newsletter               (German)
 5) Promo email              (German)
 6) Blog post                (German)
 7) Product description      (German + English)
 8) Campaign idea
 9) Image prompt             (Nano Banana / ChatGPT)
10) Content calendar
11) Reel / short-video script (English)
```

All asset types are implemented. For **9) Image prompt**, read and follow
`references/image-prompt.md`. For the others, follow the matching section below.

Note: Instagram feed posts (1) double as **Facebook** posts (cross-posted 1:1).

---

## Instagram Post (English)

Content language: **English**. Apply the `social` skill's Instagram principles +
`voice-en.md`.

### Intake (numbered options, minimal)
Ask these, each as a numbered list. Generate the option values from the Brand Kit /
her seed input. Pre-fill sensible defaults and mark assumptions.

1. **Product / topic** — list products from `products.md` as options + "Other (type it)".
   This is the one thing you usually cannot guess; ask it first.
2. **Goal** — `1) Awareness  2) Engagement  3) Drive sales  4) Educate  5) Launch`
3. **Audience** — list the segments from `audience.md` as options.
4. **Angle** — generate **3 concrete hooks** specific to this product + goal as options,
   plus "Surprise me".

If she gave a free-text brief that already answers some of these, skip those questions.

### Produce
Write the post using `voice-en.md`:
- A scroll-stopping **hook** (first line)
- **Caption body** in the brand voice
- **CTA** matching the goal
- **Hashtags** following the hashtag habits in `voice-en.md`
- A one-line **image direction** ("Pair with: …") — if she wants the actual image prompt,
  point her to menu option 9 (Image prompt).
- A short **Facebook note**: this post can be cross-posted 1:1 to Facebook (same English
  content); only flag a tweak if hashtag count should be trimmed for FB.

### After producing
1. **Save** to `output/` (see Output convention) and show in chat.
2. Offer tuning + A/B (see Follow-up actions).

---

## Newsletter (German)

Content language: **German**. This is a single broadcast newsletter (NOT a drip
sequence — do not use the `emails` sequence flow). Borrow structure/clarity principles
from `copywriting`; voice from `voice-de.md`.

### Intake (numbered options, minimal)
1. **Occasion / purpose** —
   `1) Neues Produkt  2) Aktion/Rabatt  3) Tipps/Education  4) Saisonales  5) News/Update`
2. **Featured product(s)** — from `products.md` (allow multiple), or "kein bestimmtes".
3. **Audience** — segments from `audience.md`.
4. **Primary CTA** — `1) Jetzt shoppen  2) Mehr erfahren  3) Aktion sichern  4) Andere`.
   If there's a discount/offer, ask for the detail (code, %, deadline) — don't invent it.

### Produce (in German)
- **3 subject line options** (she picks / can request more)
- **Preheader / Vorschautext**
- **Newsletter body** in `voice-de.md`: greeting → value/story → product highlight
  (facts only from `products.md`) → clear CTA → sign-off
- Keep it skimmable (short paragraphs, optional subheads).

### After producing
1. **Save** to `output/` and show in chat.
2. Offer **more subject lines**, tuning, and A/B (see Follow-up actions).

---

## Instagram Carousel (English)

Content language: **English**. Apply `social` + `voice-en.md`.

### Intake (numbered options)
1. **Product / topic** — options from `products.md` + "Other".
2. **Carousel purpose** — `1) Educate (how-to/tips)  2) Product benefits  3) Myth-busting
   4) Before/after routine  5) Listicle`
3. **Audience** — segments from `audience.md`.
4. **Number of slides** — `1) 5  2) 7  3) 10` (default 7, mark as assumption).

### Produce
- **Slide-by-slide** breakdown (Slide 1 = hook, last slide = CTA). For each slide:
  on-slide text (short) + a one-line visual direction.
- A **caption** for the post in `voice-en.md` + hashtags.

After producing: save + offer tuning/A/B.

---

## Instagram Story (English)

Content language: **English**. Short, casual, vertical. Apply `social` + `voice-en.md`.

### Intake (numbered options)
1. **Product / topic** — from `products.md` + "Other".
2. **Story goal** — `1) Quick promo  2) Poll/engagement  3) Behind-the-scenes
   4) Product tip  5) Countdown/launch`
3. **Interactive element?** — `1) Poll  2) Question sticker  3) Quiz  4) Countdown  5) None`

### Produce
- A **sequence of 1–3 story frames**: for each, the on-screen text + sticker suggestion
  + a one-line visual direction. Keep text very short.
- A clear **swipe-up/CTA** line.

After producing: save + offer tuning/A/B.

---

## Promo Email (German)

Content language: **German**. A single promotional broadcast (not a sequence).
Borrow urgency/clarity from `copywriting`; voice from `voice-de.md`.

### Intake (numbered options)
1. **Offer type** — `1) Rabatt %  2) Aktionscode  3) Gratis-Zugabe  4) Bundle
   5) Limited Edition`. Ask for the concrete detail (%, code, deadline) — never invent it.
2. **Featured product(s)** — from `products.md`.
3. **Audience** — from `audience.md`.
4. **Urgency** — `1) Klar befristet (Deadline)  2) Sanft  3) Keine`.

### Produce (German)
- **3 subject line options** (offer more on request) — punchy, offer-led.
- **Preheader**.
- **Body** in `voice-de.md`: hook → offer + value → product highlight (facts from
  `products.md`) → strong CTA → urgency line (only if a real deadline exists).

After producing: save + offer more subject lines, tuning, A/B.

---

## Blog Post (German)

Content language: **German**. Apply `copywriting` + (if available) `seo-audit` principles;
voice from `voice-de.md`.

### Intake (numbered options)
1. **Topic / angle** — if she gives a seed, generate 3 title/angle options; else ask.
2. **Goal** — `1) SEO/Ratgeber  2) Produkt-Storytelling  3) Inhaltsstoff erklären
   4) Routine/How-to  5) Saisonales`
3. **Related product(s)** — from `products.md` (for natural product mentions), or none.
4. **Length** — `1) Kurz (~500 W)  2) Mittel (~900 W)  3) Lang (~1500 W)` (default mittel).

### Produce (German)
- SEO-friendly **title** + meta description.
- **Structured article**: intro → H2 sections → conclusion with soft CTA.
- Natural product mentions using only facts from `products.md`.

After producing: save + offer tuning/A/B.

---

## Product Description (German + English)

Content language: **German AND English** (produce both). For Shopify.
Apply `copywriting`; voice from `voice-de.md` (DE) and `voice-en.md` (EN).

### Intake (numbered options)
1. **Which product** — from `products.md` (required).
2. **Length/format** — `1) Kurz (Card)  2) Standard  3) Ausführlich (mit Benefits-Liste)`.
3. **Emphasis** — `1) Inhaltsstoffe  2) Benefits/Ergebnis  3) Anwendung  4) Ausgewogen`.

### Produce
Output **both languages**, clearly separated (`## Deutsch` / `## English`):
- Compelling product title + description
- Key benefits (bullets) — facts only from `products.md`
- Ingredients highlight + how to use
Keep the two versions tonally adapted (not literal translations).

After producing: save + offer tuning/A/B.

---

## Campaign Idea

Content language: explain/brainstorm in **English** (it's internal planning); any sample
copy inside follows the target channel's language. Apply `marketing-ideas` +
`content-strategy` thinking.

### Intake (numbered options)
1. **Occasion / driver** — `1) Produkt-Launch  2) Saisonal (z.B. Sommer)  3) Sale/Aktion
   4) Awareness  5) Restock/Bestseller`.
2. **Hero product(s)** — from `products.md`, or "brand-wide".
3. **Primary goal** — `1) Sales  2) Reach/Awareness  3) List growth  4) Engagement`.

### Produce
- A **campaign concept**: theme, core message, hook, suggested duration.
- A **channel plan** across the brand's channels (Blog DE, IG EN, Email DE) — what each
  piece does, in the right language.
- 2–3 concrete content ideas per channel.
- Offer: "Want me to create any of these now?" → feed straight into the matching flow.

After producing: save + offer tuning.

---

## Content Calendar

A **plan/overview**, not a batch of finished content. Apply `content-strategy` +
`social` planning.

### Default weekly rhythm (the brand's standard cadence — use this as the template)
| Day | Blog | IG / Facebook | Stories | Newsletter / Promo |
|-----|------|---------------|---------|--------------------|
| Mon | —    | Story (Teaser / Poll) | ✓ | — |
| Tue | Blog #1 | Educational / Carousel | ✓ | — |
| Wed | —    | Product / Campaign Post | ✓ | Newsletter |
| Thu | —    | Reel / Routine | ✓ | — |
| Fri | Blog #2 or #3 | Promotion Post | ✓ | — |

Build calendars **on top of this rhythm by default** — fill the slots with concrete
topics/products rather than inventing a new structure. Deviate only if she asks.

### Intake (numbered options)
1. **Timeframe** — `1) 1 week  2) 2 weeks  3) 1 month`.
2. **Focus** — `1) Balanced mix  2) Around a launch  3) Around a sale  4) Education-heavy`.
3. **Featured product(s)** — from `products.md`, or brand-wide.

### Produce
A **table** that mirrors the weekly rhythm above:
Day | Blog | IG/Facebook | Stories | Newsletter/Promo — filled with concrete
topics/products/angles, respecting the language matrix. Keep it realistic for one person.
Save to `output/` as the calendar file.

### Bridge to creation (important)
After showing the calendar, tell her she can say e.g. **"create item 3 from the calendar"**
— then load that row's context (channel, product, angle, language) and run the matching
asset flow above **without re-asking** what's already in the calendar row.

---

## Reel / Short-Video Script (English)

Content language: **English**. This produces a **script/concept**, not a video.
Apply the `video` skill's short-form principles + `voice-en.md`.

### Intake (numbered options)
1. **Product / topic** — from `products.md` + "Other".
2. **Reel type** — `1) Routine/how-to  2) Before/after  3) Tips/educational
   4) Product reveal  5) Trend/relatable`.
3. **Length** — `1) ~15s  2) ~30s  3) ~45s` (default ~30s).
4. **Audience** — segments from `audience.md`.

### Produce
- A strong **hook** (first 1–2 seconds, on-screen + spoken).
- A **shot-by-shot script**: scene | on-screen text | voiceover/action | timing.
- **Audio idea** (trending sound type or original voiceover).
- A **caption** in `voice-en.md` + hashtags.
- Note: also cross-posts to Facebook/Reels.

After producing: save + offer tuning/A/B.

---

## Follow-up actions (offer after every asset)

Present as numbered options (English prompt, content stays in its channel language):

```
What next?
1) Shorter
2) Punchier / different tone
3) Different angle
4) Create an A/B variant
5) (emails only) More subject lines
6) I'm happy — done
…or just tell me what to change.
```

- **A/B variant:** produce a meaningfully different second version (different hook/angle),
  not a trivial reword. Label them "Version A" / "Version B".
- Free-text changes are always allowed alongside the numbered options.

## Output convention

Save every finished asset as a Markdown file in `output/`:

```
output/YYYY-MM-DD_<asset-type>_<short-slug>.md
```

e.g. `output/2026-06-18_ig-post_vitamin-c-launch.md`.
Include a small header (asset type, language, product, date) then the content.
For A/B variants, save both in the same file under "Version A" / "Version B".
Always also display the content in the chat for easy copy-paste.
