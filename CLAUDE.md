# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A French-language single-page partnership proposal for **Nomad Food Club** — a Montréal-based street food social experience concept targeting hostels and shared spaces. The site pitches a collaboration to venue partners.

## Development

No build system. Open `index.html` directly in a browser or serve it locally:

```bash
python3 -m http.server 8080
# then open http://localhost:8080
```

There are no dependencies to install, no tests, and no linter configuration.

## Architecture

Everything lives in a single file: `index.html` (574 lines). It is structured as:

1. **`<style>` block** — all CSS, including design tokens, component styles, animations, and responsive breakpoints
2. **`<body>` HTML** — page sections in order: ticker → nav → hero → photo-strip → marquee-break → `#concept` → auberge → `#comment` (steps) → esprit → `#contact` (CTA) → footer
3. **`<script>` block** — custom cursor tracking + IntersectionObserver scroll-reveal

The file is large (~300 KB) because the logo is embedded as a base64 `data:image/png` URI inside a `<div class="logo-badge-img">`.

### Design Tokens (CSS custom properties)

```css
--olive: #4A6741       /* primary green */
--olive-dark: #354d2f
--mustard: #D4A84B     /* accent gold */
--mustard-light: #f5e8c0
--piment: #D94F30      /* CTA red-orange */
--bg: #FAF7F2
--ink: #2D2A26
--ink-light: #6b6460
```

### Typography

- **Chewy** (Google Fonts) — all headings, brand name, decorative text
- **Poppins** — body copy, buttons, labels

### Photo Placeholders

Photo slots are `<div>` elements styled with a solid color background. CSS comments throughout mark where to swap in real images:

```css
/* Pour ajouter une photo : background:url('ton-image.jpg') center/cover no-repeat */
```

### Scroll Animations

Elements with `.reveal` class start invisible (`opacity:0; transform:translateY(24px)`) and gain `.visible` via an `IntersectionObserver` (threshold 0.1), staggered by 80ms per element.

### Responsive Breakpoints

- `≤860px`: collapses all two-column grids to single column; hides `.hero-right`
- `≤520px`: reduces padding on nav, sections, footer

## Available MCP Servers

### Canva (`mcp__04aae35a-*`)

Full Canva design toolset is connected. Useful for this project:
- `generate-design` / `generate-design-structured` — AI-generate marketing visuals
- `search-designs` — find existing Canva assets for NFC
- `export-design` — export PNGs/SVGs to use as photo slot replacements
- `upload-asset-from-url` — bring external images into Canva
- `start-editing-transaction` + `perform-editing-operations` + `commit-editing-transaction` — programmatic design edits
- `get-assets` / `list-brand-kits` — access brand assets and kits

### GitHub (`mcp__github__*`)

Scoped to `gabrielmassotbordenave-web/nomadfoodclub-proposal`. Use for PR management, file pushes, and issue tracking.

## Available Skills

| Skill | When to use |
|---|---|
| `review` | Review a PR before merging |
| `security-review` | Audit changes on the current branch |
| `simplify` | Refactor changed code for quality and efficiency |
| `update-config` | Modify `settings.json`, add permissions, configure hooks |
| `fewer-permission-prompts` | Reduce repeated tool permission prompts |
| `init` | Re-initialize or update this CLAUDE.md |

## Development Branch

Work on branch `claude/implement-mcp-server-ZLfr5`. Push with:

```bash
git push -u origin claude/implement-mcp-server-ZLfr5
```
