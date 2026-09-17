# Build Log

## 2026-09-11 — Project planning and repo setup

**Date:** 2026-09-11

**Time spent so far:** Approximate — roughly 1–2 hours of active work (repo/git setup, project planning discussion, and documentation). Exact wall-clock time is not tracked by this session, so this is an estimate, not a precise figure.

**Rough tokens used:** Approximate — on the order of 150,000–250,000 tokens for this session so far. This includes ~79,000 tokens reported directly by two background sub-agents used during planning (a repo inventory pass and a technical-design pass), plus the main planning conversation. Not a precise/audited figure — this session does not expose an exact cumulative token count.

**What shipped:** `plan.md` and `BUILD_LOG.md` — the initial project plan (problem, target user, proposed solution, core user experience, MVP scope and out-of-scope items, long-term goals, AI-involvement rationale, and differentiation from generic AI aesthetic judgement) and this build log.

**Decided:** Scoped the MVP to a single, domain-agnostic capability (learn a profile from 3–5 liked images, evaluate 2+ new items against it) rather than any specific domain (outfits, interiors, etc.) up front.

**Next:** Begin technical design/implementation planning for the feature-extraction and profile/scoring pipeline.

## 2026-09-17 — Assessment 2, Branch 1: custom Skill + two datasets (`assessment-2-skill-data`)

**Date:** 2026-09-17

**Time spent so far:** Approximate — roughly 2 hours of active work (planning discussion, dataset setup, reading and analyzing 23 real outfit photos, writing the Skill, and debugging the skill-loading issue below).

**Rough tokens used:** Approximate — on the order of 150,000–220,000 tokens for this session. This includes reading/analyzing 23 real outfit images (image tokens are relatively heavy) plus the planning and file-writing conversation. Not a precise/audited figure.

**What shipped:**
- `data/wardrobe.json` — the real clothing inventory (bottoms, tops, jewellery, bags, shoes), transcribed exactly as provided, no invented attributes.
- `data/favorite_outfits/` — folder holding the 23 real favorite-outfit photos provided by the user, plus a `README.md` explaining what belongs there.
- `.claude/skills/analyze-outfit-aesthetic/SKILL.md` — the custom Skill: one narrow, repeatable job (look at one outfit photo, output a fixed-shape structured JSON description of its aesthetic characteristics). It never recommends or compares outfits — only describes.
- `data/favorite_outfits/aesthetic_analysis.json` — the Skill's structured output applied to all 23 real photos (color palette, contrast, saturation, silhouette, proportions, textures/materials, accessories, visual density, styling notes per outfit).
- `data/aesthetic_profile.json` — a summary of the recurring aesthetic patterns found across all 23 outfits (e.g. fitted top + loose/baggy bottom as the dominant proportion, gold jewelry in nearly every outfit, one small saturated color accent per outfit — usually a pink bag, denim as the most common bottom fabric, mostly medium contrast and minimal-to-moderate visual density). This is the data Branch 2's agent will use as its "aesthetic profile" when building recommendations.

**What broke on the first try, and the fix:** Right after creating the Skill file, invoking it (`Skill: analyze-outfit-aesthetic`) failed with `Unknown skill` — Claude Code does not hot-load newly created project Skills into an already-running session. The fix was simply restarting the Claude Code session; the Skill then appeared in the available-skills list and ran correctly on the first real photo tested. No code change was needed, just a restart — worth knowing for Branch 2 as well (a new custom agent file will likely need the same restart before it's usable).

**Decided:** Precompute and store the aesthetic-pattern analysis in Branch 1 (rather than having the future agent re-analyze all 23 images on every single question) so Branch 2's agent can read a compact, ready-made profile via the filesystem MCP server instead of repeating expensive vision analysis on every query.

**Next:** Branch 2 (`assessment-2-agent`, created from `main` after this branch's PR merges) — add the filesystem MCP config and the custom `outfit-stylist` agent implementing the perceive → reason → act → observe loop, then run and document a real end-to-end recommendation.
