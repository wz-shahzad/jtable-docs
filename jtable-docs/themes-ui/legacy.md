# Legacy Theme

The Legacy adapter is the original jTable UI — built on jQuery UI. It provides the classic jTable look and is useful when you need maximum compatibility or are migrating an existing application.

---

## Dependencies

| Library | Version | Source |
|---|---|---|
| jQuery | 1.9.1+ | `jtable.org/Scripts/jquery-1.9.1.min.js` |
| jQuery UI | 1.10.0+ | `jtable.org/Scripts/jquery-ui-1.10.0.min.js` |
| jQuery UI Theme | metroblue | `jtable.org/Content/themes/metroblue/jquery-ui.css` |
| jTable Legacy CSS | — | `jtable.org/Scripts/jtable/themes/metro/blue/jtable.css` |

---

## Setup

```html
<!-- jQuery UI theme -->
<link href="https://www.jtable.org/Content/themes/metroblue/jquery-ui.css" rel="stylesheet" />

<!-- jTable Legacy CSS -->
<link href="https://www.jtable.org/Scripts/jtable/themes/metro/blue/jtable.css" rel="stylesheet" />

<!-- jQuery -->
<script src="https://www.jtable.org/Scripts/jquery-1.9.1.min.js"></script>

<!-- jQuery UI -->
<script src="https://www.jtable.org/Scripts/jquery-ui-1.10.0.min.js"></script>

<!-- jTable core -->
<script src="~/dev/jquery.jtable-vnext.js"></script>

<!-- jTable Legacy adapter -->
<script src="~/dev/ui/legacy/jquery.jtable.ui.legacy-ui.js"></script>
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
        defaultSorting: 'name ASC',
        actions: {
            listAction:   '/api/list',
            createAction: '/api/create',
            updateAction: '/api/update',
            deleteAction: '/api/delete'
        },
        fields: {
            id:   { key: true, create: false, edit: false, list: false },
            name: { title: 'Name', width: '25%' }
        }
    });

    $('#MyTableContainer').jtable('load');
});
```

---

## Child Table Column Width Fix

The Legacy adapter requires a manual column width reset after a child table opens:

```javascript
// In the openChildTable opened callback:
function (data) {
    data.childTable.find('thead th, tbody td').css('width', '');
    data.childTable.jtable('load');
}
```

---

## Notes

- The Legacy adapter is the only adapter that does **not** require a modern CSS framework.
- jQuery UI's datepicker handles `type: 'date'` fields (no separate date library needed).
- Dialogs use jQuery UI Dialog component.
- RTL is not supported.
- For new projects, consider a modern adapter (Bootstrap 5, Bulma, etc.) for better mobile support.
