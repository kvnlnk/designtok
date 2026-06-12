# designtok — Architecture

## Type
Single-page Vanilla HTML/CSS/JS web app

## Target User
Designers and front-end developers who manage design tokens and need them in multiple output formats.

## Value Proposition
Zero-install, zero-dependency web tool that converts JSON design tokens into CSS custom properties, Tailwind CSS config, or SASS variables — all in a single HTML file you can open in any browser or host anywhere.

## Tech Stack + Rationale

| Component | Choice | Rationale |
|-----------|--------|-----------|
| HTML/CSS/JS | Vanilla (no framework) | Zero dependencies, max portability, works offline |
| UI | Semantic HTML + CSS | Single file, no build step |
| Build | None | Self-contained; deploy by copying one file |
| Hosting | GitHub Pages / any static host | Drop the file → it works |

## Folder Structure

```
designtok/
├── index.html              # The entire app (HTML + CSS + JS in one file)
├── .gitignore
├── .env.example
├── README.md
└── ARCHITECTURE.md
```

**Rationale for single-file architecture:** The app has ~3 distinct UI states (input, transform, output) and 3 output formats. A single file keeps deployment trivial and preserves the "open in browser" UX. If complexity grows, the JS portion can be extracted into a separate `app.js`.

## Data Flow

```
 User opens index.html
       │
       ▼
 ┌─────────────────────┐
 │  Textarea: Paste JSON │  User pastes design token JSON
 │  (input area)         │    e.g. {"colors.primary": "#06f"}
 └──────────┬──────────┘
            │ JSON string
            ▼
 ┌─────────────────────┐
 │  parseAndValidate()  │  JSON.parse + validation
 │  (inline JS)         │  Shows error inline if invalid
 └──────────┬──────────┘
            │ validated tokens object
            ▼
 ┌─────────────────────┐
 │  Format selector     │  Dropdown: CSS / Tailwind / SASS
 │  (radio/select)      │
 └──────────┬──────────┘
            │ selected format
            ▼
 ┌─────────────────────┐
 │  convertTokens()     │  Transform to chosen format:
 │  (inline JS)         │    - CSS → :root { --color-primary: #06f; }
 │                      │    - Tailwind → module.exports = { theme: { extend: { colors: { primary: '#06f' } } } }
 │                      │    - SASS → $color-primary: #06f;
 └──────────┬──────────┘
            │ formatted string
            ▼
 ┌─────────────────────┐
 │  Output textarea     │  Editable output with "Copy" button
 │  (readonly+copy)     │
 └─────────────────────┘
```

## Key Design Decisions

1. **Single-file, zero dependencies** — The entire app lives in one HTML file. No CDN links, no npm, no build. This ensures it works offline and can be served from any static host or even emailed as an attachment.
2. **Flat token → nested object handling** — Input tokens can be dot-notation (`colors.primary`) or nested objects (`{ colors: { primary: "#06f" } }`). The parser normalizes both into a flat key-value map for uniform conversion.
3. **No framework, no bundler** — For a single-page app with ~3 views and ~3 output formatters, vanilla JS is simpler and more maintainable than importing React/Vue. The code stays under ~300 lines.
4. **Client-side only** — No server, no API calls. All data stays in the browser. This makes it safe for teams that can't paste tokens into external services.
5. **Copy-button UX** — `navigator.clipboard.writeText` provides one-click copy with visual feedback (button text changes to "Copied!").

## Estimated Time Budget

| Area | Estimate |
|------|----------|
| HTML structure + CSS styling | 1.5h |
| JSON input parsing + validation | 1h |
| CSS var converter | 1h |
| Tailwind config converter | 1.5h |
| SASS converter | 1h |
| Copy button + UX polish | 0.5h |
| Testing (manual) | 1h |
| **Total** | **~7.5h** |
