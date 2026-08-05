# AugmentedMD component catalog

Copy-paste CSS and markup for every component in the house style, taken from the
two reference pages. Add only the components a page actually uses.

The base rules in `assets/style-block.css` already cover the tokens, `body`,
headings, links, `.brand-bar`, `.header`, `main`, the hero, and the footer. What
follows are the components layered on top.

---

## Header and brand

Two brand treatments. Landing pages use a gradient tile with the initial; tool
pages use a solid tile with a glyph, and put the brand on the right.

```css
.header{height:76px;padding:0 max(24px,5vw);border-bottom:1px solid var(--border);background:var(--white);display:flex;align-items:center;justify-content:space-between}
.brand{display:flex;align-items:center;gap:12px;color:var(--blue);font-size:20px;font-weight:700}
.logo{display:grid;place-items:center;width:40px;height:40px;border-radius:var(--radius-btn);color:var(--white);background:var(--brand-gradient);font-size:20px;font-weight:700}
.nav{display:flex;gap:24px;align-items:center}
.nav a{color:var(--text);font-weight:600;font-size:15px}
.nav a:hover{color:var(--blue)}
```

```html
<header class="header">
  <div class="brand">
    <span class="logo">A</span>
    <span>AugmentedMD</span>
  </div>
  <nav class="nav">
    <a href="#tools">Tools</a>
    <a href="#about">About</a>
    <a href="#contact">Contact</a>
  </nav>
</header>
```

Tool-page variant — the header holds only the brand, right-aligned, with a solid
`.shield` tile after the name:

```css
.header{justify-content:flex-end}
.brand{font-size:18px}
.shield{display:grid;place-items:center;width:36px;height:36px;border-radius:var(--radius-btn);color:var(--white);background:var(--blue)}
```

```html
<header class="header">
  <div class="brand"><span>PHI Scrubber</span><span class="shield">&#10003;</span></div>
</header>
```

The `.nav` is hidden below 900px. If a page has more than four nav items it needs
a different pattern; ask rather than inventing a hamburger menu.

---

## Hero

```css
.hero{max-width:820px;margin:64px auto;text-align:center}
.eyebrow{color:var(--muted);font-size:12px;font-weight:700;letter-spacing:.08em;text-transform:uppercase}
h1{margin:16px 0;font-size:clamp(34px,4vw,48px);line-height:1.15}
h1 em{color:var(--navy);font-style:normal}
.sub{max-width:680px;margin:24px auto;font-size:18px;line-height:1.6}
.cta{display:inline-block;margin-top:32px;padding:14px 28px;border:0;border-radius:var(--radius-btn);color:var(--white);background:var(--blue);font-size:16px;font-weight:700;cursor:pointer;transition:all .2s}
.cta:hover{background:var(--navy);text-decoration:none;transform:translateY(-2px);box-shadow:0 8px 20px rgba(32,85,161,.3)}
```

```html
<section class="hero">
  <div class="eyebrow">Empowering Clinicians</div>
  <h1>Navigate the <em>post-AI digital world</em> with confidence.</h1>
  <p class="sub">Practical, open-source tools designed for doctors who want to harness AI while maintaining privacy, security, and clinical excellence.</p>
  <a href="#tools" class="cta">Explore Tools</a>
</section>
```

The `<em>` carries the phrase you want remembered — it renders upright in navy,
not italic. Exactly one per `h1`. Tool pages cap `h1` at `40px` and drop the
`.cta`, since the tool itself is immediately below.

---

## Section and section title

```css
.section{padding:64px 0}
.section-title{text-align:center;margin-bottom:48px}
.section-title h2{margin:0;font-size:32px}
.section-title p{color:var(--muted);font-size:17px;margin:12px 0 0}
```

```html
<section class="section" id="tools">
  <div class="section-title">
    <h2>Clinical Tools</h2>
    <p>Privacy-first solutions for modern medical practice</p>
  </div>
  <!-- content -->
</section>
```

To alternate surfaces, add a tinted variant. It sits full-bleed only if the
section is outside `main`; inside `main` it tints the content column:

```css
.about{background:var(--card);border-top:1px solid var(--border)}
```

---

## Tool card grid

The signature component of the landing page: a responsive grid of cards, each
with a tinted header, an icon tile, a status pill, and arrow links.

