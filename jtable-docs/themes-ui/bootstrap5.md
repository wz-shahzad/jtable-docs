# Bootstrap 5 Theme

jTable's Bootstrap 5 adapter renders all UI components using native Bootstrap 5 classes. Date fields use bootstrap-datepicker. Full RTL support is included.

---

## Dependencies

| Library | Version | CDN |
|---|---|---|
| jQuery | 3.6.0 | `ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js` |
| Bootstrap | 5.1.3 | `cdn.jsdelivr.net/npm/bootstrap@5.1.3` |
| Bootstrap Datepicker | 1.10.0 | `cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.10.0` |
| Bootstrap Icons | 1.7.0 | `cdn.jsdelivr.net/npm/bootstrap-icons@1.7.0` |

---

## Setup

```html
<!-- Bootstrap 5 CSS -->
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" />
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.10.0/css/bootstrap-datepicker.min.css" />
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.7.0/font/bootstrap-icons.css" />

<!-- jTable Bootstrap 5 CSS -->
<link href="~/dev/ui/bootstrap/jtable.ui.bootstrap-5.css" rel="stylesheet" />

<!-- jQuery -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>

<!-- Bootstrap 5 JS -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/bootstrap-datepicker/1.10.0/js/bootstrap-datepicker.min.js"></script>

<!-- jTable core -->
<script src="~/dev/jquery.jtable-vnext.js"></script>

<!-- jTable Bootstrap 5 adapter -->
<script src="~/dev/ui/bootstrap/jquery.jtable.ui.bootstrap-5.js"></script>
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
        progressBarClass: 'bg-info',
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

## RTL Support

Bootstrap 5 includes a dedicated RTL CSS build. To enable right-to-left layout:

**1. Use the Bootstrap RTL stylesheet:**

```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.rtl.min.css" />
```

**2. Set the HTML direction and add `isRtl: true` to jTable:**

```javascript
$('html').attr({ 'lang': 'ar', 'dir': 'rtl' });

$('#MyTableContainer').jtable({
    isRtl: true,
    // ... other options
});
```

**3. Apply `dir="rtl"` to the container:**

```html
<div id="MyTableContainer" dir="rtl"></div>
```

---

## Bootstrap Form Validation

Integrate Bootstrap 5's built-in validation with `formSubmitting`:

```javascript
formSubmitting: function (event, data) {
    data.form.addClass('was-validated');
    if (!data.form[0].checkValidity()) {
        return false; // cancel submit
    }
}
```

---

## Notes

- `progressBarClass: 'bg-info'` (or any Bootstrap background utility) controls the loading bar color.
- For child table form inputs, add `inputClass: 'form-control'` per field for consistent Bootstrap styling.
- jquery-migrate may be needed in some environments: `cdn.iu.edu.sa/iu-v.2.9.3/js/jquery-migrate.js`.
