---
name: landing-page
description: Build a single-file HTML landing page with a real design system — specific copy, strong type hierarchy, one accent color, and none of the generic "AI landing page" look. Use when asked for a landing page, product page, homepage hero, or LP.
---

# Landing Page

Produce one self-contained HTML file that looks art-directed, not generated.
The example in `examples/` (pulse-landing.html) is the quality bar. Match its
level of specificity: real-feeling copy, deliberate spacing, one accent.

## Before you build

Collect or invent (and clearly keep consistent) these five inputs:

1. Product in one sentence: what it is and what it does.
2. Audience: one specific person, not "everyone".
3. The single main action (sign up, buy, download, join waitlist).
4. One proof point: a number, a quote, or a concrete result. If the user has
   none, use a mechanism instead ("works offline", "no account needed") —
   never invent testimonials or statistics.
5. Tone: pick one — quiet/premium, bold/loud, warm/human, technical/precise.

If the user gave you a product and an audience, do not ask more questions.
Make reasonable choices and note them in one line at the end.

## Design tokens (default system — "Ink & Citrus")

Use these unless the user supplies brand colors. Change all values in one
place: the `:root` block.

```css
:root{
  --bg:#0F1013;        /* page background */
  --panel:#17181D;     /* raised surfaces */
  --line:#26272E;      /* hairlines, borders */
  --ink:#F4F2EA;       /* primary text */
  --muted:#9BA0A6;     /* secondary text */
  --accent:#D9F24F;    /* ONE accent — buttons, highlights */
  --radius:14px;
  --font:"Inter","Helvetica Neue",Arial,sans-serif;
}
```

Rules that make it look designed:

- **One accent color.** Everything clickable or important uses it; nothing
  else competes. No rainbow gradients, no purple-blue "AI gradient".
- **Type does the work.** Headline at 56–72px, weight 800, letter-spacing
  slightly negative (-0.02em). Body 17–18px, line-height 1.6. Small caps
  labels (12px, letter-spacing 0.12em, uppercase, muted) above headlines.
- **Space in multiples of 8.** Section padding 96px top/bottom on desktop.
  If a gap looks arbitrary, it reads as generated.
- **Hairlines over shadows.** Separate sections with 1px `--line` borders,
  not drop shadows or floating cards on colored backgrounds.
- **Numerals as design.** Big stat numbers (48px+) in the accent or ink,
  with small muted labels. One row of three stats maximum.

## Page recipe (in this order)

1. **Top bar** — wordmark left, two or three plain text links, one accent
   button (the main action). Thin bottom border.
2. **Hero** — small caps label (category), headline, one supporting sentence
   (max 22 words), primary button + one quiet secondary link. Right side or
   below: a product visual made of CSS (a mock window, a stat card cluster,
   a typographic composition). Never an empty gray placeholder box.
3. **Logo/proof strip** — one line: "Used by …" with text wordmarks, or the
   proof stat row. Skip entirely if there is no honest proof.
4. **Problem → shift** — two columns: the old way (muted, struck-through
   feel) vs the product's way. Short lines, no paragraphs over 3 lines.
5. **Features** — exactly three or four. Each: small caps number (01–04),
   title, two-line description. Grid with hairline dividers, not six
   identical icon cards.
6. **How it works** — three numbered steps, one line each.
7. **Pricing or offer** — if the user gave a price: one highlighted plan,
   what is included as a checklist, the main action button. If no price:
   a waitlist/CTA band instead.
8. **FAQ** — four questions maximum, written against real objections
   (price, effort, switching, "is this for me").
9. **Final CTA band** — accent background block, ink-colored text, headline
   repeats the main promise in different words, one button.
10. **Footer** — wordmark, one line of positioning, tiny links. No sitemap
    farm.

## Copy rules

- Headline formula: **[specific outcome] for [specific person]**, or a
  concrete claim the product can back. "Reclaim your evenings, runners" —
  not "Welcome to the future of productivity".
- Every section must contain at least one concrete noun and one number or
  name. Vague adjectives ("seamless", "powerful", "revolutionary",
  "cutting-edge", "next-level") are banned.
- Buttons say what happens: "Start free", "Get the template", "Join the
  waitlist". Never "Learn more" as the primary action.
- Write like the product's maker, first person plural sparingly ("we built
  this because…"), never corporate "solutions" language.

## Anti-patterns (the "AI look" — never do these)

- Purple/blue gradient hero backgrounds or gradient text.
- Three identical cards with emoji or generic SVG icons in circles.
- "🚀 Supercharge your workflow" style copy, exclamation marks in headlines.
- Lorem ipsum, "Feature One / Feature Two", stock-photo placeholders.
- Centered everything. Mix left-aligned text blocks with offset visuals.
- More than two font weights families, or more than one accent color.
- Fake testimonials, fake logos, invented statistics. Ever.

## Technical rules

- One HTML file, CSS in `<style>`, no external assets except a Google Fonts
  link (Inter or the user's brand font). No JavaScript required except an
  optional FAQ toggle.
- Semantic tags: `header`, `main`, `section`, `footer`. Real `<h1>` once.
- Responsive: single column under 760px, hero visual below the copy,
  tap targets at least 44px.
- Keep the file under ~700 lines. If it needs more, the page is doing too
  much — cut a section.

## QA checklist (run before delivering)

- [ ] One accent color, used consistently; no gradients except a subtle
      same-hue background fade.
- [ ] Headline contains a concrete outcome and a specific audience or
      mechanism.
- [ ] Every number on the page came from the user or the product's real
      mechanics.
- [ ] No banned words: seamless, supercharge, revolutionize, cutting-edge,
      next-level, unlock your potential.
- [ ] Reads correctly at 390px wide with no horizontal scroll.
- [ ] The main action appears at least three times (top bar, hero, final
      band).