```css
.tools-grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(320px,1fr));gap:32px;margin-top:48px}
.tool-card{border:1px solid var(--border);border-radius:var(--radius-card);background:var(--white);box-shadow:var(--shadow-card);overflow:hidden;transition:all .3s}
.tool-card:hover{box-shadow:var(--shadow-hover);transform:translateY(-4px)}
.tool-header{padding:32px 28px 24px;background:linear-gradient(135deg,var(--card) 0%,var(--white) 100%);border-bottom:1px solid var(--border)}
.tool-icon{display:inline-grid;place-items:center;width:48px;height:48px;border-radius:var(--radius-btn);color:var(--white);background:var(--blue);font-size:24px;margin-bottom:16px}
.tool-card h3{margin:0 0 8px;font-size:22px;color:var(--navy)}
.tool-tag{display:inline-block;padding:4px 12px;border-radius:var(--radius-pill);color:var(--green);background:var(--green-bg);font-size:11px;font-weight:700;letter-spacing:.06em;text-transform:uppercase}
.tool-tag.coming{color:var(--muted);background:var(--card)}
.tool-body{padding:24px 28px}
.tool-body p{margin:0 0 20px;line-height:1.7}
.tool-links{display:flex;flex-direction:column;gap:12px}
.tool-link{display:inline-flex;align-items:center;gap:8px;color:var(--blue);font-weight:700;font-size:15px}
.tool-link:hover{text-decoration:underline}
.tool-link::after{content:'→';font-size:18px}
.tool-link.github{font-size:13px;opacity:0.8}
.tool-link.github::after{content:'↗'}
```

```html
<div class="tools-grid">
  <div class="tool-card">
    <div class="tool-header">
      <div class="tool-icon">&#10003;</div>
      <h3>PHI Scrubber</h3>
      <span class="tool-tag">Available Now</span>
    </div>
    <div class="tool-body">
      <p>Remove protected health information from clinical text before sharing. Fully offline detection—no data ever leaves your browser.</p>
      <div class="tool-links">
        <a href="https://gorin-research-repo.github.io/phiscrubber/" target="_blank" rel="noopener" class="tool-link">Launch PHI Scrubber</a>
        <a href="https://github.com/gorin-research-repo/phiscrubber" target="_blank" rel="noopener" class="tool-link github">View on GitHub</a>
      </div>
    </div>
  </div>

  <div class="tool-card">
    <div class="tool-header">
      <div class="tool-icon">&#9998;</div>
      <h3>Clinical Note Assistant</h3>
      <span class="tool-tag coming">Coming Soon</span>
    </div>
    <div class="tool-body">
      <p>AI-powered assistance for clinical documentation that respects patient privacy and integrates seamlessly into your workflow.</p>
    </div>
  </div>
</div>
```

A "Coming Soon" card carries a description and no links — do not link to
something that does not exist yet. Icon glyphs in use: `&#10003;` check,
`&#9998;` pencil, `&#128200;` chart, `&#128274;` lock, `&#128197;` calendar,
`&#128172;` speech balloon.

---

## Panel

The tool-page workhorse: a bordered white card with a numbered head, a body, and
a tinted foot for counts and controls. Pair two panels around a centered action
button for an input/output workspace.

```css
.workspace{display:grid;grid-template-columns:1fr auto 1fr;gap:24px;align-items:center}
.panel{min-width:0;overflow:hidden;border:1px solid var(--border);border-radius:var(--radius-card);background:var(--white);box-shadow:var(--shadow-card)}
.panel-head,.panel-foot{padding:16px 24px;display:flex;align-items:center;justify-content:space-between;gap:16px}
.panel-head{border-bottom:1px solid var(--border)}
.panel-head div{display:flex;align-items:center;gap:12px}
.panel-head h2{margin:0;font-size:18px}
.step{display:grid;place-items:center;width:26px;height:26px;border-radius:var(--radius-pill);color:var(--white);background:var(--blue);font-size:13px;font-weight:700}
.panel-foot{min-height:60px;border-top:1px solid var(--border);background:var(--card);color:var(--muted);font-size:13px}
.panel-foot label{display:flex;align-items:center;gap:8px}
.action{display:grid;place-items:center;gap:12px}
.shortcut{color:var(--muted);font-size:12px}
```

