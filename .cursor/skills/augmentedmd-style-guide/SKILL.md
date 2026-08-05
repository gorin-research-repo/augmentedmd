---
name: augmentedmd-style-guide
description: >-
  Apply the AugmentedMD visual design system when building or restyling pages,
  landing pages, tool UIs, or HTML/CSS for AugmentedMD or related clinical tools.
  Use when the user asks for AugmentedMD styling, matching the index.html look,
  blue/teal medical UI, PHI Scrubber-style pages, or consistent branding across
  AugmentedMD sites.
---

# AugmentedMD Style Guide

Build pages that match the AugmentedMD landing page (`index.html`): a clean,
professional clinical/academic aesthetic with navy–blue–teal branding, dotted
page texture, soft cards, and clear section hierarchy.

Canonical reference: repository root `index.html`.

## When to use

- Creating new AugmentedMD pages, tool landings, or docs UIs
- Matching color, layout, or components to the existing site
- Restyling another tool (e.g. PHI Scrubber) to share branding
- User mentions AugmentedMD style, blue/teal medical look, or “like my site”

## Design principles

1. **Clinical trust** — professional medical/academic, not playful or dark-tech.
2. **One composition** — first viewport: brand bar + header + hero (eyebrow, one H1, one sub, one CTA). No stats strips or promo chips in the hero.
3. **Brand-first** — “AugmentedMD” is a clear header brand (logo mark + name), not just nav chrome.
4. **Light & airy** — white page with subtle blue-gray dot grid; use `--card` for section bands.
5. **Soft elevation** — cards use light border + soft shadow; hover lifts slightly.
6. **Blue family only** — primary actions and headings live in the navy/blue/teal system; green is reserved for “available” status tags.
7. **Standalone HTML preferred** — single-file pages (inline CSS/JS) unless the project already uses a build system.

## Color tokens (required)

Copy these CSS variables into every new page. Do not invent alternate brand colors.

```css
:root {
  --blue: #2055A1;
  --navy: #15306B;
  --teal: #06ABEB;
  --text: #33475A;
  --ink: #1F1F38;
  --card: #EEF4FB;
  --border: #C9D9EC;
  --white: #FFFFFF;
  --muted: #5C707A;
  --green: #1B7F5A;
  --green-bg: #E6F7F0;
  --brand-gradient: linear-gradient(90deg, #15306B 0%, #2A6FC0 55%, #06ABEB 100%);
  --font-sans: "Helvetica Neue", Arial, system-ui, sans-serif;
  --font-mono: "Courier New", ui-monospace, monospace;
  --radius-card: 12px;
  --radius-btn: 10px;
  --radius-pill: 999px;
  --shadow-card: 0 12px 30px rgba(27, 42, 74, 0.10);
  --shadow-hover: 0 16px 40px rgba(27, 42, 74, 0.15);
}
```

### Token usage

| Token | Use for |
| --- | --- |
| `--blue` | H1/H2/H3, links, primary CTA fill, tool icons |
| `--navy` | Emphasized words in H1, card titles, footer bg, CTA hover |
| `--teal` | Brand gradient end only (accent, not body text) |
| `--text` | Body copy, nav links |
| `--muted` | Eyebrows, section subtitles, secondary meta |
| `--card` | About/alt section backgrounds, “coming soon” tag bg |
| `--border` | Header bottom, card borders, section dividers |
| `--green` / `--green-bg` | “Available Now” status pills only |
| `--brand-gradient` | Top brand bar (8px) and logo mark square |

Full token file: `references/tokens.css`.

## Page chrome (required structure)

Every marketing/tool page should include this shell unless the user asks otherwise:

1. **Brand bar** — `height: 8px`, `background: var(--brand-gradient)`.
2. **Header** — white, 76px tall (64px mobile), bottom border `--border`, brand left / nav right.
3. **Logo mark** — 40×40, `--radius-btn`, white letter on `--brand-gradient`, next to “AugmentedMD” at 20px/700/`--blue`.
4. **Nav links** — `--text`, weight 600, 15px; hover → `--blue`. Hide nav below 900px.
5. **Main** — centered `width: min(1140px, calc(100% - 40px))`.
6. **Footer** — `--navy` background, light blue-gray link color `#C7D4EA`, white brand; stack centered on small screens.

