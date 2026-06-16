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

4. **Match the examples.** `examples/components.html` shows every component and
   `examples/starter.html` is the blank template. `screens/` holds full, real screens
   (workbench, history, auth, book-demo, confirmation) — **copy the closest one** as a
   starting point rather than building from scratch.

5. **Icons = Lucide only** (https://lucide.dev). Do **not** use Iconoir or any other set.
   Include the CDN once per screen and write `<i data-lucide="search"></i>`:
   ```html
   <script src="https://unpkg.com/lucide@latest"></script>
   <script>lucide.createIcons();</script>
   ```
   Common icons: shield-check, file-check, search, scan-eye, circle-check, triangle-alert,
   eye, arrow-right, history, plus, settings, chevron-down, x.

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
| Button sizes | `btn--xs` / `btn--sm` / (md default) / `btn--lg` / `btn--xl` |
| Destructive / status button | add a tone: `btn--error` `btn--warning` `btn--success` (× any variant = filled/outline/soft/text) |
| Button prefix/suffix | put `<i data-lucide>` before (prefix) or after (suffix) the label inside `.btn` |
| Button states | `:hover`/`:active`/`:focus-visible` automatic · `disabled` · `.is-loading` (spinner) |
| Full-width / group | `btn--block` · `.btn-group` wrapping `.btn`s |
| Icon-only button | `<button class="icon-btn" aria-label="…">` (+ `icon-btn--xs/sm/lg/xl`) |
| Text input | `.field` > `.label` + `.input` (sizes `input--sm`/`input--lg`) |
| Input status | `.input.is-error`/`.is-warning`/`.is-success` + `.field-error`/`-warning`/`-success`/`-hint` message |
| Read-only / disabled | `readonly` attr (muted) · `disabled` attr (unavailable) |
| Input prefix/suffix/compound | `.input-group` > `.input-group__addon` + `.input` (+ `.btn`/`select`) |
| Long text | `.textarea` |
| Verdict label | `.tag tag--supported/contradicted/unsupported/info/neutral` |
| Status badge (the standard) | `.status-badge status-badge--verified/pending/partial/flagged/dead/unrelated/neutral/info` — dot + uppercase mono pill with tinted bg + border. **Use this for ALL status/verdict indicators across every screen.** Always include the `<i></i>` dot. |
| Eyebrow / section label | `.label` (uppercase mono) |
| Logo / brand | `<a class="brand"><img src="…/assets/defacta-logo.svg" alt="Defacta" class="brand__logo"></a>` (stacked: `defacta-logo-stacked.svg`) |
| Container | `.card` (+ `--elevated` / `--soft`) |
| Modal / dialog | `.modal[data-open]` > `.modal__dialog--sm/md/lg` > `__header`/`__body`/`__footer` |
| Selectable choice | `.option-card` (radio inside) |
| Checkbox + description | `.checkbox` (box + label) |
| Dropdown / filter | `.select` > `<select>` |
| Search field | `.search` (icon + `.input`), or `.input-affix` > `.affix--prefix` + `.input.has-prefix` |
| Clear / password field | `.input-affix` > `.input` + trailing `.affix-btn` (X to clear, eye to toggle) |
| Collapsible panel | `<details class="accordion">` > `summary.accordion__trigger` + `.accordion__panel` |
| Data table | `.table-wrap` > `.table` (mono `<th>`, `.cell-title`/`.cell-sub`/`.cell-date`, `.row-arrow`) |
| Risk tag (table) | `.tag tag--mono risk--high/moderate/low` |
| Status (table) | `.status-badge status-badge--mono status-badge--flagged/pending/verified` |
| App header (signed-in) | `.site-header` > `.brand` + `.header-actions` (`.header-link`, `.icon-btn`) |
| Success/status icon | `.status-medallion status-medallion--success/error/warning` |
| Provider sign-in | `.btn btn--provider` |
| Report subheader | `.subheader` (title + `.subheader__meta` + actions) |
| Summary stat card | `.card.stat-card` (`.label` + `.stat-card__value` + `__sub`) |
| Report section | `.report-section` (id'd, with `<h2>`) inside `.report` grid |
| Annotated highlight | `<mark class="m-contradicted/unsupported/uncertain/supported">` + `.legend` |
| Claim verdict item | `.claim claim--accurate/unsupported/contradicted/uncertain` |
| Evidence source row | `.source-row` (no dividers) + the standard `.status-badge` |
| Audit log | `.audit` > `.audit__row` (time / event / actor) |
| On-this-page nav | `.toc` (sticky, scrollspy `.is-active`) |
| Feedback bar | `.feedback` (inside `.card`) |
| Switch | `<label class="switch"><input type="checkbox"><span class="switch__track"></span></label>` |
| Segmented toggle | `.toggle-group` > `<button class="is-active">` |
| Tabs | `.tabs` > `.tabs__tab[data-tabtarget]` + `.tabs__panel[data-tabpanel]` (JS-switched) |
| Breadcrumbs | `.breadcrumbs` > `<a>` + `.breadcrumbs__sep` (chevron-right) + `[aria-current]` |
| Alert / notification | `.alert alert--info/success/warning/error` (+ `.toast`) — icon + `__body` + `__close` |
| Pagination | `.pagination` > `.pagination__item` (+ `.is-active`, `.pagination__ellipsis`) |
| Dropdown menu | `.menu` > `.menu__trigger` + `.menu__list` > `.menu__item` (+ `--danger`, `.menu__sep`, `.menu__label`) |
| Context menu | `.menu__list.context-menu` positioned on right-click (see docs JS) |
| Tooltip | `<span class="tooltip" data-tooltip="…">` (CSS hover) |
| Upload | `<label class="upload">` dropzone + `.file-row` for uploaded files |
| Carousel | `.carousel` > `.carousel__viewport` > `.carousel__track` > `.carousel__slide` + `__btn`/`__dots` (JS) |
| Page header / footer | `.site-header` (marketing, or `.header-actions` for the signed-in app variant) · `.site-footer` |
| Sidebar / app shell | `.sidebar` > `.sidebar__item` (+ `.is-active`, `.sidebar__group`, `.sidebar__spacer`); wrap with `.app-shell` + `.app-shell__main` |

## Brand voice (visual)

Defacta is a verification tool for **high-stakes information**. The aesthetic is
**editorial and restrained — researcher, not marketer**:

- **Ink + paper.** Mostly `--grey-950` text on `--canvas`/`--paper`. Dark `.section--ink`
  bands for emphasis.
- **12-step gray scale** `--grey-950` (Ink) → `--grey-25`, derived from `#1A1A1A`. Text:
  `--grey-950`/`--grey-600`/`--grey-400`; borders `--grey-200`; hairlines `--grey-100`.
- **One accent.** `--color-accent-blue` (+ `--color-accent-soft` / `--color-accent-border`)
  used **sparingly** — focus rings, eyebrow labels, small highlights. Don't add new accent colors.
- **Semantic color = meaning, not decoration.** error/warning/success/info only signal
  state or verdict — never styling flourish. Each has three tones: base (text/icon/dot),
  `*-soft` (tinted fill), `*-border` — e.g. `--color-error` / `--color-error-soft` / `--color-error-border`.
  Put text on the `*-soft` tint, never on the saturated base.
- **Soft, low shadows. Soft corners.** Elevation `--shadow-xs/sm/md/lg/xl` — use the lowest that
  reads. Radius `--radius-2 / 4 / 6 / 8 / 12 / 16 / 20 / 24` (8–16 covers most UI); `--radius-full` (999)
  is reserved for **circular, user-related** elements only — avatars, name chips, user UI, reactions.
  Spacing is the 8px-base scale `--space-0 / 025 / 050 / 075 / 100 / 150 / 200 / 250 / 300 / 400 /
  500 / 600 / 800 / 1000` (rem-based; `--space-100` = 8px) — always a token, never arbitrary px.
  No heavy drop shadows, no gradients except the one brand gradient, no bright fills.
- **The mono uppercase `.label`** is the signature touch — use it for eyebrows and field labels.
- **Type scale** (Inter unless noted; classes in `base.css`, never raw `font-size`). Headings &
  body default to **Medium / Regular**; add `.strong` for **Semibold** emphasis.
  - Display `.display` 64 · Headings `h1` 48 · `h2` 40 · `h3` 32 · `h4` 24
  - Body `.body-xl` 20 · `.body-lg` 18 · `.body` 16 · `.text-sm` 14 · `.text-xs` 12
  - Label (IBM Plex Mono, uppercase) `.label` 12 · `.label.label-md` 14 · `.label.label-lg` 16
  - Mono / data (IBM Plex Mono) `.mono` 14 · `.mono.mono-sm` 12 · `.mono.mono-lg` 16 — IDs, timestamps, hex; never body copy.
  - Component titles: cards & modals use `h4` (24); report/page sections use `h3` (32).

## Hard "do not" list

- Do not introduce Tailwind, Bootstrap, or any other CSS framework.
- Do not use Iconoir or mixed icon sets — Lucide only.
- Do not recreate, redraw, or restyle the logo — always use the SVG in `assets/`.
- Do not add `var(--token, #fallback)` fallbacks — tokens always exist.
- Do not hardcode colors, sizes, radii, or shadows.
- Do not duplicate or restyle an existing component for a one-off.
- Do not invent new accent colors or font families.
