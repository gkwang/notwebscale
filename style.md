# notwebscale — Style Guide

## Design Philosophy

notwebscale uses a **dark glassmorphism** aesthetic: deep space-inspired gradients as a backdrop, frosted-glass cards layered on top, and a purple-to-blue accent palette. The result is a modern, privacy-tool feel — minimal, trustworthy, and focused.

---

## Color Palette

### Background Gradient
```css
background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
```
| Token | Hex | Role |
|---|---|---|
| Deep navy | `#0f0c29` | Gradient start |
| Deep purple | `#302b63` | Gradient mid |
| Dark slate | `#24243e` | Gradient end |

### Accent — Purple → Blue
```css
background: linear-gradient(135deg, #a78bfa, #60a5fa);
```
| Token | Hex | Role |
|---|---|---|
| Violet 400 | `#a78bfa` | Primary accent, spinner, focus ring |
| Violet 300 | `#c4b5fd` | Softer purple text, chain badges |
| Blue 400 | `#60a5fa` | Gradient end, status pills |
| Blue 300 | `#93c5fd` | Softer blue text |

### Semantic Colors
| Token | Value | Role |
|---|---|---|
| Success | `#6ee7b7` / `rgba(52,211,153,…)` | "Already clean" pill, copy-confirmed state |
| Error | `#fca5a5` / `rgba(239,68,68,…)` | Error message text/background |
| Muted text | `rgba(255,255,255,0.5)` | Subtitles, labels |
| Dimmed text | `rgba(255,255,255,0.35)` | Placeholder, icons |
| Body text | `#e2e8f0` | URL content, primary readable text |

---

## Typography

### Font Stacks
```css
/* UI / body */
font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;

/* Monospace — used for all URLs */
font-family: 'SF Mono', 'Monaco', 'Menlo', monospace;
```

### Scale
| Usage | Size | Weight | Notes |
|---|---|---|---|
| Page title | `2.4rem` | 800 | Gradient text fill |
| Subtitle | `1rem` | 400 | `rgba(255,255,255,0.5)` |
| Body / input | `15px` | 400–600 | |
| URL text | `13.5px` | 400 | Monospace |
| Section labels | `11px` | 700 | All-caps, `letter-spacing: 0.08em` |
| Small (chain, status) | `12px–13px` | 400–700 | |

---

## Spacing & Shape

### Layout
- Max content width: `720px`, centered, `padding: 40px 20px 60px`
- Card stack gap: `20px`

### Border Radii
| Component | Radius |
|---|---|
| Main card | `20px` |
| Input, primary button | `12px` |
| Result cards | `16px` |
| Copy button | `8px` |
| Status badge | `4px` |
| Pills | `999px` (full pill) |
| Chain step badge | `50%` (circle) |

### Padding
```css
.card          { padding: 32px; }
.result-card   { padding: 20px 24px; }
input[type="url"] { padding: 14px 14px 14px 44px; } /* 44px left for icon */
button.primary { padding: 14px 28px; }
button.copy-btn { padding: 6px 14px; }
.pill          { padding: 5px 12px; }
```

---

## Glassmorphism Cards

The core UI surface. All cards share this pattern:

```css
.card {
    background: rgba(255, 255, 255, 0.06);
    backdrop-filter: blur(12px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 20px;
    padding: 32px;
}
```

- **Background opacity** stays very low (`0.06`) so the gradient shows through.
- **Backdrop blur** (`12px`) is the key glassmorphism effect.
- **Border** at `0.1` opacity creates a subtle light edge without hard lines.

---

## Interactive Elements

### Primary Button
```css
button.primary {
    background: linear-gradient(135deg, #a78bfa, #60a5fa);
    color: #fff;
    border: none;
    border-radius: 12px;
    font-size: 15px;
    font-weight: 600;
    padding: 14px 28px;
    transition: opacity 0.2s, transform 0.15s;
}
button.primary:hover  { opacity: 0.9; transform: translateY(-1px); }
button.primary:active { transform: translateY(0); }
button.primary:disabled { opacity: 0.45; cursor: not-allowed; transform: none; }
```

### URL Input
```css
input[type="url"] {
    background: rgba(255, 255, 255, 0.08);
    border: 1.5px solid rgba(255, 255, 255, 0.12);
    border-radius: 12px;
    color: #fff;
    font-size: 15px;
    padding: 14px 14px 14px 44px; /* left pad for inline SVG icon */
    transition: border-color 0.2s, background 0.2s;
}
input[type="url"]::placeholder { color: rgba(255, 255, 255, 0.3); }
input[type="url"]:focus {
    border-color: #a78bfa;
    background: rgba(167, 139, 250, 0.08);
}
```

