---
name: augmentedmd-style-guide
description: Create or restyle web pages in the AugmentedMD visual system: clinical blue and teal colors, dotted white canvas, gradient brand accents, restrained cards, clear typography, and responsive layouts. Use for AugmentedMD sites, tools, landing pages, dashboards, forms, and documentation pages that should feel visually related to the canonical AugmentedMD page.
---

# AugmentedMD style guide

Build calm, credible, privacy-conscious clinical software that belongs to the
same family as the AugmentedMD landing page.

## Canonical reference

Treat the repository's `index.html` as the visual source of truth. Its `:root`
block contains the canonical tokens, and its page shows the preferred header,
hero, cards, content bands, and footer.

When this skill and an existing product disagree:

1. Preserve product behavior, semantic HTML, and framework conventions.
2. Preserve established product-specific interaction patterns.
3. Apply this skill's tokens, spacing, surfaces, and visual hierarchy.
4. Use `index.html` to resolve remaining visual questions.

Do not replace a framework or add a UI dependency merely to reproduce this
style. Adapt the design system to the stack already in use.

## Design character

Aim for:

- professional and clinically trustworthy, not sterile;
- modern and technical, not futuristic or flashy;
- spacious and readable, with clear task hierarchy;
- restrained use of gradients and motion;
- privacy-first language that is direct and specific.

The signature visual cues are the 8 px blue-to-teal brand strip, white dotted
canvas, navy and blue headings, pale blue cards, rounded rectangular controls,
and compact status pills.

## Tokens

Use these values unless the product already exposes equivalent design tokens.
Prefer CSS custom properties so the visual language remains consistent.

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

  --brand-gradient:
    linear-gradient(90deg, #15306B 0%, #2A6FC0 55%, #06ABEB 100%);
  --font-sans: "Helvetica Neue", Arial, system-ui, sans-serif;
  --font-mono: "Courier New", ui-monospace, monospace;
  --radius-card: 12px;
  --radius-btn: 10px;
  --radius-pill: 999px;
  --shadow-card: 0 12px 30px rgba(27, 42, 74, .10);
  --shadow-hover: 0 16px 40px rgba(27, 42, 74, .15);
}
```

### Color roles

| Role | Token | Use |
| --- | --- | --- |
| Primary action | `--blue` | Buttons, links, icons, primary headings |
| Strong emphasis | `--navy` | Key words, card titles, footer, active states |
| Brand accent | `--teal` | Gradient endpoint and rare highlights |
| Body copy | `--text` | Default text |
| High contrast copy | `--ink` | Dense or especially important text |
| Quiet copy | `--muted` | Eyebrows, help text, secondary labels |
| Soft surface | `--card` | Section bands, inactive states, header gradients |
| Structure | `--border` | Dividers, inputs, cards |
| Positive status | `--green` / `--green-bg` | Success and available states only |

Do not use teal for large text or primary controls. Do not use green as a
general accent. Introduce red, amber, or other semantic colors only when the
interface genuinely needs error, destructive, or warning states; ensure they
meet WCAG AA contrast.

## Typography

- Use the system sans stack for all interface and prose text.
- Use the mono stack only for code, identifiers, or machine-readable values.
- Headings are blue, bold, compact, and sentence case.
- Body text is 16 px with a 1.5 line height; long-form copy may use 1.7–1.8.
- Hero titles use `clamp(34px, 4vw, 48px)` and a `1.15` line height.
- Section titles are 32 px desktop and 28 px on small screens.
- Card titles are 20–22 px and preferably navy.
- Eyebrows are 12 px, bold, uppercase, muted, with `.08em` letter spacing.
- Supporting intro text may be 17–18 px. Avoid oversized marketing copy.
- Keep prose line lengths near 60–75 characters and centered intros at no more
  than 680–820 px wide.

Use `<em>` in a hero only as a semantic styling hook, then render it upright in
navy. Do not use italic body text as decoration.

## Page anatomy

Use this sequence when it fits the page:

1. An 8 px `--brand-gradient` strip at the very top.
2. A white header, 76 px high, with a subtle bottom border.
3. A centered main container:
   `width: min(1140px, calc(100% - 40px)); margin-inline: auto`.
4. A focused hero or compact page introduction.
5. Content sections with 64 px vertical padding.
6. Optional full-width pale-blue bands for explanatory content.
7. A navy footer with quiet blue-gray text and white emphasis.

On screens below 620 px, use 16 px page gutters, a 64 px header, 48 px section
padding, and stack footer content. Hide nonessential header navigation below
900 px only if there is an accessible replacement or the links are duplicated
elsewhere.

### Canvas

Use the subtle dot grid on general page backgrounds:

```css
body {
  margin: 0;
  color: var(--text);
  font-family: var(--font-sans);
  font-size: 16px;
  line-height: 1.5;
  background-color: var(--white);
  background-image: radial-gradient(#E4E9F2 1px, transparent 1px);
  background-size: 18px 18px;
}
```

Give dense work areas, tables, editors, and forms a solid white or pale-blue
surface so the dots do not compete with content.

## Components

### Brand and header

- Render the mark as a 40 px rounded square filled with the brand gradient.
- Use one white initial or a simple white product glyph inside it.
- Set the product name at 20 px, bold, in blue.
- Keep navigation sparse: 15 px, semibold, 24 px gaps.
- A header may become sticky when the tool benefits from it, but retain the
  white surface, bottom border, and restrained shadow.

### Hero and section introductions

- Center marketing and overview heroes; left-align task-oriented tool headers.
- Use an eyebrow, one clear heading, a short supporting paragraph, and at most
  one primary call to action.
- Keep a centered hero near `max-width: 820px` with `64px auto` margins.
- Use `<h1>` once. Continue section hierarchy with `<h2>` and `<h3>`.

### Buttons and links

Primary button:

```css
.button-primary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 48px;
  padding: 12px 28px;
  border: 0;
  border-radius: var(--radius-btn);
  color: var(--white);
  background: var(--blue);
  font: inherit;
  font-weight: 700;
  cursor: pointer;
  transition: background-color .2s, box-shadow .2s, transform .2s;
}

