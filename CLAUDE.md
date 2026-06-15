# Defacta Design System — Rules for Claude

You are working inside the **Defacta design system**. Your job is to help build new
screens that look like they were designed by the original designer. Consistency
matters more than cleverness. Follow these rules exactly.

## The golden rules

1. **Tokens are the only source of truth.** Every color, font, size, space, radius,
   and shadow must come from a `var(--token)` defined in `tokens.css`.
   **NEVER write a raw hex color, px font-size, or px spacing value in a screen.**
   - ❌ `color: #1A1A1A;`  ❌ `padding: 16px;`  ❌ `font-size: 20px;`
   - ✅ `color: var(--text-primary);`  ✅ `padding: var(--space-16);`  ✅ `font-size: var(--text-body-lg);`

2. **Reuse components, never reinvent them.** Buttons, inputs, tags, badges, cards,
   headers, sections already exist in `components/`. Use their classes.
   - If a screen needs something that does **not** exist as a component, STOP and say:
     **"Missing component: [name]"** — then propose adding it to `components/`,
     built from tokens, before using it. Do not hand-roll a one-off styled element.

3. **Link the system, don't copy it.** Every new screen starts with:
   ```html
   <link rel="stylesheet" href="../styles.css">
   ```
   Never paste component CSS into a screen. Never restyle a `.btn` inline.

4. **Match the examples.** `examples/components.html` shows every component.
   `examples/starter.html` is the blank screen template — copy it to start a new screen.

## How to build a screen

1. Copy `examples/starter.html` to a new file in `examples/` (or wherever the client keeps screens).
2. Compose the page from existing classes:
   - Page chrome: `.site-header`, `.site-footer`
   - Rhythm: `.section`, `.section--paper`, `.section--ink` (alternate light/dark)
   - Width: wrap content in `.container` → `.content`
   - Blocks: `.card`, `.grid--2/3/4`, `.stack`, `.cluster`
3. Use tokens for any spacing/color not covered by a component.
4. Verify it renders (run a local preview) before calling it done.

## Component cheat-sheet

| Need | Use |
|---|---|
| Action button | `<button class="btn btn--primary">` (also `--secondary` `--tertiary` `--ghost` `--link`) |
| Smaller / larger button | add `btn--sm` or `btn--lg` |
| Destructive / status button | add a tone: `btn--error` `btn--warning` `btn--success` |
| Icon-only button | `<button class="icon-btn">` (+ `icon-btn--sm/lg`) |
| Text input | `.field` > `.label` + `.input` |
| Long text | `.textarea` |
| Verdict label | `.tag tag--supported/contradicted/unsupported/info/neutral` |
| State pill | `.status-badge status-badge--verified/pending/flagged/neutral` |
| Eyebrow / section label | `.label` (uppercase mono) |
| Container | `.card` (+ `--elevated` / `--soft`) |

## Brand voice (visual)

Defacta is a verification tool for **high-stakes information**. The aesthetic is
**editorial and restrained — researcher, not marketer**:

- **Ink + paper.** Mostly `--grey-950` text on `--canvas`/`--paper`. Dark `.section--ink`
  bands for emphasis.
- **One accent.** `--color-accent-blue` is used **sparingly**. Don't add new accent colors.
- **Semantic color = meaning, not decoration.** Red/amber/green only signal
  error/warning/success or claim verdicts — never as styling flourish.
- **Soft, low shadows. Soft corners** (radius 8–16). No heavy drop shadows, no gradients
  except the one brand gradient, no bright fills.
- **The mono uppercase `.label`** is the signature touch — use it for eyebrows and field labels.

## Hard "do not" list

- Do not introduce Tailwind, Bootstrap, or any other CSS framework.
- Do not add `var(--token, #fallback)` fallbacks — tokens always exist.
- Do not hardcode colors, sizes, radii, or shadows.
- Do not duplicate or restyle an existing component for a one-off.
- Do not invent new accent colors or font families.
