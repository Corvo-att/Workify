# Workify — Front-End Developer Guide

> **Quick reference** for every team member. Read this before creating your page!

---

## 📁 Project Structure

```
Front_End/
├── css/
│   ├── variables.css      ← Design tokens (colors, fonts, spacing, etc.)
│   ├── reset.css           ← CSS reset + Google Fonts import
│   ├── layout.css          ← Grid system, topbar, sidebar, responsive breakpoints
│   ├── components.css      ← Reusable styles (buttons, cards, badges, inputs…)
│   └── utilities.css       ← Helper classes (flex, margin, padding, text…)
├── components/
│   ├── header.html         ← Sticky topbar (auto-loaded on every page)
│   ├── footer.html         ← Site footer (auto-loaded on every page)
│   └── sidebar.html        ← Dashboard sidebar (loaded only when placeholder exists)
├── js/
│   └── shared.js           ← Loads components, handles menu/sidebar/active links
├── assets/
│   └── icons/              ← Put SVGs, images, logos here
├── pages/                  ← YOUR PAGES GO HERE
│   ├── browse-jobs.html
│   ├── dashboard.html
│   └── ...
├── index.html              ← Landing page (working example)
└── README.md               ← This file
```

---

## 🚀 How to Create a New Page

### 1. Copy this starter template

Create a new file in the `pages/` folder (e.g. `pages/browse-jobs.html`):

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta name="description" content="Page description for SEO">
  <title>Page Title — Workify</title>

  <!-- Shared CSS (always include all five, in this order) -->
  <link rel="stylesheet" href="../css/variables.css">
  <link rel="stylesheet" href="../css/reset.css">
  <link rel="stylesheet" href="../css/layout.css">
  <link rel="stylesheet" href="../css/components.css">
  <link rel="stylesheet" href="../css/utilities.css">

  <!-- Page-specific styles -->
  <style>
    /* Your page-only styles here */
  </style>
</head>
<body>

  <!-- Header (auto-loaded) -->
  <div id="header-placeholder"></div>

  <!-- Main content -->
  <main class="main-content no-sidebar">
    <div class="container">
      <h1>Page Title</h1>
      <!-- Your content here -->
    </div>
  </main>

  <!-- Footer (auto-loaded) -->
  <div id="footer-placeholder"></div>

  <!-- Shared JS (always include) -->
  <script src="../js/shared.js"></script>
</body>
</html>
```

### 2. For dashboard pages (with sidebar)

Replace the body content with:

```html
<body>
  <div id="header-placeholder"></div>

  <div class="page-wrapper">
    <!-- Sidebar (auto-loaded because the placeholder exists) -->
    <div id="sidebar-placeholder"></div>

    <!-- Main content — DON'T use no-sidebar class here -->
    <main class="main-content">
      <div class="container">
        <h1>Dashboard Title</h1>
        <!-- Your content here -->
      </div>
    </main>
  </div>

  <div id="footer-placeholder"></div>
  <script src="../js/shared.js"></script>
</body>
```

### 3. Add active-link support

For your links to get highlighted in the nav, add a `data-page` attribute that matches the filename (without `.html`):

```html
<!-- In the header/sidebar, links already have data-page attributes.
     Just make sure your filename matches! -->
pages/browse-jobs.html  →  data-page="browse-jobs"
pages/dashboard.html    →  data-page="dashboard"
```

---

## 🎨 Available CSS Classes (Cheat Sheet)

### Buttons
| Class | What it does |
|-------|-------------|
| `.btn .btn-primary` | Main gradient CTA button |
| `.btn .btn-ghost` | Outline / transparent button |
| `.btn .btn-danger` | Red destructive action button |
| `.btn-sm` | Small size |
| `.btn-lg` | Large size |
| `.btn-icon` | Icon-only square button |

### Cards
| Class | What it does |
|-------|-------------|
| `.card` | Standard card with hover lift |
| `.card-static` | Card without hover effect |
| `.stat-card` | KPI stat card (label + value) |
| `.stat-card.earnings` | Green-tinted stat card |

### Badges
| Class | Color |
|-------|-------|
| `.badge .badge-primary` | Purple |
| `.badge .badge-accent` | Orange |
| `.badge .badge-success` | Green |
| `.badge .badge-warning` | Yellow |
| `.badge .badge-danger` | Red |
| `.badge .badge-muted` | Gray |

### Form Inputs
| Class | What it does |
|-------|-------------|
| `.input-field` | Text input / textarea / select |
| `.input-label` | Label above an input |
| `.input-group` | Wrapper for label + input + helper |
| `.input-helper` | Small help text below input |

### Layout
| Class | What it does |
|-------|-------------|
| `.container` | Centered max-width wrapper |
| `.grid` | 12-column CSS grid |
| `.col-1` to `.col-12` | Column span classes |
| `.split-layout` | Flex container for 70/30 layouts |
| `.section` | Large vertical padding |

### Utilities (examples)
| Class | Effect |
|-------|--------|
| `.flex .items-center .gap-4` | Horizontal centered flex with 16px gap |
| `.text-muted` | Muted gray text |
| `.text-gradient` | Gradient-filled text |
| `.mt-6` | 24px top margin |
| `.p-4` | 16px padding on all sides |
| `.hidden` | Hide element |
| `.hide-mobile` | Hide on mobile screens |
| `.truncate` | Single-line text with ellipsis |

---

## 🛠 JavaScript Utilities

These functions are available globally from `shared.js`:

```js
// Show a toast notification
showToast('Payment released!', 'success');       // types: 'success', 'warning', 'danger'

// Format currency
formatCurrency(2400);        // → "$2,400.00"

// Time ago
timeAgo('2026-03-10');       // → "1 day ago"
```

---

## ⚡ Running Locally

Use any local server. The simplest options:

```bash
# Option 1: VS Code — install "Live Server" extension, right-click index.html → Open with Live Server

# Option 2: npx
npx serve .

# Option 3: Python
python -m http.server 3000
```

> **Important:** Don't open HTML files directly with `file://` — the component loader uses `fetch()` which needs a server.

---

## ✅ Quick Rules

1. **Always include all 5 CSS files** in the order shown above
2. **Always include `shared.js`** at the bottom of `<body>`
3. **Use the existing CSS classes** — avoid writing custom CSS for things that already have a class
4. **Put page-specific styles** in a `<style>` tag in the `<head>`, not in the shared CSS files
5. **Put page-specific JS** in a separate file (e.g. `js/browse-jobs.js`), loaded AFTER `shared.js`
6. **Use CSS variables** (e.g. `var(--primary)`) instead of hardcoding hex colors
7. **Use the spacing scale** (e.g. `var(--space-4)`) for margins/padding in custom CSS
8. **Add `data-page="your-page-name"`** to nav links so active highlighting works
9. **Don't edit shared files** without discussing with the team first