.button-primary:hover {
  background: var(--navy);
  box-shadow: 0 8px 20px rgba(32, 85, 161, .3);
  transform: translateY(-2px);
}
```

- Use blue text links; underline them on hover.
- Use secondary outlined buttons only when a second action is truly needed.
- Keep action language concrete: “Scrub text”, “Download result”, or “Explore
  tools”, not “Click here”.
- Give every interactive element a visible `:focus-visible` outline.
- Disabled controls must look disabled and remain readable; never communicate
  state using opacity alone.

### Cards

- Use a 1 px border, 12 px radius, white fill, and `--shadow-card`.
- For showcase cards, use a header surface fading from `--card` to white.
- Use 28–32 px horizontal padding and 24–32 px vertical padding.
- Card hover may rise 4 px and use `--shadow-hover` when the card is
  interactive. Static cards must not imply clickability with hover motion.
- Use a 48 px blue icon tile with a 10 px radius where an icon adds meaning.
- Prefer simple SVG icons or established project icons. If using Unicode,
  verify that it renders consistently and mark decorative icons
  `aria-hidden="true"`.

Responsive card grid:

```css
.card-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(min(320px, 100%), 1fr));
  gap: 32px;
}
```

### Status pills

- Use small uppercase labels: 11 px, bold, `.06em` letter spacing.
- Use green-on-pale-green for available, complete, or successful states.
- Use muted-on-pale-blue for upcoming, inactive, or neutral states.
- Pair color with explicit text or an icon so color is never the only signal.

### Forms and tool workspaces

The landing page does not define forms, so extend its visual rules carefully:

- Labels: 14–15 px, bold, in `--text` or `--navy`.
- Inputs: white, 1 px `--border`, 10 px radius, at least 44 px tall.
- Focus: 2–3 px blue outline with sufficient offset; do not remove outlines.
- Group related controls in white cards or pale-blue sections.
- Place the primary action after the relevant inputs.
- Put validation beside the affected field and provide a summary for long
  forms.
- For clinical or sensitive data, state where processing occurs and whether
  data leaves the device. Never make an unverified privacy claim.

### Tables and data

- Use a white surface and subtle borders, not shadows on every row.
- Use navy or pale-blue headers.
- Right-align numeric values and use tabular numerals where useful.
- On narrow screens, allow horizontal scrolling with a visible affordance or
  transform simple tables into labeled rows. Do not shrink text below 14 px.

## Motion and interaction

- Keep transitions between 150 and 300 ms.
- Limit movement to 2 px for buttons and 4 px for interactive cards.
- Respect `prefers-reduced-motion`; remove smooth scrolling and transforms when
  reduced motion is requested.
- Do not use autoplay animation, parallax, glassmorphism, neon glows, or
  decorative gradient text.

## Accessibility and quality bar

Every page must:

- use semantic landmarks and a logical heading order;
- have a descriptive title and mobile viewport metadata;
- support keyboard use and visible focus;
- provide labels for controls and alternatives for meaningful imagery;
- maintain WCAG AA color contrast;
- preserve a 44 × 44 px minimum touch target where practical;
- work at 320 px wide and at 200% browser zoom;
- avoid horizontal page scrolling;
- respect reduced-motion preferences;
- keep external links safe with `rel="noopener"` when opening a new tab.

Use native HTML before adding JavaScript. Smooth anchor scrolling should be CSS
progressive enhancement (`scroll-behavior: smooth`) and must honor reduced
motion.

## Implementation workflow

1. Inspect the existing stack, components, and target page purpose.
2. Read `index.html` and reuse the canonical token values.
3. Identify the page's primary task and choose an appropriate anatomy; do not
   force a landing-page hero onto a utility screen.
4. Map existing styles to the AugmentedMD tokens before creating new colors,
   radii, or shadows.
5. Implement responsive behavior alongside desktop styles.
6. Check keyboard flow, focus, contrast, reduced motion, 320 px width, and
   content wrapping.
7. Compare the result with the canonical page. It should share the visual
   family without copying content or compromising the product's task.

## Avoid

- dark-mode-first, black, purple, or neon palettes;
- multiple competing gradients;
- excessive shadows, rounded containers, or pill-shaped controls;
- giant headings, dense all-caps text, or low-contrast gray copy;
- generic “AI sparkle” decoration, stock medical imagery, or novelty icons;
- hidden mobile functionality without an accessible alternative;
- copying clinical claims, creator details, or tool names from the reference
  page into unrelated products;
- adding dependencies for effects achievable with the existing stack.

## Completion checklist

- [ ] Canonical colors and role assignments are used consistently.
- [ ] The top gradient, dotted canvas, or another strong AugmentedMD signature
      anchors the page.
- [ ] Typography, container width, spacing, radii, and shadows match this guide.
- [ ] The layout serves the page's task instead of mechanically cloning the
      landing page.
- [ ] Responsive, keyboard, focus, contrast, zoom, and reduced-motion behavior
      have been checked.
- [ ] Privacy and clinical statements are accurate and not inferred from the
      reference design.
- [ ] No unnecessary framework or UI dependency was introduced.
