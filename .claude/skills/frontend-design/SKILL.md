---
name: frontend-design
description: Guidance for distinctive, intentional visual design for this investment/financial advisory landing page. Helps with aesthetic direction, typography, and making choices that don't read as templated defaults, tuned to a professional blue finance theme.
license: Complete terms in LICENSE.txt
---

# Frontend Design — Investment Advisory Site

Approach this as the design lead at a small studio known for giving every client a visual identity that could not be mistaken for anyone else's. This client (a wealth/investment advisory firm) has already rejected proposals that felt templated, and is paying for a distinctive point of view: make deliberate, opinionated choices about palette, typography, and layout that feel trustworthy, modern, and engaging rather than generic "corporate finance stock template."

## Project context

- This is a single-file site: everything lives in [index.html](../../../index.html) — `<style>`, body markup, and `<script>` are all inline. No build system, no frameworks/libraries (no React/Vue/Bootstrap/Tailwind/jQuery).
- Sections in order: sticky nav, hero, "Why Choose Us" benefit cards, investment process timeline, testimonials, lead magnet, enquiry form, FAQ accordion, final CTA, footer.
- Hero/background imagery uses Unsplash URLs with `?auto=format&fit=crop&...` params — keep using optimized Unsplash query params rather than adding local binary assets.
- Fonts load from Google Fonts via `<link>` tags in `<head>`.
- Don't remove the enquiry form's `e.preventDefault()`/AJAX `fetch` handling, FormSubmit hidden fields, or validation regexes when restyling.

## Ground it in the subject: a finance/investment brand

The subject is wealth management — money, growth, trust, long-term planning, precision. Distinctive choices should come from that world's own materials and vernacular: ledgers, growth curves, compounding, horizon lines, vaults, signatures, fine print, market charts, navigation/instruments — not generic "fintech app" gradients or stock photos of handshakes.

### Color: blue theme, named and specific

Replace the generic palette in `:root` with a deliberate blue-led system. Avoid a flat, single corporate blue (`#0d6efd`-style) — instead pair a deep "ink" navy with one warmer or brighter accent for contrast and energy. Example direction (adjust hex values to taste, but keep this structure):

- `--primary`: a deep navy/midnight blue (e.g. `#0B2545` – `#0F2A4A`) — anchors nav, headings, footer.
- `--secondary`: a richer mid-blue (e.g. `#1B4F8C` – `#2C5F9E`) — buttons, links, section accents.
- `--accent`: a warm contrast color used sparingly for CTAs/highlights — gold/amber (e.g. `#C9A24B` / `#D4AF37`) reads as "premium finance" without being garish, or a fresh teal/cyan (e.g. `#3FA7D6`) for a more modern fintech feel. Pick one direction and commit.
- `--background`: near-white with a faint cool tint (e.g. `#F7F9FC`) rather than pure `#FFFFFF`, to keep the blue family cohesive.
- `--text`: a near-black navy (e.g. `#1A2433`) rather than pure black, for warmth consistency with the palette.
- `--light-bg`: a pale blue-grey for alternating section backgrounds (e.g. `#EEF2F8`).

State the final 4–6 hex values explicitly before implementing, and derive every color decision (borders, shadows, hover states, focus rings) from this token set.

### Typography: nicer, more engaging pairing

The current pairing (Playfair Display + Inter) is a reasonable starting point but reads as a common default. Consider a pairing that feels more "private bank / modern advisory" and less "generic SaaS landing page":

- **Display/heading face**: something with more editorial character than Playfair's high-contrast didone — e.g. `Fraunces` (warm, slightly quirky serif with optical sizing — great for a "boutique advisory" feel), `Libre Caslon Display`, or `Cormorant Garamond` for a more classic private-bank feel. If keeping Playfair Display, use it more deliberately (tighter letter-spacing on large headings, restrained weight range).
- **Body face**: a humanist sans with good readability at small sizes — `Inter` is fine, but `Source Sans 3`, `Manrope`, or `Public Sans` can feel slightly less "default Bootstrap-adjacent." Manrope in particular pairs nicely with a serif display for a contemporary finance feel.
- **Utility/data face** (optional): for stats, numbers, captions — a tabular-figure-friendly face like `IBM Plex Mono` or `Space Mono` used sparingly (e.g. for percentages, dates in the timeline) reinforces the "precision/data" personality without overusing it.

Set a clear type scale with intentional weights and letter-spacing — large display headings should feel confident and a bit editorial, not just "bigger Inter."

## Design principles for this brief

The hero is a thesis: lead with the firm's core promise (steady, deliberate growth / partnership over time), not a generic "big number + label + gradient" hero. Consider a hero built around a horizon-line motif, a subtle animated growth-curve/line-chart accent, or a confident editorial headline over a muted navy-toned photo.

The investment process timeline is a real sequence — numbered markers (01/02/03...) are appropriate here because order genuinely matters. Lean into that: make the numbering itself a design element (e.g. large faint serif numerals in the accent color).

Use motion deliberately and sparingly: the existing `IntersectionObserver` fade-in-on-scroll is enough for most sections — don't pile on additional scroll effects. A single well-placed signature moment (e.g. an animated underline/accent draw-in on the hero headline, or a subtle parallax on the hero image) can land harder than scattered effects.

Testimonials, FAQ, and the enquiry form should feel calm and trustworthy — generous whitespace, soft shadows (not heavy/dark), rounded corners that read as "approachable but professional" (moderate radius, not pill-shaped everywhere).

## Process: brainstorm, explore, plan, critique, build, critique again

Before editing `index.html`, work out a compact token system in your reasoning:
- **Color**: 4–6 named hex values per the structure above, stated explicitly.
- **Type**: confirm the 2 (or 3) typeface roles and how/whether to update the Google Fonts `<link>` tags.
- **Layout**: note any structural tweaks (e.g. hero treatment, timeline numeral styling) as one-sentence descriptions.
- **Signature**: name the one memorable element this redesign will be remembered by.

Review that plan against generic finance-template defaults (flat corporate blue, Bootstrap-style cards, generic handshake stock photos, pill buttons everywhere) — if any part matches those defaults, revise it and note what changed and why.

When implementing in `index.html`, watch CSS selector specificity carefully — section-level and component-level selectors (e.g. `.section` vs `.cta`) can silently cancel each other's spacing/padding rules. Keep the existing structure (sticky nav, fade-in classes, FAQ accordion `.active`/`max-height` mechanism, form validation) intact unless the brief calls for structural changes.

## Restraint and self-critique

Spend boldness in one place (the signature element); keep everything else quiet and disciplined. Build to a quality floor: responsive at the existing `768px`/`992px` breakpoints, visible keyboard focus states, and respect `prefers-reduced-motion` for any new animation. After implementing, open `index.html` in a browser and review the hero, timeline, and form sections at both desktop and mobile widths before considering the work done.