```html
<section class="workspace">
  <div class="panel">
    <div class="panel-head"><div><span class="step">1</span><h2>Original text</h2></div><button class="link" id="clear" type="button">Clear</button></div>
    <textarea id="source" spellcheck="false" placeholder="Paste a clinical note, message, or document here&hellip;"></textarea>
    <div class="panel-foot"><span id="chars">0 characters</span><button class="link" id="example" type="button">Try an example</button></div>
  </div>
  <div class="action"><button class="scrub" id="run" type="button">Scrub PHI</button><span class="shortcut">Ctrl / &#8984; + Enter</span></div>
  <div class="panel">
    <div class="panel-head"><div><span class="step">2</span><h2>Scrubbed text</h2></div><button class="link" id="copy" type="button" disabled>Copy</button></div>
    <div class="output empty" id="output" aria-live="polite">Your de-identified text will appear here.</div>
    <div class="panel-foot"><span id="summary">Ready to scan</span></div>
  </div>
</section>
```

At 900px `.workspace` becomes `grid-template-columns:1fr` and `.shortcut` hides,
so the action button falls between the two panels in reading order. Keep the
markup in that order for that reason.

---

## Text input and output surfaces

Monospace, full-bleed inside the panel, no visible border of their own — the
panel supplies the frame.

```css
button,textarea,select{font-family:inherit;font-size:inherit}
textarea,.output{display:block;width:100%;height:340px;padding:24px;border:0;outline:0;resize:none;color:var(--ink);background:var(--white);font-family:var(--font-mono);font-size:14px;line-height:1.7}
textarea::placeholder{color:var(--muted)}
.output{overflow:auto;white-space:pre-wrap;overflow-wrap:anywhere}
.output.empty{display:grid;place-items:center;color:var(--muted);text-align:center;font-family:var(--font-sans);font-size:15px}
.output mark{margin:0 -2px;padding:1px 3px;border-radius:5px;color:var(--blue);background:var(--card);font-weight:700}
select{max-width:150px;padding:6px 8px;border:1px solid var(--border);border-radius:8px;color:var(--blue);background:var(--white);font-size:13px;font-weight:700}
```

An empty output pane shows placeholder guidance in sans-serif and switches to
monospace once it holds real content — toggle the `.empty` class. Heights drop to
`280px` below 620px. Highlighted spans use `<mark>`, tinted rather than yellow.

---

## Buttons

Three tiers, and nothing else:

```css
.cta{padding:14px 28px;border:0;border-radius:var(--radius-btn);color:var(--white);background:var(--blue);font-size:16px;font-weight:700;cursor:pointer;transition:all .2s}
.cta:hover{background:var(--navy);transform:translateY(-2px);box-shadow:0 8px 20px rgba(32,85,161,.3)}
.scrub{padding:12px 20px;border:0;border-radius:var(--radius-btn);color:var(--white);background:var(--blue);font-size:15px;font-weight:700;white-space:nowrap;cursor:pointer}
.scrub:hover{background:var(--navy)}
.link{padding:4px;border:0;color:var(--blue);background:none;font-size:14px;font-weight:700;cursor:pointer}
.link:hover:enabled{text-decoration:underline}
.link:disabled{color:var(--muted);cursor:default}
```

- `.cta` — the one hero-level call to action per page.
- `.scrub` (rename per verb: `.convert`, `.generate`) — the primary in-tool
  action.
- `.link` — borderless tertiary actions in panel heads and feet: Clear, Copy,
  Try an example. Disable rather than hide when unavailable, and style the
  disabled state in `--muted`.

There is no outlined or ghost button in this system. If you need a secondary
action next to a primary one, use `.link`.

---

## Chips and findings box

For summarizing results as a set of labeled counts.

```css
.findings{margin:24px 0;padding:24px;border:1px solid var(--border);border-radius:var(--radius-card);background:var(--card)}
.findings header{display:flex;align-items:center;justify-content:space-between;gap:16px}
.findings h2{margin:0;font-size:18px}
.findings header span{color:var(--muted);font-size:13px}
.chips{display:flex;flex-wrap:wrap;gap:8px;margin-top:16px}
.chip{display:inline-block;padding:6px 14px;border-radius:var(--radius-pill);color:var(--white);background:var(--blue);font-size:12px;font-weight:700;letter-spacing:.08em;text-transform:uppercase}
```

```html
<section class="findings" id="findings" hidden>
  <header><h2>Detected identifiers</h2><span id="total"></span></header>
  <div class="chips" id="chips"></div>
</section>
```

Use the `hidden` attribute for the empty state and remove it when there is
something to show, rather than rendering an empty box.

`.chip` is a solid blue pill for data. `.tool-tag` is a tinted pill for status.
They are not interchangeable.

---

## Notice

The clinical caveat. Every tool that touches patient data or clinical judgment
gets one, placed after the working area and before the footer.

