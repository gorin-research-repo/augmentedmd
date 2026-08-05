---
name: augmentedmd-page-style
description: Build web pages in the AugmentedMD visual style — the navy/blue/teal clinical design system used by augmentedmd.org and PHI Scrubber. Use whenever creating or restyling a page, landing page, tool UI, microsite, or HTML mockup for AugmentedMD, Michael Gorin MD, or any of his clinical tools, or when asked to match "my site", "the AugmentedMD style", or "the same design template".
metadata:
  owner: Michael Gorin, MD
  reference-pages: index.html (AugmentedMD landing), phi-scrubber.html (PHI Scrubber tool)
---

# AugmentedMD page style

The house style for AugmentedMD pages: a professional medical/academic look built
on a navy-to-teal blue palette, white cards on a subtly dotted background, and
generous whitespace. Every page is a single standalone HTML file with no build
step and no network dependencies.

## When to use this

Use for any new page, tool UI, or landing page in the AugmentedMD family, and for
restyling an existing page to match. If the request is to change site content
without touching presentation, you don't need this skill.

## Non-negotiable rules

These are the constraints that make a page belong to this family. Follow them
even when a more conventional approach would be easier.

1. **One file, no build.** All HTML, CSS, and JS live in a single `.html` file
   that works when double-clicked from the filesystem. No bundler, no
   `package.json`, no framework, no TypeScript.
2. **Zero external requests.** No CDN scripts, no Google Fonts, no icon
   libraries, no remote images, no analytics. A page must render identically
   offline. This is a privacy commitment, not just a performance one — these
   tools handle clinical text.
3. **System fonts only.** `"Helvetica Neue", Arial, system-ui, sans-serif` for
   prose and `"Courier New", ui-monospace, monospace` for any clinical text,
   code, or user input.
4. **Icons are HTML entities or inline SVG.** The existing pages use entities
   like `&#10003;` (check), `&#128274;` (lock), `&#128200;` (chart),
   `&#9998;` (pencil), `&#128197;` (calendar), `&#128172;` (speech balloon).
   Prefer an entity; fall back to inline SVG. Never an icon font.
5. **Style through the tokens.** Declare the `:root` block verbatim (see below)
   and reference `var(--blue)` and friends. Do not hardcode a hex value in a
   component rule; if you need a new color, add a token.
6. **Compact CSS, one rule per line.** The house CSS style puts each selector's
   declarations on a single line with no space after the colon — matching
   `index.html`. Keep it; the diffs stay readable and the file stays short.
7. **Clinical honesty in copy.** Anything that touches patient data or clinical
   judgment carries a caveat: the tool assists, it does not certify or decide.
   Use the `.notice` component for this and never soften it away.

## Design tokens

Copy this block verbatim into `<style>` as the first thing on the page. It is
the union of the tokens used across the existing pages; drop the accent pairs a
page genuinely doesn't use, but never rename or re-value them.

```css
:root{
  --blue:#2055A1;
  --navy:#15306B;
  --teal:#06ABEB;
  --text:#33475A;
  --ink:#1F1F38;
  --card:#EEF4FB;
  --border:#C9D9EC;
  --white:#FFFFFF;
  --muted:#5C707A;
  --green:#1B7F5A;
  --green-bg:#E6F7F0;
  --amber:#B77800;
  --amber-bg:#FBF1DF;
  --brand-gradient:linear-gradient(90deg,#15306B 0%,#2A6FC0 55%,#06ABEB 100%);
  --font-sans:"Helvetica Neue",Arial,system-ui,sans-serif;
  --font-mono:"Courier New",ui-monospace,monospace;
  --radius-card:12px;
  --radius-btn:10px;
  --radius-pill:999px;
  --shadow-card:0 12px 30px rgba(27,42,74,.10);
  --shadow-hover:0 16px 40px rgba(27,42,74,.15);
}
```

How each color is used:

| Token | Role |
| --- | --- |
| `--blue` | Primary. Headings, links, primary buttons, icon tiles, chips. |
| `--navy` | Deeper accent. Button hover, footer background, emphasized `<em>` in `h1`, card `h3`. |
| `--teal` | Gradient terminus only. Never a background for text. |
| `--text` | Body copy. |
| `--ink` | Monospace content: textareas, output panes. |
| `--card` | Tinted surfaces: alternating sections, panel footers, findings boxes. |
| `--border` | Every 1px border on the page. |
| `--muted` | Eyebrows, captions, secondary and disabled text. |
| `--green` / `--green-bg` | Positive status: "Available Now" tags, success. |
| `--amber` / `--amber-bg` | Cautions and clinical disclaimers. Border `#EBDCC0`. |

Two details that read as sloppy when missed: the page background is white with a
dotted overlay, `radial-gradient(#E4E9F2 1px,transparent 1px)` at
`background-size:18px 18px`. And footer text is `#C7D4EA` on `--navy`, not white
— only `.footer-brand` and link hover go full white.

## Page skeleton

Every page follows this order. Sections are optional; the order is not.

