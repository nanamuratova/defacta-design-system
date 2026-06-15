# Defacta Design System

A small, token-driven design system so anyone can build new Defacta screens that stay
on-brand — without redesigning anything. Open this folder in **Claude Code** and just
describe the screen you want.

---

## For clients: how to make a screen

You don't need to write code. Open this folder in Claude Code and ask in plain language:

> "Make a dashboard screen with a header, a 3-column grid of stat cards, and a table of
> recent verifications below."

> "Add a settings page with a form: name, email, and a notification toggle."

> "Build an empty-state screen for when there are no verifications yet."

Claude reads `CLAUDE.md` and builds the screen using the existing components and tokens,
so it comes out looking like the rest of Defacta. To tweak it:

> "Make the buttons larger." · "Use the dark section style for the hero." ·
> "Change the accent to feel warmer."

### Re-theme everything at once
Every color, font, and size lives in **`tokens.css`**. Change a value there and **every
screen updates**. For example, ask:

> "In tokens.css, make the corners sharper and the ink slightly warmer."

---

## What's in here

```
defacta-design-system/
├── CLAUDE.md            ← the rules Claude follows (keeps screens on-brand)
├── tokens.css           ← single source of truth: colors, type, spacing, radius
├── styles.css           ← the one stylesheet each screen links
├── components/
│   ├── base.css         ← reset + typography (headings, .label, body text)
│   ├── icons.css        ← Lucide icon sizing (free/open-source icon set)
│   ├── buttons.css      ← .btn variants/sizes/tones, .icon-btn
│   ├── forms.css        ← input, textarea, option-card, checkbox, select, password, OR divider
│   ├── badges.css       ← .tag, .status-badge, risk + mono variants
│   ├── table.css        ← .table data table (History)
│   ├── modal.css        ← .modal dialogs (sm/md/lg) + status medallion
│   └── layout.css       ← container, section, card, grid, header, accordion, workbench
├── examples/
│   ├── components.html  ← live catalog of every component (open this first)
│   └── starter.html     ← blank screen template — copy it to start a new screen
└── screens/             ← full real screens — copy the closest as a starting point
    ├── workbench.html   ← verification console (modes, advanced settings, char counter)
    ├── history.html     ← reports table with filters, risk tags, status badges
    ├── auth.html        ← sign in / create account modal
    ├── book-demo.html   ← scheduling modal (calendar + time slots)
    └── confirmation.html← success confirmation modal
```

## Icons

The system uses **[Lucide](https://lucide.dev)** (free, open-source). Each screen loads it
from a CDN and uses `<i data-lucide="search"></i>`. No install needed.

## Start a screen by hand (optional)

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="../styles.css">
</head>
<body>
  <header class="site-header">
    <span class="brand">Defacta</span>
    <nav><a href="#">Docs</a><a href="#">Sign in</a></nav>
  </header>

  <main class="section">
    <div class="container content stack">
      <span class="label">New screen</span>
      <h1 class="display">Your headline</h1>
      <button class="btn btn--primary">Get started</button>
    </div>
  </main>
</body>
</html>
```

## Preview

Open `examples/components.html` in a browser, or run a tiny server from this folder:

```bash
python3 -m http.server 8000
# then open http://localhost:8000/examples/components.html
```

---

## Next steps (optional upgrades)

- **Visual catalog for clients** — publish this library to a Claude Design project so
  clients browse component cards instead of reading code.
- **React** — when a client needs a production app, the tokens and markup port to React
  almost 1:1 (tokens stay identical; class names become components).