```css
.notice{margin:64px 0;padding:20px 24px;border:1px solid #EBDCC0;border-radius:var(--radius-card);color:var(--text);background:var(--amber-bg);font-size:14px}
.notice strong{color:var(--amber)}
```

```html
<aside class="notice"><strong>Review before sharing.</strong> Automated detection can miss PHI or flag non-PHI. This tool assists de-identification; it does not certify HIPAA compliance.</aside>
```

The pattern is a bold imperative lead-in, then what can go wrong, then an
explicit statement of what the tool does not guarantee. Margin drops to `48px`
below 620px.

---

## Mission box

A white box inside a tinted section, for a bio or a positioning statement.

```css
.about-content{max-width:720px;margin:0 auto;text-align:center}
.about-content p{font-size:17px;line-height:1.8;margin-bottom:24px}
.mission{margin:48px 0;padding:28px 32px;border:1px solid var(--border);border-radius:var(--radius-card);background:var(--white);box-shadow:var(--shadow-card)}
.mission h3{margin:0 0 16px;font-size:20px}
.mission p{margin:0;font-size:16px;line-height:1.7}
```

```html
<section class="section about" id="about">
  <div class="about-content">
    <div class="section-title"><h2>About the Creator</h2></div>
    <div class="mission">
      <h3>Michael Gorin, MD</h3>
      <p>Academic urologist at Mount Sinai focusing on use of technologies (AI-based and conventional) to improve patient safety, operational efficiency, and physician effectiveness.</p>
    </div>
    <p>Connecting prose between boxes goes here.</p>
    <div class="mission">
      <h3>Open Source &amp; Free</h3>
      <p>All tools on this site are <strong>open source and free for anyone to use, modify, or improve upon</strong>.</p>
    </div>
  </div>
</section>
```

---

## Footer

```css
footer{padding:32px max(24px,5vw);color:#C7D4EA;background:var(--navy);display:flex;justify-content:space-between;align-items:center;flex-wrap:wrap;gap:20px}
.footer-left{display:flex;align-items:center;gap:16px}
.footer-brand{font-weight:700;font-size:16px;color:var(--white)}
.footer-links{display:flex;gap:20px;flex-wrap:wrap}
.footer-links a{color:#C7D4EA;font-size:14px}
.footer-links a:hover{color:var(--white)}
```

```html
<footer id="contact">
  <div class="footer-left">
    <span class="footer-brand">AugmentedMD</span>
    <span>Open-source tools by Michael Gorin, MD</span>
  </div>
  <div class="footer-links">
    <a href="https://github.com/gorin-research-repo" target="_blank" rel="noopener">GitHub</a>
    <a href="https://twitter.com/michael_gorin" target="_blank" rel="noopener">Twitter</a>
    <a href="https://twitter.com/AugmentedMD" target="_blank" rel="noopener">@AugmentedMD</a>
  </div>
</footer>
```

Single-tool pages use a simpler centered footer:

```css
footer{padding:28px max(24px,5vw);color:#C7D4EA;background:var(--navy);display:flex;justify-content:center;text-align:center;font-size:13px}
```

```html
<footer><span>Tool by @michael_gorin / @AugmentedMD</span></footer>
```

---

## Responsive block

Append this at the end of the stylesheet, adding only the lines a page needs.

```css
@media(max-width:900px){
  .tools-grid{grid-template-columns:1fr}
  .workspace{grid-template-columns:1fr}
  .nav{display:none}
  .shortcut{display:none}
}
@media(max-width:620px){
  main{width:calc(100% - 32px)}
  .header{height:64px;padding:0 16px}
  .hero{margin:48px auto}
  .section{padding:48px 0}
  .section-title h2{font-size:28px}
  textarea,.output{height:280px}
  .notice{margin:48px 0}
  footer{flex-direction:column;text-align:center}
}
```

---

## Smooth scroll

The only script on a content page. Include it whenever there are in-page anchors.

```js
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
  anchor.addEventListener('click', function (e) {
    e.preventDefault();
    const target = document.querySelector(this.getAttribute('href'));
    if (target) {
      target.scrollIntoView({behavior: 'smooth', block: 'start'});
    }
  });
});
```

A keyboard shortcut for the primary action is a nice touch on tool pages, and the
`.shortcut` caption exists to advertise it:

```js
document.addEventListener('keydown', e => {
  if ((e.metaKey || e.ctrlKey) && e.key === 'Enter') run();
});
```