```
<div class="brand-bar">     8px gradient strip, flush to the top of the viewport
<header class="header">     76px, white, bottom border; brand left, nav right
<main>                      width:min(1140px,calc(100% - 40px)); margin:auto
  <section class="hero">    eyebrow -> h1 with <em> -> .sub -> optional .cta
  <section class="section">  content sections, 64px vertical padding
  <aside class="notice">    clinical caveat, when the page warrants one
<footer>                    navy, brand left, links right
<script>                    smooth scroll for in-page anchors; page logic
```

The starter file `assets/page-template.html` is this skeleton with the full
style block already in place. Copy it and replace the content rather than
retyping the CSS. `assets/style-block.css` is the same CSS on its own if you are
restyling a page that already has markup.

## Type scale

- `h1`: `clamp(34px,4vw,40px)` for tool pages, `clamp(34px,4vw,48px)` for
  landing pages. `line-height:1.15`, `margin:16px 0`. Wrap the payoff phrase in
  `<em>`, which renders as non-italic `--navy`.
- `.eyebrow`: 12px, 700, `letter-spacing:.08em`, uppercase, `--muted`.
- `.sub`: 17–18px, `line-height:1.6`, max-width 640–680px, centered.
- Section `h2`: 32px. Card `h3`: 22px. Panel `h2`: 18px.
- Body: 16px / 1.5. Prose inside cards relaxes to 1.7.

## Spacing and layout

- Section rhythm: `padding:64px 0`, collapsing to `48px` under 620px.
- Hero margin: `64px auto`, collapsing to `48px`.
- Card grid: `repeat(auto-fit,minmax(320px,1fr))` with `gap:32px`, collapsing to
  one column at 900px.
- Two breakpoints only, `900px` and `620px`. At 900px, grids go single-column and
  the header nav hides. At 620px, `main` narrows to `calc(100% - 32px)`, the
  header shrinks to 64px, and the footer stacks and centers. Don't invent a third
  breakpoint.
- Motion is understated: `transform:translateY(-2px)` on buttons,
  `translateY(-4px)` plus `--shadow-hover` on cards, transitions of `.2s`–`.3s`.
  No entrance animations, no parallax.

## Components

Read `references/components.md` for the copy-paste CSS and markup of every
component below. Load it whenever you are writing a page rather than guessing at
the rules. It uses the class names as they appear in the existing pages
(`.tool-card`, `.tool-tag`); the starter template uses neutral aliases (`.card`,
`.tag`) since not every page is a tool directory. Either is fine — pick names
from the page's own domain and stay consistent within a file.

- **Header and brand** — gradient `.logo` tile with a single letter, or a solid
  `.shield` tile with an entity glyph for tool pages.
- **Hero** — eyebrow, `h1` with `<em>`, `.sub`, `.cta` button.
- **Tool card grid** — `.tool-card` with tinted `.tool-header`, `.tool-icon`
  tile, `.tool-tag` status pill (green for available, muted for `.coming`), and
  a `.tool-body` with `.tool-link` arrow links (`→` for internal, `↗` for
  GitHub).
- **Panel** — bordered card with `.panel-head` (numbered `.step` circle plus
  `h2`), a body, and a tinted `.panel-foot` for counts and controls. The
  workhorse of tool pages.
- **Findings box** — `--card` background holding uppercase `.chip` pills.
- **Notice** — amber caution `<aside>` with a bold lead-in.
- **Mission box** — white bordered box inside a tinted section, for bio and
  positioning statements.
- **Footer** — navy bar, brand and tagline left, external links right.

## Content conventions

- Page title format: `PageName — Short Descriptor`, em dash, as in
  `AugmentedMD — Tools for the Post-AI Digital World` and
  `PHI Scrubber — Offline`.
- The audience is practicing clinicians. Write plainly, lead with what the tool
  does for them, and name the privacy property explicitly when it exists
  ("entirely in this browser", "never uploaded or stored").
- Attribution in the footer is `Tool by @michael_gorin / @AugmentedMD` for tools,
  or `Open-source tools by Michael Gorin, MD` for the landing page.
- Every external link gets `target="_blank" rel="noopener"`.

## Accessibility

- Set `<html lang="en">` and a `<meta name="viewport">` with
  `width=device-width,initial-scale=1`.
- All interactive controls are real `<button>` (with `type="button"`) or `<a>`
  elements. Never a clickable `<div>`.
- Give icon-only controls an `aria-label`, and mark regions that update from JS
  with `aria-live="polite"` — the PHI Scrubber output pane does this.
- Keep focus visible. If you reset `outline` on a text input the way the tool
  page does, the surrounding panel border must still make focus obvious;
  otherwise leave the outline alone.
- The palette is checked: `--text`, `--blue`, `--navy`, `--muted`, and `--green`
  all clear 4.5:1 on white or on `--card`. If you add a color, verify it.

## Before you finish

- Open the file directly from disk and confirm it renders with no console
  errors and no network requests.
- Check both breakpoints at roughly 1280px, 880px, and 380px wide.
- Grep the file for `http://` and `https://` and confirm every hit is a link the
  user clicks, never a resource the page loads.
- Confirm no hardcoded hex values outside `:root` (the dotted-background
  `#E4E9F2`, the notice border `#EBDCC0`, and the footer text `#C7D4EA` are the
  three sanctioned exceptions).
