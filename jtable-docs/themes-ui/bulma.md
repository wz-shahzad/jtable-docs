# Bulma Theme

jTable's Bulma adapter renders all UI components using Bulma CSS classes. Date fields use bulma-calendar.

---

## Dependencies

| Library | Version | CDN |
|---|---|---|
| jQuery | 3.1.1 | `ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js` |
| Bulma | 1.0.4 | `cdn.jsdelivr.net/npm/bulma@1.0.4/css/bulma.min.css` |
| Font Awesome | 5.15.2 | `bulma.io/vendor/fontawesome-free-5.15.2-web/css/all.min.css` |
| bulma-calendar | 6.1.19 | `cdn.jsdelivr.net/npm/bulma-calendar@6.1.19` |

---

## Setup

```html
<!-- Bulma CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma@1.0.4/css/bulma.min.css" />
<link rel="stylesheet" href="https://bulma.io/vendor/fontawesome-free-5.15.2-web/css/all.min.css" />
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bulma-calendar@6.1.19/dist/css/bulma-calendar.min.css">

<!-- jTable Bulma CSS -->
<link href="~/dev/ui/Bulma/jtable.ui.bulma-ui.css" rel="stylesheet" />

<!-- jQuery -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>

<!-- bulma-calendar JS -->
<script src="https://cdn.jsdelivr.net/npm/bulma-calendar@6.1.19/dist/js/bulma-calendar.min.js"></script>

<!-- jTable core -->
<script src="~/dev/jquery.jtable-vnext.js"></script>

<!-- jTable Bulma adapter -->
<script src="~/dev/ui/Bulma/jquery.jtable.ui.bulma.js"></script>
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

- Bulma has no built-in JavaScript — bulma-calendar is used separately for date fields.
- Font Awesome provides icons for toolbar buttons and action links.
- RTL layout is not supported in the Bulma adapter.