### Copy Button States
```css
button.copy-btn {
    background: rgba(255, 255, 255, 0.08);
    color: rgba(255, 255, 255, 0.7);
    border: 1px solid rgba(255, 255, 255, 0.12);
    border-radius: 8px;
    font-size: 12px;
    font-weight: 500;
    padding: 6px 14px;
    transition: background 0.15s, color 0.15s;
}
button.copy-btn:hover  { background: rgba(255, 255, 255, 0.14); color: #fff; }
button.copy-btn.copied {
    background: rgba(52, 211, 153, 0.2);
    color: #6ee7b7;
    border-color: rgba(52, 211, 153, 0.3);
}
```

---

## Status Pills

Three semantic variants used in the stats row:

```css
.pill {
    display: inline-flex;
    align-items: center;
    gap: 6px;
    padding: 5px 12px;
    border-radius: 999px;
    font-size: 12px;
    font-weight: 600;
}

/* Trackers removed */
.pill.purple {
    background: rgba(167, 139, 250, 0.15);
    color: #c4b5fd;
    border: 1px solid rgba(167, 139, 250, 0.25);
}

/* Redirects followed */
.pill.blue {
    background: rgba(96, 165, 250, 0.15);
    color: #93c5fd;
    border: 1px solid rgba(96, 165, 250, 0.25);
}

/* URL already clean */
.pill.green {
    background: rgba(52, 211, 153, 0.12);
    color: #6ee7b7;
    border: 1px solid rgba(52, 211, 153, 0.22);
}
```

---

## Loading & Feedback States

### Spinner
```css
.spinner {
    display: inline-block;
    width: 18px;
    height: 18px;
    border: 2px solid rgba(255, 255, 255, 0.2);
    border-top-color: #a78bfa;
    border-radius: 50%;
    animation: spin 0.7s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }
```

### Error Banner
```css
.error {
    padding: 12px 16px;
    background: rgba(239, 68, 68, 0.15);
    border: 1px solid rgba(239, 68, 68, 0.35);
    border-radius: 10px;
    color: #fca5a5;
    font-size: 14px;
}
```

---

## Redirect Chain

The chain visualiser uses numbered circle badges connected by down-arrows:

```css
.chain-badge {
    width: 24px;
    height: 24px;
    border-radius: 50%;
    background: rgba(167, 139, 250, 0.2);
    color: #c4b5fd;
    font-size: 11px;
    font-weight: 700;
    display: flex;
    align-items: center;
    justify-content: center;
}

.chain-url {
    font-family: 'SF Mono', 'Monaco', 'Menlo', monospace;
    font-size: 12px;
    color: rgba(255, 255, 255, 0.55);
    word-break: break-all;
    line-height: 1.5;
}

.status-badge {
    font-size: 10px;
    font-weight: 700;
    padding: 1px 6px;
    border-radius: 4px;
    background: rgba(96, 165, 250, 0.2);
    color: #93c5fd;
}
```

---

## URL Text Variants

Three tonal levels applied to `.result-url` to create visual hierarchy:

```css
.result-url        { color: #e2e8f0; }          /* Cleaned URL — primary */
.result-url.muted  { color: rgba(255,255,255,0.35); } /* Original URL — de-emphasized */
.result-url.accent { color: #a78bfa; }           /* Final destination — highlighted */
```

---

## Divider

```css
.divider {
    height: 1px;
    background: rgba(255, 255, 255, 0.06);
    margin: 4px 0 12px;
}
```

---

## Example: Full Reset + Base

```css
/* base.css — paste this at the top of any new stylesheet for this project */

*, *::before, *::after {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    min-height: 100vh;
    background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
    color: #e2e8f0;
}
```

## Example: New Feature Card

```css
/* A pattern to follow when adding new UI sections */

.feature-card {
    background: rgba(255, 255, 255, 0.06);
    backdrop-filter: blur(12px);
    border: 1px solid rgba(255, 255, 255, 0.1);
    border-radius: 16px;
    padding: 20px 24px;
}

.feature-card__label {
    font-size: 11px;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: rgba(255, 255, 255, 0.4);
    margin-bottom: 8px;
}

.feature-card__value {
    font-family: 'SF Mono', 'Monaco', 'Menlo', monospace;
    font-size: 13.5px;
    color: #e2e8f0;
    word-break: break-all;
    line-height: 1.5;
}

.feature-card__value--accent { color: #a78bfa; }
.feature-card__value--muted  { color: rgba(255, 255, 255, 0.35); }
```

## Example: Notification / Toast

```css
/* Follow these patterns for inline alerts */

.toast {
    padding: 12px 16px;
    border-radius: 10px;
    font-size: 14px;
}

.toast--error {
    background: rgba(239, 68, 68, 0.15);
    border: 1px solid rgba(239, 68, 68, 0.35);
    color: #fca5a5;
}

.toast--success {
    background: rgba(52, 211, 153, 0.12);
    border: 1px solid rgba(52, 211, 153, 0.22);
    color: #6ee7b7;
}

.toast--info {
    background: rgba(96, 165, 250, 0.15);
    border: 1px solid rgba(96, 165, 250, 0.25);
    color: #93c5fd;
}
```
