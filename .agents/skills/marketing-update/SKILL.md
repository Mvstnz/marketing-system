---
name: marketing-update
description: Use to keep the Brand Kit current without rebuilding it from scratch. Refreshes the product catalog from a new Shopify CSV export, and/or sharpens the brand voice from newly added example posts. Trigger with "/marketing-update", "update the brand kit", "I added new products", or "the tone is off".
metadata:
  version: 0.1.0
---

# Marketing Update — Keep the Brand Kit current

Talk to the user **in English**. This skill lets her stay independent — she can refresh
the Brand Kit herself whenever products or style change.

Ask what she wants to update (offer numbered options):

```
What would you like to update?
1) Products — I exported a fresh Shopify CSV
2) Voice — I added new example posts
3) Fix something specific (a product, a wording, the tone)
```

## 1) Products
Read the new Shopify CSV from `.agents/brand/` and rebuild `.agents/brand/products.md`
(same rules as setup: only facts from the CSV, never invent claims). Show a short
English summary of what changed (added / removed / updated products).

## 2) Voice
Read any new files in `.agents/brand/samples/` and refine `voice-de.md` / `voice-en.md`
accordingly. Keep existing good rules; only adjust where the new examples clearly shift
the tone. Show what changed and ask her to confirm.

## 3) Fix something specific (inline correction)
The user describes the problem in plain English ("the X serum is missing", "we never
say 'cure'"). Make the targeted edit to the relevant brand file and confirm.

Always confirm changes in English before considering them saved.
