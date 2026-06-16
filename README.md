# README

There are two ways to add jTable to your project — npm or direct script include.

***

## Option A — npm

```bash
npm install jquery jtable
```

Then import in your entry file:

```javascript
import 'jquery';
import 'jtable';
import 'jtable/dist/themes/bootstrap5/jtable.css';
```

***

## Option B — Script Tags (CDN / Local)

Add the following to your HTML `<head>`:

```html
<!-- jQuery -->
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

<!-- jQuery UI (for dialogs) -->
<link  rel="stylesheet" href="https://code.jquery.com/ui/1.13.2/themes/base/jquery-ui.css" />
<script src="https://code.jquery.com/ui/1.13.2/jquery-ui.min.js"></script>

<!-- jTable core -->
<script src="/scripts/jtable/jquery.jtable.js"></script>

<!-- jTable theme — pick one (see Themes & UI section) -->
<link rel="stylesheet" href="/scripts/jtable/themes/bootstrap5/jtable.css" />
```

***

## Choosing a Theme

| Theme             | CSS File                       |
| ----------------- | ------------------------------ |
| Bootstrap 5       | `themes/bootstrap5/jtable.css` |
| Bulma             | `themes/bulma/jtable.css`      |
| Semantic UI       | `themes/semantic/jtable.css`   |
| Legacy (original) | `themes/standard/jtable.css`   |

See the [Themes & UI](jtable-docs/themes-ui/overview.md) section for full setup instructions per theme.

***

## Localization (Optional)

To display the UI in a language other than English, add a localization file after the main script:

```html
<script src="/scripts/jtable/localization/jquery.jtable.tr.js"></script>
```

See the [Localization](jtable-docs/api-reference/localization.md) reference for available languages and how to write your own.

***

## Verify the Installation

Add a container `<div>` to your page and initialize a minimal jTable:

```html
<div id="TestTable"></div>

<script>
$(document).ready(function () {
    $('#TestTable').jtable({
        title: 'Test',
        actions: { listAction: '/api/test/list' },
        fields: {
            Id:   { key: true, list: false },
            Name: { title: 'Name', width: '100%' }
        }
    });
    $('#TestTable').jtable('load');
});
</script>
```

If a table with a title bar and "Add new record" link appears, the installation is working.

***

## Next Steps

* [Quick Start](/broken/pages/8wBy81mIx0V38BFC3MG0) — build a complete CRUD table step by step
