# Fomantic UI Theme

jTable's Fomantic UI adapter renders all UI components using Fomantic UI (the community fork of Semantic UI) classes and modals.

---

## Dependencies

| Library | Version | CDN |
|---|---|---|
| jQuery | 3.1.1 | `ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js` |
| Fomantic UI | 2.9.1 | `cdn.jsdelivr.net/npm/fomantic-ui@2.9.1/dist/semantic.min.css` |

---

## Setup

```html
<!-- Fomantic UI CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/fomantic-ui@2.9.1/dist/semantic.min.css" />

<!-- jTable Fomantic UI CSS -->
<link href="~/dev/ui/Fomantic-UI/jtable.ui.fomantic.css" rel="stylesheet" />

<!-- jQuery -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>

<!-- Fomantic UI JS -->
<script src="https://cdn.jsdelivr.net/npm/fomantic-ui@2.9.1/dist/semantic.min.js"></script>

<!-- jTable core -->
<script src="~/dev/jquery.jtable-vnext.js"></script>

<!-- jTable Fomantic UI adapter -->
<script src="~/dev/ui/Fomantic-UI/jquery.jtable.ui.fomantic-ui.js"></script>
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
        smallSize: true,          // recommended for Fomantic UI
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

- `smallSize: true` is recommended for Fomantic UI to achieve the compact, dense table look.
- For grouped select fields, add `inputClass: 'fluid'` to make dropdowns full-width inside the form.
- Add `style="padding: 10px;"` to the container div to provide comfortable spacing around the table.
- RTL is not supported in this adapter.
