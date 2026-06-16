# Semantic UI Theme

jTable's Semantic UI adapter targets Fomantic UI 2.5 (the closest maintained equivalent of the original Semantic UI 2.x). It renders all table components using Semantic UI / Fomantic UI class names.

---

## Dependencies

| Library | Version | CDN |
|---|---|---|
| jQuery | 3.1.1 | `ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js` |
| Fomantic UI | 2.5.0 | `cdn.jsdelivr.net/npm/fomantic-ui@2.5.0/dist/semantic.min.css` |

> **Note:** The Semantic UI adapter uses **Fomantic UI 2.5** specifically. The [Fomantic UI adapter](fomantic-ui.md) targets the newer 2.9.x branch. Choose one or the other — do not mix them on the same page.

---

## Setup

```html
<!-- Fomantic UI 2.5 CSS (Semantic UI compatible) -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/fomantic-ui@2.5.0/dist/semantic.min.css">

<!-- jTable Semantic UI CSS -->
<link href="~/dev/ui/Semantic-Ui/jtable.ui.semantic-ui.css" rel="stylesheet" />

<!-- jQuery -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>

<!-- Fomantic UI 2.5 JS -->
<script src="https://cdn.jsdelivr.net/npm/fomantic-ui@2.5.0/dist/semantic.min.js"></script>

<!-- jTable core -->
<script src="~/dev/jquery.jtable-vnext.js"></script>

<!-- jTable Semantic UI adapter -->
<script src="~/dev/ui/Semantic-Ui/jquery.jtable.ui.semantic-ui.js"></script>
```

---

## Initialization

```javascript
$(document).ready(function () {
    $('#MyTableContainer').jtable({
        title: 'My Table',
        paging: true,
        sorting: true,
        multiSorting: true,
        pageSize: 10,
        columnResizable: false,
        columnSelectable: true,
        smallSize: true,
        selecting: true,
        multiselect: true,
        selectingCheckboxes: true,
        actions: {
            listAction:   '/api/list',
            createAction: '/api/create',
            updateAction: '/api/update',
            deleteAction: '/api/delete'
        },
        fields: {
            id:   { key: true, create: false, edit: false, list: false },
            name: { title: 'Name', width: '30%' }
        }
    });

    $('#MyTableContainer').jtable('load');
});
```

---

## Notes

- `smallSize: true` is recommended for a compact Semantic UI style table.
- For fluid dropdowns (e.g. grouped selects), add `inputClass: 'fluid'` to the field definition.
- Add `style="padding: 10px;"` on the container div for proper spacing.
- RTL is not supported in this adapter.
