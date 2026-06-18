# Image Prompt Smith

Followed when the user picks **9) Image prompt** in `/marketing`.

The system does **not** generate images itself (no API, no cost). It produces a
**ready-to-paste edit prompt** that the user runs in her own app, plus Canva finishing
notes. She always supplies a **real product photo** as the input image — so this is
image *editing* (place the real product in a scene), never inventing a product.

## Golden rules
- Talk to the user in **English**.
- The goal is to **keep the real product exactly as photographed** (label, packaging,
  texture) and build a new scene/background around it.
- Always **leave deliberate negative space** for the Canva step (text overlay, logo).
- Never describe a fake/altered product label.

## Step 1 — Confirm the input
Tell her to have her **product photo** ready (the real bottle/jar/tube). Ask which
product it is (offer options from `products.md`) so the prompt can reference correct
ingredients/positioning for mood — but the *visual* comes from her photo.

## Step 2 — Choose the tool

```
Where will you generate this image?
1) Nano Banana (Gemini)
2) ChatGPT (GPT Image)
```

The two tools respond to different prompt styles — produce the matching variant below.

## Step 3 — Gather the creative brief (numbered options)
Keep it minimal; generate options from the product + Brand Kit:

1. **Use case / format** — `1) IG feed post (square)  2) IG story (vertical 9:16)
   3) Carousel slide  4) Product hero  5) Lifestyle/flatlay`
2. **Mood / setting** — generate 3–4 concrete scene options fitting the brand
   (e.g. "minimal stone bathroom shelf, soft morning light", "fresh botanicals + water
   droplets", "warm beige studio backdrop"), plus "Surprise me".
3. **Text overlay later in Canva?** — `1) Yes, leave space at top  2) Yes, at bottom
   3) No text` → drives where the negative space goes.

## Step 4 — Produce the prompt(s)

### If Nano Banana (Gemini)
Conversational, instruction-style edit prompt. Format:

> Using the attached product photo, keep the product **exactly as shown** (label,
> shape, and colors unchanged). Place it [scene/setting]. Lighting: [light]. Mood: [mood].
> Composition: [format/aspect], with clean **negative space at [top/bottom]** for text.
> Photorealistic, high detail, soft natural shadows. Do not alter the product or its label.

### If ChatGPT (GPT Image)
Slightly more descriptive, single-paragraph prompt + an explicit "edit, don't replace"
instruction:

> Edit the attached image. Preserve the real skincare product unchanged (same label,
> packaging, proportions). New background: [scene]. [light], [mood], [format/aspect ratio].
> Keep [top/bottom] area uncluttered for later text. Photorealistic product photography
> style, premium skincare aesthetic.

Give the prompt in a copy-paste code block so she can paste it directly.

## Step 5 — Canva finishing notes
Always append short, concrete next-step notes, e.g.:
- Add the headline in the reserved [top/bottom] space; keep brand font/colors.
- Drop the logo in a clean corner.
- Export at the right size (IG post 1080×1080, story 1080×1920).
- Optional: subtle brand-color overlay/border.

## Step 6 — Follow-up
Offer:
```
1) Different mood/scene
2) Other tool's version too
3) A second variant
4) Done
```
