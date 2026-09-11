# What's My Aesthetic?

## Problem

People frequently recognize what they like visually long before they can explain why. Someone might immediately know that a room, an outfit, or an image "feels right" to them, yet struggle to name the underlying pattern — is it the color palette, the level of contrast, the shapes involved, how cluttered or minimal it feels? This gap between recognizing a preference and articulating it is where most existing tools fall short. Generic aesthetic judgment — whether from a recommendation engine or from asking an AI model "does this look good?" — evaluates against a broad, averaged notion of what looks good to people in general. It has no concept of an individual's specific taste, so it cannot tell someone whether something fits *their* style; it can only offer a one-size-fits-all opinion.

## Target User

An individual who has a handful of images representing things they already like — a design student, or anyone curating a personal visual style — and wants feedback on whether something new fits their own taste, with reasons they can act on, rather than a generic aesthetic opinion.

## Proposed Solution / Digital Tool

*What's My Aesthetic?* is a tool that learns an individual's visual preferences directly from examples they already like, rather than relying on a generic standard of good design. The user provides a small number of images that represent their taste. The system analyzes these examples across concrete visual dimensions — color palette, saturation, contrast, shapes and forms, proportions, textures, and visual density — and identifies the patterns that consistently appear across them. These patterns are compiled into a personalized aesthetic profile: a structured representation of what that specific user tends to gravitate toward. From that point on, when the user considers a new item or combination, the system evaluates it against their own profile rather than against a generic aesthetic standard, and explains its reasoning in terms the user can act on.

## Core User Experience

1. **Provide examples** — the user uploads a handful of images (roughly 3–5) that represent things they like.
2. **The system learns the aesthetic** — it analyzes the examples and extracts the visual characteristics that recur across them.
3. **Receive a personalised profile** — the user sees a clear summary of what defines their aesthetic (e.g., their typical color range, contrast level, texture preferences).
4. **Consider new items** — the user uploads two or more new images or items they're deciding whether to combine.
5. **Receive a compatibility assessment** — the system returns a compatibility score along with an explanation of what fits, what clashes, why, and how the combination could be adjusted to better match their aesthetic.

## MVP Scope

The MVP is deliberately narrow and centers on a single, well-defined capability: learning one user's aesthetic from a small set of liked examples (3–5 images), and evaluating whether a new combination of 2 or more items is compatible with that learned aesthetic. The output of this evaluation is a compatibility score paired with a clear explanation of the reasoning behind it — what aligns with the user's preferences, what doesn't, and why. Keeping the MVP to this single, general capability ensures the core idea — personalized aesthetic learning and compatibility reasoning — is demonstrated clearly, without the scope expanding into multiple domains before the fundamental mechanism is proven.

## Explicitly Out of MVP Scope

- Outfit-specific modeling (garments, fit, styling rules)
- Full interior design or room/furniture arrangement modeling
- Shopping recommendations or product sourcing
- Any other domain-specific use case beyond a general "items/images" abstraction
- The MVP proves the personalization mechanism works at all, before it is pointed at any specific domain.

## Final / Long-Term Goals

Beyond the MVP, the same underlying aesthetic-learning system is designed to generalize across many kinds of visual decisions — outfits, interior spaces, furniture arrangements, individual objects, color combinations, and other combinations a user might want feedback on. The long-term vision is not a collection of separate domain-specific tools, but a single personalization engine — the ability to learn what someone's eye is drawn to and evaluate new visual choices against that — that can be pointed at whichever domain is useful, while the MVP focuses on proving that this personalization mechanism works at all before expanding its reach.

## AI-Involvement Level

**Note:** the exact AI-Involvement Level scale/definitions for this course were not available in this repository at planning time. Rather than inventing a course-specific numbered scale, this project is described here as a **high / core AI-involvement project**, with the reasoning below — map this onto the professor's actual rubric wording once available.

AI is not a peripheral feature of this product — it is the product. The core value delivered to the user comes entirely from the AI's ability to analyze visual examples, extract meaningful aesthetic characteristics from them, construct a representation of that individual's preferences, and reason about how well a new combination aligns with those preferences. Without this analysis and reasoning capability, there is no product: an interface that simply lets someone upload and view images has no value on its own. The ordinary application logic — handling uploads, displaying results, managing the interface — exists only to support and present the AI's work; it is infrastructure, not the source of value. The distinguishing, central function of this tool — turning a handful of liked examples into a usable, explainable model of someone's taste — is entirely an AI/ML capability, which is why this project is classified as high/core AI-involvement rather than AI-as-an-added-feature.

## How This Differs From Generic AI Aesthetic Judgement

It would be reasonable to ask why this couldn't simply be done by prompting an existing vision-capable AI model with "do these two things look good together?" The distinction is fundamental, not cosmetic: a generic model answering that question is drawing on a broad, averaged sense of aesthetic convention — the same answer, more or less, for any user who asks. It has no notion of a *specific individual's* taste, because it was never given the chance to learn one. This system inverts that order of operations: it first learns a person's aesthetic from their own examples, building a distinct profile for that individual, and only then evaluates new choices — relative to that person's learned preferences, not relative to a generic standard of "good." The result is a judgment that can differ from one user to the next even when shown the identical combination, because the evaluation is genuinely conditioned on who is asking. That personalization — learn first, then evaluate against what was learned — is the core idea this project is built around, and it's precisely what a one-off prompt to a generic model cannot provide.
