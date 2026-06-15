# Themes & UI Overview

jTable supports multiple UI frameworks through a pluggable adapter system. Pick the adapter that matches your project's CSS framework.

---

## Available Adapters

| Adapter | CSS Framework | Status |
|---|---|---|
| `bootstrap5` | Bootstrap 5 | ✅ Stable |
| `bootstrap4` | Bootstrap 4 | ✅ Stable |
| `bulma` | Bulma | ✅ Stable |
| `semantic` | Semantic UI / Fomantic UI | ✅ Stable |
| `uikit` | UIKit 3 | ✅ Stable |
| `materialize` | Materialize CSS | ✅ Stable |
| `legacy` | Original jTable theme | ✅ Stable |

---

## How Adapters Work

An adapter is a small JavaScript module that tells jTable how to render its UI components — buttons, modals, inputs, table markup — using a specific CSS framework's classes and patterns.

You select an adapter via the `ui` option:

```javascript
$('#MyTable').jtable({
    ui: 'bootstrap5',
    // ...
});
```

Without the `ui` option, jTable falls back to `legacy` mode (original look).

---

## Design Tokens

Every adapter ships with CSS custom properties (variables) prefixed with `--jt-`. Override them in your own stylesheet to rebrand jTable without touching any source files:

```css
:root {
    --jt-primary:        #6d28d9;   /* Main action color */
    --jt-primary-hover:  #5b21b6;   /* Hover state */
    --jt-header-bg:      #1e1b4b;   /* Table header background */
    --jt-header-color:   #ffffff;   /* Table header text */
    --jt-border-color:   #e5e7eb;   /* Table borders */
    --jt-row-hover-bg:   #f5f3ff;   /* Row hover background */
    --jt-font-size:      0.875rem;  /* Base font size */
}
```

---

## Included Theme Files

Each adapter ships with a matching CSS file:

```
dist/
└── themes/
    ├── bootstrap5/    jtable.css
    ├── bootstrap4/    jtable.css
    ├── bulma/         jtable.css
    ├── semantic/      jtable.css
    ├── uikit/         jtable.css
    ├── materialize/   jtable.css
    └── legacy/        jtable.css
                       jtable_list_limited.css
```

Include **only** the theme file for the adapter you are using.

---

## Detailed Guides

- [Bootstrap 5](bootstrap5.md) — Full setup with Bootstrap 5
- [Custom Adapter](custom-adapter.md) — Build your own adapter from scratch