## Typography & type scale

- Body: 16px / 1.5 / `--text` / `--font-sans`
- Eyebrow: 12px, weight 700, uppercase, `letter-spacing: 0.08em`, `--muted`
- H1: `clamp(34px, 4vw, 48px)`, line-height 1.15, `--blue`; emphasize phrases with `<em>` styled as `--navy` (not italic)
- H2: ~32px (28px mobile), `--blue`, section titles centered
- H3 (cards): 22px, `--navy`
- Subcopy: 17–18px, line-height 1.6–1.8
- Links: `--blue`; hover underline

## Hero pattern

```
[eyebrow]
[H1 with optional <em> accent phrase]
[one supporting paragraph .sub, max-width ~680px]
[one primary .cta]
```

- Hero block: centered, max-width ~820px, margin ~64px auto (48px mobile).
- CTA: solid `--blue`, white text, `--radius-btn`, padding `14px 28px`, weight 700.
- CTA hover: `--navy` fill, `translateY(-2px)`, soft blue shadow. No outline/ghost primary in hero.

## Sections

- `.section` padding: 64px 0 (48px mobile).
- `.section-title`: centered H2 + muted subtitle.
- Alternating band: use `.about`-style `background: var(--card)` + top border for secondary sections (About, Mission).
- Mission/callout boxes: white card, border, `--radius-card`, `--shadow-card`, padding ~28–32px.

## Tool / content cards

Use cards for interactive or browsable tool listings (not in the hero).

- Grid: `repeat(auto-fit, minmax(320px, 1fr))`, gap 32px; single column ≤900px.
- Card: white, `1px solid var(--border)`, `--radius-card`, `--shadow-card`.
- Hover: `--shadow-hover` + `translateY(-4px)`.
- Header band: gradient `135deg` from `--card` to `--white`, bottom border, icon + title + status tag.
- Icon: 48×48, `--blue` fill, white glyph, `--radius-btn`.
- Status tags:
  - Available: `--green` on `--green-bg`, pill, 11px uppercase.
  - Coming soon: `--muted` on `--card`.
- Body links: bold `--blue` with trailing `→`; external/GitHub links may use `↗` and slightly smaller opacity.

## Motion (keep subtle)

Ship light presence, not flash:

- CTA hover lift (~0.2s)
- Card hover lift (~0.3s)
- Smooth scroll for in-page anchors

Avoid glow, heavy blur, bouncing, or autoplaying carousels.

## Background texture

```css
body {
  background-color: var(--white);
  background-image: radial-gradient(#E4E9F2 1px, transparent 1px);
  background-size: 18px 18px;
}
```

Do not replace with purple gradients, cream paper, or flat dark backgrounds.

## Responsive checklist

- ≤900px: tools grid → 1 column; hide desktop nav.
- ≤620px: tighter main/header padding; hero/section spacing reduced; footer column + centered.

## Do / don’t

**Do**

- Reuse the CSS variables and shell from `assets/page-template.html`
- Keep copy concise, clinician-facing, privacy/safety minded
- Use green only for availability/success status
- Prefer single-file HTML for new tool pages unless a framework already exists

**Don’t**

- Introduce purple, indigo glow, terracotta, or cream “AI default” themes
- Put stats, schedules, or floating badges over the hero
- Use dark mode as the default AugmentedMD look
- Replace the brand gradient bar or logo mark with a generic wordmark-only header
- Overuse cards for static text that isn’t a tool/interaction unit

## Implementation workflow

1. Read `index.html` (and this skill) before inventing new UI.
2. Start from `assets/page-template.html` or copy `:root` + chrome CSS from `references/tokens.css`.
3. Keep structure: brand-bar → header → main sections → footer.
4. Match spacing, radii, and shadows to the tokens above.
5. Verify desktop and mobile breakpoints (900 / 620).
6. If extending an existing tool page, preserve AugmentedMD tokens even if layout differs slightly.

## Resources

- `references/tokens.css` — copy-paste design tokens + base element styles
- `assets/page-template.html` — minimal blank page with full chrome and hero
- Root `index.html` — canonical live design
