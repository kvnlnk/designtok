# 🎨 designtok

**Convert JSON design tokens to CSS custom properties, Tailwind config, or SASS — in your browser, no install needed.**

Paste → select format → copy. Works offline from a single HTML file.

---

## 🤖 Fully Vibecoded with Hermes Agent

This project was built entirely through natural language conversations with [Hermes Agent](https://hermes-agent.nousresearch.com) — an autonomous AI coding assistant. From architecture to deployment, every line of code was generated, tested, and shipped via chat prompts.

---

## ✨ Features

- **📋 Three Output Formats** — CSS `:root { --key: value }`, Tailwind `theme.extend` config, SASS `$key: value`
- **🔤 Dot-Notation & Nested Objects** — Handles `colors.primary` and `{ colors: { primary: "#06f" } }`
- **✅ Live Validation** — Shows line-number errors for invalid JSON
- **📋 One-Click Copy** — Copies to clipboard with "Copied!" feedback (+ keyboard shortcut `Cmd/Ctrl+Shift+C`)
- **🎲 Sample Tokens** — Pre-fill with realistic design tokens (colors, spacing, typography, shadows)
- **🌙 Dark/Light Theme** — GitHub dark mode toggle with localStorage persistence
- **📱 Responsive** — Works on mobile (375px) and desktop (1280px+)
- **🔌 Zero Dependencies** — Single HTML file, no build, no server, no CDN

---

## 🛠️ Tech Stack

| Layer        | Technology                 |
|-------------|----------------------------|
| Framework   | None — Vanilla JS          |
| Runtime     | Any modern browser         |
| Styling     | CSS custom properties      |
| Hosting     | GitHub Pages / any static host |

---

## 🚀 Usage

### Option A: Open directly

```bash
# Just open the file in any browser
open index.html

# Or serve it locally
npx serve .
```

### Option B: Use online

Deploy the single `index.html` to any static host — Vercel, Netlify, GitHub Pages, or even email it as an attachment.

### What to paste

```json
{
  "colors.primary": "#3b82f6",
  "colors.secondary": "#8b5cf6",
  "colors.neutral.100": "#f5f5f5",
  "colors.neutral.900": "#171717",
  "spacing.sm": "0.5rem",
  "spacing.md": "1rem",
  "spacing.lg": "2rem",
  "typography.fontFamily.sans": "Inter, system-ui, sans-serif",
  "typography.fontSize.base": "1rem",
  "typography.fontSize.h1": "2.5rem",
  "shadows.sm": "0 1px 2px rgba(0,0,0,0.05)",
  "shadows.md": "0 4px 6px rgba(0,0,0,0.1)",
  "borderRadius.sm": "4px",
  "borderRadius.md": "8px",
  "borderRadius.full": "9999px"
}
```

### Output examples

**CSS:**
```css
:root {
  --colors-primary: #3b82f6;
  --colors-secondary: #8b5cf6;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --typography-fontsize-base: 1rem;
}
```

**Tailwind:**
```js
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: '#3b82f6',
        secondary: '#8b5cf6',
        neutral: {
          '100': '#f5f5f5',
          '900': '#171717'
        }
      },
      spacing: {
        sm: '0.5rem',
        md: '1rem',
        lg: '2rem'
      },
      borderRadius: {
        sm: '4px',
        md: '8px',
        full: '9999px'
      }
    }
  }
}
```

**SASS:**
```scss
$colors-primary: #3b82f6;
$colors-secondary: #8b5cf6;
$spacing-sm: 0.5rem;
$spacing-md: 1rem;
$typography-fontsize-base: 1rem;
```

---

## 📁 Project Structure

```
designtok/
└── index.html              # The entire app (~1000 lines)
```

One file. Open it and it works. That's the whole point.

---

## 🧪 Manual Testing

No automated test suite (vanilla single-file app). Verified:

- [x] Valid JSON → correct output for all 3 formats
- [x] Invalid JSON → red error with line number
- [x] Dot-notation and nested objects both work
- [x] Copy button copies correct output
- [x] Sample tokens button fills input with realistic data
- [x] Dark/light theme persists across reloads
- [x] Responsive at 375px and 1280px
- [x] Zero console errors

---

## 📄 License

MIT

---

<p align="center">Made with ❤️ by <a href="https://github.com/kvnlnk">kvnlnk</a></p>
