# Themes & UI Overview

jTable supports multiple CSS frameworks through a pluggable UI adapter system. Each adapter provides a complete set of styles and component behaviors matching the target framework.

---

## Available Themes

| Theme | Framework | Date Picker | RTL Support | Adapter File |
|---|---|---|---|---|
| [Bootstrap 5](bootstrap5.md) | Bootstrap 5 | bootstrap-datepicker | ✅ | `jquery.jtable.ui.bootstrap-5.js` |
| [Bootstrap 4](bootstrap4.md) | Bootstrap 4 | bootstrap-datepicker | ✅ | `jquery.jtable.ui.bootstrap-4.js` |
| [Bulma](bulma.md) | Bulma 1.x | bulma-calendar | ❌ | `jquery.jtable.ui.bulma.js` |
| [Fomantic UI](fomantic-ui.md) | Fomantic UI 2.9 | built-in | ❌ | `jquery.jtable.ui.fomantic-ui.js` |
| [Semantic UI](semantic-ui.md) | Fomantic UI 2.5 | built-in | ❌ | `jquery.jtable.ui.semantic-ui.js` |
| [UIkit](uikit.md) | UIkit 3 | flatpickr | ❌ | `jquery.jtable.ui.uikit-ui.js` |
| [Legacy](legacy.md) | jQuery UI | jQuery UI datepicker | ❌ | `jquery.jtable.ui.legacy-ui.js` |

---

## How the Adapter System Works

Every adapter is a small JS file that tells jTable how to render its components — tables, dialogs, buttons, inputs — using a specific framework's classes and patterns.

**Include order for any theme:**

```html
<!-- 1. Framework CSS -->
<!-- 2. jTable theme CSS  (dev/ui/<Theme>/jtable.ui.<theme>.css) -->
<!-- 3. jQuery -->
<!-- 4. Framework JS -->
<!-- 5. jTable core  (dev/jquery.jtable-vnext.js) -->
<!-- 6. jTable adapter JS  (dev/ui/<Theme>/jquery.jtable.ui.<theme>.js) -->
```

---

## Common Options Across All Themes

These options work the same regardless of theme:

| Option | Description |
|---|---|
| `smallSize: true` | Compact row height (supported by most adapters) |
| `isRtl: true` | Right-to-left layout (Bootstrap 5 only) |
| `columnResizable: false` | Disable column drag-to-resize |
| `columnSelectable: true` | Allow users to show/hide columns |
| `selecting: true` | Enable row selection |
| `multiselect: true` | Allow multi-row selection |
| `selectingCheckboxes: true` | Show checkbox column for selection |
| `progressBarClass` | CSS class for the loading progress bar |

---

## File Locations

```
dev/
├── jquery.jtable-vnext.js          ← jTable core (all themes)
└── ui/
    ├── bootstrap/
    │   ├── jquery.jtable.ui.bootstrap-4.js
    │   ├── jquery.jtable.ui.bootstrap-5.js
    │   ├── jtable.ui.bootstrap-4.css
    │   └── jtable.ui.bootstrap-5.css
    ├── Bulma/
    │   ├── jquery.jtable.ui.bulma.js
    │   └── jtable.ui.bulma-ui.css
    ├── Fomantic-UI/
    │   ├── jquery.jtable.ui.fomantic-ui.js
    │   └── jtable.ui.fomantic.css
    ├── Semantic-Ui/
    │   ├── jquery.jtable.ui.semantic-ui.js
    │   └── jtable.ui.semantic-ui.css
    ├── UIKit-UI/
    │   ├── jquery.jtable.ui.uikit-ui.js
    │   └── jtable.ui.uikit-ui.css
    └── legacy/
        └── jquery.jtable.ui.legacy-ui.js
```
