---
name: analyze-outfit-aesthetic
description: Analyze the aesthetic characteristics of a single outfit (from an image) and output a fixed-shape structured JSON description — color palette, contrast, saturation, silhouette, proportions, textures/materials, accessories, visual density, and styling notes. Use this once per outfit so results are comparable across many outfits. Does NOT make outfit recommendations or compare outfits itself — that is the calling agent's job.
---

# Analyze outfit aesthetic

## Purpose

This Skill has exactly one job: look at **one** outfit photo and describe its
aesthetic characteristics in a consistent, structured way. It never decides
whether an outfit is good, never compares outfits to each other, and never
recommends anything — it only produces a structured description. Applying
this same Skill to many outfits one at a time is what lets a calling agent
later compare the results and find patterns.

## Input

The path to a single outfit image (e.g. `data/favorite_outfits/outfit_03.jpg`).

## What to do

1. Look at the image directly (read the actual image file — do not guess from
   the filename).
2. Describe only what is visibly present in the photo. Do not invent details
   that aren't visually evident (e.g. don't guess a fabric's brand or a
   garment's exact fiber content if it isn't visually obvious).
3. Produce a JSON object with exactly this shape:

```json
{
  "color_palette": ["<dominant colors observed, most prominent first>"],
  "contrast": "low | medium | high",
  "saturation": "muted | moderate | vibrant",
  "silhouette": "<short phrase, e.g. 'loose/oversized top with fitted bottom'>",
  "proportions": "<short phrase describing how volume is balanced, e.g. 'baggy bottom, cropped top'>",
  "textures_materials": ["<visible textures/materials, e.g. 'denim', 'lace', 'knit'>"],
  "accessories": ["<visible accessories, e.g. 'gold hoop earrings', 'shoulder bag'>"],
  "visual_density": "minimal | moderate | busy",
  "styling_notes": "<1-2 sentences on any other notable recurring-style cue: layering, pops of color, matching metals, etc.>"
}
```

4. Return only that JSON object (plus a one-line plain-English summary if
   useful to the calling agent) — do not add a recommendation or opinion
   about the outfit.

## Why this shape

Every field is intentionally generic and non-judgmental so that running this
Skill across 10-15 different favorite outfits produces directly comparable
records. A calling agent can then look down each field across all the
results to spot what repeats (e.g. gold jewelry appearing in most outfits,
or baggy-bottom + fitted-top being a recurring silhouette).
