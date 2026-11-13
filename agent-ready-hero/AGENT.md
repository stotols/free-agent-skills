# AGENT.md — Hero section

**For the AI coding agent (Claude Code / Codex / Cursor): read this whole file
before editing `index.html` in this folder.** It tells you what each part of the
section is, what you may change freely, and what you must not break.

Section: **Hero** (top bar + headline + product visual + proof strip)
File: `hero/index.html` — a complete standalone HTML document.
Demo product: "Pulse", a fictional focus-session app. All copy, names and
numbers are demo content and are meant to be replaced.

---

## 1. Structure map

```
<section data-section="hero">
  <div class="hero-glow">            decorative radial glow (custom CSS in <style>)
  <header>                           top bar — part of this section
    [brand] [nav links] [nav-cta]
  <div container>
    <div grid: copy | visual>
      copy:    [eyebrow] [headline] [subhead] [cta-primary] [cta-secondary] [cta-note]
      visual:  [visual] session mock card
                 [visual-timer] inside it
                 floating proof card (absolute, bottom-left of the visual)
    <dl proof strip>                 [stat-1] … [stat-4]
```

Every editable region carries a `data-slot` attribute. **Find slots with
`grep -o 'data-slot="[^"]*"' index.html`.** When you restructure, keep the
`data-slot` attributes on the elements that carry the same content.

## 2. Editable slots

| Slot | Element | What it is | Rules |
|---|---|---|---|
| `brand` | header `<a>` | Product name / wordmark | Keep ≤ 12 characters. The trailing `.` in accent color is part of the logo treatment — keep it or remove it everywhere, not just here. |
| `nav-cta` | header `<a>` | Small header button | 1–3 words. |
| `eyebrow` | pill above headline | Category claim | ≤ 5 words, uppercase is applied by CSS — write normal case. |
| `headline` | `<h1>` | The one promise of the page | ≤ 9 words. Exactly one phrase may be wrapped in `<em>` — it renders in the accent color (the `not-italic` class is required). |
| `subhead` | `<p>` | Expands the headline | 2 sentences max, ≤ 45 words. Must say what the product *does*, not adjectives. |
| `cta-primary` | `<a>` | Main conversion button | ≤ 5 words. One primary button per section — never add a second accent-filled button here. |
| `cta-secondary` | `<a>` | Lower-commitment link-button | Outline style only. |
| `cta-note` | `<p>` under buttons | Risk-removal line | Keep the three-part pattern "trial · payment · cancel" or equivalent facts. No hype words. |
| `visual` | right column | Product mock or screenshot | Keep the aspect roughly landscape. If replacing with an `<img>`, keep the `border-line` border and `rounded-2xl` corners so it sits in the system. |
| `visual-timer` | big number in mock | Demo UI content | Purely cosmetic; any plausible value works. |
| `stat-1`…`stat-4` | `<dd>` in proof strip | Proof numbers | Number first, label in the paired `<dt>`. Keep all four or remove the whole strip — never leave 3 (breaks the 4-column rhythm on desktop). |

The session rows inside the mock (task names, statuses) are free-text demo UI —
edit them like the `visual-timer`.

## 3. Design tokens (shared by the whole pack — do not fork them here)

Colors (Tailwind config in `<head>`):
`bg #0F1013` · `panel #17181D` · `panel2 #1D1E24` · `line #26272E` ·
`ink #F4F2EA` · `muted #9BA0A6` · `accent #D9F24F` · `onaccent #141503`

Type: headline `text-5xl lg:text-6xl font-extrabold tracking-tight`;
section headings `text-4xl lg:text-5xl`; body `text-base`/`text-lg`;
secondary text always `text-muted`. Font stack: Inter → Noto Sans → system.

Geometry: page container `max-w-7xl px-6 lg:px-8`; cards `rounded-2xl`
with `border border-line bg-panel`; buttons `rounded-[10px]`;
section padding `py-16 lg:py-24` (this hero), other sections `py-20 lg:py-28`.

**There is exactly one accent color.** Buttons, the headline `<em>`, the
eyebrow text, the live dot and the progress fill use it. Nothing else does.

## 4. Do / Don't

**Do**
- Keep the vertical rhythm: eyebrow → headline → subhead → buttons → note,
  with the existing margin steps (`mb-6`, `mt-6`, `mt-9`, `mt-5`).
- Keep the two-column split `lg:grid-cols-12` with 6/6 columns; on mobile the
  copy stacks above the visual — that order is intentional.
- Keep the floating proof card overlapping the mock (`absolute`, parent has
  `relative` + `pb-12` so it never clips).
- When swapping the mock for a real screenshot, keep the floating card — it
  carries the social proof, the screenshot carries the product.

**Don't**
- Don't add a second `<h1>` or a second accent-filled button.
- Don't center the copy column — left-aligned copy against a right visual is
  the layout contract of this section.
- Don't put body text in `text-ink` at small sizes if it is secondary
  information — secondary is always `text-muted`.
- Don't delete the top bar silently: if the host page has its own nav, remove
  the whole `<header>` block, not just parts of it.
- Don't animate the progress bar or the live dot with JS — this section ships
  animation-free on purpose.

## 5. Adaptation recipes

**Change the accent color:** in the `tailwind.config` in `<head>`, change
`accent` (and `onaccent` if the new accent is dark). Also update the two
`rgba(217,242,79,…)` values in `.hero-glow` to the same hue. Nothing else
references the color by value.

**Light theme:** swap tokens in the config — `bg #FFFFFF`, `panel #F7F6F2`,
`panel2 #EFEEE8`, `line #E3E1D8`, `ink #16171A`, `muted #5C6066` — and keep
`accent`/`onaccent` if contrast allows. No class changes are needed.

**No-nav version:** delete the `<header>` block and add `pt-10` to the hero
grid if the page above it has no header of its own.

**Merge into a full page:** keep ONE copy of the two `<script>` blocks
(Tailwind CDN + config) in the page `<head>` and paste only the
`<section data-section="hero">…</section>` element. The `.hero-glow` rule from
this file's `<style>` must travel with the section.
