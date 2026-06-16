# Introduction

**jTable** is a jQuery plugin that creates fully functional AJAX-based CRUD tables — with listing, paging, sorting, and create/edit/delete dialogs — without writing HTML or JavaScript by hand.

---

## What's New in This Version

This is an enhanced fork of the original jTable with significant improvements:

- **Pluggable UI Adapters** — Bootstrap 5, Bulma, Semantic UI, UIKit, Materialize, and more
- **New Themes** — Modern, responsive designs out of the box
- **Design Tokens** — Rebrand the entire UI with a few CSS variables
- **Improved Accessibility** — Better keyboard navigation and ARIA support
- **AI-ready Docs** — Structured Markdown for use with coding assistants

---

## How It Works

jTable sits between your HTML page and your server. You define:

1. **Fields** — what data columns exist
2. **Actions** — server URLs for list / create / update / delete
3. **Options** — paging, sorting, themes, etc.

jTable handles everything else: rendering the table, opening dialogs, making AJAX calls, and updating the UI.

```
Browser                          Your Server
───────                          ───────────
jTable  ──── POST /list ──────►  Returns JSON records
        ◄─── { Result, Records }

        ──── POST /create ────►  Saves new record
        ◄─── { Result, Record }

        ──── POST /update ────►  Updates record
        ◄─── { Result }

        ──── POST /delete ────►  Deletes record
        ◄─── { Result }
```

---

## Browser & Dependency Support

| Dependency | Minimum Version |
|---|---|
| jQuery | 1.9+ |
| jQuery UI | 1.10+ (for dialogs) |
| Browser | All modern browsers + IE 10+ |

---

## Next Steps

- [Installation](installation.md) — how to add jTable to your project
- [Quick Start](quick-start.md) — build your first table in minutes
