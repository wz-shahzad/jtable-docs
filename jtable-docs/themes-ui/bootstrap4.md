# Bootstrap 4 Theme

jTable's Bootstrap 4 adapter renders all UI components using native Bootstrap 4 classes and bootstrap-datepicker for date fields.

---

## Dependencies

| Library | Version | Purpose |
|---|---|---|
| jQuery | 3.x | Required by jTable |
| Bootstrap 4 | 4.x | CSS framework |
| Bootstrap Datepicker | 1.10 | Date field picker |
| Bootstrap Icons | 1.7 | Toolbar/button icons |

---

## Setup

```html
<!-- Bootstrap 4 CSS -->
<link rel="stylesheet" href="~/bootstrap4/css/bootstrap.min.css" />
<link rel="stylesheet" href="~/bootstrap4/css/bootstrap-datepicker.min.css" />
<link rel="stylesheet" href="~/bootstrap4/font/bootstrap-icons.css" />

<!-- jTable Bootstrap 4 CSS -->
<link href="~/dev/ui/bootstrap/jtable.ui.bootstrap-4.css" rel="stylesheet" />

<!-- jQuery -->
<script src="~/bootstrap4/js/jquery.min.js"></script>

<!-- Bootstrap 4 JS -->
<script src="~/bootstrap4/js/bootstrap.bundle.min.js"></script>
<script src="~/bootstrap4/js/bootstrap-datepicker.min.js"></script>

<!-- jTable core -->
<script src="~/dev/jquery.jtable-vnext.js"></script>

<!-- jTable Bootstrap 4 adapter -->
<script src="~/dev/ui/bootstrap/jquery.jtable.ui.bootstrap-4.js"></script>
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
        progressBarClass: 'bg-info',
        actions: {
            listAction:   '/api/list',
            createAction: '/api/create',
            updateAction: '/api/update',
            deleteAction: '/api/delete'
        },
        fields: {
            id: { key: true, create: false, edit: false, list: false },
            name: { title: 'Name', width: '30%' }
        }
    });

    $('#MyTableContainer').jtable('load');
});
```

---

## Notes

- Bootstrap 4 uses local files rather than CDN in this implementation — copy the `bootstrap4/` assets folder to your project.
- The `inputClass: 'form-control'` field option is recommended for form inputs to match Bootstrap 4 styling.
- For child table inputs, add `inputClass: 'form-control'` per field for consistent styling.
