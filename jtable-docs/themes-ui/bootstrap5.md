# Bootstrap 5 Theme

jTable's Bootstrap 5 adapter renders all UI components — table, dialogs, buttons, inputs — using native Bootstrap 5 classes.

---

## Prerequisites

Bootstrap 5 must be loaded before jTable. jQuery is still required.

```html
<!-- Bootstrap 5 -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" />
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

<!-- jQuery (required by jTable) -->
<script src="https://code.jquery.com/jquery-3.7.1.min.js"></script>

<!-- jTable core -->
<script src="/scripts/jtable/jquery.jtable.js"></script>

<!-- jTable Bootstrap 5 theme -->
<link rel="stylesheet" href="/scripts/jtable/themes/bootstrap5/jtable.css" />
```

> **Note:** Load Bootstrap JS **before** jQuery when using Bootstrap 5, as Bootstrap's bundle is self-contained.

---

## Initialization

Pass `ui: 'bootstrap5'` in the options:

```javascript
$('#StudentsTable').jtable({
    title: 'Students',
    ui: 'bootstrap5',
    paging: true,
    pageSize: 10,
    sorting: true,
    actions: {
        listAction:   '/api/students/list',
        createAction: '/api/students/create',
        updateAction: '/api/students/update',
        deleteAction: '/api/students/delete'
    },
    fields: {
        StudentId: { key: true, list: false },
        Name:      { title: 'Name',  width: '30%' },
        Email:     { title: 'Email', width: '35%' },
        IsActive:  {
            title: 'Active',
            width: '15%',
            type: 'checkbox',
            values: { 'false': 'Passive', 'true': 'Active' }
        }
    }
});

$('#StudentsTable').jtable('load');
```

---

## Customizing Colors

Override the design tokens after loading the theme CSS:

```css
/* your-overrides.css */
:root {
    --jt-primary:       #0d6efd;   /* Bootstrap blue (default) */
    --jt-primary-hover: #0b5ed7;
    --jt-header-bg:     #212529;   /* Dark header */
    --jt-header-color:  #ffffff;
    --jt-row-hover-bg:  #f8f9fa;
}
```

---

## Using Bootstrap Form Validation

You can integrate Bootstrap's validation styles with the `inputClass` field option and the `formSubmitting` event:

```javascript
fields: {
    Name: {
        title: 'Name',
        width: '30%',
        inputClass: 'form-control'  // already applied by adapter; shown for clarity
    }
},

formSubmitting: function (event, data) {
    // Add Bootstrap was-validated class to show inline errors
    data.form.addClass('was-validated');

    // Return false to cancel submit if invalid
    if (!data.form[0].checkValidity()) {
        return false;
    }
}
```

---

## Modal Size

The create/edit dialog uses Bootstrap's modal component. You can control the size via CSS:

```css
/* Wide dialog */
.jtable-dialog .modal-dialog {
    max-width: 700px;
}
```
